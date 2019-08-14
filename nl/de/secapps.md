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

# Zertifikatssignieranforderungen erstellen
{: #ssl_csr}

Sie können Ihre Anwendungen schützen, indem Sie SSL-Zertifikate hochladen und den Zugriff auf die Apps beschränken.
{: shortdesc}

## Zertifikatssignieranforderung erstellen
{: #create_csr}

Bevor Sie die SSL-Zertifikate hochladen können, für die Sie in {{site.data.keyword.cloud}} berechtigt sind, müssen Sie auf Ihrem Server eine Zertifikatssignieranforderung (CSR) erstellen. Bei einer CSR handelt es sich um eine Nachricht, die an eine Zertifizierungsstelle gesendet wird, um die Signierung eines öffentlichen Schlüssels und der zugehörigen Informationen anzufordern. Am häufigsten haben CSRs das Format des PKCS-Standards #10. Die CSR umfasst einen öffentlichen Schlüssel und einen allgemeinen Namen, eine Organisation, eine Stadt, ein Bundesland, ein Land sowie eine E-Mail-Adresse. SSL-Zertifikatsanforderungen werden nur mit einer CSR-Schlüssellänge von 2048 Bits akzeptiert.

Die Methoden für die Erstellung einer CSR variieren in Abhängigkeit von Ihrem Betriebssystem. Das folgende Beispiel zeigt, wie eine CSR mithilfe des [OpenSSL-Befehlszeilentools ](https://www.openssl.org/){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") erstellt wird:

```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout
    privatekey.key
```
{: codeblock}

Die OpenSSL-Implementierung SHA-512 ist von der Compilerunterstützung für den ganzzahligen 64-Bit-Typ abhängig. Sie können die SHA-1-Option für Apps verwenden, die Kompatibilitätsprobleme mit dem SHA-256-Zertifikat haben.
{: tip}

### Erforderliche CSR-Inhalte

Damit die CSR gültig ist, müssen bei ihrer Erstellung die folgenden Angaben gemacht werden:

 * **Landeskennzahl**: Ein zweistelliger Code für das Land oder die Region. So zum Beispiel ist `US` der Landescode für die Vereinigten Staaten. Ziehen Sie für weitere Länder oder Regionen vor der Erstellung der CSR die [Liste der ISO-Landescodes ](https://www.iso.org/obp/ui/#search){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") zurate.
 * **Bezirk oder Bundesland**: Der vollständige und ungekürzte Name des Bezirks oder Bundeslands/Kantons.
 * **Standort**: Der vollständige Name der Stadt.
 * **Organisation**: Der vollständige Name des Geschäfts oder des Unternehmens, das an Ihrem Standort rechtsgültig registriert ist, oder ein persönlicher Name. Bei Unternehmen müssen Sie sicherstellen, dass das Registrierungssuffix mit angegeben wird, z. B. Ltd., Inc. oder NV.
 * **Organisationseinheit**: Der Name der Abteilung Ihres Unternehmens, die das Zertifikat anfordert, z. B. Buchhaltung oder Marketing.
 * **Allgemeiner Name**: Der vollständig qualifizierte Domänenname (FQDN), für den Sie das SSL-Zertifikat anfordern.

Sie können SANs (Subject Alternative Names) verwenden, die angegebenen Hostnamen dürfen jedoch nicht in anderen bereitgestellten Zertifikaten verwendet werden, um CN-Konflikte zu vermeiden.
{: note}

Ein Zertifikat wird von einer Zertifizierungsstelle ausgegeben und von dieser Zertifizierungsstelle digital signiert. Nach dem Erstellen der Zertifikatssignieranforderung (Certificate Signing Request, CSR) können Sie Ihr SSL-Zertifikat bei einer öffentlichen Zertifizierungsstelle generieren.

## SSL-Zertifikate hochladen
{: #ssl_certificate}

Sie können ein Sicherheitsprotokoll anwenden, um die Kommunikation für Ihre App zu schützen und so ein Ausspionieren, Manipulationen und das Fälschen von Nachrichten zu verhindern. Wenn Sie über ein kostenfreies Lite-Konto verfügen, müssen Sie ein Upgrade für Ihr Konto durchführen, um ein Zertifikat hochladen zu können.

Wenn ein abgelaufenes oder ein bald ablaufendes Zertifikat verlängert werden muss, löschen Sie das vorhandene Zertifikat und fügen Sie ein neues hinzu, nachdem das neue Zertifikat bereitsteht.
{: note}

Wenn Sie eine angepasste Domäne verwenden, um das SSL-Zertifikat ordnungsgemäß bereitzustellen, müssen Sie die folgenden Regionsendpunkte verwenden, um die URL-Route für Ihre Organisation in {{site.data.keyword.cloud_notm}} anzugeben:

| Region | Endpunkt |
| ------ | -------- |
| US-South | `custom-domain.us-south.cf.cloud.ibm.com` |
| US-East | `custom-domain.us-east.cf.cloud.ibm.com` |
| EU-DE | `custom-domain.eu-de.cf.cloud.ibm.com` |
| EU-GB | `custom-domain.eu-gb.cf.cloud.ibm.com` |
| AU-SYD | `custom-domain.au-syd.cf.cloud.ibm.com` | 
{: caption="Tabelle 1. Benutzerdefinierte Endpunkte für die Cloud Foundry-Domänenregion" caption-side="top"}

Führen Sie die folgenden Schritte aus, um ein Zertifikat für Ihre Cloud Foundry-App hochzuladen:

1. Klicken Sie in der [{{site.data.keyword.cloud_notm}}-Konsole ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}){: new_window} auf das Symbol **Menü** ![Menüsymbol](../icons/icon_hamburger.svg) und wählen Sie **Ressourcenliste** aus.
2. Klicken Sie auf **Cloud Foundry-Apps**.
3. Klicken Sie auf die App, für die Sie die Domäne ändern möchten. 
4. Klicken Sie auf der Seite 'Übersicht' der App auf **Routen** und wählen Sie **Domänen verwalten** aus.
5. Klicken Sie in der Spalte 'Aktionen' auf das Symbol für Aktionen: ![Symbol 'Weitere Aktionen'](../icons/action-menu-icon.svg) und wählen Sie **Domänen** aus.
6. Klicken Sie für Ihre angepasste Domäne auf **Hochladen**.
7. Wählen Sie eine Option aus, laden Sie die Datei hoch und klicken Sie auf **Hinzufügen**.
  
  * Zertifikat: Ein digitales Dokument, das einen öffentlichen Schlüssel an die Identität des Zertifikatsinhabers bindet, sodass der Zertifikatsinhaber authentifiziert werden kann. Ein Zertifikat wird von einer Zertifizierungsstelle ausgegeben und von dieser Zertifizierungsstelle digital signiert. Ein Zertifikat wird in der Regel ausgegeben und von einer Zertifizierungsstelle signiert. Für Test- und Entwicklungszwecke können Sie ein selbst signiertes Zertifikat verwenden.
  * Privater Schlüssel: Ein algorithmisches Muster, das verwendet wird, um Nachrichten zu verschlüsseln, die nur der zugehörige öffentliche Schlüssel entschlüsseln kann. Mit dem privaten Schlüssel werden auch Nachrichten entschlüsselt, die vom entsprechenden öffentlichen Schlüssel verschlüsselt wurden. Der private Schlüssel wird im System des Benutzers gespeichert und durch ein Kennwort geschützt.
  * Zwischenzertifikat (optional): Ein untergeordnetes Zertifikat, das von der Zertifizierungsstelle für Trusted Roots speziell dafür ausgegeben wird, Serverzertifikate für End-Entitäten auszugeben. Im Ergebnis erhält man eine Zertifikatskette, die mit der Zertifizierungsstelle für Trusted Roots beginnt und über das Zwischenzertifikat zum SSL-Zertifikat gelangt, das für die Organisation ausgegeben wird. Verwenden Sie ein Zwischenzertifikat, um die Authentizität des Hauptzertifikats zu prüfen. Zwischenzertifikate werden normalerweise von einem vertrauenswürdigen Dritten angefordert. Möglicherweise benötigen Sie kein Zwischenzertifikat, wenn Sie Ihre App vor der Bereitstellung für die Produktion testen.
  * Anforderung eines Clientzertifikats aktivieren: Wenn Sie diese Option aktivieren, wird ein Benutzer bei dem Versuch, auf eine durch SSL geschützte Domäne zuzugreifen, aufgefordert, ein clientseitiges Zertifikat anzugeben. Beispiel: Wenn in einem Web-Browser ein Benutzer versucht, auf eine SSL-geschützte Domäne zuzugreifen, wird der Benutzer im Web-Browser dazu aufgefordert, für die Domäne ein Clientzertifikat bereitzustellen.   
  * Truststore für Clientzertifikate (optional): Dieser enthält die Clientzertifikate für die Benutzer, denen Sie Zugriff auf Ihre App erteilen möchten. Laden Sie eine Truststore-Datei für Clientzertifikate hoch, um die Option zum Anfordern eines Clientzertifikats zu aktivieren.
  
    Sie können die gegenseitige Authentifizierung konfigurieren, indem Sie einen Truststore mit Clientzertifikaten hochladen, der in den zugehörigen Metadaten einen öffentlichen Schlüssel enthält.
    {: tip}


