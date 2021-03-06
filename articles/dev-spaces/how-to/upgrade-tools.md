---
title: Aggiornare gli strumenti di Azure Dev Spaces
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
author: zr-msft
ms.author: zarhoads
ms.date: 07/03/2018
ms.topic: conceptual
description: Sviluppo rapido Kubernetes con contenitori e microservizi in Azure
keywords: Docker, Kubernetes, Azure, servizio Azure Kubernetes, servizio Azure Container, contenitori
ms.openlocfilehash: 4e0a3c5aa849799872371ef1c5ac0867babffebb
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60686420"
---
# <a name="how-to-upgrade-azure-dev-spaces-tools"></a>Aggiornare gli strumenti di Azure Dev Spaces

Se è presente una nuova versione e si sta già usando Azure Dev Spaces, potrebbe essere necessario aggiornare gli strumenti client di Azure Dev Spaces.

## <a name="update-the-azure-cli"></a>Aggiornare l'interfaccia della riga di comando di Azure

Quando si aggiorna l'interfaccia della riga di comando di Azure più recente, è anche possibile ottenere la versione più recente dell'estensione dell'interfaccia della riga di comando per Dev Spaces.

Non è necessario disinstallare la versione precedente: basta individuare solo il download all'indirizzo dell'[interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli?view=azure-cli-latest).


## <a name="update-the-dev-spaces-cli-extension-and-command-line-tools"></a>Aggiornare l'estensione dell'interfaccia della riga di comando di Dev Spaces e gli strumenti da riga di comando

Eseguire il comando seguente:

```cmd
az aks use-dev-spaces -n <your-aks-cluster> -g <your-aks-cluster-resource-group> --update
```

## <a name="update-the-vs-code-extension"></a>Aggiornare l'estensione di Visual Studio Code

Una volta installata, l'estensione viene aggiornata automaticamente. Per usare delle nuove funzionalità potrebbe essere necessario ricaricare l'estensione. In Visual Studio Code, aprire il riquadro **Estensioni**, scegliere le estensioni **Azure Dev Spaces**, quindi scegliere **Ricarica**.

## <a name="update-the-visual-studio-extension"></a>Aggiornare l'estensione di Visual Studio

Come con altre estensioni e aggiornamenti, Visual Studio informerà quando un aggiornamento è disponibile per Visual Studio Tools per Kubernetes, che include Azure Dev Spaces. Cercare un'icona di contrassegno nella parte superiore destra della schermata.

Per aggiornare gli strumenti di Visual Studio, scegliere la voce di menu **Strumenti > Estensioni e aggiornamenti** e, a sinistra, scegliere **Aggiornamenti**. Individuare **Visual Studio Tools per Kubernetes** e scegliere il pulsante **Aggiorna**.

## <a name="next-steps"></a>Passaggi successivi

Testare i nuovi strumenti mediante la creazione di un nuovo cluster. Provare le guide introduttive e le esercitazioni in [Azure Dev Spaces](/azure/dev-spaces).

> [!WARNING]
> Ad Azure Dev Spaces nei cluster esistenti non verranno applicate immediatamente delle patch. Per accertarsi di stare usando la versione più recente in tutte le distribuzioni di Azure, creare quindi un nuovo cluster dopo l'aggiornamento degli strumenti.
