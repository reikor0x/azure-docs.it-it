---
title: Connetti i dati di Barracuda all'anteprima di Azure Sentinel | Microsoft Docs
description: Informazioni su come connettere dati Barracuda Sentinel di Azure.
services: sentinel
documentationcenter: na
author: rkarlin
manager: rkarlin
editor: ''
ms.assetid: 3b33b4aa-7286-4d79-b461-8e1812edc2e1
ms.service: sentinel
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2019
ms.author: rkarlin
ms.openlocfilehash: dd45be69ec29fdcd00710b7366348846f325b151
ms.sourcegitcommit: d73c46af1465c7fd879b5a97ddc45c38ec3f5c0d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65921974"
---
# <a name="connect-your-barracuda-appliance"></a>Connettersi all'appliance di Barracuda 

> [!IMPORTANT]
> Azure Sentinel è attualmente in anteprima pubblica.
> Questa versione di anteprima viene messa a disposizione senza contratto di servizio e non è consigliata per i carichi di lavoro di produzione. Alcune funzionalità potrebbero non essere supportate o potrebbero presentare funzionalità limitate. Per altre informazioni, vedere [Condizioni supplementari per l'utilizzo delle anteprime di Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Connettore di barracuda Web Application Firewall (WAF) consente di connettere facilmente i log di Barracuda con il Sentinel di Azure, per visualizzare i dashboard, creare avvisi personalizzati e migliorare l'analisi. Questo ti offre informazioni più dettagliate sulla rete dell'organizzazione e migliorare le funzionalità di sicurezza. Sentinel Azure sfrutta l'integrazione nativa tra **Barracuda** e Microsoft Monitoring Agent per fornire l'integrazione. 


> [!NOTE]
> I dati verranno archiviati nella posizione geografica dell'area di lavoro in cui in esecuzione Azure Sentinel.

## <a name="configure-and-connect-barracuda-waf"></a>Configurare e connettersi a Barracuda WAF
Barracuda Web Application Firewall è possibile integrare ed esportare i log direttamente da Azure Sentinel tramite Microsoft Monitoring Agent.
1. Passare a [flusso di configurazione di Barracuda WAF](https://campus.barracuda.com/product/webapplicationfirewall/doc/73696965/configure-the-barracuda-web-application-firewall-to-integrate-with-the-oms-server-and-export-logs/)e seguire le istruzioni per configurare la connessione, grazie a questi parametri:
    - **ID area di lavoro**: copiare il valore dell'ID dell'area di lavoro dalla pagina del connettore Azure Sentinel Barracuda.
    - **Chiave primaria**: copiare il valore della chiave primaria dalla pagina del connettore Azure Sentinel Barracuda.
2. Nel portale di Azure Sentinel, passare all'area di lavoro in cui è stato distribuito Azure Sentinel e selezionare i puntini di sospensione (...) alla fine della riga e selezionare **impostazioni avanzate**. 
1. Selezionare **Data** e quindi **Syslog**.
1. Assicurarsi che la funzionalità è impostato in Barracuda esista e imposta il livello di gravità e fare clic su **salvare**.
6. Per usare lo schema appropriato nel Log Analitica per gli eventi di Barracuda, cercare **CommonSecurityLog**.


## <a name="validate-connectivity"></a>Convalidare la connettività

Potrebbero occorrere fino a 20 minuti fino a quando i log di avvio venga visualizzato nel Log Analitica. 



## <a name="next-steps"></a>Passaggi successivi
In questo documento è stato descritto come connettere dispositivi Barracuda per Sentinel di Azure. Per altre informazioni su Azure Sentinel, vedere gli articoli seguenti:
- Informazioni su come [ottenere la visibilità di dati e le potenziali minacce](quickstart-get-visibility.md).
- Iniziare a usare [rilevando minacce con Azure Sentinel](tutorial-detect-threats.md).

