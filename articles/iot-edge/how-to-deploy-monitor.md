---
title: Creare distribuzioni automatiche dal portale di Azure - Azure IoT Edge | Microsoft Docs
description: Usare il portale di Azure per creare distribuzioni automatiche per gruppi di dispositivi IoT Edge
keywords: ''
author: kgremban
manager: philmea
ms.author: kgremban
ms.date: 02/19/2019
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.custom: seodec18
ms.openlocfilehash: 69ba0a882c0e52e7c0d063b8f77e7a0fe22526a1
ms.sourcegitcommit: 61c8de2e95011c094af18fdf679d5efe5069197b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62126365"
---
# <a name="deploy-and-monitor-iot-edge-modules-at-scale-using-the-azure-portal"></a>Distribuire e monitorare i moduli di IoT Edge su larga scala tramite il portale di Azure

[!INCLUDE [iot-edge-how-to-deploy-monitor-selector](../../includes/iot-edge-how-to-deploy-monitor-selector.md)]

Azure IoT Edge consente di spostare le attività di analisi sul perimetro e offre un'interfaccia cloud per gestire e monitorare i dispositivi IoT Edge senza dover accedere fisicamente a ciascuno di essi. La possibilità di gestire in remoto i dispositivi è sempre più importante con il progressivo diffondersi di soluzioni IoT (Internet delle cose) sempre più estese e complesse. Azure IoT Edge è progettato per supportare gli obiettivi aziendali, indipendentemente dal numero di dispositivi aggiunti.

È possibile gestire singoli dispositivi e distribuire i moduli in tali dispositivi uno alla volta. Tuttavia, per apportare modifiche ai dispositivi su larga scala, è possibile creare una **distribuzione automatica IoT Edge**, che rientra nella gestione automatica dei dispositivi nell'hub IoT. Le distribuzioni sono processi dinamici che consentono di distribuire più moduli in più dispositivi contemporaneamente, di tenere traccia dello stato e dell'integrità dei moduli, nonché di apportare modifiche all'occorrenza. 

## <a name="identify-devices-using-tags"></a>Identificare i dispositivi tramite tag

Prima di poter creare una distribuzione, è necessario essere in grado di specificare i dispositivi a cui la si vuole applicare. Azure IoT Edge identifica i dispositivi tramite **tag** nel dispositivo gemello. Ogni dispositivo può avere più tag ed è possibile definirli in qualsiasi modo risulti appropriato per una soluzione specifica. Ad esempio, il responsabile di un complesso di edifici intelligenti potrebbe aggiungere a un dispositivo i tag seguenti:

```json
"tags":{
    "location":{
        "building": "20",
        "floor": "2"
    },
    "roomtype": "conference",
    "environment": "prod"
}
```

Per altre informazioni sui dispositivi gemelli e i tag, vedere [Comprendere e usare dispositivi gemelli nell'hub IoT](../iot-hub/iot-hub-devguide-device-twins.md).

## <a name="create-a-deployment"></a>Creare una distribuzione

1. Nel [portale di Azure](https://portal.azure.com) passare all'hub IoT. 
1. Selezionare **IoT Edge**.
1. Selezionare **Add IoT Edge device** (Aggiungi il dispositivo di IoT Edge).

La creazione di una distribuzione prevede cinque passaggi, illustrati nelle sezioni seguenti. 

### <a name="step-1-name-and-label"></a>Passaggio 1: Nome ed etichetta

1. Assegnare alla distribuzione un nome univoco contenente al massimo 128 lettere minuscole. Evitare gli spazi e i seguenti caratteri non validi: `& ^ [ ] { } \ | " < > /`.
1. È possibile aggiungere etichette come coppie chiave-valore per tenere traccia delle distribuzioni. Ad esempio, **PiattaformaHost** e **Linux** oppure **Versione** e **3.0.1**.
1. Selezionare **Avanti** per procedere al passaggio due. 

### <a name="step-2-add-modules-optional"></a>Passaggio 2: Aggiungere moduli (facoltativo)

Esistono due tipi di moduli che è possibile aggiungere a una distribuzione. Il primo è un modulo basato su un servizio di Azure, ad esempio un account di archiviazione o Analisi di flusso. Il secondo è un modulo che usa codice personalizzato. È possibile aggiungere più moduli di entrambi i tipi a una distribuzione. 

Se si crea una distribuzione senza moduli, tutti i moduli correnti vengono rimossi dai dispositivi. 

>[!NOTE]
>Funzioni di Azure non supporta ancora la distribuzione automatica dei servizi di Azure. Usare la distribuzione dei moduli personalizzata per aggiungere manualmente il servizio alla distribuzione. 

Per aggiungere un modulo da Analisi di flusso di Azure, seguire questa procedura:

1. Nella sezione dei **moduli di distribuzione** della pagina fare clic su **Aggiungi**.
1. Selezionare **Azure Stream Analytics module** (Modulo di Analisi di flusso di Azure).
1. Scegliere una voce dall'elenco a discesa **Sottoscrizione**.
1. Scegliere una voce dall'elenco a discesa **Processo Edge**.
1. Selezionare **Save** (Salva) per aggiungere il modulo alla distribuzione. 

Per aggiungere codice personalizzato come modulo o aggiungere manualmente un modulo per un servizio di Azure, seguire questa procedura:

1. Nella sezione **Impostazioni del Registro Container** della pagina specificare i nomi e le credenziali per i registri contenitori privati che contengono le immagini dei moduli per la distribuzione. L'agente di Edge restituisce l'errore 500 se non trova le credenziali del registro contenitori per un'immagine Docker.
1. Nella sezione dei **moduli di distribuzione** della pagina fare clic su **Aggiungi**.
1. Selezionare **Modulo IoT Edge**.
1. Assegnare un nome al modulo in **Name** (Nome).
1. Nel campo **URI immagine** immettere l'immagine del contenitore per il modulo. 
1. Specificare le eventuali **Container Create Options** (Opzioni di creazione container) da passare al contenitore. Per altre informazioni, vedere [docker create](https://docs.docker.com/engine/reference/commandline/create/).
1. Usare il menu a discesa per selezionare **Restart policy** (Criteri di riavvio). È possibile scegliere tra le opzioni seguenti: 
   * **Always** (Sempre): il modulo viene sempre riavviato se viene arrestato per qualsiasi motivo.
   * **Never** (Mai): il modulo non viene mai riavviato se viene arrestato per qualsiasi motivo.
   * **On-failed** (In caso di errore): il modulo viene riavviato in caso di arresto anomalo, ma non se viene chiuso normalmente. 
   * **On-unhealthy** (Se non integro): il modulo viene riavviato in caso di arresto anomalo o se restituisce uno stato non integro. Ogni modulo deve implementare la funzione di stato di integrità. 
1. Usare il menu a discesa per selezionare lo **stato desiderato** per il modulo. È possibile scegliere tra le opzioni seguenti:
   * **Running** (In esecuzione): questa è l'opzione predefinita. Il modulo verrà avviato immediatamente dopo la distribuzione.
   * **Stopped** (Arrestato): dopo la distribuzione, il modulo resta inattivo fino a quando non viene chiamato per l'avvio dall'utente o da un altro modulo.
1. Selezionare **Impostare le proprietà desiderate del modulo gemello** per aggiungere tag o altre proprietà al modulo gemello.
1. Immettere **Variabili di ambiente** per il modulo. Le variabili di ambiente consentono di inserire informazioni supplementari in un modulo facilitando il processo di configurazione.
1. Selezionare **Save** (Salva) per aggiungere il modulo alla distribuzione. 

Dopo aver configurato tutti i moduli per una distribuzione, selezionare **Avanti** per procedere al passaggio tre.

### <a name="step-3-specify-routes-optional"></a>Passaggio 3: Specificare le route (facoltativo)

Le route definiscono le modalità di comunicazione tra i moduli in una distribuzione. Per impostazione predefinita, la procedura guidata presenta una route denominata **route** e definita come **FROM /\* INTO $upstream**, per indicare che i messaggi generati dai moduli vengono inviati all'hub IoT.  

Aggiungere o aggiornare le route con le informazioni riportate in [Dichiarare le route](module-composition.md#declare-routes) e quindi scegliere **Avanti** per proseguire con la sezione di verifica.

### <a name="step-4-specify-metrics-optional"></a>Passaggio 4: Specificare le metriche (facoltativo)

Le metriche forniscono i conteggi di riepilogo dei diversi stati che un dispositivo può segnalare dopo l'applicazione del contenuto della configurazione.

1. Immettere un nome per **Nome della metrica**

1. Immettere una query per **Metric Criteria** (Criteri metrica). La query è basata sulle [proprietà segnalate](module-edgeagent-edgehub.md#edgehub-reported-properties) del modulo gemello hub di IoT Edge. La metrica rappresenta il numero di righe restituite dalla query.

Ad esempio: 

```sql
SELECT deviceId FROM devices
  WHERE properties.reported.lastDesiredStatus.code = 200
```

### <a name="step-5-target-devices"></a>Passaggio 5: Dispositivi di destinazione

Usare la proprietà tags dai dispositivi per selezionare i dispositivi specifici che devono ricevere la distribuzione. 

Dato che più distribuzioni potrebbero avere come destinazione lo stesso dispositivo, è necessario assegnare a ogni distribuzione un numero di priorità. In caso di conflitto, prevale la distribuzione con la priorità più alta, ovvero con il valore più elevato. Se due distribuzioni hanno lo stesso numero di priorità, prevale quella creata più di recente. 

1. Immettere un numero intero positivo in **Priority** (Priorità) per la distribuzione. Nel caso in cui due o più distribuzioni abbiano lo stesso dispositivo di destinazione, verrà applicata quella con valore di priorità più alto.
1. Specificare una condizione in **Target condition** (Condizione di destinazione) per determinare i dispositivi di destinazione di questa distribuzione. La condizione è basata sui tag o sulle proprietà segnalate dei dispositivi gemelli e deve corrispondere al formato di espressione. Ad esempio, `tags.environment='test'` o `properties.reported.devicemodel='4000x'`. 
1. Selezionare **Avanti** per procedere al passaggio finale.

### <a name="step-6-review-deployment"></a>Passaggio 6: Esaminare la distribuzione

Controllare le informazioni sulla distribuzione e quindi selezionare **Submit** (Invia).

## <a name="deploy-modules-from-azure-marketplace"></a>Distribuire i moduli da Azure Marketplace

Azure Marketplace è un marketplace online di servizi e applicazioni dove è possibile trovare un'ampia gamma di soluzioni e applicazioni aziendali certificate e ottimizzate per l'esecuzione in Azure, tra cui i [moduli IoT Edge](https://azuremarketplace.microsoft.com/marketplace/apps/category/internet-of-things?page=1&subcategories=iot-edge-modules). È anche possibile accedere ad Azure Marketplace tramite il portale di Azure scegliendo **Crea una risorsa**.

È possibile installare un modulo IoT Edge da Azure Marketplace o dal portale di Azure:

1. Trovare un modulo e iniziare il processo di distribuzione.

   * Portale di Azure: Trovare un modulo e selezionare **Crea**.

   * Azure Marketplace:

     1. Trovare un modulo e selezionare **Scarica adesso**.
     1. Accettare le condizioni per l'utilizzo e l'informativa sulla privacy del provider selezionando **Continua**.

1. Scegliere la sottoscrizione e l'hub IoT a cui è collegato il dispositivo di destinazione.

1. Scegliere **Distribuisci su vasta scala**.

1. Scegliere se aggiungere il modulo a una nuova distribuzione o a un clone di una distribuzione esistente. In caso di uso di un clone, selezionare la distribuzione esistente nell'elenco.

1. Selezionare **Crea** per continuare il processo di creazione di una distribuzione su vasta scala. È possibile specificare gli stessi dettagli che si indicano per qualsiasi distribuzione.

## <a name="monitor-a-deployment"></a>Monitorare una distribuzione

Per visualizzare i dettagli di una distribuzione e monitorare i dispositivi che la eseguono, seguire questa procedura:

1. Accedere al [portale di Azure](https://portal.azure.com) e passare all'hub IoT. 
1. Selezionare **IoT Edge**.
1. Selezionare **IoT Edge deployments** (Distribuzioni IoT Edge). 

   ![Visualizzare le distribuzioni IoT Edge](./media/how-to-deploy-monitor/iot-edge-deployments.png)

1. Esaminare l'elenco delle distribuzioni. Per ogni distribuzione, è possibile visualizzare i dettagli seguenti:
   * **ID**: nome della distribuzione.
   * **Target condition** (Condizione di destinazione): tag usato per definire i dispositivi di destinazione.
   * **Priority** (Priorità): numero di priorità assegnato alla distribuzione.
   * **System metrics** -  (Metriche di sistema): **Targeted** (Assegnati) specifica il numero di dispositivi gemelli nell'hub IoT che corrispondono alla condizione di destinazione, mentre **Applied** (Applicati) specifica il numero di dispositivi il cui contenuto di distribuzione è stato applicato ai rispettivi dispositivi gemelli nell'hub IoT. 
   * **Metriche del dispositivo**: specifica il numero di dispositivi Edge presenti nella distribuzione che segnalano il completamento dell'operazione o gli errori generati dal runtime del client di IoT Edge.
   * **Metriche personalizzate**: specifica il numero di dispositivi Edge presenti nella distribuzione che segnalano i dati per le metriche definite per la distribuzione.
   * **Creation time** (Data/ora di creazione): timestamp di creazione della distribuzione. Questo timestamp viene usato per stabilire la prevalenza quando due distribuzioni hanno la stessa priorità. 
1. Selezionare la distribuzione che si vuole monitorare.  
1. Esaminare i dettagli della distribuzione. Per esaminare i dettagli della distribuzione sono disponibili schede.

## <a name="modify-a-deployment"></a>Modificare una distribuzione

Quando si modifica una distribuzione, le modifiche vengono replicate immediatamente in tutti i dispositivi di destinazione. 

Se si aggiorna la condizione di destinazione, vengono eseguiti gli aggiornamenti seguenti:

* Se un dispositivo non soddisfa la condizione di destinazione precedente, ma soddisfa la nuova condizione di destinazione e questa distribuzione ha la priorità più alta per il dispositivo, la distribuzione viene applicata al dispositivo. 
* Se un dispositivo che esegue la distribuzione non soddisfa più la condizione di destinazione, disinstalla questa distribuzione e riceve la distribuzione successiva nell'ordine di priorità. 
* Se un dispositivo che esegue la distribuzione non soddisfa più la condizione di destinazione e non soddisfa la condizione di destinazione di tutte le altre distribuzioni, nel dispositivo non viene apportata alcuna modifica. Il dispositivo continua a eseguire i moduli corrente nello stato corrente, ma non è più gestito come parte di questa distribuzione. Quando soddisfa la condizione di destinazione di qualsiasi altra distribuzione, disinstalla questa distribuzione e riceve quella nuova. 

Per modificare una distribuzione, seguire questa procedura: 

1. Accedere al [portale di Azure](https://portal.azure.com) e passare all'hub IoT. 
1. Selezionare **IoT Edge**.
1. Selezionare **IoT Edge deployments** (Distribuzioni IoT Edge). 

   ![Visualizzare le distribuzioni IoT Edge](./media/how-to-deploy-monitor/iot-edge-deployments.png)

1. Selezionare la distribuzione che si vuole modificare. 
1. Apportare modifiche nei campi seguenti: 
   * Condizione di destinazione
   * Metriche: è possibile modificare o eliminare le metriche definite o aggiungerne di nuove.
   * Etichette
   * Priorità
1. Selezionare **Salva**.
1. Seguire i passaggi in [Monitorare una distribuzione](#monitor-a-deployment) per controllare la distribuzione delle modifiche. 

## <a name="delete-a-deployment"></a>Eliminare una distribuzione

Quando si elimina una distribuzione, tutti i dispositivi ricevono la distribuzione successiva nell'ordine di priorità. Se i dispositivi non soddisfano la condizione di destinazione di qualsiasi altra distribuzione, i moduli non vengono rimossi in seguito all'eliminazione della distribuzione. 

1. Accedere al [portale di Azure](https://portal.azure.com) e passare all'hub IoT. 
1. Selezionare **IoT Edge**.
1. Selezionare **IoT Edge deployments** (Distribuzioni IoT Edge). 

   ![Visualizzare le distribuzioni IoT Edge](./media/how-to-deploy-monitor/iot-edge-deployments.png)

1. Usare la casella di controllo per selezionare la distribuzione che si vuole eliminare. 
1. Selezionare **Elimina**.
1. Un messaggio indicherà che questa azione comporta l'eliminazione della distribuzione e il ripristino dello stato precedente per tutti i dispositivi.  Ciò significa che verrà applicata una distribuzione con una priorità più bassa.  Se non viene assegnata alcun'altra distribuzione, i moduli non verranno rimossi. Per rimuovere tutti i moduli dai dispositivi, creare una distribuzione senza moduli e assegnarla agli stessi dispositivi. Selezionare **Yes** (Sì) per continuare. 

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sulla [distribuzione di moduli nei dispositivi perimetrali](module-deployment-monitoring.md).
