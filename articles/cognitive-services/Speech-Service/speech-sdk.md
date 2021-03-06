---
title: Informazioni su Speech SDK - Servizi di riconoscimento vocale
titleSuffix: Azure Cognitive Services
description: Speech Software Development Kit (SDK) fornisce alle applicazioni l'accesso nativo alle funzioni del servizio Voce, rendendo più semplice lo sviluppo di software. Questo articolo fornisce dettagli aggiuntivi sull'SDK per Windows, Linux e Android.
services: cognitive-services
author: erhopf
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 04/08/2019
ms.author: wolfma
ms.openlocfilehash: 2bfe111cbe1e352c16c9cbdd6d2ecc999bbe444f
ms.sourcegitcommit: 13cba995d4538e099f7e670ddbe1d8b3a64a36fb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66003004"
---
# <a name="about-the-speech-sdk"></a>Informazioni su Speech SDK

Il Software Development Kit (SDK) di sintesi vocale offre l'accesso delle applicazioni alle funzioni di servizi di riconoscimento vocale, rendendo più semplice sviluppare software abilitate al riconoscimento vocale. Attualmente, gli SDK offrono accesso a **per il riconoscimento vocale**, **sintesi vocale**, **traduzione vocale**, e **riconoscimento delle intenzioni**. Una panoramica generale sulle funzionalità e le piattaforme supportate sono reperibili nella documentazione di [pagina di immissione](https://aka.ms/csspeech).

[!INCLUDE [Speech SDK Platforms](../../../includes/cognitive-services-speech-service-speech-sdk-platforms.md)]

[!INCLUDE [License Notice](../../../includes/cognitive-services-speech-service-license-notice.md)]

## <a name="get-the-sdk"></a>Ottenere l'SDK

### <a name="windows"></a>Windows

Per Windows sono supportati le lingue seguenti:

* C# (UWP e .NET), C++: è possibile fare riferimento alla versione più recente del pacchetto Speech SDK NuGet e usare tale versione. Il pacchetto include librerie client a 32 e 64 bit e librerie gestite (.NET). Per installare l'SDK in Visual Studio, è possibile usare NuGet. Cercare **Microsoft.CognitiveServices.Speech**.

* Java: è possibile fare riferimento alla versione più recente del pacchetto Speech SDK Maven, che supporta solo Windows x64, e usare tale versione. Nel progetto Maven aggiungere `https://csspeechstorage.blob.core.windows.net/maven/` come repository aggiuntivo e fare riferimento a `com.microsoft.cognitiveservices.speech:client-sdk:1.5.1` come dipendenza.

### <a name="linux"></a>Linux

> [!NOTE]
> Attualmente è supportato solo Ubuntu 16.04, 18.04 Ubuntu e Debian 9 in un computer (x86 o x64 per C++ sviluppo e x64 per .NET Core, Java e Python).

Assicurarsi di avere le librerie richieste installate eseguendo i comandi della shell seguenti:

In Ubuntu:

```sh
sudo apt-get update
sudo apt-get install libssl1.0.0 libasound2
```

In Debian 9:

```sh
sudo apt-get update
sudo apt-get install libssl1.0.2 libasound2
```

* C#: è possibile fare riferimento alla versione più recente del pacchetto Speech SDK NuGet e usare tale versione. Per fare riferimento all'SDK, aggiungere al progetto il riferimento al pacchetto seguente:

  ```xml
  <PackageReference Include="Microsoft.CognitiveServices.Speech" Version="1.5.1" />
  ```

* Java: è possibile fare riferimento alla versione più recente del pacchetto Speech SDK Maven e usare tale versione. Nel progetto Maven aggiungere `https://csspeechstorage.blob.core.windows.net/maven/` come repository aggiuntivo e fare riferimento a `com.microsoft.cognitiveservices.speech:client-sdk:1.5.1` come dipendenza.

* C++: scaricare l'SDK come [pacchetto con estensione tar](https://aka.ms/csspeech/linuxbinary) e decomprimere i file nella directory desiderata. La tabella seguente illustra la struttura di cartelle dell'SDK:

  |`Path`|Descrizione|
  |-|-|
  |`license.md`|Licenza|
  |`ThirdPartyNotices.md`|Comunicazioni di terze parti|
  |`include`|File di intestazione per C e C++|
  |`lib/x64`|Libreria x64 nativa per il collegamento all'applicazione|
  |`lib/x86`|Libreria x86 nativa per il collegamento all'applicazione|

  Per creare un'applicazione, copiare o spostare i file binari e le librerie necessari nell'ambiente di sviluppo e includerli nel processo di compilazione come richiesto.

### <a name="android"></a>Android

Java SDK per Android viene inserito in un pacchetto come una [AAR (libreria Android)](https://developer.android.com/studio/projects/android-library), che include le librerie necessarie, nonché le autorizzazioni Android richieste. È ospitato in un repository Maven in `https://csspeechstorage.blob.core.windows.net/maven/` come pacchetto `com.microsoft.cognitiveservices.speech:client-sdk:1.5.1`.

Per usare il pacchetto dal progetto Android Studio apportare le modifiche seguenti:

* Nel file build.gradle a livello di progetto aggiungere quanto segue nella sezione `repository`:

  ```gradle
  maven { url 'https://csspeechstorage.blob.core.windows.net/maven/' }
  ```

* Nel file build.gradle a livello di modulo aggiungere quanto segue nella sezione `dependencies`:

  ```gradle
  implementation 'com.microsoft.cognitiveservices.speech:client-sdk:1.5.1'
  ```

Java SDK fa inoltre parte di [Speech Devices SDK](speech-devices-sdk.md).

[!INCLUDE [Get the samples](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]

## <a name="next-steps"></a>Passaggi successivi

* [Ottenere una sottoscrizione di valutazione gratuita del Servizio di riconoscimento vocale](https://azure.microsoft.com/try/cognitive-services/)
* [Informazioni sul riconoscimento vocale in C#](quickstart-csharp-dotnet-windows.md)
