---
title: Esempi di interfaccia della riga di comando di Azure per Azure Cosmos DB
description: Esempi dell'interfaccia della riga di comando di Azure - Creare e gestire account, database, contenitori, aree e firewall di Azure Cosmos DB.
author: markjbrown
ms.service: cosmos-db
ms.topic: sample
ms.date: 10/26/2018
ms.author: mjbrown
ms.reviewer: sngun
ms.openlocfilehash: a6348024d4e84c27610f1294f916cca9a851b6b9
ms.sourcegitcommit: 8330a262abaddaafd4acb04016b68486fba5835b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2019
ms.locfileid: "54034200"
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a>Esempi dell'interfaccia della riga di comando di Azure Cosmos DB

La tabella seguente include collegamenti a esempi di script di interfaccia della riga di comando di Azure per Azure Cosmos DB. Per tutti i comandi dell'interfaccia della riga di comando di Azure Cosmos DB sono disponibili pagine di riferimento in [Informazioni di riferimento sull'interfaccia della riga di comando di Azure](/cli/azure/cosmosdb).

| |  |
|---|---|
|**Creare account di database e contenitori di Azure Cosmos DB**||
| [Creare un account Azure Cosmos DB usando l'API SQL](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Crea un singolo account, un database e un contenitore Azure Cosmos DB. |
| [Creare un account Azure Cosmos DB usando l'API Cosmos DB per MongoDB](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un singolo account, un database e una raccolta Azure Cosmos DB. |
| [Creare un account Azure Cosmos DB usando l'API Gremlin](scripts/create-gremlin-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un singolo account, un database e un grafo Azure Cosmos DB. |
| [Creare un account Azure Cosmos DB usando l'API Cassandra](scripts/create-cassandra-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un singolo account e un database Azure Cosmos DB. |
| [Creare un account Azure Cosmos DB usando l'API Tabella](scripts/create-table-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un singolo account, un database e una tabella di Azure Cosmos DB. |
|**Scalare Azure Cosmos DB**||
| [Scalare la velocità effettiva del contenitore](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Modifica la velocità effettiva con provisioning in un contenitore.|
| [Replicare l'account di database di Azure Cosmos DB in più aree e configurare le priorità di failover](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Replica a livello globale i dati dell'account in più aree con una priorità di failover specificata.|
|**Proteggere Azure Cosmos DB**||
| [Ottenere le chiavi dell'account](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Ottiene le chiavi di scrittura master primarie e secondarie e le chiavi di sola lettura primarie e secondarie per l'account.|
| [Ottenere la stringa di connessione per l'account Cosmos configurata con l'API di Azure Cosmos DB per MongoDB](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Ottiene la stringa di connessione per connettere l'app MongoDB all'account Azure Cosmos DB.|
| [Rigenerare le chiavi dell'account](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Rigenera le chiavi per l'account.|
| [Creare un firewall](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Crea un criterio di controllo di accesso IP in ingresso per limitare l'accesso all'account da un set di macchine e/o servizi cloud approvati.|
|**Disponibilità elevata, ripristino di emergenza, backup e ripristino**||
| [Configurare i criteri di failover](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Imposta la priorità di failover di ogni area in cui l'account viene replicato.|
|**Connettere Azure Cosmos DB alle risorse**||
| [Connettere un'app Web ad Azure Cosmos DB](../app-service/scripts/cli-connect-to-documentdb.md?toc=%2fcli%2fazure%2ftoc.json)|Creare e collegare un database Azure Cosmos DB e un'app Web di Azure.|
|||
