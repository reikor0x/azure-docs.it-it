---
title: Vulnerabilità rilevate da Azure Active Directory Identity Protection
description: Panoramica delle vulnerabilità rilevate da Azure Active Directory Identity Protection
services: active-directory
ms.service: active-directory
ms.subservice: identity-protection
ms.topic: article
ms.date: 04/09/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: sahandle
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e792551f4cac857f56454c67d527e01cb9c4281
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66113116"
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Vulnerabilità rilevate da Azure Active Directory Identity Protection

Le vulnerabilità sono punti deboli in un ambiente che possono essere sfruttati da un utente malintenzionato. Si consiglia agli amministratori di risolvere le vulnerabilità per migliorare le condizioni di sicurezza della propria organizzazione.

![Vulnerabilità segnalate da Identity Protection](./media/vulnerabilities/identity-protection-vulnerabilities.png)

Le sezioni seguenti presentano una panoramica delle vulnerabilità segnalate da Identity Protection.

## <a name="multi-factor-authentication-registration-not-configured"></a>Registrazione per l'autenticazione a più fattori non configurata

Questa vulnerabilità consente di valutare la distribuzione di Azure multi-Factor Authentication all'interno dell'organizzazione.

Azure multi-Factor Authentication fornisce un secondo livello di sicurezza per l'autenticazione dell'utente. Consente di proteggere l'accesso ai dati e alle applicazioni dell'utente, garantendo al tempo stesso una procedura di accesso semplice. Azure multi-Factor Authentication offre le opzioni di verifica facile da usare, ad esempio:

* Telefonata
* SMS
* Notifica dell'app per dispositivi mobili
* Codice di verifica OTP

È consigliabile richiedere l'autenticazione a più fattori di Azure per l'accesso degli utenti. L'autenticazione a più fattori svolge un ruolo chiave nei criteri di accesso condizionale basati sul rischio disponibili tramite Identity Protection.

Per altre informazioni, vedere [Informazioni su Azure Multi-Factor Authentication](../authentication/multi-factor-authentication.md).

## <a name="unmanaged-cloud-apps"></a>App cloud non gestite

Questa vulnerabilità consente di identificare le app per cloud non gestite all'interno dell'organizzazione.

IL personale IT spesso non sono consapevoli di tutte le applicazioni cloud nell'organizzazione. L'accesso non autorizzato ai dati aziendali, le possibili perdite di dati e altri rischi di sicurezza rappresentano una preoccupazione per gli amministratori.

È consigliabile distribuire Cloud Discovery per individuare le applicazioni cloud non gestite e per gestire tali applicazioni tramite Azure Active Directory.

Per altre informazioni, vedere [Cloud Discovery](/cloud-app-security/set-up-cloud-discovery).

## <a name="security-alerts-from-privileged-identity-management"></a>Avvisi di sicurezza da Privileged Identity Management

Questa vulnerabilità permette di identificare e risolvere gli avvisi sulle identità con privilegi all'interno dell'organizzazione.  

Per consentire agli utenti di eseguire operazioni con privilegi, le organizzazioni devono concedere agli utenti accessi con privilegi temporanei o permanenti in Azure AD, per le risorse di Azure o Office 365 o per altre app SaaS. Ognuno di questi utenti con privilegi aumenta la superficie di attacco dell'organizzazione. Questa vulnerabilità consente di identificare gli utenti che hanno un accesso con privilegi non necessario e di intraprendere le azioni appropriate per ridurre o eliminare il rischio.

Si consiglia alle organizzazioni di usare Azure AD Privileged Identity Management per gestire, controllare e monitorare le identità con privilegi in Azure AD, nonché altri servizi online Microsoft come Office 365 o Microsoft Intune.

Per altre informazioni, vedere [Azure AD Privileged Identity Management](../privileged-identity-management/pim-configure.md).

## <a name="see-also"></a>Vedere anche 

[Azure Active Directory Identity Protection](../active-directory-identityprotection.md)
