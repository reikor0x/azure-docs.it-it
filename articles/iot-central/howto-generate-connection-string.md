---
title: Generare una stringa di connessione del dispositivo per Azure IoT Central | Microsoft Docs
description: Come uno sviluppatore di dispositivi, come è possibile generare una stringa di connessione per il dispositivo che deve connettersi a un'applicazione IoT Central?
author: dominicbetts
ms.author: dobett
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: philmea
ms.openlocfilehash: f302cbfa7152ae30be434f560c0c39056d40f9f4
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60885651"
---
# <a name="generate-a-device-connection-string-to-connect-to-an-azure-iot-central-application"></a>Generare una stringa di connessione del dispositivo per la connessione a un'applicazione Azure IoT Central

Questo articolo descrive come, come uno sviluppatore di dispositivi, per generare una stringa di connessione per il dispositivo che deve connettersi a un'applicazione IoT Central. La procedura descritta in questo articolo illustra come connettere rapidamente un singolo dispositivo tramite una firma di accesso condiviso (SAS). Questo approccio è utile quando si esegue la sperimentazione con IoT Central o si testano i dispositivi. Per approcci alternativi da usare in un ambiente di produzione, vedere [connettività dei dispositivi in Azure IoT Central](concepts-connectivity.md).

## <a name="prerequisites"></a>Prerequisiti

Per seguire la procedura descritta in questo articolo, sono necessari gli elementi seguenti:

- Un'applicazione Azure IoT Central. Per altre informazioni, vedere la [guida introduttiva per la creazione di un'applicazione](quick-deploy-iot-central.md).
- Un computer di sviluppo con [Node. js](https://nodejs.org/) version 8.0.0 installato o versione successiva. Per controllare la versione, è possibile eseguire `node --version` nella riga di comando. Node.js è disponibile per un'ampia gamma di sistemi operativi.

## <a name="get-connection-information"></a>Ottenere informazioni di connessione

I passaggi seguenti descrivono come ottenere le informazioni necessarie per generare una stringa di connessione di firma di accesso condiviso per un dispositivo:

1. Nel **Device Explorer**, trovare il dispositivo reale si desidera connettersi all'applicazione:

    ![Selezionare un dispositivo reale](media/howto-generate-connection-string/real-devices.png)

1. Nel **periferica** pagina, selezionare **Connect**:

    ![Selezionare Connetti](media/howto-generate-connection-string/connect.png)

1. Prendere nota dei dettagli della connessione, **ambito ID**, **ID dispositivo**, e **chiave dispositivo primario**, da usare nei passaggi seguenti:

    ![Dettagli della connessione](media/howto-generate-connection-string/device-connect.png)

    È possibile copiare i valori da questa pagina per salvare.

## <a name="generate-the-connection-string"></a>Generare la stringa di connessione

[!INCLUDE [iot-central-howto-connection-string](../../includes/iot-central-howto-connection-string.md)]

## <a name="next-steps"></a>Passaggi successivi

Ora che è stata generata una stringa di connessione per un dispositivo reale per la connessione all'applicazione Azure IoT Central, ecco i passaggi successivi consigliati:

* [Preparare e connettere un dispositivo DevKit (C)](howto-connect-devkit.md)
* [Preparare e connettere un'applicazione Raspberry Pi (Python)](howto-connect-raspberry-pi-python.md)
* [Preparare e connettere un'applicazione Raspberry Pi (C#)](howto-connect-raspberry-pi-csharp.md)
* [Preparare e connettere un dispositivo Windows 10 IoT Core (C#)](howto-connect-windowsiotcore.md)
* [Connettere un'applicazione client Node.js generica all'applicazione Azure IoT Central](howto-connect-nodejs.md)