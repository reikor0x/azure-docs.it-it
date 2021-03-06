---
title: Creare un'applicazione Node.js Azure Cosmos DB tramite l'API Gremlin
description: Presenta un esempio di codice Node.js che permette di connettersi ad Azure Cosmos DB ed eseguire query sul servizio
author: luisbosquez
ms.service: cosmos-db
ms.subservice: cosmosdb-graph
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 01/08/2018
ms.author: lbosq
ms.openlocfilehash: b81cedc9376b33b27f3a742fbe5d7410535fa727
ms.sourcegitcommit: 7723b13601429fe8ce101395b7e47831043b970b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/21/2019
ms.locfileid: "56587804"
---
# <a name="quickstart-build-a-nodejs-application-by-using-azure-cosmos-db-gremlin-api-account"></a>Avvio rapido: Creare un'applicazione Node.js usando l'account dell'API Gremlin di Azure Cosmos DB

> [!div class="op_single_selector"]
> * [Console Gremlin](create-graph-gremlin-console.md)
> * [.NET](create-graph-dotnet.md)
> * [Java](create-graph-java.md)
> * [Node.js](create-graph-nodejs.md)
> * [Python](create-graph-python.md)
> * [PHP](create-graph-php.md)
>  

Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft. È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave-valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB. 

Questa guida introduttiva illustra come creare un account, un database e un grafo dell'[API Gremlin](graph-introduction.md) in Azure Cosmos DB tramite il portale di Azure. Si creerà ed eseguirà quindi un'app console usando il driver open source [Gremlin Node.js](https://www.npmjs.com/package/gremlin).

## <a name="prerequisites"></a>Prerequisiti

Prima di poter eseguire questo esempio, è necessario soddisfare i prerequisiti seguenti:
* [Node.js](https://nodejs.org/en/) versione v0.10.29 o versioni successive
* [Git](https://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creare un account di database

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Aggiungere un grafo

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a>Clonare l'applicazione di esempio

Per clonare un'app API Gremlin da GitHub, impostare la stringa di connessione ed eseguirla. Come si noterà, è facile usare i dati a livello di codice. 

1. Aprire un prompt dei comandi, creare una nuova cartella denominata git-samples e quindi chiudere il prompt dei comandi.

    ```bash
    md "C:\git-samples"
    ```

2. Aprire una finestra del terminale Git, ad esempio Git Bash, ed eseguire il comando `cd` per passare a una nuova cartella in cui installare l'app di esempio.

    ```bash
    cd "C:\git-samples"
    ```

3. Eseguire il comando seguente per clonare l'archivio di esempio. Questo comando crea una copia dell'app di esempio nel computer in uso.

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. Aprire il file della soluzione in Visual Studio. 

## <a name="review-the-code"></a>Esaminare il codice

Questo passaggio è facoltativo. Per scoprire in che modo le risorse del database vengono create nel codice, è possibile esaminare i frammenti di codice seguenti. In alternativa, è possibile passare ad [Aggiornare la stringa di connessione](#update-your-connection-string). 

Tutti i frammenti di codice seguenti sono tratti dal file app.js.

* Viene creato il client di Gremlin.

    ```javascript
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  Le configurazioni sono tutte incluse in `config.js`, che verrà modificato nella [sezione seguente](#update-your-connection-string).

* Sono definite varie funzioni per eseguire diverse operazioni Gremlin. Questa è una di esse:

    ```javascript
    function addVertex1(callback)
    {
        console.log('Running Add Vertex1'); 
        client.execute("g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44).property('userid', 1)", { }, (err, results) => {
          if (err) callback(console.error(err));
          console.log("Result: %s\n", JSON.stringify(results));
          callback(null)
        });
    }
    ```

* Ogni funzione esegue un metodo `client.execute` con un parametro di stringa della query Gremlin. Di seguito è riportato un esempio di come `g.V().count()` viene eseguito:

    ```javascript
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

* Alla fine del file vengono richiamati tutti i metodi usando il metodo `async.waterfall()`. In questo modo vengono eseguiti uno dopo l'altro:

    ```javascript
    try{
        async.waterfall([
            dropGraph,
            addVertex1,
            addVertex2,
            addEdge,
            countVertices
            ], finish);
    } catch(err) {
        console.log(err)
    }
    ```


## <a name="update-your-connection-string"></a>Aggiornare la stringa di connessione

1. Aprire il file config.js. 

2. In config.js compilare la chiave `config.endpoint` con il valore **URI Gremlin** disponibile nella pagina **Panoramica** del portale di Azure. 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Visualizzazione e copia di una chiave di accesso nel portale di Azure, pannello Chiavi](./media/create-graph-nodejs/gremlin-uri.png)

   Se il valore di **URI Gremlin** è vuoto, è possibile generarlo dalla pagina **Chiavi** nel portale. Usare il valore di **URI**, rimuovere https:// e sostituire documents con gremlin.cosmosdb. Se l'account Graph è stato creato prima del 20 dicembre 2017, sostituire documents con graphs. 

   L'endpoint Gremlin deve essere solo il nome host senza protocollo/numero di porta, ad esempio `mygraphdb.gremlin.cosmosdb.azure.com` (non `https://mygraphdb.gremlin.cosmosdb.azure.com` o `mygraphdb.gremlin.cosmosdb.azure.com:433`).

3. Nel file config.js compilare il valore di config.primaryKey con il valore **Chiave primaria** disponibile nella pagina **Chiavi** del portale di Azure. 

    `config.primaryKey = "PRIMARYKEY";`

   ![Pannello "Chiavi" del portale di Azure](./media/create-graph-nodejs/keys.png)

4. Immettere il nome del database e il nome del grafo (contenitore) per il valore di config.database e config.collection. 

Ecco un esempio dell'aspetto che dovrebbe avere il file config.js completato:

```javascript
var config = {}

// Note that this must not have HTTPS or the port number
config.endpoint = "testgraphacct.gremlin.cosmosdb.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-the-console-app"></a>Eseguire l'app console

1. Aprire una finestra del terminale e usare il comando `cd` per passare alla directory di installazione del file package.json incluso nel progetto.

2. Eseguire `npm install` per installare i moduli npm necessari, tra cui `gremlin`.

3. Eseguire `node app.js` in un terminale per avviare l'applicazione Node.js.

## <a name="browse-with-data-explorer"></a>Esplorare con Esplora dati

È ora possibile tornare a Esplora dati nel portale di Azure per visualizzare, modificare e usare i nuovi dati del grafo ed eseguire query su di essi.

In Esplora dati il nuovo database viene visualizzato nel riquadro **Graph**. Espandere il database e il contenitore, quindi fare clic su **Graph**.

I dati generati dall'app di esempio vengono visualizzati nel riquadro successivo nella scheda **Graph** quando si fa clic su **Applica filtro**.

Provare a completare `g.V()` con `.has('firstName', 'Thomas')` per testare il filtro. Il valore distingue tra maiuscole e minuscole.

## <a name="review-slas-in-the-azure-portal"></a>Esaminare i contratti di servizio nel portale di Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a>Pulire le risorse

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a>Passaggi successivi

In questo articolo si è appreso come creare un account Azure Cosmos DB, come creare un grafo con Esplora dati e come eseguire un'app. È ora possibile creare query più complesse e implementare la potente logica di attraversamento dei grafi usando Gremlin. 

> [!div class="nextstepaction"]
> [Eseguire query con Gremlin](tutorial-query-graph.md)
