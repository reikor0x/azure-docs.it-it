---
title: Supporto di Azure Resource Manager per il bilanciamento del carico | Documentazione Microsoft
description: Usare PowerShell per il bilanciamento del carico con Azure Resource Manager. Uso di modelli per il bilanciamento del carico
services: load-balancer
documentationcenter: na
author: KumudD
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/25/2017
ms.author: kumud
ms.openlocfilehash: 596ac871067886ee3124c0f21beb35cb3b8fe1ae
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60888997"
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>Usare il supporto di Azure Resource Manager per Azure Load Balancer



Azure Resource Manager è il framework di gestione preferito dei servizi in Azure. È ora possibile gestire Azure Load Balancer con API e strumenti basati su Azure Resource Manager.

## <a name="concepts"></a>Concetti

Con Resource Manager, Azure Load Balancer contiene le seguenti risorse figlio:

* Configurazione IP front-end: un bilanciamento del carico può includere uno o più indirizzi IP front-end, anche noti come IP virtuali (indirizzi VIP). Questi indirizzi IP vengono usati come ingresso per il traffico.
* Pool di indirizzi back-end: indirizzi IP associati alla scheda di interfaccia di rete della macchina virtuale a cui viene distribuito il carico.
* Le regole di bilanciamento del carico: una proprietà della regola esegue il mapping a e combinazione di porta a un set di indirizzi IP back-end e combinazione di porta IP front-end specifico. Un bilanciamento del carico singolo può avere più regole di bilanciamento del carico. Ogni regola è una combinazione di un IP front-end e porte back-end IP e porta associata alle VM.
* Probe: le probe consentono di tenere traccia dell'integrità delle istanze della macchina virtuale. Se un probe di integrità non riesce, l'istanza della macchina virtuale viene esclusa automaticamente dalla rotazione.
* Regole NAT in ingresso: NAT regole che definiscono il traffico in ingresso attraversa l'IP front-end e distribuito all'IP back-end.

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>Modelli di Guida introduttiva

Gestione risorse di Azure consente di effettuare il provisioning delle applicazioni usando un modello dichiarativo. Con un unico modello, puoi distribuire più servizi insieme alle rispettive dipendenze. Si usa lo stesso modello per distribuire più volte l'applicazione durante ogni fase del ciclo di vita dell'applicazione.

I modelli possono includere definizioni per macchine virtuali, reti virtuali, set di disponibilità, interfacce di rete, account di archiviazione, bilanciamenti del carico, gruppi di sicurezza di rete e IP pubblici. Con i modelli è possibile creare tutto il necessario per un'applicazione complessa. Il file modello può essere verificato nel sistema di gestione dei contenuti per il controllo della versione e la collaborazione.

[Altre informazioni sui modelli](../azure-resource-manager/resource-manager-template-walkthrough.md)

[Altre informazioni sulle risorse di rete](../networking/networking-overview.md)

Per i modelli di avvio rapido che usano Azure Load Balancer, vedere il [repository GitHub](https://github.com/Azure/azure-quickstart-templates) che ospita un set di modelli generati dalla community.

Esempi di modelli:

* [2 macchine virtuali in un bilanciamento del carico e regole di bilanciamento del carico](https://go.microsoft.com/fwlink/?LinkId=544799)
* [2 macchine virtuali in una rete virtuale con un bilanciamento del carico interno e regole di bilanciamento del carico](https://go.microsoft.com/fwlink/?LinkId=544800)
* [2 macchine virtuali in un bilanciamento del carico e regole NAT di configurazione per il bilanciamento del carico](https://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>Configurazione del bilanciamento del carico di Azure con PowerShell o l'interfaccia della riga di comando

Introduzione ai cmdlet, agli strumenti da riga di comando e alle API REST di Azure Resource Manager

* [cmdlet di rete di Azure](https://docs.microsoft.com/powershell/module/az.network#networking) possono essere usati per creare un bilanciamento del carico.
* [Come creare un servizio di bilanciamento del carico tramite Gestione risorse di Azure](load-balancer-get-started-ilb-arm-ps.md)
* [Uso dell'interfaccia della riga di comando di Azure con Gestione risorse di Azure](../xplat-cli-azure-resource-manager.md)
* [API REST di bilanciamento del carico](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>Passaggi successivi

È anche possibile [iniziare a creare un bilanciamento del carico con connessione Internet](load-balancer-get-started-internet-arm-ps.md) e configurare il tipo di [modalità di distribuzione](load-balancer-distribution-mode.md) per il comportamento specifico del traffico di rete per il bilanciamento del carico.

Informazioni su come gestire [le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md). Questo è importante quando l'applicazione deve mantenere le connessioni attive per i server di bilanciamento del carico.
