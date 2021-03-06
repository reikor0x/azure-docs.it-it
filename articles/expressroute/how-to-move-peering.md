---
title: Spostare un peering pubblico nel peering Microsoft - Azure ExpressRoute | Microsoft Docs
description: Questo articolo illustra i passaggi per spostare il peering pubblico nel peering Microsoft su ExpressRoute.
services: expressroute
author: cherylmc
ms.service: expressroute
ms.topic: article
ms.date: 03/12/2018
ms.author: cherylmc
ms.custom: seodec18
ms.openlocfilehash: 6b2bce6b488698db0a72c9a17f67c2555c6afa5b
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60883151"
---
# <a name="move-a-public-peering-to-microsoft-peering"></a>Spostare un peering pubblico nel peering Microsoft

Questo articolo descrive come spostare una configurazione di peering pubblico nel peering Microsoft senza tempi di inattività. ExpressRoute supporta ora i servizi PaaS Azure, come l'archiviazione di Azure e il database SQL di Azure, usando il peering Microsoft con i filtri di route. È ora necessario un solo dominio di routing per accedere ai servizi PaaS e SaaS Microsoft. È possibile usare i filtri di route per annunciare in modo selettivo i prefissi dei servizi PaaS per le aree di Azure che si vuole usare. Per altre informazioni sul routing di domini e i peering, vedere l'articolo relativo ai [domini di routing e i circuiti ExpressRoute](expressroute-circuit-peerings.md).

## <a name="before"></a>Prima di iniziare

* Per connettersi al peering Microsoft, è necessario configurare e gestire i requisiti NAT. Il provider di connettività può configurare e gestire NAT come servizio gestito. Se si intende accedere ai servizi PaaS e SaaS Azure nel peering Microsoft, è importante ridimensionare il pool di indirizzi IP NAT correttamente. Per altre informazioni su NAT per ExpressRoute, vedere i [requisiti NAT per il peering Microsoft](expressroute-nat.md#nat-requirements-for-microsoft-peering).

* Se si usa il peering pubblico e si dispone di regole di rete IP per gli indirizzi IP pubblici che vengono usati per accedere all'[Archiviazione di Azure](../storage/common/storage-network-security.md) o al [database SQL di Azure](../sql-database/sql-database-vnet-service-endpoint-rule-overview.md), è necessario assicurarsi che il pool di indirizzi IP NAT configurato con il peering Microsoft sia incluso nell'elenco di indirizzi IP pubblici per l'account di archiviazione di Azure o per l'account SQL di Azure.

* Per passare nel peering Microsoft senza tempi di inattività, usare i passaggi in questo articolo nell'ordine in cui sono elencati.

## <a name="create"></a>1. Creare il peering Microsoft

Se il peering Microsoft non è stato creato, consultare uno qualsiasi dei seguenti articoli per creare il peering Microsoft. Se il provider di connettività offre servizi gestiti di livello 3, è possibile chiedere al provider di abilitare il peering Microsoft per il circuito.

  * [Creare il peering Microsoft usando il Portale di Azure](expressroute-howto-routing-portal-resource-manager.md#msft)
  * [Creare il peering Microsoft usando Azure Powershell](expressroute-howto-routing-arm.md#msft)
  * [Creare il peering Microsoft usando l'interfaccia della riga di comando di Azure](howto-routing-cli.md#msft)

## <a name="validate"></a>2. Verificare che il peering Microsoft sia abilitato.

Verificare che il peering Microsoft sia abilitato e che i prefissi pubblici annunciati si trovino nello stato configurato.

  * [Portale di Azure](expressroute-howto-routing-portal-resource-manager.md#getmsft)
  * [Azure PowerShell](expressroute-howto-routing-arm.md#getmsft)
  * [Interfaccia della riga di comando di Azure](howto-routing-cli.md#getmsft)

## <a name="routefilter"></a>3. Configurare e associare un filtro di route al circuito

Per impostazione predefinita, i nuovi peering Microsoft non annunciano i prefissi fino a quando non viene associato un filtro di route al circuito. Quando si crea una regola di filtro di route, è possibile specificare l'elenco di community di servizio per le aree di Azure che si vuole usare per i servizi PaaS Azure, come illustrato nella schermata seguente:

![Unire il peering pubblico](./media/how-to-move-peering/public.png)

Usare uno dei seguenti articoli per configurare i filtri di route:

  * [Configurare i filtri di route per il peering Microsoft usando il Portale di Azure](how-to-routefilter-portal.md)
  * [Configurare i filtri di route per il peering Microsoft usando Azure PowerShell](how-to-routefilter-powershell.md)
  * [Configurare i filtri di route per il peering Microsoft usando l'interfaccia della riga di comando di Azure](how-to-routefilter-cli.md)

## <a name="delete"></a>4. Eliminare il peering pubblico.

Dopo avere verificato la corretta configurazione del peering Microsoft e il corretto annuncio dei prefissi da usare nel peering Microsoft, sarà possibile eliminare il peering pubblico. Per eliminare il peering pubblico, leggere uno dei seguenti articoli:

  * [Eliminare il peering pubblico di Azure usando il Portale di Azure](expressroute-howto-routing-portal-resource-manager.md#deletepublic)
  * [Eliminare il peering pubblico di Azure usando Azure PowerShell](expressroute-howto-routing-arm.md#deletepublic)
  * [Eliminare il peering pubblico di Azure usando l'interfaccia della riga di comando](howto-routing-cli.md#deletepublic)
  
## <a name="view"></a>5. Visualizzare i peering
  
È possibile visualizzare un elenco di tutti i circuiti ExpressRoute e i peering nel portale di Azure. Per altre informazioni, vedere [Per visualizzare i dettagli del peering Microsoft](expressroute-howto-routing-portal-resource-manager.md#getmsft).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su ExpressRoute, vedere le [Domande frequenti su ExpressRoute](expressroute-faqs.md).
