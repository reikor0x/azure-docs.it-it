---
author: rayne-wiselman
ms.service: site-recovery
ms.topic: include
ms.date: 10/26/2018
ms.author: raynew
ms.openlocfilehash: cd18d71d26410767a2d3119c12a1339bdc84bd33
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60301460"
---
1. Nel server di configurazione avviare il file CSPSConfigtool.exe. È disponibile come collegamento sul desktop e nella cartella *percorso di installazione*\home\svsystems\bin.
2. Fare clic su **Gestisci account** > **Aggiungi account**.

    ![Aggiungi account](./media/site-recovery-add-vcenter-account/credentials1.png)
3. In **Dettagli dell'account** aggiungere l'account che verrà usato per l'individuazione automatica.

    ![Dettagli](./media/site-recovery-add-vcenter-account/credentials2.png)

    > [!Note]
   > Possono trascorrere 15 minuti o più prima che il nome dell'account venga visualizzato nel portale. Per aggiornarlo immediatamente, fare clic su **Server di configurazione** > ***nome del server*** > **Aggiorna server**.
