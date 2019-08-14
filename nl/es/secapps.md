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

# Creación de solicitudes de firma de certificado
{: #ssl_csr}

Puede proteger las aplicaciones subiendo certificados SSL y limitando el acceso a las apps.
{: shortdesc}

## Creación de una solicitud de firma de certificado
{: #create_csr}

Para poder cargar los certificados SSL a los que esté autorizado con {{site.data.keyword.cloud}}, debe crear una solicitud de firma de certificado (CSR) en el servidor. Una CSR es un mensaje que se envía a una entidad emisora de certificados para solicitar la firma de una clave pública
y de información asociada. De forma más común, las CSR se encuentran en el formato PKCS número 10. La CSR incluye una clave pública, un nombre común, una organización, una ciudad, un estado, un país y un correo electrónico. Las solicitudes de certificados SSL
sólo están aceptadas con una longitud de claves CSR de 2048 bits.

Los métodos para crear una CSR varían en función del sistema operativo. En el ejemplo siguiente se muestra cómo crear una CSR utilizando [la herramienta de línea de mandatos OpenSSL](https://www.openssl.org/){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo"):

```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout privatekey.key
```
{: codeblock}

La implementación SHA-512 de OpenSSL depende del soporte de compilador para el tipo de entero de 64 bits. Puede utilizar la opción SHA-1 para las apps que tienen problemas de compatibilidad con el certificado SHA-256.
{: tip}

### Contenido necesario de CSR

Para que la CSR sea válida, debe especificarse la siguiente información al crear la CSR:

 * **Nombre de país**: un código de dos dígitos correspondiente al país o a la región. Por ejemplo, `US` es el código de país correspondiente a Estados Unidos. Para otros países o regiones, antes de crear la CSR, consulte la [lista de códigos de países ISO](https://www.iso.org/obp/ui/#search){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").
 * **Estado o provincia**: el nombre completo no abreviado del estado o de la provincia.
 * **Localidad**: el nombre completo del pueblo o la ciudad.
 * **organización**: el nombre completo de la empresa, como esté registrada legalmente en su localidad, o el nombre personal. Para las empresas, asegúrese de incluir el sufijo de registro, como por ejemplo Ltd., Inc. o NV.
 * **Unidad organizativa**: nombre de la rama de su empresa que está pidiendo el certificado, como por ejemplo contabilidad o
marketing.
 * **Nombre común**: nombre de dominio completo (FQDN) para el que está solicitando el certificado SSL.

Puede utilizar Nombres alternativos de sujeto (SAN, Subject Alternative Names), pero los nombres de host proporcionados no pueden haberse emitido en otros certificados desplegados para evitar conflictos de CN.
{: note}

Un certificado lo emite una entidad emisora de certificados, que lo firma digitalmente. Después de crear la CSR, puede generar el certificado SSL en una entidad emisora de certificados pública.

## Carga de certificados SSL
{: #ssl_certificate}

Puede aplicar un protocolo de seguridad para proporcionar privacidad de comunicación a la app a fin de impedir escuchas no autorizadas, manipulación indebida e interferencia de mensajes. Si tiene una cuenta Lite, debe actualizar su cuenta para cargar un certificado.

Cuando se tiene que renovar un certificado caducado o próximo a caducar, y una vez el certificado nuevo está listo, suprima el certificado existente y, a continuación, añada el nuevo.
{: note}

Si utiliza un dominio personalizado para servir el certificado SSL, utilice los siguientes puntos finales de región para proporcionar la ruta de URL asignada a la organización en {{site.data.keyword.cloud_notm}}:

| Región | Punto final |
| ------ | -------- |
| US-South | `custom-domain.us-south.cf.cloud.ibm.com` |
| US-East | `custom-domain.us-east.cf.cloud.ibm.com` |
| EU-DE | `custom-domain.eu-de.cf.cloud.ibm.com` |
| EU-GB | `custom-domain.eu-gb.cf.cloud.ibm.com` |
| AU-SYD | `custom-domain.au-syd.cf.cloud.ibm.com` | 
{: caption="Tabla 1. Puntos finales de regiones de dominios personalizados de Cloud Foundry" caption-side="top"}

Para cargar un certificado para su app Cloud Foundry, complete los siguientes pasos:

1. En la [consola de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}){: new_window}, pulse el icono **Menú** ![Icono Menú](../icons/icon_hamburger.svg) y seleccione **Lista de recursos**.
2. Pulse **Apps de Cloud Foundry**.
3. Pulse sobre la app para la cual desee cambiar el dominio. 
4. En la página Visión general de la app, pulse **Rutas** y seleccione **Gestionar dominios**.
5. En la columna Acciones, pulse el icono Acciones ![Icono Más acciones](../icons/action-menu-icon.svg) y seleccione
**Dominios**.
6. Pulse **Cargar** para el dominio personalizado.
7. Seleccione una opción, cargue el archivo y pulse **Añadir**.
  
  * Certificado: documento digital que enlaza una clave pública con la identidad del propietario
del certificado, permitiendo de este modo autenticar al propietario de este certificado. Un certificado lo emite una entidad emisora de certificados, que lo firma digitalmente. Por lo general un certificado lo emite y firma una entidad emisora de certificados. Sin embargo, para fines de prueba y desarrollo puede utilizar un certificado autofirmado.
  * Clave privada: patrón algorítmico utilizado para cifrar mensajes que solo se pueden descifrar con la clave pública correspondiente. La clave privada también se utiliza para descifrar mensajes que se han cifrado mediante la clave pública correspondiente. La clave privada se guarda en el sistema del usuario y se
protege mediante una contraseña.
  * Certificado intermedio (opcional): certificado subordinado emitido por la entidad emisora de certificados (CA) raíz de confianza específicamente para emitir certificados del servidor de la entidad final. El resultado es una cadena de certificados que empieza en la entidad emisora de certificados raíz de confianza, pasa por el certificado intermedio y termina con la emisión del certificado SSL a la organización. Utilice a un certificado intermedio para verificar la autenticidad del certificado principal. Los certificados intermedios normalmente se obtienen de un tercero de confianza. Es posible que no necesite un certificado intermedio para probar la app antes de desplegarla en producción.
  * Habilitar solicitud de certificado de cliente: si habilita esta opción, a los usuarios que intenten acceder a un dominio protegido por SSL se les solicitará que especifiquen un certificado del lado del cliente. Por ejemplo en un navegador web, cuando un usuario intenta acceder a un dominio protegido por SSL, el navegador web le solicita que especifique un certificado de cliente para el dominio.   
  * Almacén de confianza de certificados de cliente (opcional): incluye los certificados de cliente para los usuarios a los que desea permitir el acceso a la app. Cargue un archivo de almacén de confianza de certificado de cliente para habilitar la opción de solicitud de certificado de cliente.
  
    Puede configurar la autenticación mutua cargando un almacén de confianza de certificado de cliente que incluya una clave pública en sus metadatos.
    {: tip}


