---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-15"

keywords: apps, credentials, Cloud Foundry

subcollection: creating-apps

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Aggiunta di credenziali al tuo ambiente Cloud Foundry
{: #add-credentials-cf}

Acquisisci informazioni su come aggiungere credenziali del servizio al tuo ambiente di distribuzione Cloud Foundry. Queste istruzioni si applicano a entrambi gli ambienti [Cloud Foundry pubblico](/docs/cloud-foundry-public?topic=cloud-foundry-public-about-cf) e [Cloud Foundry Enterprise](/docs/cloud-foundry-public?topic=cloud-foundry-public-cfee).
{: shortdesc}

## Il tuo codice + Cloud Foundry
{: #credentials-byoc-cf}

Nello spazio Cloud Foundry in cui esiste la tua applicazione, puoi definire quello che Cloud Foundry chiama un servizio fornito dall'utente. Un servizio fornito dall'utente è un JSON in stringhe archiviato come se fosse un servizio associabile mediante build nello spazio Cloud Foundry. Dopo che hai eseguito l'accesso e stabilito una connessione all'organizzazione e allo spazio Cloud Foundry, completa la seguente procedura per creare un servizio ed eseguirne il bind.

1. Crea un servizio fornito dall'utente eseguendo il seguente comando:
  ```console
  cf cups customcreds -p '{"username":"Leeroy","password":"Jenkins"}'
  ```
  {: codeblock}

2. Configura la tua applicazione Cloud Foundry per eseguire il bind al servizio fornito dall'utente mediante aggiunta alla sezione services:
  ```yaml
  ---
  applications:
  - instances: 1
    timeout: 180
    name: Blarg3
    buildpack: sdk-for-nodejs
    command: npm start
    memory: 256MB
    domain: mybluemix.net
    host: blarg3
    services:
      - customcreds
  ```

3. Codifica la tua applicazione per leggere l'ambiente per una variabile di ambiente `VCAP_SERVICES`, eseguine l'analisi in JSON e trova la credenziale di cui hai bisogno (pseudocodice tipo node.js):
  ```
  // get the 'password' from "customcreds" user-provided service
  vcapServices = getEnvironment('VCAP_SERVICES');
  vcapServicesAsJSON = JSON.parse(vcapServices);
  upsArray = vcapServicesAsJSON['user-provided'];
  if (upsArray) {
      for (var i = 0, len = upsArray.length; i < len; i++) {
          if (upsArray[i].name === 'customcreds') {
              return upsArray[i].credentials.password
          }
      }
  }
  ```
{: codeblock}


## Applicazione kit starter + Cloud Foundry
{: #credentials-starterkit-cf}

### Come viene preparato lo spazio Cloud Foundry

Utilizza la funzione **Configure continuous delivery** per distribuire la tua applicazione al tuo spazio Cloud Foundry.

Se l'istanza del servizio basata su Cloud Foundry è nello stesso spazio Cloud Foundry dell'applicazione Cloud Foundry distribuita, vedi la [prossima sezione](/docs/apps?topic=creating-apps-add-credentials-cf).

Se l'istanza del servizio basata su Cloud Foundry si trova in uno spazio diverso da quello di destinazione per l'applicazione Cloud Foundry, vedi la [sezione successiva](/docs/apps?topic=creating-apps-add-credentials-cf#cf_resource_different).

Se il servizio che hai associato alla tua applicazione è basato su Resource Controller, vedi [Resource Controller](/docs/apps?topic=creating-apps-add-credentials-cf#cf_resource_controller).

#### Il servizio basato su Cloud Foundry si trova nello stesso spazio dell'applicazione distribuita
{: #cf_resource_same}

Se il servizio che hai associato alla tua applicazione è basato su Cloud Foundry, il servizio è "associabile mediante bind" in Cloud Foundry. Puoi vedere il tuo servizio nel tuo spazio Cloud Foundry connettendo la tua riga di comando `cf` alla corretta combinazione di regione + organizzazione + spazio. Puoi notare se il servizio è basato su Cloud Foundry in fase di creazione del servizio, se ti è stato richiesto in quale organizzazione e spazio Cloud Foundry creare il servizio.

Puoi visualizzare le applicazioni di cui è stato eseguito il bind eseguendo questo comando:
```console
cf services
```
{: codeblock}

Output di esempio:
```
Getting services in org test_user@us.ibm.com / space dev as test_user@us.ibm.com...

name                                   service             plan              bound apps   last operation
blarg3-alertnotificati-1538417831070   alertnotification   authorizedusers                create succeeded
```
{: screen}

#### Il servizio basato su Cloud Foundry si trova in uno spazio differente rispetto all'applicazione distribuita
{: #cf_resource_different}

Cloud Foundry non supporta l'"associazione mediante bind" di un'applicazione Cloud Foundry a un servizio Cloud Foundry quando l'applicazione e il servizio non si trovano nello stesso spazio Cloud Foundry. Lo spazio Cloud Foundry deve essere preparato con i servizi "forniti dall'utente" ed è applicabile la seguente sezione.

#### Il servizio basato su Resource Controller è associato alla tua applicazione
{: #cf_resource_controller}

Se il servizio che hai associato alla tua applicazione è basato su Resource Controller, il servizio _non_ è "associabile mediante bind" in Cloud Foundry. Puoi notare se è basato su Resource Controller nel momento in cui crei il servizio se ti viene chiesto in quale gruppo di risorse creare il servizio. Lo spazio Cloud Foundry deve essere preparato con le credenziali del servizio in modo che l'applicazione possa fare riferimento ad esse nel codice. La preparazione viene eseguita per tuo conto automaticamente e puoi osservare i risultati della preparazione dello spazio connettendo la riga di comando `cf` al tuo spazio eseguendo:
```console
cf services
```
{: codeblock}

Output di esempio:
```
Getting services in org test_user@us.ibm.com / space dev as test_user@us.ibm.com...

name                                   service             plan              bound apps   last operation
blarg-cloudant-1538408663553           user-provided
```
{: screen}

Cloud Foundry non consente la visibilità al valore di eventuali credenziali del servizio, codificate o altrimenti, alla riga di comando `cf service` o `cf services`. Funzionalmente, un servizio fornito dall'utente è un JSON in stringhe definito come una "istanza del servizio" denominata nel tuo spazio Cloud Foundry. Per visualizzare i valori, devi prima eseguire il bind di un'applicazione al servizio Cloud Foundry indicando il nome dell'istanza del servizio nel file `manifest.yml` dell'applicazione sotto l'intestazione `services`. Esegui quindi l'applicazione nello spazio Cloud Foundry e ottieni l'ambiente di tale applicazione eseguendo `cf env $APP_NAME`.

Fortunatamente, il codice generato da un kit starter viene compilato automaticamente con i bind corretti per richiamare e utilizzare i valori dall'ambiente per esso definito nello spazio Cloud Foundry in cui viene eseguita l'applicazione.

### Il codice generato dal kit starter
{: #starterkit-generated-code-cf}

Prima di continuare, vedi [Applicazione kit starter + kube](/docs/apps?topic=creating-apps-add-credentials-kube#credentials-starterkit-kube-gencode). Applica quindi la seguente modifica:

* Anche se il codice generato fornisce il `deployment.yml`, non è applicabile per un'applicazione distribuita a Cloud Foundry. _È_ piuttosto `manifest.yml` ad essere applicabile e il suo contenuto viene visualizzato per eseguire il _bind_ ai due servizi creati nello spazio Cloud Foundry:
  ```yaml
  ---
  applications:
  - instances: 1
    timeout: 180
    name: Blarg3
    buildpack: sdk-for-nodejs
    command: npm start
    memory: 256MB
    domain: mybluemix.net
    host: blarg3
    services:
      - blarg3-alertnotificati-1538417831070
      - blarg-cloudant-1538408663553
  ```
  {: codeblock}

Ancora una volta, è valido il resto della documentazione dalla sottosezione precedente. La libreria `IBMCloudEnv` astrae il richiamo dei valori dall'ambiente in cui viene eseguita l'applicazione.

La libreria astrae parte della complessità legata al richiamo dei valori di ambiente da Cloud Foundry. In Cloud Foundry, un'applicazione in esecuzione viene fornita con una variabile di ambiente denominata `VCAP_SERVICES` il cui valore è JSON in stringhe, e detiene i valori per le credenziali del servizio associate mediante bind, indipendentemente dal fatto che il servizio sia un'istanza del servizio _nello_ spazio Cloud Foundry oppure un valore di servizio definito dall'utente. Le chiavi di livello superiore nel JSON analizzato dalla variabile di ambiente `VCAP_SERVICES` sono l'etichetta (`label`) Cloud Foundry associata ai servizi basati su Cloud Foundry e la chiave fornita dall'utente (`user-provided`), il cui valore detiene un array di credenziali per tutti i servizi "forniti dall'utente".
