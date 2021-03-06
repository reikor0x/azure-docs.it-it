---
title: 'Esercitazione: Integrazione di Azure Active Directory con Replicon | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Replicon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 04/14/2019
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: be006cd49041a33c13b5cc5c459a1d54c46c3b47
ms.sourcegitcommit: 44a85a2ed288f484cc3cdf71d9b51bc0be64cc33
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64727614"
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>Esercitazione: Integrazione di Azure Active Directory con Replicon

Questa esercitazione descrive come integrare Replicon con Azure Active Directory (Azure AD).
L'integrazione di Replicon con Azure AD offre i vantaggi seguenti:

* È possibile controllare in Azure AD chi può accedere a Replicon.
* È possibile abilitare gli utenti per l'accesso automatico (Single Sign-On) a Replicon con gli account Azure AD personali.
* È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Replicon, sono necessari gli elementi seguenti:

* Una sottoscrizione di Azure AD. Se non si dispone di un ambiente di Azure AD, è possibile ottenere un [account gratuito](https://azure.microsoft.com/free/).
* Sottoscrizione di Replicon abilitata per l'accesso Single Sign-On

## <a name="scenario-description"></a>Descrizione dello scenario

In questa esercitazione vengono eseguiti la configurazione e il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.

* Replicon supporta l'accesso SSO avviato da **SP**

## <a name="adding-replicon-from-the-gallery"></a>Aggiunta di Replicon dalla raccolta

Per configurare l'integrazione di Replicon in Azure AD, è necessario aggiungere Replicon dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Replicon dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Pulsante Azure Active Directory](common/select-azuread.png)

2. Passare ad **Applicazioni aziendali** e quindi selezionare l'opzione **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali](common/enterprise-applications.png)

3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione](common/add-new-app.png)

4. Nella casella di ricerca digitare **Replicon**, selezionare **Replicon** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Replicon nell'elenco dei risultati](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Replicon usando un utente di test di nome **Britta Simon**.
Per il corretto funzionamento dell'accesso Single Sign-On, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Replicon.

Per configurare e testare l'accesso Single Sign-On di Azure AD con Replicon, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)** : per consentire agli utenti di usare questa funzionalità.
2. **[Configurare l'accesso Single Sign-On di Replicon](#configure-replicon-single-sign-on)** : per configurare le impostazioni di Single Sign-On sul lato applicazione.
3. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
4. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Creare un utente di test di Replicon](#create-replicon-test-user)** : per avere una controparte di Britta Simon in Replicon collegata alla rappresentazione dell'utente in Azure AD.
6. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure.

Per configurare Single Sign-On di Azure AD con Replicon, seguire questa procedura:

1. Nella pagina di integrazione dell'applicazione **Replicon** del [portale di Azure](https://portal.azure.com/) selezionare **Single Sign-On**.

    ![Collegamento Configura accesso Single Sign-On](common/select-sso.png)

2. Nella finestra di dialogo **Selezionare un metodo di accesso Single Sign-On** selezionare la modalità **SAML/WS-Fed** per abilitare il Single Sign-On.

    ![Selezione della modalità Single Sign-On](common/select-saml-option.png)

3. Nella pagina **Configura l'accesso Single Sign-On con SAML** fare clic sull'icona **Modifica** per aprire la finestra di dialogo **Configurazione SAML di base**.

    ![Modificare la configurazione SAML di base](common/edit-urls.png)

4. Nella sezione **Configurazione SAML di base** seguire questa procedura:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Replicon](common/sp-identifier-reply.png)

    a. Nella casella di testo **URL accesso** digitare un URL nel formato seguente: `https://na2.replicon.com/<companyname>/saml2/sp-sso/post`

    b. Nella casella di testo **Identificatore** digitare un URL usando il modello seguente: `https://global.replicon.com/<companyname>`

    c. Nella casella di testo **URL di risposta** digitare un URL nel formato seguente: `https://global.replicon.com/!/saml2/<companyname>/sso/post`

    > [!NOTE]
    > Poiché questi non sono i valori reali, è necessario aggiornarli con l'identificatore e l'URL di accesso effettivi. Per ottenere questi valori, contattare il [team di supporto clienti di Replicon](https://www.replicon.com/customerzone/contact-support). È anche possibile fare riferimento ai modelli mostrati nella sezione **Configurazione SAML di base** del portale di Azure.

5. Nella pagina **Configura l'accesso Single Sign-On con SAML**, nella sezione **Certificato di firma SAML**, fare clic su **Scarica** per scaricare il file **XML metadati federazione** definito dalle opzioni specificate in base ai propri requisiti e salvarlo in questo computer.

    ![Collegamento di download del certificato](common/metadataxml.png)

6. Nella sezione **Configura Replicon** copiare gli URL appropriati in base alle proprie esigenze.

    ![Copiare gli URL di configurazione](common/copy-configuration-urls.png)

    a. URL di accesso

    b. Identificatore di Azure AD

    c. URL di chiusura sessione

### <a name="configure-replicon-single-sign-on"></a>Configurare l'accesso Single Sign-On di Replicon

1. In un'altra finestra del Web browser accedere al sito aziendale di Replicon come amministratore.

2. Per configurare SAML 2.0, eseguire la procedura seguente:

    ![Abilita autenticazione SAML](./media/replicon-tutorial/ic777805.png "autenticazione SAML abilitare")

    a. Per visualizzare la finestra di dialogo **EnableSAML Authentication2** accodare i seguenti elementi all'URL, dopo la chiave della società: `/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`

    * Di seguito è illustrato lo schema dell'URL completo: `https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`

   b. Fare clic su **+** per espandere la sezione **v20Configuration**.

   c. Fare clic su **+** per espandere la sezione **metaDataConfiguration**.

   d. Fare clic su **Scegli file** per selezionare il file XML dei metadati del provider di identità, quindi scegliere **Invia**.

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

1. Nel riquadro sinistro del portale di Azure, selezionare **Azure Active Directory**, **Utenti** e quindi **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](common/users.png)

2. Selezionare **Nuovo utente** in alto nella schermata.

    ![Pulsante Nuovo utente](common/new-user.png)

3. In Proprietà utente seguire questa procedura.

    ![Finestra di dialogo Utente](common/user-properties.png)

    a. Nel campo **Nome** immettere **BrittaSimon**.
  
    b. Nel campo **Nome utente** digitare `brittasimon@yourcompanydomain.extension`. Ad esempio: BrittaSimon@contoso.com

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella Password.

    d. Fare clic su **Create**(Crea).

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Replicon.

1. Nel portale di Azure selezionare **Applicazioni aziendali**, quindi **Tutte le applicazioni** e infine **Replicon**.

    ![Pannello delle applicazioni aziendali](common/enterprise-applications.png)

2. Nell'elenco di applicazioni selezionare **Replicon**.

    ![Collegamento di Replicon nell'elenco delle applicazioni](common/all-applications.png)

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"](common/users-groups-blade.png)

4. Fare clic sul pulsante **Aggiungi utente** e quindi selezionare **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione](common/add-assign-user.png)

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti e quindi fare clic sul pulsante **Seleziona** in basso nella schermata.

6. Se si prevede un valore di ruolo nell'asserzione SAML, nella finestra di dialogo **Selezionare un ruolo** selezionare il ruolo appropriato per l'utente dall'elenco, quindi fare clic sul pulsante **Seleziona** nella parte inferiore della schermata.

7. Nella finestra di dialogo **Aggiungi assegnazione** fare clic sul pulsante **Assegna**.

### <a name="create-replicon-test-user"></a>Creare un utente di test di Replicon

Questa sezione descrive come creare un utente chiamato Britta Simon in Replicon.

**Per creare un utente manualmente, seguire questa procedura:**

1. In una finestra del Web browser accedere al sito aziendale di Replicon come amministratore.

2. Passare ad **Amministrazione \> Utenti**.

    ![Utenti](./media/replicon-tutorial/ic777806.png "Utenti")

3. Fare clic su **+Aggiungi utente**.

    ![Aggiungere un utente](./media/replicon-tutorial/ic777807.png "Aggiungere un utente")

4. Nella sezione **Profilo utente** , eseguire la procedura seguente:

    ![Profilo utente](./media/replicon-tutorial/ic777808.png "Profilo utente")

    a. Nella casella di testo **Login Name** (Nome di accesso) digitare l'indirizzo di posta elettronica dell'utente di Azure AD di cui si vuole effettuare il provisioning, ad esempio `BrittaSimon\@contoso.com`.

    b. In **Tipo di autenticazione** selezionare **SSO**.

    c. Nella casella di testo **Reparto** , digitare il reparto dell'utente.

    d. In **Tipo di dipendente** selezionare **Amministratore**.

    e. Fare clic su **Salva profilo utente**.

> [!NOTE]
> È possibile usare qualsiasi altro strumento o API di creazione di account utente offerti da Replicon per eseguire il provisioning degli account utente di Azure AD.

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro di Replicon nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Replicon per cui si è configurato l'accesso SSO. Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Risorse aggiuntive

- [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Che cos'è l'accesso condizionale in Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)