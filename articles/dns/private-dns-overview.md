---
title: Usare DNS di Azure per i domini privati
description: Panoramica del servizio di hosting DNS privato in Microsoft Azure.
services: dns
author: vhorne
ms.service: dns
ms.topic: article
ms.date: 3/1/2019
ms.author: victorh
ms.openlocfilehash: 7f5f377f34a43dfb01ea516e023bb98f118d0dd4
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60596583"
---
# <a name="use-azure-dns-for-private-domains"></a>Usare DNS di Azure per i domini privati

Domain Name System o DNS è responsabile della conversione (o risoluzione) del nome di un servizio nel relativo indirizzo IP. DNS di Azure è un servizio di hosting per i domini DNS che offre la risoluzione dei nomi usando l'infrastruttura di Microsoft Azure. Oltre ai domini DNS con connessione Internet, DNS di Azure ora supporta anche i domini DNS privati come una funzionalità di anteprima.

[!INCLUDE [private-dns-public-preview-notice](../../includes/private-dns-public-preview-notice.md)]

DNS di Azure offre un servizio DNS protetto e affidabile per gestire e risolvere i nomi di dominio in una rete virtuale senza la necessità di aggiungere una soluzione DNS personalizzata. Usando le zone DNS private è possibile usare i nomi di dominio personalizzati anziché i nomi forniti da Azure attualmente disponibili. L'uso di nomi di dominio personalizzati consente di personalizzare l'architettura di rete virtuale in base alle esigenze della propria organizzazione. Offre la risoluzione dei nomi per le macchine virtuali all'interno di una rete virtuale e tra reti virtuali. È anche possibile configurare i nomi di zone con una visualizzazione di tipo split-horizon, che consente a una zona DNS privata e pubblica di condividere il nome.

Per pubblicare una zona DNS privata nella rete virtuale, specificare l'elenco di reti virtuali autorizzate a risolvere i record nella zona. Tali reti vengono definite *reti virtuali di risoluzione*. È anche possibile specificare una rete virtuale per cui DNS di Azure manterrà i record dei nomi host ogni volta che una macchina virtuale viene creata o eliminata oppure ne viene modificato l'indirizzo IP. Tale rete viene definita *rete virtuale di registrazione*.

Se si specifica una rete virtuale di registrazione, i record DNS per le macchine virtuali di tale rete che sono registrati nella zona privata non sono visualizzabili né recuperabili tramite Azure PowerShell o le API dell'interfaccia della riga di comando di Azure, ma sono effettivamente registrati e vengono risolti correttamente.

![Panoramica del servizio DNS](./media/private-dns-overview/scenario.png)

> [!NOTE]
> Come procedura consigliata, non utilizzare un dominio. Local per la zona DNS privata. Non tutti i sistemi operativi supportano questo.

## <a name="benefits"></a>Vantaggi

DNS di Azure offre i vantaggi seguenti:

* **Elimina la necessità di soluzioni DNS personalizzate**. Molti clienti in precedenza creavano soluzioni personalizzate DNS per gestire le zone DNS nella rete virtuale. È ora possibile gestire le zone DNS usando l'infrastruttura nativa di Azure eliminando così le attività di creazione e gestione di soluzioni DNS personalizzate.

* **Consente di usare tutti i tipi di record DNS comuni**. DNS di Azure supporta i record A, AAAA, CNAME, MX, PTR, SOA, SRV e TXT.

* **Gestione automatica dei record dei nomi host**. Oltre a ospitare i record DNS personalizzati, Azure mantiene automaticamente i record dei nomi host per le macchine virtuali nelle reti virtuali specificate. In questo scenario è possibile ottimizzare i nomi di dominio usati senza dover creare soluzioni DNS personalizzate o modificare le applicazioni.

* **Risoluzione di nomi host tra reti virtuali**. A differenza dei nomi host forniti da Azure, le zone DNS private possono essere condivise tra le reti virtuali. Questa funzionalità semplifica gli scenari tra più reti e l'individuazione dei servizi come il peering di rete virtuale.

* **Strumenti comuni ed esperienza utente**. Per ridurre la curva di apprendimento, questa nuova offerta usa gli strumenti DNS di Azure già noti, ovvero PowerShell, modelli di Azure Resource Manager e API REST.

* **Supporto DNS split-horizon**. DNS di Azure consente di creare zone con lo stesso nome che si risolvono in risposte diverse dall'interno di una rete virtuale e dalla rete Internet pubblica. Uno scenario tipico di DNS split-horizon consiste nel fornire una versione dedicata di un servizio da usare all'interno della rete virtuale.

* **Disponibile in tutte le aree di Azure**. La funzionalità zone private di DNS di Azure è disponibile in tutte le aree di Azure nel cloud pubblico di Azure.

## <a name="capabilities"></a>Capabilities

DNS di Azure offre le funzionalità seguenti:

* **Registrazione automatica di macchine virtuali da un'unica rete virtuale collegata a una zona privata come rete virtuale di registrazione**. Le macchine virtuali sono registrate (aggiunte) alla zona privata come record A che puntano ai rispettivi indirizzi IP privati. Quando una macchina virtuale in una rete virtuale di registrazione viene eliminata, Azure rimuove automaticamente anche il record DNS corrispondente dalla zona privata collegata. 

  Per impostazione predefinita le reti virtuali di registrazione agiscono anche come reti virtuali di risoluzione, in quanto la risoluzione DNS per la zona funziona da una delle macchine virtuali all'interno della rete virtuale di registrazione.

  > [!NOTE]
  > Se si specifica una rete virtuale di registrazione, i record DNS per le macchine virtuali di tale rete che sono registrati nella zona privata non sono visualizzabili né recuperabili tramite Azure PowerShell o le API dell'interfaccia della riga di comando di Azure, ma sono effettivamente registrati e vengono risolti correttamente.

* **Inoltro della risoluzione DNS supportato sulle reti virtuali collegate alla zona privata come reti virtuali di risoluzione**. Per la risoluzione DNS fra reti virtuali non è presente alcuna dipendenza esplicita per cui sia possibile eseguire il peering delle reti virtuali tra loro. Tuttavia i clienti potrebbero voler eseguire il peer di reti virtuali per altri scenari, ad esempio il traffico HTTP.

* **Ricerca DNS inversa supportata nell'ambito della rete virtuale**. La ricerca DNS inversa di un indirizzo IP privato all'interno della rete virtuale assegnata a una zona privata restituisce l'FQDN che include il nome dell'host/record, nonché il nome della zona come suffisso.

## <a name="limitations"></a>Limitazioni

DNS di Azure presenta le limitazioni seguenti:

* È consentita una sola rete virtuale di registrazione per zona privata.
* Sono consentite fino a 10 reti virtuali di risoluzione per zona privata. Il limite verrà rimosso quando la funzionalità sarà disponibile a livello generale.
* Una determinata rete virtuale può essere collegata a una sola zona privata come rete virtuale di registrazione.
* Una determinata rete virtuale può essere collegata a un massimo di 10 zone private come rete virtuale di risoluzione. Il limite verrà rimosso quando la funzionalità sarà disponibile a livello generale.
* Se si specifica una rete virtuale di registrazione, i record DNS per le macchine virtuali di tale rete che sono registrati nella zona privata non sono visualizzabili né recuperabili tramite Azure PowerShell o le API dell'interfaccia della riga di comando di Azure, ma sono effettivamente registrati e vengono risolti correttamente.
* Il DNS inverso funziona solo per lo spazio IP privato nella rete virtuale di registrazione.
* Il DNS inverso per un indirizzo IP privato che non è registrato nella zona privata, ad esempio un indirizzo IP privato per una macchina virtuale in una rete virtuale collegata a una zona privata come rete virtuale di risoluzione a una zona privata, restituisce *internal.cloudapp.net* come suffisso DNS. Tuttavia questo suffisso non è risolvibile.
* Quando viene collegata per la prima volta a una zona privata come rete virtuale di registrazione o di risoluzione, la rete virtuale deve essere completamente vuota. Questo requisito tuttavia non si applica quando la rete virtuale viene successivamente collegata come rete virtuale di registrazione o di risoluzione ad altre zone private.
* Attualmente l'inoltro condizionale non è supportato, ad esempio per abilitare la risoluzione tra reti di Azure e locali. Per informazioni su come i clienti possono creare questo scenario tramite altri meccanismi, vedere [Risoluzione dei nomi per le macchine virtuali e le istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Per alcune domande e risposte comuni sulle zone private in DNS di Azure, inclusi comportamenti di registrazione e risoluzione DNS specifici che è possibile prevedere per determinati tipi di operazioni, consultare le [Domande frequenti](./dns-faq.md#private-dns).  

## <a name="pricing"></a>Prezzi

La funzionalità zone DNS private è gratuita nell'anteprima pubblica. Durante la disponibilità generale, questa funzionalità offre un modello di determinazione prezzi basato sull'uso simile a quello dell'offerta DNS di Azure esistente. 

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come creare una zona privata nel DNS di Azure tramite [Azure PowerShell](./private-dns-getstarted-powershell.md) o l'[interfaccia della riga di comando di Azure](./private-dns-getstarted-cli.md).

Consultare alcuni [scenari comuni sulle zone private](./private-dns-scenarios.md) che possono essere realizzati con le zone private in DNS di Azure.

Per domande e risposte comuni sulle zone private in DNS di Azure, inclusi comportamenti specifici che è possibile prevedere per determinati tipi di operazioni, consultare le [Domande frequenti](./dns-faq.md#private-dns). 

Per informazioni sui record e le zone DNS visitare la pagina [Panoramica delle zone e dei record DNS](dns-zones-records.md).

Informazioni su alcune altre [funzionalità di rete](../networking/networking-overview.md) chiave di Azure.
