---
title: Chiavi di sottoscrizione
titleSuffix: Language Understanding - Azure Cognitive Services
description: LUIS usa due chiavi, la chiave di creazione gratuita per creare il modello e la chiave di endpoint a consumo per l'esecuzione di query sull'endpoint di stima con espressioni utente.
services: cognitive-services
author: diberry
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: conceptual
ms.date: 01/18/2019
ms.author: diberry
ms.openlocfilehash: feb4622be14b51cfa72c33cda6c2477f799758c6
ms.sourcegitcommit: cababb51721f6ab6b61dda6d18345514f074fb2e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2019
ms.locfileid: "66473584"
---
# <a name="authoring-and-query-prediction-endpoint-keys-in-luis"></a>Chiavi di creazione e di endpoint per query di stima in LUIS
LUIS usa due chiavi: [creazione](#programmatic-key) ed [endpoint](#endpoint-key). La chiave di creazione viene creata automaticamente quando si crea l'account LUIS. Quando si è pronti a pubblicare l'app LUIS, è necessario [creare la chiave endpoint](luis-how-to-azure-subscription.md), [assegnarla](luis-how-to-azure-subscription.md) all'app LUIS e [usarla con la query endpoint](#use-endpoint-key-in-query). 

|Chiave|Scopo|
|--|--|
|[Chiave di creazione](#programmatic-key)|Creazione, pubblicazione, gestione di collaboratori, controllo versioni|
|[Chiave endpoint](#endpoint-key)| Query|

È importante creare app LUIS in [regioni](luis-reference-regions.md#publishing-regions) in cui si desidera pubblicare ed eseguire query.

<a name="programmatic-key" ></a>
## <a name="authoring-key"></a>Chiave di creazione

Una chiave di creazione, nota anche come chiave di avvio, viene creata automaticamente quando si crea un account LUIS ed è gratuita. È presente una chiave di creazione per tutte le app LUIS per ogni [regione](luis-reference-regions.md) di creazione. La chiave di creazione viene fornita per creare l'app LUIS o per testare le query endpoint. 

Per trovare la chiave di creazione, accedere a [LUIS](luis-reference-regions.md#luis-website) e fare clic sul nome dell'account nella barra di spostamento superiore destra per aprire **Account Settings** (Impostazioni account).

![chiave di creazione](./media/luis-concept-keys/programatic-key.png)

Per eseguire **query endpoint di produzione**, creare la [sottoscrizione LUIS](https://azure.microsoft.com/pricing/details/cognitive-services/language-understanding-intelligent-services/). 

> [!CAUTION]
> Per praticità, molti degli esempi usano la chiave di creazione poiché fornisce alcune chiamate endpoint nella relativa [quota](luis-boundaries.md#key-limits).  

## <a name="endpoint-key"></a>Chiave endpoint
Per eseguire **query endpoint di produzione**, creare una risorsa di Azure e assegnarla all'app LUIS. 

[!INCLUDE [Azure resource creation for Language Understanding and Cognitive Service resources](../../../includes/cognitive-services-luis-azure-resource-instructions.md)]

Al termine del processo di creazione della risorsa di Azure, [assegnare la chiave](luis-how-to-azure-subscription.md) all'app. 

* La chiave endpoint consente una quota di accessi endpoint in base al piano di utilizzo specificato durante la creazione della chiave. Per informazioni sui prezzi, vedere [Prezzi dei Servizi cognitivi](https://azure.microsoft.com/pricing/details/cognitive-services/language-understanding-intelligent-services/?v=17.23h).

* La chiave endpoint può essere usata per tutte le app LUIS o per app LUIS specifiche. 

* Non usare la chiave endpoint per la creazione di app LUIS. 

## <a name="use-endpoint-key-in-query"></a>Usare la chiave endpoint nella query
L'endpoint LUIS accetta due stili di query, entrambi usano la chiave endpoint, ma in posizioni diverse:

|Verbo|URL di esempio e posizione della chiave|
|--|--|
|[GET](https://westus.dev.cognitive.microsoft.com/docs/services/5819c76f40a6350ce09de1ac/operations/5819c77140a63516d81aee78)|`https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/df67dcdb-c37d-46af-88e1-8b97951ca1c2?subscription-key=your-endpoint-key-here&verbose=true&timezoneOffset=0&q=turn%20on%20the%20lights`<br><br>valore stringa di query per `subscription-key`<br><br>Modificare il valore della query endpoint per `subscription-key` dalla chiave di creazione (avvio) alla nuova chiave endpoint per usare il limite di quota della chiave endpoint LUIS. Se si crea e si assegna la chiave, ma non si modifica il valore della query endpoint per `subscription-key`, non si usa la quota della chiave endpoint.|
|[POST](https://westus.dev.cognitive.microsoft.com/docs/services/5819c76f40a6350ce09de1ac/operations/5819c77140a63516d81aee79)| `https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/df67dcdb-c37d-46af-88e1-8b97951ca1c2`<br><br> valore intestazione per `Ocp-Apim-Subscription-Key`<br><br>Modificare il valore della query endpoint per `Ocp-Apim-Subscription-Key` dalla chiave di creazione (avvio) alla nuova chiave endpoint per usare il limite di quota della chiave endpoint LUIS. Se si crea e si assegna la chiave, ma non si modifica il valore della query endpoint per `Ocp-Apim-Subscription-Key`, non si usa la quota della chiave endpoint.|

L'ID app usato nell'URL precedente, `df67dcdb-c37d-46af-88e1-8b97951ca1c2`, è l'app IoT pubblica usata per la [dimostrazione interattiva](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/). 

## <a name="api-usage-of-ocp-apim-subscription-key"></a>Uso API di Ocp-Apim-Subscription-Key
Le API LUIS usano l'intestazione, `Ocp-Apim-Subscription-Key`. Il nome dell'intestazione non cambia in base alla chiave e al set di API in uso. Impostare l'intestazione sulla chiave di creazione per le API di creazione. Se si utilizza l'endpoint, impostare l'intestazione sulla chiave endpoint. 

Non è possibile passare la chiave endpoint per le API di creazione. Se si tenta questa operazione, si riceve l'errore 401 (accesso negato a causa di una chiave endpoint non valida). 

## <a name="key-limits"></a>Limiti delle chiavi
Vedere [Limiti delle chiavi](luis-boundaries.md#key-limits) e [Regioni di Azure](luis-reference-regions.md). La chiave di creazione è gratuita. La chiave endpoint LUIS presenta un livello gratuito, ma deve essere creata e associata all'app LUIS nella pagina **Publish** (Pubblica). Non può essere usata per la creazione, ma solo per le query endpoint.

Le regioni di pubblicazione sono diverse dalle regioni di creazione. Assicurarsi di creare un'app nella regione di creazione corrispondente alla regione di pubblicazione desiderata.

## <a name="key-limit-errors"></a>Errori relativi ai limiti delle chiavi
Se si supera la quota al secondo, viene visualizzato un errore HTTP 429. Se si supera la quota al mese, viene visualizzato un errore HTTP 403. Correggere questi errori ottenendo una chiave [endpoint](#endpoint-key) LUIS, [assegnando](luis-how-to-azure-subscription.md) la chiave all'app nella pagina **Publish** (Pubblica) del sito Web [LUIS](luis-reference-regions.md#luis-website).

## <a name="assignment-of-the-endpoint-key"></a>Assegnazione della chiave endpoint

È possibile [assegnare](luis-how-to-azure-subscription.md) la chiave endpoint nel [portale LUIS](https://www.luis.ai) o tramite le API corrispondenti. 


## <a name="next-steps"></a>Passaggi successivi

* Ulteriori informazioni sui [concetti](luis-how-to-azure-subscription.md) relativi a chiavi di creazione ed endpoint.
