---
title: File di inclusione
description: File di inclusione
services: iot-central
author: dominicbetts
ms.service: iot-central
ms.topic: include
ms.date: 04/09/2019
ms.author: dobett
ms.custom: include file
ms.openlocfilehash: eae4b1e919270413d4ca6627964fad9c7f5bd9bf
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66151977"
---
1. Usare il `dps-keygen` utilità della riga di comando per generare una stringa di connessione:

    Per installare il [utilità di generazione della chiave](https://github.com/Azure/dps-keygen), eseguire il comando seguente:

    ```cmd/sh
    npm i -g dps-keygen
    ```

1. Per generare una stringa di connessione, eseguire il comando seguente con i dettagli della connessione annotata in precedenza:

    ```cmd/sh
    dps-keygen -di:<Device ID> -dk:<Primary or Secondary Key> -si:<Scope ID>
    ```

1. Copiare la stringa di connessione di `dps-keygen` output per l'uso del codice di dispositivo.