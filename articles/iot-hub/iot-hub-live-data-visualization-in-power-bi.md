---
title: Visualizzazione in tempo reale dei dati del sensore dall'hub IoT di Azure - Power BI | Microsoft Docs
description: Usare Power BI per visualizzare i dati di temperatura e umidità raccolti dal sensore e inviati all'hub IoT di Azure.
author: robinsh
keywords: visualizzazione dei dati in tempo reale, visualizzazione dei dati dal vivo, visualizzazione dei dati del sensore
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 4/11/2018
ms.author: robinsh
ms.openlocfilehash: 7c770aced36e4c90f654de8d31c12d55ad80c8d0
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60780122"
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a>Visualizzare i dati del sensore in tempo reale da IoT Hub di Azure tramite Power BI

![Diagramma end-to-end](./media/iot-hub-live-data-visualization-in-power-bi/1_end-to-end-diagram.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

Informazioni su come visualizzare i dati del sensore in tempo reale che l'hub IoT di Azure riceve usando Power BI. Se si vuole provare a visualizzare i dati nell'hub IoT con App Web, consultare [Usare App Web di Azure per visualizzare i dati del sensore in tempo reale da Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).

## <a name="what-you-do"></a>Operazioni da fare

* Preparare l'hub IoT per l'accesso dei dati mediante l'aggiunta di un gruppo di consumer.

* Creare, configurare ed eseguire un processo di analisi di flusso per il trasferimento dei dati dall'hub IoT all'account Power BI.

* Creare e pubblicare un report di Power BI per visualizzare i dati.

## <a name="what-you-need"></a>Elementi necessari

* Completare la [simulatore online Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md) esercitazione, oppure una delle esercitazioni dispositivo; ad esempio [Raspberry Pi con Node. js](iot-hub-raspberry-pi-kit-node-get-started.md). Questi descrivono i requisiti seguenti:
  
  * Una sottoscrizione di Azure attiva.
  * Un hub IoT di Azure nella sottoscrizione.
  * Un'applicazione client che invia messaggi ad Azure IoT hub.

* Un account di Power BI. ([Provare gratuitamente Power BI](https://powerbi.microsoft.com/))

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Configurare, configurare ed eseguire un processo di analisi di flusso

Iniziare creando un processo di Analisi di flusso. Dopo aver creato il processo, definire gli input, gli output e la query usata per recuperare i dati.

### <a name="create-a-stream-analytics-job"></a>Creare un processo di Analisi di flusso.

1. Nel [portale di Azure](https://portal.azure.com) fare clic su **Crea una risorsa** > **Internet delle cose** > **Processo di Analisi di flusso**.

2. Immettere le seguenti informazioni per il processo.

   **Nome processo**: Nome del processo. Il nome deve essere univoco a livello globale.

   **Gruppo di risorse**: usare lo stesso gruppo di risorse usato dall'hub IoT.

   **Località**: usare lo stesso percorso del gruppo di risorse.

   **Aggiungi al dashboard**: selezionare questa opzione per semplificare l'accesso all'hub IoT dal dashboard.

   ![Creare un processo di analisi di flusso in Azure](./media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

3. Fare clic su **Create**(Crea).

### <a name="add-an-input-to-the-stream-analytics-job"></a>Aggiungere un input al processo di analisi di flusso

1. Aprire il processo di analisi di flusso.

2. In **Topologia processo** fare clic su **Input**.

3. Nel riquadro **Input** fare clic su **Aggiungi input del flusso**, quindi immettere le informazioni seguenti:

   **Alias di input**: l'alias univoco per l'input e selezionare **Specificare le impostazioni dell'hub IoT manualmente** sotto.

   **Origine**: Selezionare **Hub IoT**.
   
   **Endpoint**: fare clic su **Messaggistica**.

   **Gruppo di consumer**: selezionare il gruppo di consumer appena creato.

4. Fare clic su **Create**(Crea).

   ![Aggiungere un input al processo di analisi di flusso in Azure](./media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-to-the-stream-analytics-job"></a>Aggiungere un output al processo di Analisi di flusso

1. In **Topologia processo** fare clic su **Output**.

2. Nel riquadro **Output** fare clic su **Aggiungi** e **Power BI**, quindi immettere le informazioni seguenti:

   **Alias di output**: l'alias univoco per l'output.

   **Area di lavoro del gruppo**: selezionare l'area di lavoro del gruppo di destinazione.

   **Nome del set di dati**: immettere un nome per il set di dati.

   **Nome della tabella**: Immettere un nome per la tabella.

3. Fare clic su **Autorizza** e quindi accedere all'account di Power BI.

4. Fare clic su **Create**(Crea).

   ![Aggiungere un output al processo di analisi di flusso in Azure](./media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-the-query-of-the-stream-analytics-job"></a>Configurare la query del processo di Analisi di flusso

1. In **Topologia processo** fare clic su **Query**.

2. Sostituire `[YourInputAlias]` con l'alias di input del processo.

3. Sostituire `[YourOutputAlias]` con l'alias di output del processo.

4. Fare clic su **Save**.

   ![Aggiungere una query al processo di analisi di flusso in Azure](./media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-the-stream-analytics-job"></a>Eseguire il processo di Analisi di flusso

Nel processo di analisi di flusso, **Avvia** > **Ora** > **Avvia**. Dopo aver avviato correttamente il processo, lo stato del processo passa da **Interrotto** a **In esecuzione**.

![Eseguire un processo di analisi di flusso in Azure](./media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-to-visualize-the-data"></a>Creare e pubblicare un report di Power BI per visualizzare i dati

1. Verificare che l'applicazione di esempio sia in esecuzione nel dispositivo. Se non lo fosse, è possibile fare riferimento alle esercitazioni descritte in [Configurare il dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).

2. Accedere all'account [Power BI](https://powerbi.microsoft.com/en-us/).

3. Fare clic sull'area di lavoro che è stata usata, **Area di lavoro personale**.

4. Fare clic su **Set di dati**.

   Dovrebbero essere visualizzati i set di dati specificati quando è stato creato l'output per il processo di Analisi di flusso.

5. Per il set di dati creato, fare clic su **Aggiungi report** (la prima icona a destra del nome del set di dati).

   ![Creare un report di Microsoft Power BI](./media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

6. Creare un grafico a linee per visualizzare la temperatura in tempo reale nel tempo.

   1. Nella pagina di creazione del report, aggiungere un grafico a linee.

   2. Nel riquadro **Campi** espandere la tabella specificata durante la creazione di output per il processo di analisi di flusso.
   
   3. Trascinare **EventEnqueuedUtcTime** in **Asse** sul riquadro **Visualizzazioni**.
   
   4. Trascinare la **temperatura** in **Valori**.

      Viene creato un grafico a linee. L'asse x mostra data e ora per il fuso orario UTC. L'asse y mostra la temperatura dal sensore.

      ![Aggiungere un grafico a linee per la temperatura a un report di Microsoft Power BI](./media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

7. Creare un altro grafico a linee in modo da visualizzare in tempo reale l'umidità nel tempo. A tale scopo, attenersi alla stessa procedura precedente e inserire **EventEnqueuedUtcTime** sull'asse x e l'**umidità** sull'asse y.

   ![Aggiungere un grafico a linee per l'umidità a un report di Microsoft Power BI](./media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

8. Fare clic su **Salva** per salvare il report.

9. Fare clic su **Report** nel riquadro sinistro, quindi sul report appena creato.

10. Fare clic su **File** > **Pubblica sul Web**.

11. Fare clic su **Crea codice di incorporamento**, quindi fare clic su **Pubblica**.

Viene indicato il collegamento al report che è possibile condividere con utenti che debbano accedere al report e un frammento di codice per integrare il report nel blog o nel sito Web.

![Pubblicare un report di Microsoft Power BI](./media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

Microsoft offre anche le [App per dispositivi mobili di Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) per la visualizzazione e l'interazione con i dashboard di Power BI e i report sul tuo dispositivo mobile.

## <a name="next-steps"></a>Passaggi successivi

Si è utilizzato correttamente Power BI per visualizzare i dati del sensore in tempo reale dall'hub IoT di Azure.

Esiste un modo alternativo per visualizzare i dati dall'hub IoT di Azure. Vedere [Usare App Web di Azure per visualizzare i dati del sensore in tempo reale dall'hub IoT di Azure](iot-hub-live-data-visualization-in-web-apps.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
