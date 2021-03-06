---
title: Domande frequenti per Azure Red Hat OpenShift | Microsoft Docs
description: Di seguito vengono fornite le risposte alle domande frequenti su Microsoft Azure Red Hat OpenShift
services: container-service
author: jimzim
ms.author: jzim
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 05/08/2019
ms.openlocfilehash: 2001b849e9c43d552889475ca237c52b141f3f04
ms.sourcegitcommit: 009334a842d08b1c83ee183b5830092e067f4374
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/29/2019
ms.locfileid: "66306273"
---
# <a name="azure-red-hat-openshift-faq"></a>Azure Red Hat OpenShift, domande frequenti

Questo articolo risponde alle domande frequenti (FAQ) su Microsoft Azure Red Hat OpenShift.

## <a name="how-do-i-get-started"></a>Come iniziare?

Prima di poter usare Azure Red Hat OpenShift, è necessario acquistare un minimo di 4 nodi di applicazione di Azure Red Hat OpenShift riservato.

Se si è clienti di Azure[acquistare istanze riservate di Azure Red Hat OpenShift](https://aka.ms/openshift/buy) tramite il portale di Azure. Dopo l'acquisto, la sottoscrizione verrà attivata entro 24 ore, dopodiché sarà in grado di provisioning di cluster.

Se non si è clienti di Azure [contatta il reparto vendite](https://aka.ms/openshift/contact-sales) e compilare il modulo nella parte inferiore della pagina per avviare il processo di vendita.

Vedere le [pagina dei prezzi Azure Red Hat OpenShift](https://aka.ms/openshift/pricing) per altre informazioni.

## <a name="which-azure-regions-are-supported"></a>Quali aree di Azure sono supportati?

Visualizzare [risorse supportate](supported-resources.md#azure-regions) per un elenco di aree globali in cui è supportato Azure Red Hat OpenShift.

## <a name="can-i-deploy-a-cluster-into-an-existing-virtual-network"></a>È possibile distribuire un cluster in una rete virtuale esistente?

 No. Ma è possibile connettersi a un cluster Azure Red Hat OpenShift a una rete virtuale esistente tramite il peering. Visualizzare [connettere la rete virtuale di un cluster a una rete virtuale esistente ](tutorial-create-cluster.md#optional-connect-the-clusters-virtual-network-to-an-existing-virtual-network) per informazioni dettagliate.

## <a name="what-cluster-operations-are-available"></a>Le operazioni di cluster sono disponibili?

È possibile solo aumentare o ridurre il numero di nodi di calcolo. Nessuna altra modifica è autorizzata al `Microsoft.ContainerService/openShiftManagedClusters` risorsa dopo la creazione. Il numero massimo di nodi di calcolo è limitato a 20.

## <a name="what-virtual-machine-sizes-can-i-use"></a>Le dimensioni delle macchine virtuali è possibile usare?

Visualizzare [dimensioni delle macchine virtuali di Azure Red Hat OpenShift](supported-resources.md#virtual-machine-sizes) per un elenco delle dimensioni delle macchine virtuali è possibile usare con un cluster Azure Red Hat OpenShift.

## <a name="is-data-on-my-cluster-encrypted"></a>Sia i dati sul cluster crittografati?

Per impostazione predefinita, è presente crittografia dei dati inattivi. La piattaforma di archiviazione di Azure crittografa automaticamente i dati prima di renderli persistenti e consente di decrittografare i dati prima del recupero. Visualizzare [la crittografia del servizio di archiviazione di Azure per dati inattivi](https://docs.microsoft.com/azure/storage/common/storage-service-encryption) per informazioni dettagliate.

## <a name="can-i-use-prometheusgrafana-to-monitor-containers-and-manage-capacity"></a>È possibile usare Prometheus/Grafana per monitorare i contenitori e gestire la capacità?

No, non l'ora corrente.

## <a name="is-the-docker-registry-available-externally-so-i-can-use-tools-such-as-jenkins"></a>È il registro Docker disponibili esternamente in modo che è possibile usare strumenti come Jenkins?

È disponibile il registro Docker `https://docker-registry.apps.<clustername>.<region>.azmosa.io/` , tuttavia, una garanzia di durabilità di archiviazione sicuro non viene specificata. È anche possibile usare [registro contenitori di Azure](https://azure.microsoft.com/services/container-registry/).

## <a name="is-cross-namespace-networking-supported"></a>Rete cross-spazio dei nomi è supportata?

Clienti e gli amministratori di singolo progetto personalizzabili rete cross-spazio dei nomi (tra cui viene negato) in base al progetto usando `NetworkPolicy` oggetti.

## <a name="can-an-admin-manage-users-and-quotas"></a>Un amministratore può gestire quote e gli utenti?

Sì. Un amministratore di Azure Red Hat OpenShift può gestire utenti e le quote oltre all'accesso a tutti gli utenti creati progetti.

## <a name="can-i-restrict-a-cluster-to-only-certain-azure-ad-users"></a>È possibile limitare un cluster solo determinati utenti di Azure AD?

Sì. È possibile limitare quali Azure AD gli utenti possono accedere a un cluster configurando l'applicazione Azure AD. Per informazioni dettagliate, vedere [come: Limitare l'app a un set di utenti](https://docs.microsoft.com/azure/active-directory/develop/howto-restrict-your-app-to-a-set-of-users)

## <a name="can-a-cluster-have-compute-nodes-across-multiple-azure-regions"></a>Un cluster possono avere nodi di calcolo in più aree di Azure?

 No. Tutti i nodi in un cluster Azure Red Hat OpenShift devono provenire dalla stessa area di Azure.

## <a name="are-master-and-infrastructure-nodes-abstracted-away-as-they-are-with-azure-kubernetes-service-aks"></a>Sono i nodi master e l'infrastruttura speditamente così come sono con Azure Kubernetes Service (AKS)?

 No. Tutte le risorse, incluso il database master del cluster, eseguire nella propria sottoscrizione dei clienti. Questi tipi di risorse vengono inseriti in un gruppo di risorse di sola lettura.

## <a name="is-open-service-broker-for-azure-osba-supported"></a>È Open Service Broker for Azure (OSBA) è supportato?

Sì. È possibile usare OSBA con Azure Red Hat OpenShift. Visualizzare [Open Service Broker for Azure](https://github.com/Azure/open-service-broker-azure#openshift-project-template) per altre informazioni.
