---
title: File di inclusione
description: File di inclusione
services: container-instances
author: dlepow
ms.service: container-instances
ms.topic: include
ms.date: 03/20/2018
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: da63a5418ab94623f6ce3c9f35a085dd8b198d1a
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66148989"
---
Per completare questa esercitazione, è necessario soddisfare i requisiti seguenti:

**Interfaccia della riga di comando di Azure**: è necessario che nel computer locale sia installata la versione 2.0.29 o successiva dell'interfaccia della riga di comando di Azure. Eseguire `az --version` per trovare la versione. Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure][azure-cli-install].

**Docker**: questa esercitazione presuppone una conoscenza di base dei concetti principali di Docker, tra cui contenitori, immagini dei contenitori e comandi `docker` di base. Per una panoramica sui concetti fondamentali relativi a Docker e al contenitore, vedere [Docker overview][docker-get-started] (Panoramica su Docker).

**Motore Docker**: per completare questa esercitazione, è necessario che il motore Docker sia installato in locale. Docker offre pacchetti che configurano l'ambiente Docker in [macOS][docker-mac], [Windows][docker-windows] e [Linux][docker-linux].

> [!IMPORTANT]
> Poiché Azure Cloud Shell non include il daemon Docker, per completare questa esercitazione è *necessario* installare nel *computer locale* sia l'interfaccia della riga di comando di Azure che il motore Docker. Per questa esercitazione non è possibile usare Azure Cloud Shell.

<!-- LINKS - External -->
[docker-get-started]: https://docs.docker.com/engine/docker-overview/
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-windows]: https://docs.docker.com/docker-for-windows/

<!-- LINKS - Internal -->
[azure-cli-install]: /cli/azure/install-azure-cli
