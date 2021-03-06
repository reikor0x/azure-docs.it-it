---
title: File di inclusione
description: File di inclusione
services: event-hubs
author: sethmanheim
ms.service: event-hubs
ms.topic: include
ms.date: 05/22/2019
ms.author: spelluru
ms.custom: include file
ms.openlocfilehash: 3f3b60c3744ce9dea61054b3fa0aaccfea27d784
ms.sourcegitcommit: 509e1583c3a3dde34c8090d2149d255cb92fe991
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2019
ms.locfileid: "66238705"
---
Nella tabella seguente sono elencate le quote e i limiti specifici di [Hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/). Per informazioni sui prezzi di Hub eventi, vedere [Prezzi di Hub eventi](https://azure.microsoft.com/pricing/details/event-hubs/).

| Limite | `Scope` | Note | Value |
| --- | --- | --- | --- |
| Numero di spazi dei nomi di Hub eventi per sottoscrizione |Sottoscrizione |- |100 |
| Numero di hub eventi per ogni spazio dei nomi |Spazio dei nomi |Le successive richieste per la creazione di un nuovo hub eventi vengono rifiutate. |10 |
| Numero di partizioni per hub eventi |Entità |- |32 |
| Numero di gruppi consumer per hub eventi |Entità |- |20 |
| Numero di connessioni AMQP per spazio dei nomi |Spazio dei nomi |Le successive richieste di connessioni aggiuntive vengono rifiutate e il codice chiamante riceve un'eccezione. |5.000 |
| Dimensione massima degli eventi di Hub eventi|Entità |- |1 MB |
| Dimensione massima del nome di un hub eventi |Entità |- |50 caratteri |
| Numero di ricevitori non epoch per gruppo consumer |Entità |- |5 |
| Periodo di conservazione massimo dei dati dell'evento |Entità |- |1-7 giorni |
| Numero massimo di unità di velocità effettiva |Spazio dei nomi |Che superano il limite di unità elaborate provoca il limitazione dei dati e genera una [eccezioni di server occupato](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception). Per richiedere un numero maggiore di unità elaborate per un livello Standard, file di un [richiesta di supporto](/azure/azure-supportability/how-to-create-azure-support-request). Le [unità elaborate aggiuntive](../articles/event-hubs/event-hubs-auto-inflate.md) sono disponibili in blocchi da 20 in base a un acquisto con impegno. |20 |
| Numero di regole di autorizzazione per spazio dei nomi |Spazio dei nomi|Le successive richieste di creazione della regola di autorizzazione vengono rifiutate.|12 |
| Numero di chiamate al metodo GetRuntimeInformation | Entità | - | 50 al secondo | 

### <a name="event-hubs-dedicated---quotas-and-limits"></a>Dedicato di hub eventi - quote e limiti
L'offerta dedicato di hub eventi viene fatturato a un prezzo mensile fisso, con un minimo di 4 ore di utilizzo. Il livello dedicato offre tutte le funzionalità del piano Standard, ma con capacità su scala aziendale e i limiti per i clienti con carichi di lavoro intensi. 

| Funzionalità | Limiti |
| --- | ---|
| Larghezza di banda |  20 unità di capacità |
| Spazi dei nomi | 50 per ogni unità di capacità |
| Hub eventi |  Nessun limite per hub eventi e gli argomenti |
| Eventi in ingresso | Incluso |
| Dimensioni del messaggio | 1 milione di byte |
| Partitions | 2000 per unità di capacità |
| Gruppi di consumer | Nessun limite per ogni unità di capacità, 1000 per hub eventi |
| Connessioni negoziate | 100 K incluse |
| Conservazione dei messaggi | 90 giorni, 10 TB, incluse per ogni unità di capacità |
| Acquisizione | Incluso |
