---
title: 'Esempio di criteri di Gestione API di Azure: aggiungere funzionalità a un servizio back-end | Microsoft Docs'
description: Esempio di criteri di Gestione API di Azure che illustra come aggiungere funzionalità a un servizio back-end, ad esempio per accettare il nome di un luogo anziché latitudine e longitudine in un'API di previsioni meteo.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/13/2017
ms.author: apimpm
ms.openlocfilehash: 7c9edbf4b2d231453cd336521a04ba6b7714b696
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "61062208"
---
# <a name="add-capabilities-to-a-backend-service"></a>Aggiungere funzionalità a un servizio back-end

Questo articolo offre un esempio di criteri di Gestione API di Azure che illustra come aggiungere funzionalità a un servizio back-end, ad esempio per accettare il nome di un luogo anziché latitudine e longitudine in un'API di previsioni meteo. Per impostare o modificare il codice dei criteri, seguire la procedura descritta nell'articolo su come [impostare o modificare criteri](../set-edit-policies.md). Per altri esempi, vedere l'articolo relativo agli [esempi di criteri](../policy-samples.md).

## <a name="policy"></a>Policy

Incollare il codice nel blocco **inbound**.

[!code-xml[Main](../../../api-management-policy-samples/examples/Call out to an HTTP endpoint and cache the response.policy.xml)]

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sui criteri di Gestione API:

+ [Criteri di trasformazione](../api-management-transformation-policies.md)
+ [Esempi di criteri](../policy-samples.md)

