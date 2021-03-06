---
title: Piani tariffari di Database di Azure per PostgreSQL - Server singolo
description: Questo articolo descrive i piani tariffari per il Database di Azure per PostgreSQL - singolo Server.
author: jan-eng
ms.author: janeng
ms.service: postgresql
ms.topic: conceptual
ms.date: 5/6/2019
ms.openlocfilehash: ed534f910fa1e44d3d53ab61ee86378eba788036
ms.sourcegitcommit: 509e1583c3a3dde34c8090d2149d255cb92fe991
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2019
ms.locfileid: "66240391"
---
# <a name="pricing-tiers-in-azure-database-for-postgresql---single-server"></a>Piani tariffari in Database di Azure per PostgreSQL - Server singolo

È possibile creare un server di Database di Azure per PostgreSQL in uno dei tre piani tariffari disponibili: piani Basic, Per utilizzo generico e Con ottimizzazione per la memoria. I piani tariffari si differenziano per le risorse di calcolo in vCore di cui è possibile effettuare il provisioning, per la memoria in ogni vCore e per la tecnologia usata per l'archiviazione dei dati. Il provisioning di tutte le risorse viene effettuato a livello di server PostgreSQL. Un server può avere uno o più database.

|    | **Basic** | **Utilizzo generico** | **Con ottimizzazione per la memoria** |
|:---|:----------|:--------------------|:---------------------|
| Generazione di calcolo | Generazione 4, Generazione 5 | Generazione 4, Generazione 5 | Generazione 5 |
| vCore | 1, 2 | 2, 4, 8, 16, 32, 64 |2, 4, 8, 16, 32 |
| Memoria per vCore | 2 GB | 5 GB | 10 GB |
| Dimensioni della risorsa di archiviazione | Da 5 GB a 1 TB | Da 5 GB a 4 TB | Da 5 GB a 4 TB |
| Tipo di archiviazione | Archiviazione Standard di Azure | Archiviazione Premium di Azure | Archiviazione Premium di Azure |
| Periodo di conservazione dei backup dei database | Da 7 a 35 giorni | Da 7 a 35 giorni | Da 7 a 35 giorni |

Per scegliere un piano tariffario, usare la tabella seguente come punto di partenza.

| Piano tariffario | Carichi di lavoro di destinazione |
|:-------------|:-----------------|
| Basic | Carichi di lavoro con esigenze di calcolo e di prestazioni I/O ridotte. Ad esempio, server usati per lo sviluppo o i test oppure applicazioni su scala ridotta usate raramente. |
| Utilizzo generico | La maggior parte dei carichi di lavoro aziendali che richiedono risorse di calcolo e di memoria bilanciate con velocità effettiva di I/O scalabile. Ad esempio, server per l'hosting di app Web e di app per dispositivi mobili e altre applicazioni aziendali.|
| Con ottimizzazione per la memoria | Carichi di lavoro di database ad alte prestazioni che richiedono prestazioni in memoria per l'elaborazione più rapida delle transazioni e una concorrenza maggiore. Ad esempio, server per l'elaborazione di dati in tempo reale e app transazionali o analitiche a prestazioni elevate.|

Dopo aver creato un server, il numero di vCore, la generazione dell'hardware e il piano tariffario (ad eccezione del passaggio da/a Basic) possono essere aumentati o ridotti in pochi secondi. È anche possibile aumentare autonomamente lo spazio di archiviazione e aumentare o ridurre il periodo di conservazione dei backup senza tempi di inattività per le applicazioni. Non è possibile modificare il tipo di archiviazione dei backup dopo aver creato il server. Per altre informazioni, vedere la sezione [Ridimensionare le risorse](#scale-resources).

## <a name="compute-generations-and-vcores"></a>Generazioni di calcolo e vCore

Le risorse di calcolo vengono fornite come vCore, che rappresentano la CPU logica dell'hardware sottostante. Cina orientale 1, 1 Nord China, US DoD Central e US DoD East utilizzare CPU logiche generazione 4 basati su Intel E5-2673 v3 processori 2,4 GHz (Haswell). Tutte le altre aree usano CPU logiche generazione 5 basati su Intel E5-2673 v4 (Broadwell) a 2,3GHz processori.

## <a name="storage"></a>Archiviazione

Lo spazio di archiviazione di cui si esegue il provisioning è la capacità di archiviazione disponibile per il server Database di Azure per PostgreSQL. Lo spazio di archiviazione viene usato per i file del database, i file temporanei, i log delle transazioni e i log del server PostgreSQL. Lo spazio di archiviazione totale di cui si effettua il provisioning definisce anche la capacità di I/O disponibile per il server.

|    | **Basic** | **Utilizzo generico** | **Con ottimizzazione per la memoria** |
|:---|:----------|:--------------------|:---------------------|
| Tipo di archiviazione | Archiviazione Standard di Azure | Archiviazione Premium di Azure | Archiviazione Premium di Azure |
| Dimensioni della risorsa di archiviazione | Da 5 GB a 1 TB | Da 5 GB a 4 TB | Da 5 GB a 4 TB |
| Dimensioni di incremento dell'archiviazione | 1 GB | 1 GB | 1 GB |
| IOPS | Variabile |3 operazioni di I/O al secondo/GB<br/>Min 100 operazioni di I/O al secondo<br/>Massimo 6000 operazioni di I/O al secondo | 3 operazioni di I/O al secondo/GB<br/>Min 100 operazioni di I/O al secondo<br/>Massimo 6000 operazioni di I/O al secondo |

È possibile aggiungere capacità di archiviazione durante e dopo la creazione del server e consentire al sistema di aumento delle dimensioni di archiviazione automaticamente in base all'utilizzo di archiviazione del carico di lavoro. Il piano Basic non offre la garanzia relativa alle operazioni di I/O al secondo. Nei piani tariffari Utilizzo generico e Con ottimizzazione per la memoria, la scalabilità delle operazioni di I/O al secondo rispetto allo spazio di archiviazione sottoposto a provisioning è in un rapporto di 3 a 1.

È possibile monitorare il consumo di I/O nel portale di Azure oppure usando i comandi dell'interfaccia della riga di comando di Azure. Le metriche pertinenti al monitoraggio sono il [limite di archiviazione, la percentuale di archiviazione, lo spazio di archiviazione usato e la percentuale di I/O](concepts-monitoring.md).

### <a name="reaching-the-storage-limit"></a>Raggiungimento del limite di archiviazione

Server con meno di 100 GB effettuato il provisioning di archiviazione vengono contrassegnati in sola lettura se la memoria disponibile è inferiore a 512MB o del 5% le dimensioni di archiviazione con provisioning. I server con più di 100 GB effettuato il provisioning di archiviazione sono contrassegnati lettura solo quando la memoria disponibile è inferiore a 5 GB.

Ad esempio, se è stato effettuato il provisioning di 110 GB di spazio di archiviazione e l'utilizzo effettivo utilizzato supera 105 GB, il server è di sola lettura. In alternativa, se è stato eseguito il provisioning di 5 GB di spazio di archiviazione, il server viene contrassegnato come sola lettura quando lo spazio di archiviazione libero raggiunge almeno 512 MB.

Quando il server è impostato come di sola lettura, tutte le sessioni esistenti vengono disconnesse e viene eseguito il rollback delle transazioni non sottoposte a commit. Eventuali operazioni di scrittura e di esecuzione del commit delle transazioni hanno esito negativo. Tutte le query in lettura funzioneranno senza interruzioni.  

È possibile aumentare lo spazio di archiviazione sottoposto a provisioning per il server o avviare una nuova sessione in modalità lettura/scrittura ed eliminare i dati per recuperare spazio di archiviazione. Se si esegue `SET SESSION CHARACTERISTICS AS TRANSACTION READ WRITE;` la sessione corrente viene impostata sulla modalità di lettura/scrittura. Per evitare il danneggiamento dei dati, non eseguire operazioni di scrittura quando il server è ancora in stato di sola lettura.

Si consiglia di abilitare archiviazione l'aumento automatico o configurare un avviso per ricevere una notifica quando l'archiviazione server sta per raggiungere la soglia così è possibile evitare di trovarsi nello stato di sola lettura. Per altre informazioni, vedere la documentazione sulla [procedura di configurazione di un avviso](howto-alert-on-metric.md).

### <a name="storage-auto-grow"></a>Archiviazione l'aumento automatico

Se l'aumento automatico di archiviazione è abilitata, lo spazio di archiviazione si espande automaticamente senza conseguenze per il carico di lavoro. Per i server con meno di 100 GB effettuato il provisioning di archiviazione, le dimensioni di archiviazione sottoposte a provisioning vengano aumentata da 5 GB, non appena la memoria disponibile è di sotto di maggiore di 1 GB o 10% dello spazio di archiviazione con provisioning. Per i server con più di 100 GB di spazio di archiviazione, le dimensioni di archiviazione con provisioning aumenta del 5% quando lo spazio di archiviazione disponibile è inferiore al 5% le dimensioni di archiviazione con provisioning. Si applicano i limiti di spazio di archiviazione massimo come specificato in precedenza.

Ad esempio, se è stato effettuato il provisioning di 1000 GB di spazio di archiviazione e l'utilizzo effettivo utilizzato supera 950 GB, le dimensioni di archiviazione di server è stato aumentato a 1050 GB. In alternativa, se è stato eseguito il provisioning di 10 GB di spazio di archiviazione, le dimensioni di archiviazione sono aumenta fino a 15 GB quando minore di 1 GB di spazio di archiviazione è gratuito.

## <a name="backup"></a>Backup

Il servizio esegue automaticamente il backup del server. Il periodo di conservazione minimo dei backup è di sette giorni. È possibile impostare un periodo di conservazione massimo di 35 giorni. È possibile modificare il periodo di conservazione in qualsiasi momento durante il ciclo di vita del server. È possibile scegliere tra backup con ridondanza locale e backup con ridondanza geografica. Anche i backup con ridondanza geografica vengono archiviati nell'[area geografica abbinata](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) all'area in cui è stato creato il server. Questa ridondanza consente un livello di protezione in caso di emergenza. È anche possibile ripristinare il server in qualsiasi altra area di Azure in cui sia disponibile il servizio con backup con ridondanza geografica. Non è possibile cambiare opzione di archiviazione dei backup dopo aver creato il server.

## <a name="scale-resources"></a>Ridimensionare le risorse

Dopo aver creato il server, è possibile modificare in modo indipendente il numero di vCore, la generazione dell'hardware, il piano tariffario (ad eccezione del passaggio da/a Basic), lo spazio di archiviazione e il periodo di conservazione dei backup. Non è possibile modificare il tipo di archiviazione dei backup dopo aver creato il server. Il numero di vCore può essere aumentato o ridotto. Il periodo di conservazione dei backup può essere aumentato o ridotto da 7 a 35 giorni. Le dimensioni dello spazio di archiviazione possono essere solo aumentate. Il ridimensionamento delle risorse può essere eseguito tramite il portale o l'interfaccia della riga di comando di Azure. Per un esempio di ridimensionamento tramite l'interfaccia della riga di comando di Azure, vedere [Monitorare e scalare un server di Database di Azure per PostgreSQL usando l'interfaccia della riga di comando di Azure](scripts/sample-scale-server-up-or-down.md).

Quando si modifica il numero di vCore, la generazione dell'hardware o il piano tariffario, viene creata una copia del server di origine con la nuova allocazione del calcolo. Quando il nuovo server è in esecuzione, le connessioni vengono trasferite al nuovo server. Durante l'intervallo nel quale il sistema passa al nuovo server, non è possibile stabilire nuove connessioni e viene effettuato il rollback di tutte le transazioni di cui non è stato eseguito il commit. Questo intervallo è variabile, ma nella maggior parte dei casi è inferiore al minuto.

Il ridimensionamento dello spazio di archiviazione e la modifica del periodo di conservazione dei backup sono realmente operazioni online. Non si registrano tempi di inattività e l'applicazione non viene influenzata. Le operazioni di I/O al secondo vengono ridimensionate in funzione dello spazio di archiviazione sottoposto a provisioning, quindi è possibile aumentare le operazioni di I/O al secondo disponibili per il server aumentando lo spazio di archiviazione.

## <a name="pricing"></a>Prezzi

Per le informazioni più aggiornate sui prezzi, vedere la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/PostgreSQL/). Per informazioni sui costi della configurazione desiderata, consultare la scheda **Piano tariffario** del [portale di Azure](https://portal.azure.com/#create/Microsoft.PostgreSQLServer) che illustra il costo mensile in base alle opzioni selezionate. Se non è disponibile una sottoscrizione di Azure, è possibile usare il calcolatore dei prezzi di Azure per ottenere una stima. Passare al sito Web del [calcolatore dei prezzi di Azure](https://azure.microsoft.com/pricing/calculator/), selezionare **Aggiungi elementi**, espandere la categoria **Database** e scegliere **Database di Azure per PostgreSQL** per personalizzare le opzioni.

## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni su come [creare un server PostgreSQL nel portale](tutorial-design-database-using-azure-portal.md).
- Informazioni sui [limiti dei servizi](concepts-limits.md). 
- Altre informazioni su come [ampliare un livello di servizio con repliche in lettura](howto-read-replicas-portal.md).
