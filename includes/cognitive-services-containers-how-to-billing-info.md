---
author: diberry
ms.author: diberry
ms.service: cognitive-services
ms.topic: include
ms.date: 04/16/2019
ms.openlocfilehash: 05961f8dd2788179a15e6bfe094484cf4770067b
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66124291"
---
Le query sul contenitore vengono fatturate secondo il piano tariffario della risorsa di Azure usata per `<ApiKey>`.

I contenitori di Servizi cognitivi di Azure non vengono concessi in licenza per l'esecuzione senza connessione all'endpoint di fatturazione per la misurazione. È necessario consentire ai contenitori di comunicare sempre le informazioni di fatturazione all'endpoint di fatturazione. I contenitori di Servizi cognitivi non inviano a Microsoft i dati dei clienti, ad esempio l'immagine o il testo analizzato. 

### <a name="connect-to-azure"></a>Connect to Azure

Per eseguire il contenitore, sono necessari i valori dell'argomento di fatturazione. Questi valori consentono al contenitore di connettersi all'endpoint di fatturazione. Il contenitore segnala l'utilizzo ogni 10-15 minuti. Se il contenitore non si connette ad Azure entro la finestra temporale consentita, continuerà a essere eseguito ma non fornirà query finché l'endpoint di fatturazione non verrà ripristinato. Il tentativo di connessione viene effettuato 10 volte nello stesso intervallo di tempo di 10-15 minuti. Se non è possibile stabilire la connessione con l'endpoint di fatturazione entro i 10 tentativi, l'esecuzione del contenitore verrà arrestata. 

### <a name="billing-arguments"></a>Argomenti di fatturazione

Per avviare il contenitore con il comando `docker run`, è necessario che vengano specificate tutte e tre le opzioni seguenti con valori validi.

| Opzione | DESCRIZIONE |
|--------|-------------|
| `ApiKey` | La chiave API della risorsa di Servizi cognitivi usata per tenere traccia delle informazioni di fatturazione.<br/>Il valore di questa opzione deve essere impostato su una chiave API per la risorsa di cui è stato effettuato il provisioning specificata in `Billing`. |
| `Billing` | L'endpoint della risorsa di Servizi cognitivi usata per tenere traccia delle informazioni di fatturazione.<br/>Il valore di questa opzione deve essere impostato sull'URI dell'endpoint di una risorsa di Azure di cui è stato effettuato il provisioning.|
| `Eula` | Indica che è la licenza per il contenitore è stata accettata.<br/>Il valore di questa opzione deve essere impostato su `accept`. |


