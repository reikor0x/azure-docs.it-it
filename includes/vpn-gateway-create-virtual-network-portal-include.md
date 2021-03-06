---
title: File di inclusione
description: File di inclusione
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 04/04/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: d35da4f1eaed91411c015ed7665944d886f9d79c
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66170157"
---
Per creare una rete virtuale nel modello di distribuzione Resource Manager usando il portale di Azure, seguire questa procedura. Usare i [valori di esempio](#values) se si usa questa procedura come esercitazione. In caso contrario, assicurarsi di sostituire i valori di esempio con valori reali. Per altre informazioni sull'uso delle reti virtuali, vedere la [panoramica sulla rete virtuale](../articles/virtual-network/virtual-networks-overview.md).

>[!NOTE]
>Per consentire a questa rete virtuale di connettersi a una posizione locale, è necessario coordinarsi con l'amministratore di rete locale per definire un intervallo di indirizzi IP da usare in modo specifico per questa rete virtuale. Se su entrambi i lati della connessione VPN è presente un intervallo di indirizzi duplicato, il traffico non viene indirizzato nel modo previsto. Se inoltre si vuole connettere questa rete virtuale a un'altra rete virtuale, lo spazio degli indirizzi non può sovrapporsi a un'altra rete virtuale. Pianificare quindi con attenzione la configurazione della rete.
>
>

1. In un browser passare al [portale di Azure](http://portal.azure.com) e accedere con l'account Azure.
2. Fare clic su **Crea una risorsa**. Nel campo **Cerca nel Marketplace** digitare "rete virtuale". Individuare **Rete virtuale** nell'elenco restituito e fare clic per aprire la pagina **Rete virtuale**.
3. Nella parte inferiore della pagina Rete virtuale selezionare **Resource Manager** nell'elenco **Selezionare un modello di distribuzione** e quindi fare clic su **Crea**. Verrà visualizzata la pagina "Crea rete virtuale".

   ![Pagina Crea rete virtuale](./media/vpn-gateway-create-virtual-network-portal-include/create-virtual-network.png "Pagina Crea rete virtuale")
4. Nella pagina **Crea rete virtuale** configurare le impostazioni della rete virtuale. Durante la compilazione dei campi, il punto esclamativo rosso diventa un segno di spunta verde se i caratteri immessi nel campo sono validi.

   - **Nome**: immettere un nome per la rete virtuale. In questo esempio viene usato VNet1.
   - **Spazio degli indirizzi**: immettere lo spazio indirizzi. Se si hanno più spazi di indirizzi da aggiungere, aggiungere il primo. È possibile aggiungere altri spazi di indirizzi in un secondo momento, dopo aver creato la rete virtuale. Assicurarsi che lo spazio degli indirizzi specificato non si sovrapponga allo spazio degli indirizzi per la posizione locale.
   - **Sottoscrizione** verificare che la sottoscrizione riportata sia quella corretta. È possibile cambiare sottoscrizione tramite l'elenco a discesa.
   - **Gruppo di risorse**: selezionare un gruppo di risorse esistente o crearne uno nuovo immettendone il nome. Se si crea un nuovo gruppo, denominare il gruppo di risorse in base ai valori di configurazione pianificati. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Gestione risorse di Azure](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
   - **Località**: selezionare la località della rete virtuale. La località determina la posizione in cui risiedono le risorse distribuite in questa rete virtuale.
   - **Subnet**: aggiungere il nome e l'intervallo di indirizzi della prima subnet. È possibile aggiungere altre subnet e la subnet del gateway in un secondo momento, al termine della creazione della rete virtuale. 

5. Selezionare **Aggiungi al dashboard** se si vuole trovare facilmente la rete virtuale nel dashboard e quindi fare clic su **Crea**. Dopo aver fatto clic su **Crea**, verrà visualizzato un riquadro nel dashboard che riflette lo stato di avanzamento della rete virtuale. Il riquadro cambia durante la creazione della rete virtuale.
