---
title: "Autenticazione dell'utente finale: Azure Data Lake Store Gen1 con Azure Active Directory | Microsoft Docs"
description: Informazioni su come ottenere l'autenticazione dell'utente finale con Azure Data Lake Storage Gen1 tramite Azure Active Directory
services: data-lake-store
documentationcenter: ''
author: twooley
manager: mtillman
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: twooley
ms.openlocfilehash: 4c2b774c304e46f9fc68f3beaf64218e614ecad1
ms.sourcegitcommit: 509e1583c3a3dde34c8090d2149d255cb92fe991
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2019
ms.locfileid: "66234064"
---
# <a name="end-user-authentication-with-azure-data-lake-storage-gen1-using-azure-active-directory"></a>Autenticazione dell'utente finale con Azure Data Lake Storage Gen1 tramite Azure Active Directory
> [!div class="op_single_selector"]
> * [Autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md)
> * [Autenticazione da servizio a servizio](data-lake-store-service-to-service-authenticate-using-active-directory.md)
> 
> 

Per eseguire l'autenticazione, Azure Data Lake Storage Gen1 usa Azure Active Directory. Prima di creare un'applicazione che funzioni con Data Lake Storage Gen1 o Azure Data Lake Analytics, è necessario stabilire come autenticare l'applicazione con Azure Active Directory (Azure AD). Le opzioni disponibili sono due:

* Autenticazione dell'utente finale (questo articolo)
* Autenticazione da servizio a servizio (selezionare questa opzione dall'elenco a discesa precedente)

Entrambe queste opzioni comportano che l'applicazione venga fornita con un token OAuth 2.0 che viene associato a ogni richiesta effettuata a Data Lake Storage Gen1 o Azure Data Lake Analytics.

Questo articolo illustra come creare un'**applicazione nativa di Azure AD per l'autenticazione dell'utente finale**. Per istruzioni sulla configurazione dell'applicazione Azure AD per l'autenticazione da servizio a servizio, vedere [Autenticazione da servizio a servizio con Data Lake Storage Gen1 tramite Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Prerequisiti
* Una sottoscrizione di Azure. Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

* ID sottoscrizione personale. È possibile recuperarlo dal portale di Azure. Ad esempio, è disponibile dal pannello dell'account Data Lake Storage Gen1.
  
    ![Ottenere l'ID sottoscrizione](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* Il nome di dominio di Azure AD. È possibile recuperarlo passando il cursore del mouse sull'angolo superiore destro del portale di Azure. Nello screenshot seguente il nome di dominio è **contoso.onmicrosoft.com**, mentre il GUID racchiuso tra parentesi quadre è l'ID tenant. 
  
    ![Ottenere il dominio AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

* ID del tenant di Azure. Per istruzioni su come recuperare l'ID tenant, vedere [Ottenere l'ID tenant](../active-directory/develop/howto-create-service-principal-portal.md#get-values-for-signing-in).

## <a name="end-user-authentication"></a>Autenticazione dell'utente finale
Questo meccanismo di autenticazione è l'approccio consigliato se si desidera che un utente finale di accedere all'applicazione tramite Azure AD. L'applicazione può quindi accedere alle risorse di Azure con lo stesso livello di accesso dell'utente che ha effettuato l'accesso. L'utente finale deve fornire le sue credenziali periodicamente affinché l'applicazione possa mantenere attivo l'accesso.

Il risultato di disporre di accesso l'utente finale è che l'applicazione viene assegnato un token di accesso e un token di aggiornamento. Il token di accesso viene associato a ogni richiesta effettuata a Data Lake Storage Gen1 o Data Lake Analytics ed è valido per un'ora per impostazione predefinita. Il token di aggiornamento può essere usato per ottenere un nuovo token di accesso e, per impostazione predefinita, è valido per un massimo di due settimane. È possibile usare due diversi approcci per l'accesso degli utenti finali.

### <a name="using-the-oauth-20-pop-up"></a>Usando la finestra popup OAuth 2.0
L'applicazione può attivare una finestra popup di autorizzazione OAuth 2.0, in cui l'utente finale può immettere le credenziali. Questa opzione funziona anche con il processo di autenticazione a due fattori (2FA) di Azure AD, se necessario. 

> [!NOTE]
> Questo metodo non è ancora supportato in Azure AD Authentication Library (ADAL) per Python o Java.
> 
> 

### <a name="directly-passing-in-user-credentials"></a>Accesso diretto tramite le credenziali dell'utente
L'applicazione può fornire direttamente le credenziali utente ad Azure AD. Questo metodo funziona solo con gli account utente con ID aziendale. Non è compatibile con gli account utente personali o con "Live ID", inclusi quelli che terminano con @outlook.com o @live.com. Inoltre, questo metodo non è compatibile con gli account utente che richiedono l'autenticazione a due fattori (2FA) di Azure AD.

### <a name="what-do-i-need-for-this-approach"></a>Di cosa ho bisogno per questo approccio?
* Il nome di dominio di Azure AD. Questo requisito è già elencato nei prerequisiti riportati in questo articolo.
* ID tenant di Azure AD. Questo requisito è già elencato nei prerequisiti riportati in questo articolo.
* **L'applicazione nativa** di Azure AD
* L'ID applicazione per l'applicazione nativa di Azure AD
* L'URI di reindirizzamento per l'applicazione nativa di Azure AD
* Impostare autorizzazioni delegate


## <a name="step-1-create-an-active-directory-native-application"></a>Passaggio 1: Creare un'applicazione nativa di Active Directory

Creare e configurare un'applicazione nativa di Azure AD per l'autenticazione dell'utente finale con Data Lake Storage Gen1 tramite Azure Active Directory. Per istruzioni, vedere [Creare un'applicazione Azure AD](../active-directory/develop/howto-create-service-principal-portal.md).

Mentre si seguono le istruzioni nel collegamento, assicurarsi di selezionare **Nativo** come tipo di applicazione, come illustrato nello screenshot seguente:

![Creare un'app Web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Creare un'app nativa")

## <a name="step-2-get-application-id-and-redirect-uri"></a>Passaggio 2: Ottieni ID applicazione e URI di reindirizzamento

Per recuperare l'ID applicazione, vedere [Ottenere l'ID applicazione](../active-directory/develop/howto-create-service-principal-portal.md#get-values-for-signing-in).

Per recuperare l'URI di reindirizzamento, attenersi alla procedura seguente.

1. Dal portale di Azure selezionare **Azure Active Directory**, fare clic su **Registrazioni per l'app**, trovare l'applicazione nativa di Azure AD Azure creata e fare clic su di essa.

2. Dal pannello **Impostazioni** per l'applicazione fare clic su **URI di reindirizzamento**.

    ![Ottenere l'URI di reindirizzamento](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. Copiare il valore visualizzato.


## <a name="step-3-set-permissions"></a>Passaggio 3: Impostare le autorizzazioni

1. Dal portale di Azure selezionare **Azure Active Directory**, fare clic su **Registrazioni per l'app**, trovare l'applicazione nativa di Azure AD Azure creata e fare clic su di essa.

2. Dal pannello **Impostazioni** dell'applicazione selezionare **Autorizzazioni necessarie** e fare clic su **Aggiungi**.

    ![ID client](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. Nel pannello **Aggiungi accesso all'API** fare clic su **Selezionare un'API**, fare clic su **Azure Data Lake**, quindi fare clic su **Seleziona**.

    ![ID client](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  Nel pannello **Aggiungi accesso all'API** fare clic su **Selezionare le autorizzazioni**, selezionare la casella di controllo per concedere l'**accesso completo a Data Lake Store** e quindi fare clic su **Seleziona**.

    ![ID client](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    Fare clic su **Done**.

5. Ripetere gli ultimi due passaggi per concedere le autorizzazioni anche per le **API Gestione dei servizi di Windows Azure**.
   
## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stata creata un'applicazione nativa di Azure AD e sono state raccolte le informazioni necessarie nelle applicazioni client create usando .NET SDK, Java SDK, API REST e così via. È ora possibile passare agli articoli seguenti che illustrano come usare l'applicazione Web di Azure AD per eseguire prima l'autenticazione con Data Lake Storage Gen1 e quindi altre operazioni nell'archivio.

* [Autenticazione dell'utente finale con Data Lake Storage Gen1 tramite Java SDK](data-lake-store-end-user-authenticate-java-sdk.md)
* [Autenticazione dell'utente finale con Data Lake Storage Gen1 tramite .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md)
* [Autenticazione dell'utente finale con Data Lake Storage Gen1 tramite Python](data-lake-store-end-user-authenticate-python.md)
* [Autenticazione dell'utente finale con Data Lake Storage Gen1 tramite API REST](data-lake-store-end-user-authenticate-rest-api.md)

