---
title: Informazioni sul Centro sicurezza di Azure per l'architettura della soluzione IoT Preview | Microsoft Docs
description: Informazioni sul flusso di informazioni nel Centro sicurezza di Azure per il servizio IoT.
services: asc-for-iot
ms.service: ascforiot
documentationcenter: na
author: mlottner
manager: rkarlin
editor: ''
ms.assetid: 2cf6a49b-5d35-491f-abc3-63ec24eb4bc2
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2019
ms.author: mlottner
ms.openlocfilehash: 3c775c8cb99b056c7f468c028a80dd0b27ae6438
ms.sourcegitcommit: 0568c7aefd67185fd8e1400aed84c5af4f1597f9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65200687"
---
# <a name="azure-security-center-for-iot-architecture"></a>Il Centro sicurezza di Azure per l'architettura di IoT

Questo articolo illustra l'architettura del sistema funzionale di Azure Security Center (ASC) per la soluzione IoT. 

> [!IMPORTANT]
> Centro sicurezza di Azure per IoT è attualmente in versione di anteprima pubblica.
> Questa versione di anteprima viene messa a disposizione senza contratto di servizio e non è consigliata per i carichi di lavoro di produzione. Alcune funzionalità potrebbero non essere supportate o potrebbero presentare funzionalità limitate. Per altre informazioni, vedere [Condizioni supplementari per l'utilizzo delle anteprime di Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="asc-for-iot-components"></a>Centro sicurezza di AZURE per i componenti di IoT

Centro sicurezza di AZURE per IoT è costituita dai componenti seguenti:
- Agenti di dispositivo
- Inviare il messaggio di sicurezza SDK
- Integrazione dell'IoT Hub
- Pipeline di Analitica
 
### <a name="asc-for-iot-workflow"></a>Centro sicurezza di AZURE per IoT del flusso di lavoro

Centro sicurezza di AZURE per gli agenti di dispositivi IoT consente di raccogliere facilmente gli eventi di sicurezza non elaborati dai dispositivi. Gli eventi di sicurezza non elaborati possono includere le connessioni IP, la creazione del processo, gli accessi utente e altre informazioni relative alla sicurezza. Centro sicurezza di AZURE per gli agenti di dispositivi IoT gestire anche l'aggregazione di eventi al fine di evitare di velocità effettiva di rete elevato. Gli agenti sono altamente personalizzabili, consentendo di utilizzarle per attività specifiche, ad esempio inviare solo informazioni importanti con il contratto di servizio più veloce, o per aggregare le informazioni di sicurezza completo e il contesto in segmenti più grandi, evitando i costi di servizio più elevati.
 
Dispositivo agenti e altre applicazioni utilizza il **Centro sicurezza di Azure, AZURE Invia messaggio di sicurezza SDK** per inviare informazioni di sicurezza nell'IoT Hub di Azure. L'IoT Hub acquisisce queste informazioni e lo inoltra al Centro sicurezza di AZURE per il servizio IoT.

Dopo aver abilitato il Centro sicurezza di AZURE per il servizio IoT, oltre ai dati inoltrati, l'IoT Hub invia tutti i relativi dati interni per l'analisi dal Centro sicurezza di AZURE per IoT. Questi dati includono i log delle operazioni da dispositivo a cloud, le identità dei dispositivi e la configurazione dell'Hub. Tutte queste informazioni consente di creare il Centro sicurezza di AZURE per la pipeline di analitica IoT.
 
Centro sicurezza di AZURE per la pipeline di analitica IoT riceve anche flussi intelligence delle minacce aggiuntivi da varie origini all'interno di Microsoft e Microsoft partner. Il Centro sicurezza di AZURE per la pipeline di analitica intero IoT funziona con tutte le configurazioni dei clienti eseguite nel servizio (ad esempio avvisi personalizzati e l'utilizzo del messaggio di sicurezza di trasmissione SDK).
 
Tramite la pipeline di analitica, Centro sicurezza di AZURE per IoT combina tutti i flussi di informazioni per generare gli avvisi e suggerimenti pratici. La pipeline contiene due regole personalizzate create da ricercatori dediti alla protezione e gli esperti, nonché modelli la ricerca di deviazione dall'analisi del comportamento e i rischi di dispositivo standard di machine learning.
 
Centro sicurezza di AZURE per IoT raccomandazioni e avvisi (analitica pipeline output) viene scritto nell'area di lavoro di Log Analitica di ogni cliente. Inclusi gli eventi non elaborati nell'area di lavoro, nonché gli avvisi e raccomandazioni consente l'analisi approfondita e le query che utilizzano i dettagli esatti delle attività sospette rilevate.  

## <a name="next-steps"></a>Passaggi successivi

In questo articolo sono illustrate l'architettura di base e del flusso di lavoro del Centro sicurezza di AZURE per la soluzione IoT. Per altre informazioni sui prerequisiti, come iniziare a usare e abilitare la soluzione di sicurezza nell'IoT Hub, vedere gli articoli seguenti:

- [Prerequisiti del servizio](service-prerequisites.md)
- [Introduzione](getting-started.md)
- [Configurare la soluzione](quickstart-configure-your-solution.md)
- [Abilitare la sicurezza nell'IoT Hub](quickstart-onboard-iot-hub.md)
- [Centro sicurezza di AZURE per IoT domande frequenti](resources-frequently-asked-questions.md)
- [Centro sicurezza di AZURE per gli avvisi di sicurezza IoT](concept-security-alerts.md)

