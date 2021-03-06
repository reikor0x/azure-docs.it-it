---
title: Verificare la presenza di errori in pool e nodi - Azure Batch
description: Informazioni sugli errori da controllare e su come evitarli durante la creazione di pool e nodi
services: batch
ms.service: batch
author: mscurrell
ms.author: markscu
ms.date: 05/28/2019
ms.topic: conceptual
ms.openlocfilehash: b0a9d04fccce7ccbacb700f7af5126c6ae05140a
ms.sourcegitcommit: 8e76be591034b618f5c11f4e66668f48c090ddfd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/29/2019
ms.locfileid: "66357772"
---
# <a name="check-for-pool-and-node-errors"></a>Verificare la presenza di errori in pool e nodi

Durante la creazione e la gestione di pool di Azure Batch, alcune operazioni vengono eseguite immediatamente, mentre altre sono asincrone e vengono eseguite in background. Il loro completamento può richiedere diversi minuti.

Rilevare gli errori per le operazioni che si verificano immediatamente è semplice, in quanto tutti gli eventuali errori vengono restituiti immediatamente dall'API, dall'interfaccia della riga di comando o dall'interfaccia utente.

Questo articolo illustra le operazioni in background che possono verificarsi per pool e nodi di pool e spiega come rilevare ed evitare gli errori.

## <a name="pool-errors"></a>Errori dei pool

### <a name="resize-timeout-or-failure"></a>Timeout ridimensionamento o errore

Durante la creazione di un nuovo pool o il ridimensionamento di un pool esistente, si specifica il numero di nodi di destinazione.  L'operazione viene completata immediatamente, ma l'effettiva allocazione dei nuovi nodi o la rimozione dei nodi esistenti potrebbe richiedere diversi minuti.  Il timeout dell'operazione di ridimensionamento viene specificato nell'API di [creazione](https://docs.microsoft.com/rest/api/batchservice/pool/add) o [ridimensionamento](https://docs.microsoft.com/rest/api/batchservice/pool/resize). Se Azure Batch non riesce a ottenere il numero di nodi di destinazione durante il periodo di timeout del ridimensionamento, interrompe l'operazione. Il pool entra in uno stato stabile e segnala errori di ridimensionamento.

La proprietà [ResizeError](https://docs.microsoft.com/rest/api/batchservice/pool/get#resizeerror) relativa alla valutazione più recente segnala un timeout di ridimensionamento ed elenca gli errori che si sono verificati.

Cause comuni per i timeout di ridimensionamento:

- Il timeout ridimensionamento è troppo breve
  - Nella maggior parte dei casi il timeout predefinito di 15 minuti è sufficiente per completare l'allocazione o la rimozione dei nodi del pool.
  - Se occorre allocare un numero elevato di nodi, è consigliabile impostare il timeout di ridimensionamento su 30 minuti. È il caso ad esempio del ridimensionamento a più di 1.000 nodi da un'immagine di Azure Marketplace o a più di 300 nodi da un'immagine di macchina virtuale personalizzata.
- Quota di core insufficiente
  - Un account Batch può allocare un numero limitato di core in tutti i pool. Quando viene raggiunta la quota limite, Batch smette di allocare nodi. È possibile [aumentare](https://docs.microsoft.com/azure/batch/batch-quota-limit) la quota di core per consentire a Batch di allocare più nodi.
- Indirizzi IP di subnet insufficienti quando un [pool è in una rete virtuale](https://docs.microsoft.com/azure/batch/batch-virtual-network)
  - Una subnet di rete virtuale deve disporre di un numero sufficiente di indirizzi IP non assegnati da allocare a ogni nodo di pool richiesto. In caso contrario non è possibile creare i nodi.
- Risorse insufficienti quando un [pool è in una rete virtuale](https://docs.microsoft.com/azure/batch/batch-virtual-network)
  - Se si creano risorse come servizi di bilanciamento del carico, IP pubblici e gruppi di sicurezza di rete nella stessa sottoscrizione dell'account Batch, verificare che le quote della sottoscrizione siano sufficienti per queste risorse.
- Pool di grandi dimensioni con immagini di macchina virtuale personalizzate
  - L'allocazione di pool di grandi dimensioni che usano immagini di macchina virtuale personalizzate può richiedere più tempo, pertanto possono verificarsi timeout di ridimensionamento.  Per suggerimenti sui limiti e sulla configurazione, vedere [Usare un'immagine personalizzata per creare un pool di macchine virtuali](https://docs.microsoft.com/azure/batch/batch-custom-images).

### <a name="automatic-scaling-failures"></a>Errori di ridimensionamento automatico

Si può anche impostare Azure Batch in modo da ridimensionare automaticamente il numero di nodi in un pool. A questo scopo occorre definire i parametri per la [formula di ridimensionamento automatico per un pool](https://docs.microsoft.com/azure/batch/batch-automatic-scaling). Il servizio Batch usa quindi la formula per valutare periodicamente il numero di nodi nel pool e impostare un nuovo numero di destinazione. Possono verificarsi i tipi di problemi seguenti:

- La valutazione del ridimensionamento automatico non riesce.
- L'operazione di ridimensionamento risultante non riesce con conseguente timeout.
- Un problema nella formula di ridimensionamento automatico genera valori di destinazione dei nodi non corretti. Il ridimensionamento riesce oppure raggiunge il timeout.

È possibile ottenere informazioni sull'ultima valutazione del ridimensionamento automatico usando la proprietà [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/pool/get#autoscalerun). Questa proprietà indica il periodo della valutazione, i valori e il risultato, oltre agli eventuali errori di prestazioni.

L'[evento di completamento del ridimensionamento del pool](https://docs.microsoft.com/azure/batch/batch-pool-resize-complete-event) acquisisce le informazioni su tutte le valutazioni.

### <a name="delete"></a>Delete

Quando si elimina un pool che contiene nodi, Batch elimina prima di tutto i nodi, quindi l'oggetto pool stesso. L'eliminazione dei nodi del pool può richiedere alcuni minuti.

Lo [stato del pool](https://docs.microsoft.com/rest/api/batchservice/pool/get#poolstate) viene impostato su **deleting** durante il processo di eliminazione. L'applicazione chiamante può rilevare se l'eliminazione del pool richiede troppo tempo usando le proprietà **state** e **stateTransitionTime**.

## <a name="pool-compute-node-errors"></a>Errori dei nodi di calcolo dei pool

Anche se Batch alloca correttamente i nodi in un pool, vari problemi possono compromettere l'integrità di alcuni nodi e renderli inutilizzabili. Per questi nodi vengono però addebitati dei costi. È quindi importante individuare i problemi in modo da evitare un esborso per nodi inutilizzabili.

### <a name="start-task-failure"></a>Errore dell'attività di avvio

È possibile specificare un'[attività di avvio](https://docs.microsoft.com/rest/api/batchservice/pool/add#starttask) facoltativa per un pool. Come per qualsiasi attività, è possibile usare una riga di comando e file di risorse da scaricare dallo spazio di archiviazione. Una volta avviata, l'attività di avvio viene eseguita per ogni nodo. La proprietà **waitForSuccess** specifica se Batch deve attendere il corretto completamento dell'attività di avvio prima di pianificare qualsiasi attività su un nodo.

Se il nodo è stato configurato in modo da attendere che l'attività di avvio venga completata correttamente, ma invece questa non riesce, il nodo diventa inutilizzabile, ma resta soggetto ad addebiti.

È possibile rilevare errori nell'attività di avvio mediante le proprietà [result](https://docs.microsoft.com/rest/api/batchservice/computenode/get#taskexecutionresult) e [failureInfo](https://docs.microsoft.com/rest/api/batchservice/computenode/get#taskfailureinformation) della proprietà del nodo [startTaskInfo](https://docs.microsoft.com/rest/api/batchservice/computenode/get#starttaskinformation) di primo livello.

Se un'attività di avvio non riesce, inoltre, Batch imposta lo [stato](https://docs.microsoft.com/rest/api/batchservice/computenode/get#computenodestate) del nodo su **starttaskfailed**, se la proprietà **waitForSuccess** è impostata su **true**.

Come per qualsiasi attività, l'esito negativo di un'attività di avvio può essere riconducibile a vari fattori.  Per risolvere il problema, controllare i file stdout, stderr e qualsiasi altro file di log specifico dell'attività.

### <a name="application-package-download-failure"></a>Errore di download del pacchetto dell'applicazione

È possibile specificare uno o più pacchetti dell'applicazione per un pool. Batch scarica i file di pacchetto specificati in ogni nodo e li decomprime dopo l'avvio del nodo ma prima della pianificazione delle attività. È prassi comune usare la riga di comando di un'attività di avvio insieme ai pacchetti dell'applicazione, ad esempio per copiare file n una posizione diversa o per eseguire il programma di installazione.

La proprietà[errors](https://docs.microsoft.com/rest/api/batchservice/computenode/get#computenodeerror) del nodo indica un errore di download e decompressione di un pacchetto dell'applicazione. Batch imposta lo stato del nodo su **unusable**.

### <a name="container-download-failure"></a>Errore di download di contenitore

È possibile specificare uno o più riferimenti di contenitore in un pool. Batch consente di scaricare i contenitori specificati per ogni nodo. Il nodo [errori](https://docs.microsoft.com/rest/api/batchservice/computenode/get#computenodeerror) segnala un errore durante il download di un contenitore e imposta lo stato del nodo a **inutilizzabile**.

### <a name="node-in-unusable-state"></a>Nodo in stato inutilizzabile

Azure Batch può impostare lo [stato del nodo](https://docs.microsoft.com/rest/api/batchservice/computenode/get#computenodestate) su **unusable** per diversi motivi. Quando lo stato del nodo è impostato su **unusable**, non è possibile pianificare attività sul nodo, il quale però rimane soggetto ad addebiti.

I nodi in un **unsuable**, ma senza [errori](https://docs.microsoft.com/rest/api/batchservice/computenode/get#computenodeerror) stato significa che Batch è in grado di comunicare con la macchina virtuale. In questo caso, Batch tenta sempre di ripristinare la macchina virtuale. Batch non tenterà automaticamente di ripristinare le macchine virtuali che non è riuscito a installare i pacchetti dell'applicazione o i contenitori anche se il relativo stato è **inutilizzabile**.

Se Batch è in grado di determinare la causa, questa viene indicata nella proprietà [errors](https://docs.microsoft.com/rest/api/batchservice/computenode/get#computenodeerror).

Altri esempi di cause di nodi inutilizzabili, con stato **unusable**, includono:

- Un'immagine di macchina virtuale personalizzata non è valida. È il caso ad esempio di un'immagine preparata in modo non corretto.

- Una macchina virtuale viene spostata a causa di un errore di infrastruttura o un aggiornamento di basso livello. Batch recupera il nodo.

- È stata distribuita un'immagine di macchina virtuale su un hardware che non la supporta. Ad esempio un'immagine di macchina virtuale "HPC" in esecuzione su hardware non HPC. Ad esempio, il tentativo di eseguire un'immagine HPC CentOS in una [Standard_D1_v2](../virtual-machines/linux/sizes-general.md#dv2-series) della macchina virtuale.

- Le macchine virtuali sono un [rete virtuale di Azure](batch-virtual-network.md), e il traffico è stato bloccato per porte chiave.

### <a name="node-agent-log-files"></a>File di log dell'agente del nodo

Il processo dell'agente Batch in esecuzione in ogni nodo del pool può fornire file di log che potrebbero risultare utili se occorre contattare il supporto in relazione a un problema in un nodo del pool. I file di log relativi a un nodo possono essere caricati tramite il portale di Azure, Batch Explorer o un'[API](https://docs.microsoft.com/rest/api/batchservice/computenode/uploadbatchservicelogs). È utile caricare e salvare i file di log. In seguito è possibile eliminare il nodo o il pool per evitare un addebito per i nodi in esecuzione.

## <a name="next-steps"></a>Passaggi successivi

Assicurarsi di aver configurato l'applicazione in modo da implementare un sistema completo di controllo degli errori, specialmente per le operazioni asincrone. Rilevare e diagnosticare tempestivamente i problemi può avere un'importanza fondamentale.
