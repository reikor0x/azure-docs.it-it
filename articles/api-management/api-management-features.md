---
title: Confronto basato sulle funzionalità dei livelli di Gestione API di Azure | Microsoft Docs
description: Questo articolo mette a confronto i livelli di Gestione API basati sulle funzionalità offerte.
services: api-management
documentationcenter: ''
author: vladvino
manager: erikre
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/26/2018
ms.author: apimpm
ms.openlocfilehash: 34c4ef2885a82b6c392b814eeb624e616e341d48
ms.sourcegitcommit: 009334a842d08b1c83ee183b5830092e067f4374
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/29/2019
ms.locfileid: "66304339"
---
# <a name="feature-based-comparison-of-the-azure-api-management-tiers"></a>Confronto basato sulle funzionalità dei livelli di Gestione API di Azure

Ogni [piano tariffario](https://aka.ms/apimpricing) di Gestione API offre un set diverso di funzionalità e di[ capacità](api-management-capacity.md) per unità. La tabella seguente riepiloga le funzionalità chiave disponibili in ciascuno dei livelli. Alcune funzionalità potrebbero funzionare diversamente o avere capacità diverse a seconda del livello. In questi casi le differenze vengono indicate negli articoli della documentazione, i quali descrivono le singole funzionalità.

| Funzionalità                                                                                      | Consumo | Sviluppatore      | Basic          | Standard       | Premium        |
| -------------------------------------------------------------------------------------------- | ----------------------------- | -------------- | -------------- | -------------- | -------------- |
| Integrazione di Azure AD<sup>1</sup>                                                             | No                             | Sì            | No              | Yes            | Yes            |
| Supporto della Rete virtuale di Microsoft Azure (VNet)                                                               | No                            | Sì            | No              | No             | Yes            |
| Distribuzione in più aree                                                                      | No                             | No             | No              | No             | Yes            |
| Più nomi di dominio personalizzati                                                                 | No                             | No              | No              | No             | Yes            |
| Portale per sviluppatori<sup>2</sup>                                                                 | No                             | Yes            | Sì            | Sì            | Yes            |
| Cache incorporata                                                                               | No                             | Yes            | Sì            | Sì            | Yes            |
| Analisi incorporata                                                                           | No                             | Yes            | Sì            | Sì            | Yes            |
| [Impostazioni SSL](api-management-howto-manage-protocols-ciphers.md)                             | Yes                            | Sì            | Sì            | Sì            | Yes            |
| [Cache esterna](https://aka.ms/apimbyoc)                                                    | Yes                           | Sì            | Sì            | Sì            | Yes            |
| [Autenticazione con certificato client](api-management-howto-mutual-certificates-for-clients.md) | Yes                | Sì            | Sì            | Sì            | Yes            |
| [Backup e ripristino](api-management-howto-disaster-recovery-backup-restore.md)               | No                            | Yes            | Sì            | Sì            | Yes            |
| [Gestione tramite Git](api-management-configuration-repository-git.md)                        | No                            | Yes            | Sì            | Sì            | Yes            |
| API di gestione diretta                                                                        | No                             | Yes            | Sì            | Sì            | Yes            |
| Metriche e log di Monitoraggio di Azure                                                               | No                | Yes            | Sì            | Sì            | Yes            |

<sup>1</sup> consente l'uso di Azure Active Directory (e Azure AD B2C) come un'identità provider per l'utente accede da portale per sviluppatori.<br/>
<sup>2</sup> Sono incluse le funzionalità correlate, ad esempio utenti, gruppi, problemi, modelli di posta elettronica e applicazioni, nonché notifiche.<br/>
