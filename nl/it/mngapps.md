---

copyright:
  years: 2015, 2018
lastupdated: "2019-03-15"

subcollection: creating-apps

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Controllo dello stato della tua applicazione
{: #manageapps}

Il tuo elenco risorse nella console {{site.data.keyword.cloud}} fornisce delle informazioni di riepilogo per le applicazioni da te create. Le informazioni di riepilogo includono nome, icona, URL, runtime, stato di esecuzione e istanze del servizio associate all'applicazione.
{:shortdesc}

## Descrizione dello stato della tua applicazione
{: #status}

Dal tuo elenco risorse, puoi visualizzare lo stato di ciascuna applicazione. Nella colonna dello stato di ogni applicazione, puoi vedere se le istanze dell'applicazione sono in esecuzione.

<dl>
<dt>
<strong>
Arrestato o Sconosciuto (grigio)
</strong>
</dt>
<dd>
La tua applicazione è arrestata oppure lo stato è sconosciuto. L'icona grigia indica che l'applicazione è arrestata oppure che lo stato è sconosciuto.
</dd>
<dt>
<strong>
In esecuzione (verde)
</strong>
</dt>
<dd>
La tua applicazione è in esecuzione. L'icona verde indica che l'applicazione è avviata e tutte le istanze sono in esecuzione.
</dd>
<dt>
<strong>
_Numero_  in esecuzione (giallo)
</strong>
</dt>
<dd>
L'applicazione è stata avviata ma non tutte le istanze sono in esecuzione. L'icona gialla indica che è in esecuzione meno del 100% delle istanze. Viene visualizzato il numero di istanze in esecuzione e il numero di istanze non riuscite.
</dd>
<dt>
<strong>
Non in esecuzione (rosso)
</strong>
</dt>
<dd>
La tua applicazione non è in esecuzione. L'icona rossa indica che l'applicazione è avviata, ma nessuna istanza è in esecuzione.
</dd>
</dl>

## Visualizzazione dei dettagli della tua applicazione
{: #viewingapps}

Puoi visualizzare ulteriori informazioni su un'applicazione facendo clic sul suo nome nel tuo elenco risorse. Quindi, puoi visualizzare la pagina Panoramica dell'applicazione.

Nella pagina Panoramica dell'applicazione, dopo che un'applicazione viene distribuita, puoi avviare, arrestare, riavviare o, nel caso di applicazioni web, modificare il numero di istanze e la quantità di memoria utilizzata dall'applicazione. Per le applicazioni web, {{site.data.keyword.cloud_notm}} non ridimensiona automaticamente la tua applicazione in base al suo carico, quindi devi essere tu a gestire questo aspetto.

Se viene apportato un aggiornamento, le applicazioni possono essere ridistribuite. Il meccanismo di aggiornamento dell'applicazione è uguale al meccanismo utilizzato per la sua originale distribuzione. {{site.data.keyword.cloud_notm}} arresta
tutte le istanze in esecuzione e le sostituisce con le nuove istanze automaticamente.
