---
title: I piani di offerta di applicazione SaaS Azure | Azure Marketplace
description: Creare un piano per un'offerta di applicazione SaaS in Azure Marketplace.
services: Azure, Marketplace, Cloud Partner Portal,
author: dan-wesley
ms.service: marketplace
ms.topic: conceptual
ms.date: 12/04/2018
ms.author: pabutler
ms.openlocfilehash: 2ff86b39f67b170ce99b045f5cfa888e06057bbe
ms.sourcegitcommit: c53a800d6c2e5baad800c1247dce94bdbf2ad324
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/30/2019
ms.locfileid: "64943334"
---
# <a name="saas-application-plans-tab"></a>Scheda Piani per un'applicazione SaaS

Usare la scheda Piani per creare un nuovo piano. Se si usa l'opzione Sell through Microsoft (Vendi tramite Microsoft) per l'app SaaS, è necessario aggiungere almeno un piano.

![Creare un nuovo piano](./media/saas-plans-new-plan.png)

## <a name="create-a-new-plan"></a>Creare un nuovo piano

Per creare un nuovo piano:

1. In **Piani** selezionare **+ Nuovo piano**.
2. Nella finestra popup **Nuovo piano** digitare un **ID piano**. La lunghezza massima consentita è di 50 caratteri. Questo ID deve contenere solo caratteri alfanumerici minuscoli, trattini o caratteri di sottolineatura. Dopo aver pubblicato l'offerta, non sarà possibile modificare questo ID.
3. Scegliere **OK** per salvare l'ID piano.

   ![ID piano per il nuovo piano](./media/saas-plans-plan-ID.png)

### <a name="to-configure-the-plan"></a>Per configurare il piano:

1. In **Dettagli piano** specificare le informazioni per i campi seguenti:

   - Titolo: immettere un titolo per il piano. Il titolo non può superare i 50 caratteri.
   - Descrizione: fornire una descrizione. La descrizione non può superare i 500 caratteri.
   - Is this a private plan? (Piano privato?) : se il piano è disponibile solo per un gruppo selezionato di clienti, selezionare **Sì**.
   - Disponibilità per paese/area geografica: il piano deve essere disponibile per almeno un paese o un'area geografica. Fare clic su **Seleziona aree**. Selezionare un paese o un'area geografica dall'elenco **Selezione disponibilità per paese/area geografica** e quindi scegliere **OK**. 
   - Legacy Pricing (Prezzo legacy): specificare il costo, in USD al mese.

2. In **Prezzi in valuta semplificati** specificare le informazioni seguenti:

   - Billing Term (Termine di fatturazione): l'opzione Prezzo mensile è selezionata per impostazione predefinita. È anche possibile specificare un prezzo annuale.
   - Prezzo mensile: specificare il prezzo mensile, che deve corrispondere al prezzo legacy.

   >[!NOTE] 
   >Se si aggiunge un prezzo annuale al termine di fatturazione, potrebbe essere richiesto di specificare il **Prezzo annuale** in USD all'anno.

3. Selezionare **Salva** per completare la configurazione del piano.

   >[!NOTE] 
   >Dopo aver salvato le modifiche ai prezzi, è possibile esportare/importare i dati relativi ai prezzi.

![Configurare i dettagli del piano](./media/saas-plans-plan-details.png)

## <a name="next-steps"></a>Passaggi successivi

[Scheda Informazioni canale](./cpp-channel-info-tab.md)

