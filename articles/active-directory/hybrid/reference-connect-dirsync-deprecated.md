---
title: Aggiornamento da DirSync e Azure AD Sync | Documentazione Microsoft
description: Informazioni su come eseguire l'aggiornamento da DirSync e Azure AD Sync ad Azure AD Connect.
services: active-directory
documentationcenter: ''
author: billmath
manager: daveba
editor: ''
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 07/13/2017
ms.subservice: hybrid
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.collection: M365-identity-device-management
ms.openlocfilehash: 803fcc0161f2a092006e60db5a98f5bf18dce1c1
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60381179"
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Aggiornare il servizio di sincronizzazione di Microsoft Azure Active Directory e Azure Active Directory Sync
Azure AD Connect è il modo migliore per collegare la directory locale con Azure AD e Office 365. Questo è il momento giusto per eseguire l'aggiornamento ad Azure AD Connect dallo strumento di sincronizzazione di Windows Azure Active Directory (DirSync) o Azure AD Sync in quanto questi strumenti sono stati deprecati e non sono più supportati a partire dal 13 aprile 2017.

I due strumenti di sincronizzazione delle identità deprecati erano disponibili per i clienti a foresta singola (DirSync) e per i clienti avanzati e con più foreste (Azure AD Sync). Gli strumenti obsoleti sono stati sostituiti da un'unica soluzione disponibile per tutti gli scenari: Azure AD Connect. Questa soluzione offre nuove funzionalità, miglioramenti e supporto per nuovi scenari. Per poter continuare a sincronizzare i dati delle identità locali con Azure AD e Office 365, è consigliabile eseguire l'aggiornamento ad Azure AD Connect. Microsoft non garantisce il funzionamento delle versioni precedenti dopo il 31 dicembre 2017.

L'ultima versione di DirSync è stata rilasciata a luglio 2014, mentre l'ultima versione di Azure AD Sync è stato rilasciata nel mese di maggio 2015.

## <a name="what-is-azure-ad-connect"></a>Cos'è Azure AD Connect
Azure AD Connect è il successore di DirSync e Azure AD Sync. La soluzione combina tutti gli scenari dei due strumenti supportati. Per altre informazioni sull'argomento, vedere [Integrazione delle identità locali con Azure Active Directory](whatis-hybrid-identity.md).

## <a name="deprecation-schedule"></a>Pianificazione della deprecazione
| Data | Comment |
| --- | --- |
| 13 aprile 2016 |Annuncio della deprecazione dei servizi di sincronizzazione di Azure Active Directory ("DirSync") e Microsoft Azure Active Directory Sync ("Azure AD Sync"). |
| 13 aprile 2017 |Termine del supporto. I clienti non potranno più aprire un caso di supporto senza prima eseguire l'aggiornamento ad Azure AD Connect. |
|31 dicembre 2017|Azure AD potrebbe non accettare più comunicazioni provenienti da Azure Active Directory Sync ("DirSync") e Microsoft Azure Active Directory Sync ("Azure AD Sync").

## <a name="how-to-transition-to-azure-ad-connect"></a>Come eseguire la transizione ad Azure AD Connect
Se si usa DirSync, esistono due modi per eseguire l'aggiornamento: aggiornamento sul posto e distribuzione parallela. L'aggiornamento sul posto è consigliato per la maggior parte dei clienti e se si dispone di un sistema operativo recente con meno di 50.000 oggetti. In altri casi è consigliabile eseguire una distribuzione in parallelo in cui la configurazione di DirSync viene trasferita su un nuovo server che esegue Azure AD Connect.

| Soluzione | Scenario |
| --- | --- |
| [Aggiornamento da DirSync](how-to-dirsync-upgrade-get-started.md) |<li>Se è presente un server DirSync esistente già in esecuzione.</li> |
| [Aggiornamento da Azure AD Sync](how-to-upgrade-previous-version.md) |<li>Se si esegue l'aggiornamento da Azure AD Sync.</li> |

Per istruzioni su come eseguire un aggiornamento sul posto da DirSync ad Azure AD Connect, vedere questo video di Channel 9:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>Domande frequenti
**D: È stata ricevuta una notifica di posta elettronica dal team di Azure e/o un messaggio dal Centro messaggi di Office 365 anche se si usa Connect.**  
La notifica è stata inviata anche agli utenti di Azure AD Connect con numero di build 1.0.\*.0 e rilascio precedente all'1.1. Si consiglia ai clienti di rimanere aggiornati con le versioni di Azure AD Connect. La funzionalità di [aggiornamento automatico](how-to-connect-install-automatic-upgrade.md) disponibile nella versione 1.1 consente di assicurare che sia sempre installata una versione recente di Azure AD Connect.

**D: DirSync/Azure AD Sync smetterà di funzionare il 13 aprile 2017?**  
DirSync e Azure AD Sync continueranno a funzionare a partire dal 13 aprile 2017.  Dopo il 31 dicembre 2017, tuttavia, Azure AD potrebbe non accettare più comunicazioni provenienti da DirSync/Azure AD Sync.

**D: Da quali versioni di DirSync è possibile eseguire l'aggiornamento?**  
 È supportato l'aggiornamento da qualsiasi versione di DirSync attualmente in uso. 

**D: E per quanto riguarda il connettore Azure AD per FIM/MIM?**  
Azure AD Connector per FIM/MIM **non** è stato dichiarato deprecato. Si tratta di un **blocco delle funzionalità**: non vengono aggiunte nuove funzionalità e non si ricevono correzioni dei bug. Microsoft consiglia ai clienti che ne fanno uso di pianificare la transizione ad Azure AD Connect. È consigliabile non avviare nuove distribuzioni tramite questo strumento. Nel futuro il connettore verrà deprecato.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Integrazione delle identità locali con Azure Active Directory](whatis-hybrid-identity.md)
