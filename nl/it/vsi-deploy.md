---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-15"

keywords: apps, deploy, virtual server, App Service, vsi, virtual machine, delivery pipeline

subcollection: creating-apps

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:table: .aria-labeledby="caption"}

# Distribuzione a un server virtuale
{: #vsi-deploy}

Se hai un account Pagamento a consumo, puoi utilizzare {{site.data.keyword.cloud}} [App Service](https://{DomainName}/developer/appservice/starter-kits){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") per distribuire le tue applicazioni a molti tipi di ambienti, comprese le istanze del server virtuale (o VSI, Virtual Server Instance). Un'istanza del server virtuale (o VSI, Virtual Server Instance) emula una macchina bare metal ed è una scelta di distribuzione comune quando si spostano sul cloud i carichi di lavoro .
{: shortdesc}

Un'istanza del server virtuale (o VSI, Virtual Server Instance) offre trasparenza, prevedibilità e automazione migliori per tutti i tipi di carico di lavoro quando confrontata con altre configurazioni. Combinala con un server bare metal per creare combinazioni di carico di lavoro uniche. Ad esempio, puoi creare la logica di database ad alte prestazioni o machine learning con configurazioni bare metal e GPU che eseguono un sistema operativo basato su Linux Debian.

Il provisioning di un'istanza del server virtuale (o VSI, Virtual Server Instance) e la sua distribuzione può essere un processo complesso e dispendioso in termini di tempo ma puoi essere operativo rapidamente utilizzando {{site.data.keyword.cloud_notm}} App Service.

Non viene eseguito il bind dei servizi all'istanza del server virtuale (o VSI, Virtual Server Instance). Non puoi aggiungere servizi a un'applicazione in un server virtuale.
{: important}

## Creazione e distribuzione di applicazioni
{: #create-deploy-vsi}

L'App Service esegue il provisioning di un'istanza del server virtuale (o VSI, Virtual Server Instance) per tuo conto, carica un'immagine che include la tua applicazione, crea una toolchain DevOps e avvia il primo ciclo di distribuzione per tuo conto.

1. [Crea un'applicazione](/docs/apps?topic=creating-apps-tutorial-scratch#tutorial-scratch). 
2. Fai clic su **Configure continuous delivery** dalla pagina **App details**.
3. Seleziona **Deploy to a Virtual Server** insieme alla regione in cui eseguire il tuo server.

## Modalità di funzionamento del processo di distribuzione

Il processo di distribuzione del server virtuale consiste in diverse tecnologie chiave che includono Terraform, l'abilitazione di pipeline, la gestione di chiavi API (operazioni Git) e la comprensione del processo toolchain. 

### Distribuzione tramite Terraform

Tutti i kit starter App Service possono essere distribuiti in un'istanza virtuale creata dinamicamente tramite [Terraform](https://ibm-cloud.github.io/tf-ibm-docs/v0.10.0/){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"), un'infrastruttura open source come framework del codice. 

### Abilitazione della tua distribuzione della pipeline

Quando crei un kit starter che utilizza {{site.data.keyword.cloud_notm}} [App Service](https://{DomainName}/developer/appservice/starter-kits){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"), viene abilitata l'istanza del server virtuale (o VSI, Virtual Server Instance). Dopo aver creato l'applicazione, puoi scegliere dove vuoi distribuirla. I kit starter sono abilitati per supportare la distribuzione utilizzando una toolchain di Continuous Delivery. I kit starter possono avere come destinazione istanze di Virtual Server, Kubernetes e Cloud Foundry. La toolchain include un repository del codice di origine e una delivery pipeline.

L'opzione del server virtuale funziona a fasi. Per prima cosa, il codice dell'applicazione viene preparato e memorizzato in un repository GitLab Git e il codice di origine crea una toolchain con una pipeline. La pipeline viene definita per creare il codice e impacchettarlo in un formato del gestore pacchetti Debian. Quindi, Terraform fornisce un'istanza virtuale. Infine, l'applicazione viene distribuita, installata e avviata all'interno dell'immagine virtuale in esecuzione e il relativo stato di integrità viene convalidato.

La pipeline utilizza una serie di proprietà account utente e una nuova coppia di chiavi SSH per la distribuzione all'infrastruttura. Queste proprietà vengono automaticamente passate nella toolchain, ma non memorizzate nel codice di origine Git per motivi di sicurezza.

Per visualizzare queste proprietà di ambiente, completa la seguente procedura. 

1. Dalla pagina dei dettagli dell'applicazione, fai clic su **Visualizza toolchain**.
2. Fai clic sul tile **Delivery Pipeline**.
3. Fai clic sull'icona **Stage Configure** e quindi su **Configure Stage** nella fase di build.
4. Fai clic sulla scheda **Environment Properties** per visualizzare le proprietà. Utilizza la seguente tabella per ulteriori informazioni sulle proprietà disponibili.

| Proprietà  | Descrizione  |
|-----------|--------------|
| `TF_VAR_ibm_sl_api_key` | La [chiave API dell'infrastruttura](/docs/apps?topic=creating-apps-vsi-deploy#iaas-key) viene dalla console dell'infrastruttura classica. |
| `TF_VAR_ibm_sl_username` | Il [nome utente dell'infrastruttura](/docs/apps?topic=creating-apps-vsi-deploy#user-key) che identifica l'account dell'infrastruttura classica |
| `TF_VAR_ibm_cloud_api_key` | La [chiave API](/docs/apps?topic=creating-apps-vsi-deploy#platform-key) {{site.data.keyword.cloud_notm}} viene utilizzata per abilitare la creazione del servizio. |
| `PUBLIC_KEY` | La [chiave pubblica](/docs/apps?topic=creating-apps-vsi-deploy#public-key) definita per abilitare l'accesso all'istanza del server virtuale (o VSI, Virtual Server Instance). |
| `PRIVATE_KEY` | La [chiave privata](/docs/apps?topic=creating-apps-vsi-deploy#public-key) definita per abilitare l'accesso all'istanza del server virtuale (o VSI, Virtual Server Instance). Devi utilizzare la formattazione di stile nuova riga `\n`. |
| `VI_INSTANCE_NAME` | Il nome generato automaticamente per l'istanza del server virtuale (o VSI, Virtual Server Instance). |
| `GIT_USER` | Se imposti lo [stato Terraform](/docs/apps?topic=creating-apps-vsi-deploy#tform-state) per memorizzare lo stato del comando di applicazione, è obbligatorio il nome utente GitLab. |
| `GIT_PASSWORD` | Se imposti lo [stato Terraform](/docs/apps?topic=creating-apps-vsi-deploy#tform-state) per memorizzare lo stato del comando di applicazione, è obbligatoria la password GitLab. |
{: caption="Tabella 1. Variabili di ambiente da modificare per l'abilitazione" caption-side="top"}


#### Chiave API dell'infrastruttura classica
{: #iaas-key}

Terraform richiede una chiave API dell'infrastruttura classica per creare le risorse dell'infrastruttura. La chiave API viene ottenuta automaticamente durante la distribuzione. Per richiamare manualmente una chiave, completa la seguente procedura.

1. Vai all'[elenco utenti](https://{DomainName}/iam#/users){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"). Puoi anche fare clic su **Gestisci** > **Accesso (IAM)** e selezionare **Utenti**.
2. Fai clic su un nome utente e fai quindi clic su **Dettagli utente**.
3. Fai clic su **Aggiungi chiave infrastruttura classica** nella sezione Chiavi API.
4. Copia o scarica la chiave API `TF_VAR_ibm_sl_api_key` e salvala in un luogo sicuro. Puoi richiamare i dettagli della chiave API in un secondo momento utilizzando l'opzione **Visualizza dettagli** dal menu **Azioni** ![Icona di elenco di azioni](../icons/action-menu-icon.svg).
5. Incolla il valore di chiave API copiato nella configurazione della toolchain per sostituire il valore `TF_VAR_ibm_sl_api_key`.

Per ulteriori informazioni, vedi i documenti relativi alla [gestione delle chiavi API dell'infrastruttura classica](/docs/iam?topic=iam-classic_keys#classic_keys) e alle [autorizzazioni dell'infrastruttura classica](/docs/iam?topic=iam-infrapermission#infrapermission).

#### Nome utente dell'infrastruttura classica
{: #user-key}

Anche il nome utente dell'infrastruttura classica viene ottenuto automaticamente e utilizzato durante la distribuzione. Per ottenere manualmente il nome utente, completa la seguente procedura.

1. Vai all'[elenco utenti](https://{DomainName}/iam#/users){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"). Puoi anche fare clic su **Gestisci** > **Accesso (IAM)** e selezionare **Utenti**.
2. Fai clic su un nome utente e fai quindi clic su **Dettagli utente**.
3. Individua la proprietà **Nome utente VPN**.
4. Taglia e incolla questo valore e sostituisci il valore `TF_VAR_ibm_sl_username` della configurazione della toolchain.

#### Chiave API {{site.data.keyword.cloud_notm}}
{: #platform-key}

Per creare servizi a livello di piattaforma in Terraform, come i database e i servizi Compose, la chiave API {{site.data.keyword.cloud_notm}} viene automaticamente ottenuta e memorizzata come una variabile di ambiente nella tua pipeline. Per richiamare manualmente una chiave API {{site.data.keyword.cloud_notm}}, completa la seguente procedura.

1. Vai all'[elenco utenti](https://{DomainName}/iam#/users){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"). Puoi anche fare clic su **Gestisci** > **Accesso (IAM)** e selezionare **Utenti**.
2. Fai clic su un nome utente e fai quindi clic su **Dettagli utente**.
3. Individua la sezione Chiavi API e fai clic su **Crea una chiave API IBM Cloud**.
4. Immetti un nome e una descrizione e fai clic su **Crea**.
5. Quando si apre la finestra, fai clic su **Mostra** per esaminare la chiave.
6. Copia e incolla la chiave negli appunti oppure scarica la chiave.
7. Sostituisci il valore nella configurazione della toolchain `TF_VAR_ibm_cloud_api_key` con il valore che è stato generato.

#### Chiavi pubbliche e private
{: #public-key}

Perché la toolchain installi il pacchetto Debian nell'istanza del server virtuale (o VSI, Virtual Server Instance), l'infrastruttura di distribuzione genera automaticamente una coppia di chiavi SSH privata e pubblica per trasferire i contenuti Git all'istanza.

Per effettuare questa operazione manualmente:
1. Nel tuo client, utilizza le seguenti istruzioni per creare una [coppia di chiavi pubblica e privata](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").
2. Vai alla [vista delle chiavi SSH dell'infrastruttura](https://{DomainName}/iam/#/users){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"). Puoi anche fare clic su **Menu** > **Infrastruttura classica** > **Dispositivi** > **Gestisci** > **Chiavi SSH**.
3. Fai clic su **Aggiungi**.
4. Copia il contenuto della chiave pubblica che hai precedentemente creato e incollalo nel contenuto della chiave.
5. Assegna un nome alla chiave e fai clic su **Aggiungi**.

La chiave privata deve essere su una singola riga. Sostituisci le nuove righe con `\n`. Vedi il seguente esempio.
{: tip}

```
---------BEGIN RSA KEY----------\nasdfasdfeqwtqf13rf1eqwfwe\netq3efaewf23fa23f23f\n.....\n----------END RSA KEY-------------
```
{: screen}

#### Abilitazione dello stato di Terraform
{: #tform-state}

Terraform supporta l'archiviazione dello stato del comando `apply` di Terraform. Questo file di stato esegue il comando `apply` una seconda volta per determinare se uno qualsiasi dei file di configurazione di Terraform è stato modificato. Lo stato viene archiviato nel repository Git in cui l'applicazione e la configurazione vengono impostate automaticamente.

Per abilitare l'archiviazione dello stato, `GIT_USER` e `GIT_PASSWORD` vengono automaticamente configurate come proprietà nelle variabili di ambiente della toolchain. Se hai bisogno di accedere a questi valori, segui queste istruzioni:

1. Dalla vista delle toolchain, accedi al repository Git dallo strumento del codice.
2. In GIT Lab, fai clic sull'**Icona profilo** e poi su **Settings**.
3. Fai clic su **Account** e copia il nome utente e sostituisci il valore `GIT_USER`.
4. Fai clic su **Access Tokens**.
5. Definisci un nome per il tuo token, seleziona un ambito e fai clic su **Create Personal Access Token**.
6. Fai clic su **Copy** dal campo `Your New Personal Access Token` e sostituisci il valore di `GIT_PASSWORD` nelle proprietà della toolchain.

Lo stato di Terraform viene memorizzato in un ramo denominato `terraform` e non attiva l'esecuzione della pipeline se viene modificato.

### Abilitazione delle operazioni Git
{: #git-repo-vsi}

Quando l'applicazione viene distribuita a {{site.data.keyword.cloud_notm}}, viene creato un repository GitLab per ospitare il codice per la gestione del codice di origine. Puoi utilizzare le operazioni Git per consentire ai team di lavorare e distribuire le modifiche alla tua applicazione. Le cartelle incluse in questo repository e una spiegazione del loro contenuto.

#### Cartella Debian
{: #debian-folder}

La cartella `debian` contiene la configurazione richiesta per abilitare l'impacchettamento dell'applicazione in un [pacchetto Debian](https://www.debian.org/doc/manuals/debian-faq/ch-pkgtools.en.html){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").

#### Cartella Terraform
{: #terraform-folder}

La cartella `terraform` contiene la configurazione dell'infrastruttura come codice che può essere utilizzato per eseguire il provisioning delle risorse dell'infrastruttura. Il file `main.tf` è l'origine principale per modificare le opzioni per la tua configurazione Terraform.

```json
resource "ibm_compute_vm_instance" "vm1" {
    hostname = "${var.vi_instance_name}"
    domain = "example.com"
    os_reference_code = "DEBIAN_8_64"
    datacenter = "${var.datacenter}"
    network_speed = 100
    hourly_billing = true
    private_network_only = false
    cores = 1
    memory = 1024
    disks = [25]
    local_disk = false
    ssh_key_ids = [
        "${ibm_compute_ssh_key.ssh_key_gip.id}"
    ]
}
```

Puoi anche eseguire il provisioning di server bare metal con Terraform. Per ulteriori informazioni, consulta la [documentazione di IBM Terraform Provider](https://ibm-cloud.github.io/tf-ibm-docs/v0.10.0/){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") e il [repository GIT IBM Terraform](https://github.com/IBM-Cloud/terraform-provider-ibm){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").

`variables.tf` può essere utilizzato per modificare il data center che vuoi destinare alla creazione dell'istanza virtuale. Per visualizzare l'elenco dei data center definiti sulla piattaforma, consulta [Data Centers](https://www.ibm.com/cloud-computing/bluemix/data-centers){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").

Per impostazione predefinita, il file Terraform è configurato per Washington e `wdc04`.
```json
variable "datacenter" {
  description = "Washington"
  default = "wdc04"
}
```

### Descrizione delle fasi della toolchain
{: #toolchain-stages-vsi}

La toolchain mostra la distribuzione dell'infrastruttura e dell'applicazione in una semplice pipeline. Suddividi l'infrastruttura come parte di codice in una pipeline e la distribuzione dell'applicazione in un'altra pipeline.

Il processo della toolchain ha cinque fasi.

1. La fase di build clona il repository Git e assembla il codice in un pacchetto Debian.
2. La fase di pianificazione di Terraform prepara un piano Terraform.
  ```console
  terraform init -input=false
  terraform validate
  terraform plan -var "ssh_public_key=$PUBLIC_KEY" -input=false -out tfplan
  ```

3. La fase di applicazione di Terraform applica la configurazione Terraform e attende finché non è disponibile l'indirizzo IP del server virtuale.

  ```console
  terraform apply -auto-approve -input=false tfplan
  terraform output "host ip" > hostip.txt
  ```

4. La fase di distribuzione, installazione, avvio sposta il pacchetto Debian creato nella prima fase nel server virtuale in esecuzione, lo installa e quindi lo avvia.
5. La fase di controllo di integrità convalida che l'endpoint di integrità sia disponibile nell'applicazione e quindi completa la pipeline.

Per accedere all'applicazione dopo che è stata avviata, controlla i log della fase del controllo di integrità. Fai clic sui link URL elencati nei log che mostrano l'indirizzo IP e la porta dell'applicazione.
