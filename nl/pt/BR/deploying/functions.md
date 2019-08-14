---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-18"

keywords: apps, serverless, serverless app, functions, cli, api, sdk

subcollection: creating-apps

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Criando apps serverless
{: #serverless}

Para desenvolvimento sem servidor, é possível usar a oferta Functions as a service (FaaS) da IBM, {{site.data.keyword.openwhisk}}. É possível executar a lógica do aplicativo com o {{site.data.keyword.openwhisk_short}} em resposta a eventos ou chamadas diretas de apps da web ou móveis sobre HTTP sem provisionar ou gerenciar servidores. O {{site.data.keyword.openwhisk_short}} executa administração do sistema, como auto-scaling, gerenciamento de disponibilidade e manutenção para que você, como desenvolvedor, possa se concentrar na gravação de lógica do aplicativo.
{:shortdesc}

É possível usar a interface com o usuário (UI) ou a interface da linha de comandos (CLI) do {{site.data.keyword.openwhisk_short}} para desenvolver seus aplicativos. Ambas têm recursos semelhantes para desenvolver aplicativos. A CLI fornece mais controle sobre sua implementação e operações. Para obter informações mais detalhadas sobre o {{site.data.keyword.openwhisk_short}}, verifique a [documentação](/docs/openwhisk?topic=cloud-functions-index).

## {{site.data.keyword.openwhisk_short}} UI
{: #serverless-apps-ui}

Experimente o {{site.data.keyword.openwhisk_short}} em seu [navegador](https://{DomainName}/openwhisk/actions){: new_window}![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")}. Acesse a página [Conceitos ](https://{DomainName}/openwhisk/learn){: new_window} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo") para obter um tour rápido da interface com o usuário do {{site.data.keyword.openwhisk_short}}.

## Desenvolvendo com a CLI
{: #openwhisk_start_configure_cli}

Para saber mais sobre como instalar e desenvolver com a CLI do {{site.data.keyword.openwhisk_short}}, consulte [Configurando a CLI do {{site.data.keyword.openwhisk_short}}](https://{DomainName}/openwhisk/cli){: new_window} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo").

## Expondo APIs e conjuntos de dados como ações da web
{: #expose-actions}

Por padrão, o {{site.data.keyword.openwhisk_short}} define ações que requerem uma chave de autenticação. Em ambientes de dispositivo móvel de produção, muitas vezes é necessário autorizar clientes móveis com base em fluxos OAuth para expor APIs e conjuntos de dados específicos.

O {{site.data.keyword.openwhisk_short}} permite que os desenvolvedores exponham suas funções como ações da web, que são anotadas, para construir rapidamente aplicativos baseados na web. É possível programar a lógica de backend com ações anotadas que seu aplicativo da web pode acessar anonimamente, sem requerer uma chave de autenticação do {{site.data.keyword.openwhisk_short}}.

Para expor uma ação como uma ação da web, acesse a guia **Terminais** de sua ação e selecione **Ativar como ação da web**.

Agora, os usuários podem acessar a ação por meio de um navegador ou solicitação cURL, por exemplo:
```
curl https://openwhisk.cloud.ibm.com/api/v1/web/aaron.m.liberatore_dev/MyPackage/helloWorld.json?name=aaron
```
{: codeblock}

**Saída:**
```json
{
    message: "Hello aaron!"
}
```
{: screen}

### SDK
{: #sdk}

O {{site.data.keyword.openwhisk_short}} fornece um [SDK móvel](/docs/openwhisk?topic=cloud-functions-openwhisk_mobile_sdk) para dispositivos iOS e watchOS que permite que os apps móveis enviem facilmente acionadores remotos e chamem ações remotas. Ele também fornece um [SDK de estrutura sem servidor ](/docs/openwhisk?topic=cloud-functions-openwhisk_goserverless){: new_window} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo") que permite aplicativos sem servidor.

