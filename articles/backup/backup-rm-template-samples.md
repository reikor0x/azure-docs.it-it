---
title: Modelli di Azure Resource Manager per Backup di Azure
description: Esempi PowerShell di Backup di Azure
services: backup
author: rayne-wiselman
manager: carmonm
ms.service: backup
ms.topic: sample
ms.date: 01/31/2019
ms.author: raynew
ms.custom: mvc
ms.openlocfilehash: bed2c002cacdac1e47852e6fa3181885af6733d2
ms.sourcegitcommit: 509e1583c3a3dde34c8090d2149d255cb92fe991
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2019
ms.locfileid: "66236793"
---
# <a name="azure-resource-manager-templates-for-azure-backup"></a>Modelli di Azure Resource Manager per Backup di Azure

La tabella seguente contiene collegamenti ai modelli di Azure Resource Manager da usare con gli insiemi di credenziali dei servizi di ripristino e le funzionalità di Backup di Azure. Per informazioni sulla sintassi e le proprietà JSON, vedere [Tipi di risorse Microsoft.RecoveryServices](/azure/templates/microsoft.recoveryservices/allversions).

|   |   |
|---|---|
|**Insieme di credenziali dei servizi di ripristino** | |
| [Creare un insieme di credenziali di Servizi di ripristino](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-vault-create)| Creare un insieme di credenziali dei servizi di ripristino. L'insieme di credenziali può essere usato per Backup di Azure e Azure Site Recovery. |
|**Eseguire il backup di macchine virtuali**| |
| [Eseguire il backup di macchine virtuali di Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-backup-vms). | Usare l'insieme di credenziali dei servizi di ripristino e i criteri di backup esistenti per eseguire il backup delle macchine virtuali di Resource Manager nello stesso gruppo di risorse.|
| [Eseguire il backup di macchine virtuali IaaS in un insieme di credenziali dei servizi di ripristino](https://github.com/Azure/azure-quickstart-templates/tree/master/201-recovery-services-backup-classic-resource-manager-vms) | Modello per il backup di macchine virtuali classiche e di Resource Manager. |
| [Creare criteri di backup settimanale per le macchine virtuali IaaS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-weekly-backup-policy-create) | Il modello crea un insieme di credenziali di Servizi di ripristino e un criterio di backup settimanale per il backup di macchine virtuali classiche e di Resource Manager.|
| [Creare criteri di backup giornaliero per le macchine virtuali IaaS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-daily-backup-policy-create) | Il modello crea un insieme di credenziali di Servizi di ripristino e un criterio di backup giornaliero per il backup di macchine virtuali classiche e di Resource Manager.|
| [Distribuire la macchina virtuale di Windows Server con backup abilitato](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-create-vm-and-configure-backup) | Il modello consente di creare una macchina virtuale di Windows Server e un insieme di credenziali dei servizi di ripristino con il criterio di backup predefinito abilitato.|
|**Monitorare i processi di backup** |  |
| [Usare log di Monitoraggio di Azure con Backup di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-backup-oms-monitoring) | Il modello distribuisce i log di Monitoraggio di Azure con Backup di Azure, per monitorare i processi di backup e ripristino, gli avvisi di backup e lo spazio di archiviazione cloud usato per gli insiemi di credenziali di Servizi di ripristino.|  
|**Eseguire il backup di SQL Server in VM di Azure** |  |
| [Eseguire il backup di SQL Server in VM di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-vm-workload-backup) | Il modello crea un insieme di credenziali di Servizi di ripristino e un criterio di backup specifico del carico di lavoro. Registra la VM per il servizio Backup di Azure e configura la protezione per tale macchina virtuale. Attualmente funziona solo per le immagini della raccolta di SQL. |
|   |   |
