---
title: Collaborazione
titleSuffix: Language Understanding - Azure Cognitive Services
description: Con le app LUIS è richiesto un singolo proprietario e collaboratori facoltativi per consentire a più persone di creare una singola app.
services: cognitive-services
author: diberry
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: conceptual
ms.date: 06/03/2019
ms.author: diberry
ms.openlocfilehash: 294905ccfd0ce8db6da8737277b0ce978ba837ea
ms.sourcegitcommit: cababb51721f6ab6b61dda6d18345514f074fb2e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2019
ms.locfileid: "66473525"
---
# <a name="collaborating-with-other-authors"></a>Collaborazione con altri autori

Con le app LUIS è richiesto un singolo proprietario e collaboratori facoltativi per consentire a più persone di creare una singola app.

## <a name="luis-account"></a>Account LUIS
Un account LUIS è associato a un singolo account [Microsoft Live](https://login.live.com/). A ogni account LUIS viene assegnata una [chiave di creazione](luis-concept-keys.md#authoring-key) da usare per creare tutte le app LUIS a cui l'account ha accesso. 

Un account LUIS può disporre di più app LUIS.

Per altre informazioni sugli account utente Active Directory vedere [Tenant di Active Directory di Azure](luis-how-to-collaborate.md#azure-active-directory-tenant-user). 

## <a name="luis-app-owner"></a>Proprietario dell'app LUIS

L'account che consente di creare un'app è il proprietario e ogni app ha un solo proprietario. Il proprietario è indicato per l'app **[delle impostazioni](luis-how-to-collaborate.md)** pagina. Il proprietario riceve tramite posta elettronica al 75% del limite mensile di raggiungimento della quota di endpoint. 

## <a name="authorization-roles"></a>Ruoli di autorizzazione
LUIS non supporta i diversi ruoli per proprietari e collaboratori, con un'eccezione. L'account proprietario è l'unico che può eliminare l'app.

Se si desidera controllare l'accesso al modello, l'utente può sezionare il modello in app LUIS più piccole, in cui ogni app ha un numero più ristretto di collaboratori. Usare [Spedisci](https://aka.ms/dispatch-tool) per consentire a un'app LUIS padre di gestire il coordinamento tra le app padre e figlio.

## <a name="transfer-ownership"></a>Trasferire la proprietà
LUIS non consente il trasferimento della proprietà, tuttavia qualsiasi collaboratore può esportare l'app e crearne un'altra importandola. Ricordare che la nuova app dispone di un ID app diverso. La nuova app deve essere sottoposta a training e pubblicata e deve essere utilizzato il nuovo endpoint.

## <a name="luis-app-collaborators"></a>Collaboratori dell'app LUIS
Il proprietario di un'app può aggiungere collaboratori alla stessa. Il proprietario deve aggiungere l'indirizzo di posta elettronica del collaboratore nelle **[impostazioni](luis-how-to-collaborate.md)** dell'app. Il collaboratore dispone dell'accesso completo all'app. Se il collaboratore elimina l'app, viene rimossa dall'account del collaboratore, ma rimane nell'account del proprietario. 

Se si desidera condividere più app con i collaboratori, a ogni app è necessario aggiungere l'indirizzo di posta elettronica del collaboratore. 

## <a name="managing-multiple-authors"></a>Gestione di più autori
Al momento il sito Web [LUIS](luis-reference-regions.md#luis-website) non offre la creazione a livello di transazione. È possibile consentire agli autori di lavorare su versioni indipendenti da una versione base. Le sezioni seguenti descrivono due diversi metodi.

## <a name="manage-multiple-versions-inside-the-same-app"></a>Gestione di più versioni all'interno della stessa app
Eseguire innanzitutto la [clonazione](luis-how-to-manage-versions.md#clone-a-version) da una versione base per ogni autore. 

Ogni autore apporta modifiche alla propria versione dell'app. Dopo che ogni autore è soddisfatto del proprio modello, esportare le nuove versioni in file JSON.  

Le app esportate sono file in formato JSON confrontabili a livello di modifiche. Combinare i file per creare un singolo file JSON della nuova versione. Modificare la proprietà **versionId** nel file JSON affinché indichi la nuova versione unita. Importare la versione nell'app originale. 

Questo metodo consente di disporre di una versione attiva, di una versione di staging e di una versione pubblicata. È possibile confrontare i risultati nel riquadro di test interattivo tra le tre versioni.

## <a name="manage-multiple-versions-as-apps"></a>Gestione di più versioni come app
[Esportare](luis-how-to-manage-versions.md#export-version) la versione base. Ogni autore importa la versione. L'utente che importa l'app è il proprietario della versione. Dopo aver modificato l'app, esportare la versione. 

Le app esportate sono file in formato JSON confrontabili con l'esportazione base a livello di modifiche. Combinare i file per creare un singolo file JSON della nuova versione. Modificare la proprietà **versionId** nel file JSON affinché indichi la nuova versione unita. Importare la versione nell'app originale.

## <a name="collaborator-roles-vs-entity-roles"></a>Ruoli di collaboratore entità di Visual Studio

[I ruoli delle entità](luis-concept-roles.md) applicabili al modello di dati dell'app LUIS. Ruoli di collaboratore si applicano ai livelli di accesso di creazione. 

## <a name="next-steps"></a>Passaggi successivi

Informazioni sui concetti di [controllo delle versioni](luis-concept-version.md). 

Vedere [Impostazioni dell'app](luis-how-to-collaborate.md) per informazioni sulla gestione dei collaboratori nell'app LUIS.

Vedere [Aggiungere l'indirizzo di posta elettronica all'elenco degli accessi](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/58fcccdd5aca2f08a4104342) alle API di creazione.
