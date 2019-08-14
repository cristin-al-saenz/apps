---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-25"

keywords: apps, application, ssl, certificates, access, restrict access, create, csr, upload, import

subcollection: creating-apps

---

{:shortdesc: .shortdesc}
{:tip: .tip}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:note: .note}

# Creazione di richieste di firma del certificato
{: #ssl_csr}

Puoi proteggere le tue applicazioni caricando dei certificati SSL e limitando l'accesso alle applicazioni.
{: shortdesc}

## Creazione di una richiesta di firma del certificato (CSR, certificate signing request)
{: #create_csr}

Prima di poter caricare i certificati SSL a cui hai diritto con {{site.data.keyword.cloud}}, devi creare una richiesta di firma del certificato, o CSR, sul tuo server. Una CSR è un messaggio che viene inviato a un'autorità di certificazione per richiedere la firma di una chiave pubblica
e le informazioni associate. Più comunemente, le CSR sono in formato PKCS #10. La CSR include una chiave pubblica, un nome comune, un'organizzazione, una città, uno stato, un paese ed una e-mail. Le richieste di certificati SSL
vengono accettate solo con una lunghezza di chiave CSR pari a 2048 bit.

I metodi per creare una CSR variano a seconda del tuo sistema operativo. Il seguente esempio mostra come creare una CSR utilizzando [lo strumento riga di comando OpenSSL ](https://www.openssl.org/){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"):

```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout
    privatekey.key
```
{: codeblock}

L'implementazione OpenSSL SHA-512 dipende dal supporto del compilatore per il tipo intero a 64 bit. Puoi utilizzare l'opzione SHA-1 per le applicazioni che presentano problemi di compatibilità con il certificato SHA-256.
{: tip}

### Contenuto CSR richiesto

Affinché la CSR sia valida, quando la crei è necessario immettere le seguenti informazioni:

 * **Nome paese**: un codice a due cifre per il paese o la regione. Ad esempio, `US` è il codice paese per gli Stati Uniti. Per altri paesi o regioni, prima di creare la CSR, controlla l'[elenco di codici paese ISO ](https://www.iso.org/obp/ui/#search){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").
 * **Stato o provincia**: il nome completo senza abbreviazioni dello stato o provincia.
 * **Località**: il nome completo della città.
 * **Organizzazione**: il nome completo dell'azienda o società, come legalmente registrata nella tua località, o il nome personale. Per le società, assicurati di includere il suffisso di registrazione, ad esempio Ltd., Inc. o NV.
 * **Unità organizzativa**: il nome della sezione della tua società che ordina il certificato, ad esempio contabilità o marketing.
 * **Nome comune**: il nome di dominio completo (FQDN) per il quale stai richiedendo il certificato SSL.

Puoi utilizzare i SAN (Subject Alternative Name), ma i nomi host forniti non devono essere emessi in altri certificati distribuiti per evitare conflitti di CN.
{: note}

Un certificato viene emesso da un'autorità di
certificazione e viene firmato in maniera digitale da tale autorità. Dopo aver creato la CSR, puoi generare il tuo certificato SSL su un'autorità di certificazione pubblica.

## Caricamento di certificati SSL
{: #ssl_certificate}

Puoi applicare un protocollo di sicurezza per garantire la riservatezza delle comunicazioni della tua applicazione in modo da prevenire l'intercettazione delle comunicazioni, la manomissione e la falsificazione dei messaggi. Se hai un account Lite, devi eseguire l'upgrade del tuo account per caricare un certificato.

Quando un certificato scaduto o in scadenza deve essere rinnovato e dopo che il nuovo certificato è pronto, elimina il certificato esistente e aggiungi quello nuovo.
{: note}

Quando utilizzi un dominio personalizzato per servire il certificato SSL, utilizza i seguenti endpoint della regione per fornire la rotta URL per la tua organizzazione in {{site.data.keyword.cloud_notm}}:

| Regione | Endpoint |
| ------ | -------- |
| US-South | `custom-domain.us-south.cf.cloud.ibm.com` |
| US-East | `custom-domain.us-east.cf.cloud.ibm.com` |
| EU-DE | `custom-domain.eu-de.cf.cloud.ibm.com` |
| EU-GB | `custom-domain.eu-gb.cf.cloud.ibm.com` |
| AU-SYD | `custom-domain.au-syd.cf.cloud.ibm.com` | 
{: caption="Tabella 1. Endpoint della regione del dominio personalizzato Cloud Foundry" caption-side="top"}

Per caricare un certificato per la tua applicazione Cloud Foundry, completa la seguente procedura:

1. Dalla [console {{site.data.keyword.cloud_notm}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}){: new_window}, fai clic sull'icona **Menu** ![icona Menu](../icons/icon_hamburger.svg) e seleziona **Elenco risorse**.
2. Fai clic su **Applicazioni Cloud Foundry**.
3. Fai clic sull'applicazione di cui vuoi modificare il dominio. 
4. Nella pagina Panoramica dell'applicazione, fai clic su **Rotte** e seleziona **Gestisci rotte**.
5. Dalla colonna Azioni, fai clic sull'icona Azioni ![Icona Ulteriori azioni](../icons/action-menu-icon.svg) e seleziona **Domini**.
6. Fai clic su **Carica** per il tuo dominio personalizzato.
7. Seleziona un'opzione, carica il file e fai clic su **Aggiungi**.
  
  * Certificato: un documento digitale che esegue il bind di una chiave pubblica all'identità del proprietario del certificato,
che abilita il proprietario del certificato a essere autenticato. Un certificato viene emesso da un'autorità di
certificazione e viene firmato in maniera digitale da tale autorità. Un certificato viene in genere emesso e firmato da un'autorità di certificazione. Tuttavia, per scopi di test e di sviluppo, puoi utilizzare un certificato autofirmato.
  * Chiave privata: un modello algoritmico utilizzato per crittografare messaggi che possono essere decrittografati
solo dalla chiave pubblica corrispondente. Inoltre, la chiave privata viene utilizzata per decrittografare i messaggi crittografati con la chiave pubblica corrispondente. La chiave privata è conservata sul sistema dell'utente e protetta da password.
  * Certificato intermedio (facoltativo): un certificato subordinato emesso dall'autorità di certificazione (CA) radice attendibile
specificamente per emettere certificati server per l'entità finale. Il risultato è una catena di certificati che inizia dalla CA radice
attendibile, passa per quello intermedio e termina con il certificato SSL emesso per l'organizzazione. Utilizza un certificato intermedio per verificare l'autenticità del certificato principale. I certificati intermedi vengono di norma ottenuti da una terza parte attendibile. Potresti non aver bisogno di un certificato intermedio durante il test della tua applicazione prima che ne esegui la distribuzione in produzione.
  * Abilita la richiesta del certificato client: se abiliti questa opzione, a un utente che prova ad accedere a un dominio protetto da SSL viene richiesto di fornire un certificato lato client. Ad esempio, in un browser web, quando un utente prova ad accedere a un dominio protetto da SSL,
il browser web gli richiede di fornire un certificato client per il dominio.   
  * Truststore certificato client (facoltativo): include i certificati client per gli utenti a cui vuoi consentire l'accesso alla tua applicazione. Carica un file truststore certificato client per abilitare l'opzione per richiedere un certificato client.
  
    Puoi configurare l'autenticazione reciproca caricando un truststore certificato client che includa una chiave pubblica nei suoi metadati.
    {: tip}


