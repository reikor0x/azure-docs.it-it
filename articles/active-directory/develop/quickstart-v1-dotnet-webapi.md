---
title: Creare un'API Web .NET che si integra con Azure AD per l'autenticazione e l'autorizzazione| Microsoft Docs
description: Come compilare un'API Web MVC per Node.js che si integra con Azure AD per l'autenticazione e l'autorizzazione.
services: active-directory
documentationcenter: .net
author: rwike77
manager: CelesteDG
editor: ''
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.subservice: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 05/21/2019
ms.author: ryanwi
ms.reviewer: jmprieur, andret
ms.custom: aaddev
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e2eca253bc5d1495d26506e0e6f8a83762e8bc5
ms.sourcegitcommit: 13cba995d4538e099f7e670ddbe1d8b3a64a36fb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66001101"
---
# <a name="quickstart-build-a-net-web-api-that-integrates-with-azure-ad-for-authentication-and-authorization"></a>Guida introduttiva: Compilare un'API Web .NET che si integra con Azure AD per l'autenticazione e l'autorizzazione

[!INCLUDE [active-directory-develop-applies-v1](../../../includes/active-directory-develop-applies-v1.md)]

Se si compila un'applicazione che fornisce l'accesso alle risorse protette, è necessario sapere come prevenire l'accesso non protetto a tali risorse. Azure Active Directory (Azure AD) rende semplici e dirette le operazioni per la protezione di un'API Web usando i token di connessione dell'accesso di OAuth 2.0 con solo poche righe di codice.

Nelle app Web Asp.NET, a questo scopo si usa l'implementazione di Microsoft del middleware OWIN gestito dalla community e incluso in .NET Framework 4.5. Qui OWIN verrà usato per creare un'API Web "Elenco attività" in grado di:

* Designare le API protette.
* Verificare che le chiamate all'API Web contengano un token di accesso valido.

In questa guida introduttiva verrà creta l'API To Do List e verrà appreso come:

1. Registrare un'applicazione con Azure AD.
2. Configurare l'app per l'uso della pipeline di autenticazione OWIN.
3. Configurare un'applicazione client per chiamare l'API Web.

## <a name="prerequisites"></a>Prerequisiti

Per iniziare, completare questi prerequisiti:

* Scaricare la [struttura dell'app](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) oppure l'[esempio completato](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Ognuno è una soluzione di Visual Studio 2013.
* È necessario anche un tenant di Azure AD in cui registrare l'applicazione. Se non si ha già un tenant, vedere le [informazioni su come ottenerne uno](quickstart-create-new-tenant.md).

## <a name="step-1-register-an-application-with-azure-ad"></a>Passaggio 1: Registrare un'applicazione con Azure AD.

Per proteggere l'applicazione, si dovrà per prima cosa creare un'applicazione nel proprio tenant e fornire ad Azure AD alcune informazioni fondamentali.

1. Accedere al [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure AD selezionando l'account nell'angolo superiore destro della pagina. Selezionare il menu di spostamento **Cambia directory** e selezionare il tenant appropriato.
    * Ignorare questo passaggio se è presente un solo tenant di Azure AD nell'account o se è già stato selezionato il tenant di Azure AD appropriato.

3. Selezionare **Azure Active Directory** nel riquadro di navigazione a sinistra.
4. Selezionare **Registrazioni app** e quindi **Nuova registrazione**.
5. Nella pagina **Registra un'applicazione** visualizzata immettere il nome dell'applicazione.
In **Tipi di account supportati** selezionare **Account in qualsiasi directory organizzativa e account Microsoft personali**.
6. Selezionare la piattaforma **Web** nella sezione **URI di reindirizzamento** e impostare il valore su `https://localhost:44321/`, corrispondente alla posizione in cui Azure AD restituirà i token.
7. Al termine, selezionare **Registra**. Nella pagina **Panoramica**  dell'app prendere nota del valore del campo **ID applicazione (client)** .
6. Selezionare **Esporre un'API** e quindi aggiornare l'URI dell'ID applicazione facendo clic su **Imposta**. Immettere un identificatore specifico del tenant. Ad esempio, immettere `https://contoso.onmicrosoft.com/TodoListService`.
7. Salvare la configurazione. Lasciare aperto il portale, poiché tra poco si dovrà registrare anche l'applicazione client.

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a>Passaggio 2: Configurare l'app per l'uso della pipeline di autenticazione OWIN

Per convalidare le richieste in ingresso e i token, è necessario configurare l'applicazione per la comunicazione con Azure AD.

1. Per iniziare, aprire la soluzione e aggiungere i pacchetti NuGet del middleware OWIN al progetto TodoListService usando la Console di Gestione pacchetti.

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. Aggiungere al progetto TodoListService una OWIN Startup Class denominata `Startup.cs`.  Fare clic con il pulsante destro del mouse sul progetto, scegliere **Aggiungi > Nuovo** elemento e cercare **OWIN**. Il middleware OWIN richiamerà il metodo `Configuration(…)` all'avvio dell'app.

3. Modificare la dichiarazione di classe in `public partial class Startup`. Parte di questa classe è stata già implementata in un altro file. Nel metodo `Configuration(…)` effettuare una chiamata a `ConfgureAuth(…)` per configurare l'autenticazione per l'app Web.

    ```csharp
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. Aprire il file `App_Start\Startup.Auth.cs` e implementare il metodo `ConfigureAuth(…)`. I parametri forniti in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` fungeranno da coordinate per consentire all'app di comunicare con Azure AD. Per usarli è necessario specificare le classi dello spazio dei nomi `System.IdentityModel.Tokens`.

    ```csharp
    using System.IdentityModel.Tokens;
    ```

    ```csharp
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                 Tenant = ConfigurationManager.AppSettings["ida:Tenant"],
                 TokenValidationParameters = new TokenValidationParameters
                 {
                    ValidAudience = ConfigurationManager.AppSettings["ida:Audience"]
                 }
            });
    }
    ```

5. Usare gli attributi `[Authorize]` per proteggere i controller e le azioni con l'autenticazione della connessione al token JSON Web (JWT). Decorare la classe `Controllers\TodoListController.cs` con un tag di autorizzazione, che impone all'utente di eseguire l'accesso prima di accedere a tale pagina.

    ```csharp
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    Quando un chiamante autorizzato riesce a chiamare una delle API `TodoListController` , l'azione potrebbe richiedere l'accesso alle informazioni relative al chiamante. OWIN fornisce l'accesso alle attestazioni all'interno del token di connessione tramite l'oggetto `ClaimsPrincpal` .  

6. Un requisito comune per le API Web riguarda la convalida degli "ambiti" presenti nel token per assicurare che l'utente abbia acconsentito alle autorizzazioni richieste per accedere a To do List Service.

    ```csharp
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. Aprire il file `web.config` nella radice del progetto TodoListService e immettere i valori di configurazione nella sezione `<appSettings>`.
    * `ida:Tenant` è il nome del tenant di Azure AD, ad esempio contoso.onmicrosoft.com.
    * `ida:Audience` è l'URI ID app dell'applicazione immesso nel portale di Azure.

## <a name="step-3-configure-a-client-application-and-run-the-service"></a>Passaggio 3: Configurare un'applicazione client ed eseguire il servizio

Prima di poter vedere To Do List Service in azione, è necessario configurare To Do List Client, in modo che possa ricevere i token da Azure AD ed effettuare chiamate al servizio.

1. Tornare al [portale di Azure](https://portal.azure.com).
1. Creare una nuova registrazione dell'applicazione nel tenant di Azure AD.  Nel campo **Nome** specificare un nome descrittivo dell'applicazione per gli utenti, immettere `http://TodoListClient/` come valore di **URI di reindirizzamento** e quindi selezionare **Client pubblico (per dispositivi mobili e desktop)** dall'elenco a discesa.
1. Dopo aver completato la registrazione, Azure AD assegna all'app un ID applicazione univoco. Poiché questo valore sarà necessario nelle sezioni successive, copiarlo dalla pagina dell'applicazione.
1. Selezionare **Autorizzazioni API** e quindi **Aggiungi un'autorizzazione**.  Individuare e selezionare To Do List Service, aggiungere l'autorizzazione **user_impersonation Access TodoListService** in **Autorizzazioni delegate** e quindi selezionare **Aggiungi autorizzazioni**.
1. In Visual Studio aprire `App.config` nel progetto TodoListClient e quindi immettere i valori di configurazione nella sezione `<appSettings>`.

    * `ida:Tenant` è il nome del tenant di Azure AD, ad esempio contoso.onmicrosoft.com.
    * `ida:ClientId` è l'ID app copiato dal portale di Azure.
    * `todo:TodoListResourceId` è l'URI ID app dell'applicazione To Do List Service immesso nel portale di Azure.

1. Pulire, compilare ed eseguire ogni progetto.
1. Se non si è ancora creato un nuovo utente nel tenant con un dominio *.onmicrosoft.com, ora è possibile farlo.
1. Accedere al client To Do List come l'utente creato e aggiungere alcune attività all'elenco delle attività dell'utente.

## <a name="next-steps"></a>Passaggi successivi

* Per riferimento, scaricare l'esempio completato, che non contiene i valori di configurazione immessi durante la procedura sopra indicata da [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). È ora possibile passare ad altri scenari relativi alle identità.
