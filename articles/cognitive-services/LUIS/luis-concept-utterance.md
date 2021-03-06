---
title: Espressioni di esempio corrette
titleSuffix: Language Understanding - Azure Cognitive Services
description: Le espressioni sono gli input dell'utente che l'app ha bisogno di interpretare. Raccogliere le frasi che si ritiene verranno immesse dagli utenti. Includere espressioni con lo stesso significato ma con una costruzione diversa in termini di lunghezza e posizione delle parole.
services: cognitive-services
author: diberry
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: conceptual
ms.date: 05/07/2019
ms.author: diberry
ms.openlocfilehash: fdf5508475d868ccb8c271daaac7449d3c940301
ms.sourcegitcommit: 13cba995d4538e099f7e670ddbe1d8b3a64a36fb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "65073161"
---
# <a name="understand-what-good-utterances-are-for-your-luis-app"></a>Comprendere quali sono le espressioni ottimali per l'app LUIS

Le **espressioni** sono gli input dell'utente che l'app ha bisogno di interpretare. Per insegnare a LUIS a estrarre le finalità e le entità, è importante acquisire una varietà di espressioni di esempio diverse per ogni finalità. L'apprendimento attivo, o processo di training continuativo di nuove espressioni, è fondamentale per l'intelligenza con apprendimento automatico fornito da LUIS.

Raccogliere le espressioni che si ritiene verranno immesse dagli utenti. Includere espressioni che hanno lo stesso significato ma vengono costruite in modi diversi:

* Lunghezza dell'espressione - breve, media e lunga per l'applicazione client
* Lunghezza della parola e della frase 
* Posizione della parola - entità all'inizio, nel mezzo e alla fine dell'espressione
* Grammatica 
* Pluralizzazione
* Stemming
* Scelta di sostantivo e verbo
* Punteggiatura - varietà di casi con uso corretto, errato e senza grammatica

## <a name="how-to-choose-varied-utterances"></a>Come scegliere espressioni varie

Di seguito sono descritti alcuni principi da tenere a mente quando si inizia [aggiungendo espressioni di esempio](luis-how-to-add-example-utterances.md) al modello LUIS.

### <a name="utterances-arent-always-well-formed"></a>Le espressioni non sono sempre ben formate

Un'espressione potrebbe essere una frase come "Prenotami un biglietto per Parigi" oppure un frammento di frase, come "Prenotazione" o "Volo Parigi".  Spesso gli utenti fanno errori di ortografia. Quando si pianifica l'app, valutare se eseguire il [Controllo ortografico Bing](luis-tutorial-bing-spellcheck.md) o meno sull'input dell'utente prima di passarlo a LUIS. 

Se non si esegue il controllo ortografico sulle espressioni dell'utente, è necessario formare LUIS sulle espressioni che includono errori di digitazione e di ortografia.

### <a name="use-the-representative-language-of-the-user"></a>Usare il linguaggio rappresentativo dell'utente

Quando si scelgono le espressioni, tenere presente che quello che si ritiene un termine o una frase comune potrebbe non essere corretto per l'utente tipico dell'applicazione client. L'utente potrebbe non avere esperienza nel dominio. Fare attenzione quando si usano termini o frasi che l'utente pronuncerebbe solo se fosse esperto.

### <a name="choose-varied-terminology-as-well-as-phrasing"></a>Scegliere terminologia e frasi alternative

Si noterà che, anche se si fanno sforzi per creare una modelli di frase alternativi, alcuni termini verranno comunque ripetuti.

Considerare queste espressioni di esempio:

|Espressioni di esempio|
|--|
|come ottenere un computer?|
|Dove ottenere un computer?|
|Voglio ottenere un computer, come posso fare?|
|Quando posso ottenere un computer?| 

In questo caso non vengono usate alternative per il termine fondamentale "computer". Usare alternative quali computer desktop, portatile, workstation o anche solo macchina. LUIS deduce in modo intelligente i sinonimi dal contesto, ma quando vengono create espressioni per il training, è comunque preferibile variare.

## <a name="example-utterances-in-each-intent"></a>Espressioni di esempio in ogni finalità

Ogni finalità deve avere almeno 15 espressioni di esempio. Se la finalità non prevede espressioni di esempio, non sarà possibile formare LUIS. Se una finalità contiene una o qualche espressione di esempio, LUIS non è in grado di prevederla con precisione. 

## <a name="add-small-groups-of-15-utterances-for-each-authoring-iteration"></a>Aggiungere piccoli gruppi di 15 espressioni per ogni iterazione di creazione

In ogni iterazione del modello, non aggiungere un'ampia quantità di espressioni. Aggiungere espressioni in gruppi di 15. Ripetere [training](luis-how-to-train.md), [pubblicazione](luis-how-to-publish-app.md) e [test](luis-interactive-test.md).  

LUIS compila modelli efficaci con espressioni selezionate con attenzione dall'autore del modello LUIS. L'aggiunta di un numero eccessivo di espressioni non è utile perché introduce confusione.  

È consigliabile iniziare con poche espressioni, poi [esaminare le espressioni dell'endpoint](luis-how-to-review-endpoint-utterances.md) per prevederne correttamente la finalità e per estrarre l'entità.

## <a name="utterance-normalization"></a>Normalizzazione utterance

Normalizzazione utterance è il processo di ignorare gli effetti dei segni di punteggiatura e i segni diacritici durante il training e stima.

## <a name="utterance-normalization-for-diacritics-and-punctuation"></a>Normalizzazione utterance per i segni diacritici e punteggiatura

Normalizzazione utterance viene definita quando si crea o si importa l'app perché è un'impostazione nel file JSON dell'app. Le impostazioni di normalizzazione utterance sono disattivate per impostazione predefinita. 

I segni diacritici sono contrassegni o segni all'interno del testo, ad esempio: 

```
İ ı Ş Ğ ş ğ ö ü
```

Se l'app attiva la normalizzazione, assegna un punteggio nel **Test** riquadro test in batch e query endpoint verranno apportate modifiche per tutte le espressioni utilizzando i segni diacritici o segni di punteggiatura.

Attivare la normalizzazione utterance per i segni diacritici o la punteggiatura al file app LUIS JSON nel `settings` parametro.

```JSON
"settings": [
    {"name": "NormalizePunctuation", "value": "true"},
    {"name": "NormalizeDiacritics", "value": "true"}
] 
```

Normalizzazione **punteggiatura** significa che, prima che i modelli di corsi di formazione e prima l'endpoint ottenere stimata query, segni di punteggiatura verrà rimossa dalle espressioni. 

Normalizzazione **i segni diacritici** sostituisce i caratteri con accenti in espressioni con caratteri normali. Ad esempio: `Je parle français` diventa `Je parle francais`. 

Normalizzazione non significa che sarà non vedere punteggiatura e i segni diacritici nel espressioni di esempio o le risposte di stima, semplicemente che tali valori verranno ignorati durante il training e stima.


### <a name="punctuation-marks"></a>Segni di punteggiatura

Se la punteggiatura non è normalizzata, LUIS non vengono tralasciate segni di punteggiatura, per impostazione predefinita, in quanto alcune applicazioni client possono effettuare significato in questi contrassegni. Assicurarsi che le espressioni di esempio usino sia lo stile con punteggiatura sia quello senza punteggiatura, in modo che entrambi gli stili restituiscano gli stessi punteggi relativi. 

Se la punteggiatura non ha alcun significato specifico nell'applicazione client, prendere in considerazione [ignorando i segni di punteggiatura](#utterance-normalization) dalla normalizzazione dei segni di punteggiatura. 

### <a name="ignoring-words-and-punctuation"></a>Ignorare parole e punteggiatura

Se si desidera ignorare la punteggiatura nei modelli o parole specifiche, usare una [pattern](luis-concept-patterns.md#pattern-syntax) con il _ignora_ sintassi di parentesi quadre, `[]`. 

## <a name="training-utterances"></a>Eseguire il training sulle espressioni

In genere, il training non è determinante, in quanto la previsione delle espressioni potrebbe variare leggermente a seconda delle versioni o delle app. È possibile rimuovere il training non deterministico aggiornando l'[API delle impostazioni della versione ](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/versions-update-application-version-settings) con la coppia nome/valore `UseAllTrainingData` in modo da usare tutti i dati di training.

## <a name="testing-utterances"></a>Eseguire il test delle espressioni 

Gli sviluppatori devono iniziare il test dell'applicazione LUIS con traffico reale inviando espressioni all'URL dell'[endpoint di stima](luis-how-to-azure-subscription.md). Queste espressioni vengono usate per migliorare le prestazioni di finalità ed entità con l'[esame delle espressioni](luis-how-to-review-endpoint-utterances.md). I test inviati attraverso il riquadro di test del sito Web LUIS non vengono mandati attraverso l'endpoint e pertanto non contribuiscono all'apprendimento attivo. 

## <a name="review-utterances"></a>Esaminare le espressioni

Dopo che il modello è stato formato e pubblicato e dopo aver ricevuto le query dell'[endpoint](luis-glossary.md#endpoint), [esaminare le espressioni](luis-how-to-review-endpoint-utterances.md) inviate da LUIS. LUIS seleziona le espressioni dell'endpoint con punteggi bassi in termini di finalità o entità. 

## <a name="best-practices"></a>Procedure consigliate

Rivedere le [procedure consigliate](luis-concept-best-practices.md) e applicarle come parte del normale ciclo di creazione e modifica.

## <a name="next-steps"></a>Passaggi successivi
Consultare [Add example utterances](luis-how-to-add-example-utterances.md) (Aggiungere espressioni di esempio) per informazioni su come insegnare a un'app LUIS a capire le espressioni degli utenti.

