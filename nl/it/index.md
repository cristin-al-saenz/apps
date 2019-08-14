---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-15"

keywords: apps, create apps, add resources, deploy apps

subcollection: creating-apps

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Esercitazione introduttiva
{: #tutorial-getting-started}

Puoi creare delle applicazioni web e mobili pronte per l'azienda in {{site.data.keyword.cloud}} e avvalerti delle estensioni cloud ospitate da {{site.data.keyword.cloud_notm}}. Hai diverse opzioni per iniziare a lavorare. Crea un'applicazione con un kit starter che gestisce il processo per tuo conto oppure, se sai cosa desideri, inizia da zero e crea la tua applicazione con le risorse di cui hai bisogno oppure utilizza il tuo repository esistente e porta il tuo codice.
{: shortdesc}

## Prima di iniziare
{: #prereqs-getting-started}

Puoi creare la tua applicazione utilizzando l'interfaccia di riga di comando (o CLI, command-line interface) o la console {{site.data.keyword.cloud_notm}}. Se desideri utilizzare la CLI, vedi la [procedura di installazione](/docs/cli?topic=cloud-cli-ibmcloud-cli).

## Passo 1. Crea la tua applicazione
{: #create-getting-started}

Crea un'applicazione selezionando uno dei seguenti punti di ingresso:
* [Kit starter](/docs/apps/tutorials?topic=creating-apps-tutorial-starterkit): crea un'applicazione da una selezione di kit starter App Service che gestiscono il processo per tuo conto.
* [Personalizzata](/docs/apps/tutorials?topic=creating-apps-tutorial-scratch): se sai cosa desideri, crea un'applicazione personalizzata da zero con le risorse di cui hai bisogno utilizzando un kit starter vuoto.
* [Porta il tuo codice](/docs/apps/tutorials?topic=creating-apps-tutorial-byoc): porta il tuo codice mediante un collegamento al tuo repository di contenuto esistente. La tua applicazione e l'immagine Docker si devono trovare nello stesso repository.
* [CLI](/docs/apps?topic=creating-apps-create-deploy-app-cli): crea e distribuisci un'applicazione personalizzata o kit starter utilizzando gli strumenti per gli sviluppatori e la CLI.
* [Modelli di codice](/docs/apps/tutorials?topic=creating-apps-tutorial-codepattern): utilizza un modello di codice IBM Developer come base per creare la tua applicazione.
* [Catalogo {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/catalog){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"): puoi sfogliare o cercare nel catalogo le applicazioni e i servizi che puoi creare e iniziare a utilizzare oggi stesso.

## Passo 2. Aggiungi risorse
{: #resources-getting-started}

Quando utilizzi un kit starter per creare la tua applicazione, i tuoi servizi vengono creati automaticamente per tuo conto. Puoi associare più servizi alla tua applicazione facendo clic su **Add service** nella pagina **App details** nella console.

Per aggiungere servizi utilizzando la CLI, esegui il seguente comando per aggiungere un servizio alla tua applicazione. Puoi selezionare un servizio esistente da uno già abilitato sul tuo account o aggiungerne uno nuovo. 
```
ibmcloud dev edit
```
{: codeblock}

Per ulteriori informazioni, vedi [Aggiunta di un servizio alla tua applicazione](/docs/apps?topic=creating-apps-add-resource).

## Passo 3. Distribuisci la tua applicazione
{: #deploy-getting-started}

Puoi distribuire la tua applicazione utilizzando la console o la riga di comando.

### Utilizzo della console
{: #console-getting-started}

Per distribuire la tua applicazione utilizzando la console, completa la seguente procedura:

1. Nella pagina **App details**, fai clic su **Configure continuous delivery**.
2. Seleziona una destinazione di distribuzione, le impostazioni della toolchain e fai clic su **Create**. {{site.data.keyword.cloud_notm}} crea automaticamente una toolchain aperta completa di un repository Git e della pipeline di fornitura continua.
3. Apri la fase pipeline della tua nuova toolchain per visualizzare il processo di creazione e sviluppo in modo da poter vedere la tua nuova applicazione nel giro di qualche minuto.

Per ulteriori informazioni, consulta la tabella dei contenuti per diversi argomenti di distribuzione nella sezione "Distribuzione e integrazione delle applicazioni".

### Utilizzo della riga di comando
{: #cli-getting-started}

Per distribuire la tua applicazione utilizzando la riga di comando, esegui il comando `ibmcloud dev deploy`. Per ulteriori informazioni, vedi [Creazione e distribuzione delle applicazioni utilizzando la CLI](/docs/apps?topic=creating-apps-create-deploy-app-cli).

Ora sei pronto per lo sviluppo iterativo e la fornitura continua.
