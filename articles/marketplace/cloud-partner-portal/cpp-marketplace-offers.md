---
title: Offerte di Azure Marketplace e del marketplace di AppSource
description: Creazione e gestione delle offerte di Azure Marketplace e del marketplace di AppSource
services: Azure, AppSource, Marketplace, Cloud Partner Portal,
author: v-miclar
ms.service: marketplace
ms.topic: conceptual
ms.date: 03/27/2019
ms.author: pabutler
ms.openlocfilehash: 2d440adc5111db11486d1fc606abbda0ffae9595
ms.sourcegitcommit: c53a800d6c2e5baad800c1247dce94bdbf2ad324
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/30/2019
ms.locfileid: "64942519"
---
# <a name="azure-and-appsource-marketplace-offers"></a>Offerte di Azure Marketplace e del marketplace di AppSource

La prima parte di questa sezione presenta le operazioni generali usate per creare e gestire le offerte per Azure Marketplace e per il marketplace di AppSource.  Vengono fornite le informazioni di base necessarie per comprendere come gestire tipi di offerta specifici, nonché informazioni tecniche comuni a tutti i tipi di offerta.  Gran parte di questa sezione contiene istruzioni dettagliate su come creare e gestire tipi di offerta specifici.  

Il video seguente presenta le varie funzionalità e i diversi tipi di offerta disponibili in Azure Marketplace o AppSource.  Vengono inoltre illustrati aspetti importanti a livello tecnico e aziendale riguardanti la pubblicazione di un'applicazione o un servizio in questi marketplace.

> [!VIDEO https://channel9.msdn.com/Events/Build/2018/BRK2513/player]

**Creazione di app e servizi per Azure Marketplace e AppSource - Build 2018**

Per altre informazioni su questi marketplace, vedere la [Guida alla pubblicazione per Azure Marketplace e AppSource](../marketplace-publishers-guide.md).


## <a name="common-offer-operations"></a>Operazioni comuni per le offerte

Il processo di creazione di una nuova offerta varia in modo significativo a seconda dei tipi di offerta, ad esempio per un'[offerta di applicazione Azure](./azure-applications/cpp-azure-app-offer.md) o per un'[offerta di servizio di consulenza](./consulting-services/cloud-partner-portal-consulting-services-publishing-offer.md).  Molte delle altre operazioni eseguite su un'offerta nel [portale Cloud Partner](https://cloudpartner.azure.com) invece sono piuttosto standardizzate per tutti i tipi di offerta.  Queste operazioni comuni, tra cui la pubblicazione, la visualizzazione, l'aggiornamento e l'eliminazione, sono illustrate nella sezione [Gestire le offerte](./manage-offers/cpp-manage-offers.md)


## <a name="test-drive"></a>Test drive

Il *test drive* è una funzionalità del marketplace che offre ai clienti un'opzione di dimostrazione di "prova prima dell'acquisto" per ogni offerta abilitata.  La funzionalità test drive è limitata al sottoinsieme di tipi di offerte seguente: [applicazioni Azure](./azure-applications/cpp-azure-app-offer.md), [Dynamics 365 Business Central](../cloud-partner-portal-orig/cpp-business-central-offer.md), [Dynamics 365 for Customer Engagement](./dyn365ce/cpp-customer-engagement-offer.md), [Dynamics 365 per Finanza e operazioni](../cloud-partner-portal-orig/cpp-dynamics-365-operations-offer.md), [applicazioni SaaS](./saas-app/cpp-saas-offer.md) e [macchine virtuali](./virtual-machine/cpp-virtual-machine-offer.md).  Questa funzionalità richiede che l'editore crei un modello di test drive personalizzato per l'offerta.  Per altre informazioni, vedere la sezione [Test drive](./test-drive/what-is-test-drive.md).

È possibile esplorare le offerte del marketplace esistenti con dimostrazioni di test drive applicando il [filtro Test Drive](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?filters=test-drive). 


## <a name="azure-marketplace-and-appsource-offer-types"></a>Tipi di offerta di Azure Marketplace e AppSource

La tabella seguente contiene l'elenco dei tipi di offerta correnti supportati dal [portale Cloud Partner](https://cloudpartner.azure.com).  Per ogni tipo sono indicati i marketplace in cui è possibile includere l'offerta, nonché una descrizione generale della tecnologia della soluzione fornita.

|                Tipo di offerta                |  Marketplace  |   DESCRIZIONE                                                           |
|                ----------                |  -----------  |   -----------                                                           |
| [Applicazione di Azure](./azure-applications/cpp-azure-app-offer.md) | Azure | La soluzione è costituita da una o più macchine virtuali, codice di Azure personalizzato facoltativo, distribuiti tramite un modello Azure Resource Manager.  La distribuzione può essere eseguita dal cliente tramite un modello di soluzione o gestita dall'editore. Questo tipo viene usato per offrire maggiore flessibilità rispetto all'offerta fornita di tipo macchina virtuale.  |
| [Servizio di consulenza](./consulting-services/cloud-partner-portal-consulting-services-publishing-offer.md) | Entrambi | I consulenti qualificati Microsoft possono offrire servizi specifici di dominio in Azure Marketplace o AppSource.  Le competenze offerte consentono ai clienti di valutare i problemi riscontrati e creare e distribuire le soluzioni più appropriate per soddisfare gli obiettivi fi business.  |
| [Contenitore](./containers/cpp-containers-offer.md)  | Azure | La soluzione è un'immagine del contenitore Docker di cui è stato effettuato il provisioning come servizio basato su Kubernetes o come Istanze di Azure Container. |
| [Dynamics 365 Business Central](../cloud-partner-portal-orig/cpp-business-central-offer.md) | AppSource | Pacchetto che estende il sistema ERP (Enterprise Resource Planning) e di gestione aziendale. |
| [Dynamics 365 for Customer Engagement](./dyn365ce/cpp-customer-engagement-offer.md) | AppSource | Un pacchetto che estende questo cliente risorse sistema CRM (management), tramite relative vendite, service, servizio di progetto e moduli del servizio campo  |
| [Dynamics 365 for Finance and Operations](../cloud-partner-portal-orig/cpp-dynamics-365-operations-offer.md) | AppSource | Un pacchetto che estende questa pianificazione del servizio (ERP) delle risorse aziendali che supporta avanzato finance, operazioni, produzione e gestione della supply chain |
| [Modulo IoT Edge](./iot-edge-module/cpp-offer-process-parts.md) | Azure | Contenitore compatibile con Docker in esecuzione in un dispositivo IoT Edge.  Contiene moduli di calcolo di piccole dimensioni che usano una combinazione di codice personalizzato, altri servizi di Azure e servizi di terze parti. |
| [App Power BI](./power-bi/cpp-power-bi-offer.md) | AppSource | Un'app di Power BI che crea un pacchetto di contenuto di Power BI personalizzabile, inclusi i set di dati, report e dashboard |
| [App SaaS](./saas-app/cpp-saas-offer.md) | Azure | Soluzione è una sottoscrizione di software-as-a-service, gestita dal server di pubblicazione, gli utenti che l'accesso tramite un'interfaccia personalizzata che usa Azure Active Directory. |
| [Macchina virtuale](./virtual-machine/cpp-virtual-machine-offer.md)  | Azure  | La soluzione è inclusa in una singola macchina virtuale distribuita nella sottoscrizione del cliente.  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |   |   |

Per altre informazioni, vedere la [Guida alla pubblicazione per tipo di offerta](../publisher-guide-by-offer-type.md).


## <a name="next-steps"></a>Passaggi successivi

Apprenderanno nozioni relative operazioni generali è possibile eseguire sulle offerte del marketplace e attributi tecnici più comuni e gli asset nell'articolo [gestione di offerte](./manage-offers/cpp-manage-offers.md).
