---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-15"

keywords: apps, application, migrating apps, hosting apps, migrating, hosting

subcollection: creating-apps

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Migrazione e hosting delle applicazioni
{: #hosting}

Se disponi di un'applicazione esistente, puoi ospitarla su {{site.data.keyword.cloud}} con tutti i servizi di infrastruttura o piattaforma di cui hai bisogno. Puoi anche migrare la tua applicazione a {{site.data.keyword.cloud_notm}} in modo incrementale invece di spostarla all'ambiente cloud in una singola operazione.

## Migrazione di applicazioni
{: #migrating}

Se hai bisogno della tua applicazione per accedere ai tuoi servizi o dati in loco, puoi utilizzare [{{site.data.keyword.SecureGatewayfull}}](/docs/services/SecureGateway?topic=securegateway-getting-started-with-sg#getting-started-with-sg) per stabilire un tunnel protetto tra un'organizzazione {{site.data.keyword.cloud_notm}} e la rete di backend aziendale. Per i dettagli, vedi [Reaching enterprise backend with {{site.data.keyword.cloud_notm}} Secure Gateway via console ](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").

Se hai bisogno di aiuto con la tua migrazione, [{{site.data.keyword.cloud_notm}}Migration Services](https://www.ibm.com/cloud/migration-services){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") sono disponibili.

## Host delle applicazioni
{: #ht_hostapp}

Nel {{site.data.keyword.cloud_notm}} [catalogo](https://{DomainName}/catalog/?taxonomyNavigation=apps){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"), puoi scegliere un ambiente gestito come Kubernetes o Cloud Foundry o puoi ospitare la tua applicazione direttamente su un server bare metal o un server virtuale.

In una distribuzione virtuale, la maggior parte delle operazioni della tua applicazione sono gestite da {{site.data.keyword.cloud_notm}}. Una distribuzione [virtuale](/docs/vsi?topic=virtual-servers-about-virtual-servers#about-virtual-servers) è la soluzione migliore se il carico di lavoro è distribuito su aree geografiche e desideri utilizzare un hypervisor {{site.data.keyword.cloud_notm}} per gestire le tue distribuzioni. Un distribuzione [bare metal](/docs/bare-metal?topic=bare-metal-bm-getting-started#getting-started) è la soluzione migliore se hai bisogno dell'accesso diretto a un server fisico dedicato per prestazioni più elevate.

Hai anche molte opzioni per:
* Selezionare il tipo di [archiviazione](https://{DomainName}/catalog/?taxonomyNavigation=apps&category=slstorage){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") più adattato a te tra archiviazione blocchi, archiviazione file e Object Storage.
* Selezionare il tipo di [rete](https://{DomainName}/catalog/?taxonomyNavigation=apps&category=slnetwork){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")} di cui hai bisogno.
* Selezionare un servizio di [containerizzazione](https://{DomainName}/catalog/?taxonomyNavigation=apps&category=containers){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") per sfruttare la tecnologia di {{site.data.keyword.cloud_notm}} Kubernetes.
