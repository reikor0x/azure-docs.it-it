---
title: Codificare un asset con Media Encoder Standard mediante .NET | Microsoft Docs
description: Questo articolo illustra come usare .NET per codificare un asset con Media Encoder Standard.
services: media-services
documentationcenter: ''
author: juliako
manager: femila
editor: ''
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/18/2019
ms.author: juliako;anilmur
ms.openlocfilehash: d3eb2affe76374eb35ac724dff0204f43b567e09
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "61225729"
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a>Codificare un asset con Media Encoder Standard mediante .NET  

I processi di codifica sono tra le operazioni di elaborazione più frequenti in Servizi multimediali. Questi processi vengono creati per convertire i file multimediali da una codifica all'altra. Durante la codifica è possibile usare il codificatore multimediale incorporato in Servizi multimediali. È anche possibile usare un codificatore fornito da un partner di Servizi multimediali. I codificatori di terze parti sono disponibili tramite Azure Marketplace. 

Questo articolo illustra come usare .NET per codificare gli asset con Media Encoder Standard (MES). Media Encoder Standard viene configurato mediante un set di impostazioni descritto [qui](https://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

È consigliabile codificare sempre i file di origine con un set MP4 a velocità in bit adattiva e quindi convertire il set nel formato desiderato mediante la [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md). 

Se l'asset di output è protetto con crittografia di archiviazione, è necessario configurare i criteri di distribuzione degli asset. Per altre informazioni, vedere [Configurazione dei criteri di distribuzione degli asset](media-services-dotnet-configure-asset-delivery-policy.md).

> [!NOTE]
> MES produce un file di output con un nome contenente i primi 32 caratteri del nome del file di input. Il nome è basato su quanto specificato nel file preimpostato. Ad esempio, "FileName": "{Basename}_{Index}{Extension}". {Basename} viene sostituito dai primi 32 caratteri del nome del file di input.
> 
> 

### <a name="mes-formats"></a>Formati MES
[Codec e formati](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a>Impostazioni predefinite MES
Media Encoder Standard viene configurato mediante un set di impostazioni descritto [qui](https://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Metadati di input e output
Quando si codifica un asset di input (o asset) tramite MES, al completamento dell'attività di codifica si ottiene un asset di output. L'asset di output contiene video, audio, anteprime, manifesto e così via a seconda del set di impostazioni di codifica che si usa.

L'asset di output include anche un file contenente i metadati dell'asset di input. Il nome del file XML dei metadati ha il seguente formato: <asset_id>_metadata.xml (ad esempio, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), dove <asset_id> è il valore AssetId dell'asset di input. Lo schema di questo file XML di metadati di input è descritto [qui](media-services-input-metadata-schema.md).

L'asset di output include anche un file contenente i metadati dell'asset di output. Il nome del file XML dei metadati ha il seguente formato: <nome_file_origine>_manifest.xml (ad esempio BigBuckBunny_manifest.xml). Lo schema del file XML dei metadati di output viene descritto [qui](media-services-output-metadata-schema.md).

Se si desidera esaminare uno dei due file di metadati, è possibile creare un localizzatore SAS e scaricare il file nel computer locale. È possibile trovare un esempio su come creare un localizzatore SAS e scaricare un file tramite le estensioni dell'SDK .NET di Servizi multimediali.

## <a name="download-sample"></a>Scaricare un esempio
È possibile ottenere ed eseguire da [qui](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/) un esempio che mostra come codificare con MES.

## <a name="net-sample-code"></a>Codice di esempio .NET

Il seguente codice usa l'SDK .NET di Servizi multimediali per eseguire le seguenti attività: 

* Creare un processo di codifica.
* Ottenere un riferimento al codificatore Media Encoder Standard.
* Specificare l'uso del set di impostazioni [Flusso adattivo](media-services-autogen-bitrate-ladder-with-mes.md). 
* Aggiungere una singola attività di codifica al processo. 
* Specificare l’asset di input da codificare.
* Creare un asset di output che contenga l'asset codificato.
* Aggiungere un gestore eventi per controllare l'avanzamento del processo.
* Inviare il processo.

#### <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio

Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Esempio 

```csharp
using System;
using System.Linq;
using System.Configuration;
using System.IO;
using System.Threading;
using Microsoft.WindowsAzure.MediaServices.Client;

namespace MediaEncoderStandardSample
{
    class Program
    {
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AMSAADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["AMSRESTAPIEndpoint"];
        private static readonly string _AMSClientId =
            ConfigurationManager.AppSettings["AMSClientId"];
        private static readonly string _AMSClientSecret =
            ConfigurationManager.AppSettings["AMSClientSecret"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _supportFiles =
            Path.GetFullPath(@"../..\Media");

        static void Main(string[] args)
        {
            AzureAdTokenCredentials tokenCredentials =
                new AzureAdTokenCredentials(_AADTenantDomain,
                    new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                    AzureEnvironments.AzureCloudEnvironment);

            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);


            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate the output using the "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
                case JobState.Finished:
                    Console.WriteLine();
                    Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
                    break;
                case JobState.Canceling:
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    Console.WriteLine("Please wait...\n");
                    break;
                case JobState.Canceled:
                case JobState.Error:

                    // Cast sender as a job.
                    IJob job = (IJob)sender;

                    // Display or log error details as needed.
                    break;
                default:
                    break;
            }
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
    }
}
```

## <a name="advanced-encoding-features-to-explore"></a>Funzionalità di codifica avanzate da esplorare
* [Come generare anteprime](media-services-dotnet-generate-thumbnail-with-mes.md)
* [Generazione di anteprime durante la codifica](media-services-dotnet-generate-thumbnail-with-mes.md#example-of-generating-a-thumbnail-while-encoding)
* [Ritagliare video durante la codifica](media-services-crop-video.md)
* [Personalizzazione di set di impostazioni di codifica](media-services-custom-mes-presets-with-dotnet.md)
* [Impostare un'immagine come sovrimpressione o filigrana in un video](media-services-advanced-encoding-with-mes.md#overlay)

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Passaggi successivi
[Come generare l'anteprima mediante Media Encoder Standard con .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Panoramica della codifica dei servizi multimediali](media-services-encode-asset.md)

