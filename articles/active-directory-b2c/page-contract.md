---
title: Selezionare un contratto di pagina - Azure Active Directory B2C | Microsoft Docs
description: Informazioni su come selezionare un contratto di pagina in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: celestedg
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/25/2019
ms.author: davidmu
ms.subservice: B2C
ms.openlocfilehash: 4cd29df19179f07fd9b61a2f484b1d49cc05c4cf
ms.sourcegitcommit: 44a85a2ed288f484cc3cdf71d9b51bc0be64cc33
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64570569"
---
# <a name="select-a-page-contract-in-azure-active-directory-b2c-using-custom-policies"></a>Selezionare un contratto di pagina in Azure Active Directory B2C tramite criteri personalizzati

[!INCLUDE [active-directory-b2c-public-preview](../../includes/active-directory-b2c-public-preview.md)]

È possibile abilitare il codice lato client JavaScript nei criteri di Azure Active Directory (Azure AD) B2C, indipendentemente dal fatto che si usino flussi utente o criteri personalizzati. Per abilitare JavaScript per le applicazioni, è necessario aggiungere un elemento per il [criteri personalizzati](active-directory-b2c-overview-custom.md), selezionare un contratto di pagina e usare [b2clogin.com](b2clogin.md) nelle richieste. Un contratto di pagina è un'associazione di elementi forniti da Azure AD B2C e del contenuto fornito dall'utente. Questo articolo illustra come selezionare un contratto di pagina in Azure AD B2C mediante la configurazione in un criterio personalizzato.

> [!NOTE]
> Se si desidera abilitare JavaScript per i flussi utente, vedere [JavaScript e pagina Contratto di versioni in Azure Active Directory B2C](user-flow-javascript-overview.md).

## <a name="replace-datauri-values"></a>Sostituire i valori di DataUri

Nei criteri personalizzati possono essere inclusi elementi [ContentDefinition](contentdefinitions.md) che definiscono i modelli HTML usati nel percorso utente. L'elemento **ContentDefinition** contiene un elemento **DataUri** che fa riferimento agli elementi della pagina forniti da Azure AD B2C. L'elemento **LoadUri** è il percorso relativo del contenuto HTML e CSS specificato dall'utente.

```XML
<ContentDefinition Id="api.idpselections">
  <LoadUri>~/tenant/default/idpSelector.cshtml</LoadUri>
  <RecoveryUri>~/common/default_page_error.html</RecoveryUri>
  <DataUri>urn:com:microsoft:aad:b2c:elements:contract:providerselection:1.0.0</DataUri>
  <Metadata>
    <Item Key="DisplayName">Idp selection page</Item>
    <Item Key="language.intro">Sign in</Item>
  </Metadata>
</ContentDefinition>
```

Per selezionare un contratto di pagina, è necessario modificare i valori di **DataUri** negli elementi [ContentDefinition](contentdefinitions.md) nei criteri. Passando dai valori di **DataUri** precedenti a quelli nuovi, si seleziona un pacchetto non modificabile. Il vantaggio dell'uso di questo pacchetto è la certezza che non cambierà e non provocherà un comportamento imprevisto nella pagina. 

Per configurare un contratto di pagina, usare la tabella seguente per trovare i valori di **DataUri**. 

| Valore di DataUri precedente | Nuovo valore di DataUri |
| ----------------- | ----------------- |
| urn:com:microsoft:aad:b2c:elements:idpselection:1.0.0 | urn:com:microsoft:aad:b2c:elements:contract:providerselection:1.0.0 |
| urn:com:microsoft:aad:b2c:elements:unifiedssd:1.0.0 | urn:com:microsoft:aad:b2c:elements:contract:unifiedssd:1.0.0 | 
| urn:com:microsoft:aad:b2c:elements:claimsconsent:1.0.0 | urn:com:microsoft:aad:b2c:elements:contract:claimsconsent:1.0.0 |
| urn:com:microsoft:aad:b2c:elements:multifactor:1.0.0 | urn:com:microsoft:aad:b2c:elements:contract:multifactor:1.0.0 |
| urn:com:microsoft:aad:b2c:elements:multifactor:1.1.0 | urn:com:microsoft:aad:b2c:elements:contract:multifactor:1.1.0 |
| urn:com:microsoft:aad:b2c:elements:selfasserted:1.0.0 | urn:com:microsoft:aad:b2c:elements:contract:selfasserted:1.0.0 |
| urn:com:microsoft:aad:b2c:elements:selfasserted:1.1.0 | urn:com:microsoft:aad:b2c:elements:contract:selfasserted:1.1.0 | 
| urn:com:microsoft:aad:b2c:elements:unifiedssp:1.0.0 | urn:com:microsoft:aad:b2c:elements:contract:unifiedssp:1.0.0 |
| urn:com:microsoft:aad:b2c:elements:unifiedssp:1.1.0 | urn:com:microsoft:aad:b2c:elements:contract:unifiedssp:1.1.0 |
| urn:com:microsoft:aad:b2c:elements:globalexception:1.0.0 | urn:com:microsoft:aad:b2c:elements:contract:globalexception:1.0.0 |
| urn:com:microsoft:aad:b2c:elements:globalexception:1.1.0 | urn:com:microsoft:aad:b2c:elements:contract:globalexception:1.1.0 |

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni su come personalizzare l'interfaccia utente delle applicazioni sono disponibili nell'argomento [Personalizzare l'interfaccia utente dell'applicazione usando un criterio personalizzato in Azure Active Directory B2C](active-directory-b2c-ui-customization-custom.md).



