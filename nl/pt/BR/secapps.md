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

# Criando solicitações de assinatura de certificado
{: #ssl_csr}

É possível proteger seus aplicativos fazendo upload de certificados SSL e restringindo o acesso aos apps.
{: shortdesc}

## Criando um Certificate Signing Request
{: #create_csr}

Antes que seja possível fazer upload dos certificados SSL aos quais você está autorizado com o {{site.data.keyword.cloud}}, deve-se criar uma solicitação de assinatura de certificado (CSR) no servidor. Uma CSR é uma mensagem que é enviada a uma autoridade de certificado para solicitar
a assinatura de uma chave pública e as informações associadas. O mais comum é que as CSRs estejam no formato PKCS #10. A CSR inclui uma chave pública, um nome comum, uma organização, uma cidade, um estado, um país e um e-mail. As
solicitações de certificado SSL são aceitas somente com um comprimento da chave CSR de 2048 bits.

Os métodos para criar uma CSR veriam dependendo de seu sistema operacional. O exemplo a seguir mostra como criar uma CSR usando a [ferramenta de linha de comandos OpenSSL ](https://www.openssl.org/){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo"):

```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout privatekey.key
```
{: codeblock}

A implementação OpenSSL SHA-512 depende do suporte
do compilador para o tipo de número inteiro de 64 bits. É possível usar a opção SHA-1 para apps que têm problemas de compatibilidade com o certificado SHA-256.
{: tip}

### Conteúdos CSR obrigatórios

Para que a CSR seja válida, as informações a seguir devem ser inseridas ao criar a CSR:

 * **Nome do país**: um código de dois dígitos para o país ou a região. Por exemplo, `US` é o código do país para os Estados Unidos. Para
outros países ou regiões, antes de criar a CSR, verifique a [lista
de códigos de país ISO ](https://www.iso.org/obp/ui/#search){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").
 * **Estado ou município**: o nome completo, sem abreviação, do estado ou da província.
 * **Localidade**: o nome completo da cidade.
 * **Organização**: o nome completo do negócio ou da empresa, como legalmente registrado em sua localidade, ou o nome pessoal. Para
empresas, certifique-se de incluir o sufixo de registro, como Ltd., Inc. ou NV.
 * **Unidade da organização**: o nome da ramificação de sua empresa que está pedindo o certificado, como contabilidade ou marketing.
 * **Nome comum**: O nome completo do domínio (FQDN) para o qual você está solicitando o certificado SSL.

É possível usar Subject Alternnative Names (SAN), mas os nomes de host fornecidos não devem ser emitidos em outros certificados implementados para evitar colisões de CN.
{: note}

Um
certificado é emitido por uma autoridade de certificação e é assinado digitalmente por
essa autoridade. Depois de criar o CSR, é possível gerar seu certificado SSL em uma autoridade de certificado público.

## Fazendo upload de certificados SSL
{: #ssl_certificate}

É possível aplicar um protocolo de segurança para fornecer privacidade de comunicação para seu app para evitar espionagem de tráfego de rede, violação e falsificação de mensagens. Se você tiver uma conta Lite, deverá fazer upgrade de sua conta para fazer upload de um certificado.

Quando um certificado expirado ou expirando precisar ser renovado e depois que o novo certificado estiver pronto, exclua o certificado existente e, em seguida, inclua o novo.
{: note}

Ao usar um domínio customizado para entregar o certificado SSL, use os terminais de região a seguir para fornecer a rota de URL para sua organização no {{site.data.keyword.cloud_notm}}:

| Região | Nó de
extremidade |
| ------ | -------- |
| Sul dos EUA | `custom-domain.us-south.cf.cloud.ibm.com` |
| Leste dos EUA | `custom-domain.us-east.cf.cloud.ibm.com` |
| EU-DE | `custom-domain.eu-de.cf.cloud.ibm.com` |
| EU-GB | `custom-domain.eu-gb.cf.cloud.ibm.com` |
| AU-SYD | `custom-domain.au-syd.cf.cloud.ibm.com` | 
{: caption="Tabela 1. Terminais de região de domínio customizado do Cloud Foundry" caption-side="top"}

Para fazer upload de um certificado para seu app Cloud Foundry, conclua as etapas a seguir:

1. No [console do {{site.data.keyword.cloud_notm}}![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}){: new_window}, clique no ícone **Menu** ![ícone Menu](../icons/icon_hamburger.svg) e selecione **Lista de recursos**.
2. Clique em **Apps Cloud Foundry**.
3. Clique no app para o qual você deseja mudar o domínio. 
4. Na página Visão geral do app, clique em **Rotas**e selecione **Gerenciar domínios**.
5. Na coluna Ações, clique no ícone Ações ![Ícone Mais ações](../icons/action-menu-icon.svg) e selecione **Domínios**.
6. Clique em **Upload** para seu domínio customizado.
7. Selecione uma opção, faça upload do arquivo e clique em **Incluir**.
  
  * Certificado: um documento digital que liga uma chave pública à identidade do proprietário do certificado, o que permite
que o proprietário do certificado seja autenticado. Um
certificado é emitido por uma autoridade de certificação e é assinado digitalmente por
essa autoridade. Um certificado é geralmente emitido e assinado por uma autoridade de certificação. No entanto, para
propósitos de teste e desenvolvimento, você pode usar um certificado autoassinado.
  * Chave privada: um padrão algorítmico que é usado para criptografar mensagens que somente a chave pública correspondente
pode decriptografar. A chave privada também é usada para decriptografar mensagens que foram criptografadas pela chave pública correspondente. A chave privada é
mantida no sistema do usuário e é protegida por uma senha.
  * Certificado intermediário (opcional): um certificado subordinado emitido pela autoridade de certificação (CA) raiz
confiável especificamente para emitir certificados de servidor de entidade final. O resultado é uma cadeia de certificados que inicia na autoridade de certificação raiz
confiável, passa pelo certificado intermediário e termina com o
certificado SSL emitido para a organização. Use um certificado intermediário para verificar a autenticidade do certificado principal. Os certificados intermédios geralmente são obtidos de um terceiro confiável. Você pode não requerer um certificado intermediário ao testar seu app antes de implementá-lo na produção.
  * Ativar solicitação de certificado de cliente: ao ativar essa opção, quando um usuário tentar acessar um domínio
protegido por SSL, um certificado do lado do cliente será solicitado a ele. Por exemplo, em um navegador da web, quando um usuário tentar acessar um domínio protegido por SSL, o navegador da web solicitará ao usuário que forneça um certificado de cliente para o domínio.   
  * Armazenamento confiável de certificado de cliente (opcional): inclui os certificados de cliente para os usuários para os quais você deseja permitir acesso ao seu app. Faça upload de um arquivo de armazenamento confiável de certificado de cliente para ativar a opção para solicitar um certificado de cliente.
  
    É possível configurar a autenticação mútua fazendo upload de um armazenamento confiável de certificado de cliente que inclui uma chave pública em seus metadados.
    {: tip}


