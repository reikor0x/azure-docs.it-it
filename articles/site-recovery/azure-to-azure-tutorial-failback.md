---
title: Eseguire il failback di VM di Azure replicate in un'area di Azure secondaria per il ripristino di emergenza con il servizio Azure Site Recovery.
description: Informazioni su come eseguire il failback di VM di Azure con il servizio Azure Site Recovery.
services: site-recovery
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
ms.topic: tutorial
ms.date: 03/18/2019
ms.author: raynew
ms.custom: mvc
ms.openlocfilehash: 339cbf18d79053dfb0704d928b8c9251c73b3a6e
ms.sourcegitcommit: 24fd3f9de6c73b01b0cee3bcd587c267898cbbee
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65951779"
---
# <a name="fail-back-an-azure-vm-between-azure-regions"></a>Eseguire il failback di una VM di Azure tra aree di Azure

Il servizio [Azure Site Recovery](site-recovery-overview.md) favorisce l'attuazione della strategia di ripristino di emergenza gestendo e coordinando le operazioni di replica, failover e failback di computer locali e macchine virtuali di Azure.

Questa esercitazione illustra come eseguire il failback di una singola VM di Azure. Dopo aver eseguito il failover, si deve eseguire il failback nell'area primaria, non appena torna disponibile. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> 
> * Eseguire il failback della VM nell'area secondaria.
> * Riprotteggere la macchina virtuale primaria anche nell'area secondaria.
> 
> [!NOTE]
> 
> Questa esercitazione illustra come eseguire il failover di alcune VM in un'area di destinazione e quindi il failback nell'area di origine con personalizzazioni minime. Per istruzioni più approfondite, vedere le [guide pratiche per le VM di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/).

## <a name="before-you-start"></a>Prima di iniziare

* Verificare che lo stato della VM sia **Commit del failover eseguito**.
* Controllare che l'area primaria sia disponibile e che sia possibile crearvi nuove risorse e accedere a tali risorse.
* Verificare che la riprotezione sia abilitata.

## <a name="fail-back-to-the-primary-region"></a>Eseguire il failback nell'area primaria

Dopo la riprotezione delle VM, è possibile eseguire il failback nell'area primaria in base alle esigenze.

1. Nell'insieme di credenziali selezionare **Elementi replicati** e selezionare la VM che è stata riprotetta.

    ![Failback nell'area primaria](./media/site-recovery-azure-to-azure-failback/azure-to-azure-failback.png)

3. Selezionare **Failover di test** per rieseguire un failover di test nell'area primaria.
4. Selezionare il punto di ripristino e la rete virtuale per il failover di test e selezionare **OK**. È possibile esaminare la VM di test creata nell'area primaria.
5. Al termine del failover di test, selezionare **Pulisci failover di test** per eseguire la pulizia delle risorse create nell'area di origine per il failover di test.
6. In **Elementi replicati** selezionare la VM e quindi **Failover**.
7. In **Failover** selezionare un punto di ripristino in cui eseguire il failover:
    - **Più recente** (impostazione predefinita): determina l'elaborazione di tutti i dati nel servizio Site Recovery e offre il valore RPO (obiettivo punto di ripristino) più basso.
    - **Elaborato più recente**: ripristina la VM all'ultimo punto di ripristino che è stato elaborato da Site Recovery.
    - **Personalizzato**: consente di eseguire il failover in un determinato punto di ripristino ed è particolarmente utile per eseguire un failover di test.

8. Selezionare **Arrestare la macchina prima di iniziare il failover** se si vuole tentare un arresto delle macchine virtuali di origine tramite Site Recovery prima di attivare il failover. Il failover continua anche se l'arresto ha esito negativo. Si noti che Site Recovery non esegue la pulizia dell'origine dopo il failover.
9. Nella pagina **Processi** è possibile seguire lo stato di avanzamento del failover.
10. Una volta che il failover è completato, convalidare la VM eseguendo l'accesso. È possibile modificare il punto di ripristino in base alle esigenze.
11. Dopo aver verificato il failover, selezionare per eseguirne il **commit**. Con il commit vengono eliminati tutti i punti di ripristino disponibili. L'opzione di modifica del punto di ripristino non è più disponibile.
12. La VM risulterà sottoposta a failover e a failback.

    ![VM nell'area primaria e in quella secondaria](./media/site-recovery-azure-to-azure-failback/azure-to-azure-failback-vm-view.png)

> [!NOTE]
> Le VM del ripristino di emergenza rimarranno nello stato di arresto/deallocazione. Questo comportamento è predefinito perché Site Recovery salva le informazioni delle VM, che potrebbero essere utili per il successivo failover dall'area primaria a quella secondaria. Non vengono effettuati addebiti per le VM deallocate ed è quindi consigliabile non modificarne lo stato.

## <a name="next-steps"></a>Passaggi successivi

[Altre informazioni](azure-to-azure-how-to-reprotect.md#what-happens-during-reprotection) sul flusso di riprotezione.
