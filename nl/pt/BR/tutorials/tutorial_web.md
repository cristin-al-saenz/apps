---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-15"

keywords: apps, web app, starter kit, App Service, developer tools, DevOps toolchain

subcollection: creating-apps

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Criando um app básico da web com um kit do iniciador
{: #tutorial-webapp}

O {{site.data.keyword.cloud}} oferece vários kits do iniciador para ajudar você a obter a codificação rapidamente. Escolha uma linguagem, estrutura e ferramentas dos kits do iniciador do App Service para começar a trabalhar com um aplicativo customizado pré-configurado. Neste tutorial, você percorrerá as etapas para instalar as ferramentas necessárias e, em seguida, construirá e executará o app localmente e o implementará na nuvem.
{: shortdesc}

## Etapa 1. Instale as ferramentas
{: #prereqs-webapp}

Instale as [ferramentas do desenvolvedor](/docs/cli?topic=cloud-cli-ibmcloud-cli).

O Docker é instalado como parte das ferramentas do desenvolvedor. O Docker deve estar em execução para que os comandos de construção funcionem. Deve-se criar uma conta do Docker, executar o app Docker e conectar-se.

## Etapa 2. Selecione um kit do iniciador
{: #create-webapp}

Há kits do iniciador disponíveis em várias linguagens e estruturas no {{site.data.keyword.cloud_notm}} {{site.data.keyword.dev_console}}. Selecione a linguagem que for melhor para seu projeto ser iniciado.

1. Na página [Kits do iniciador ](https://{DomainName}/developer/appservice/starter-kits/){: new_window} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo") no {{site.data.keyword.dev_console}}, selecione um kit do iniciador para sua linguagem.
2. Insira o nome do app e um nome de host exclusivo, por exemplo, `abc-devhost`. Esse nome do host é a rota do app, `abc-devhost.mybluemix.net`.
3. Opcional. Forneça identificações para classificar o seu app. Para obter mais informações, consulte [Trabalhando com tags](/docs/resources?topic=resources-tag).
4. Selecione a linguagem e a estrutura. Alguns kits do iniciador podem estar disponíveis apenas em uma linguagem.
5. Selecione seu plano de precificação. Há uma opção grátis que pode ser usada para este tutorial.
6. Clique em **Criar**.

O domínio compartilhado padrão é `mybluemix.net`, mas o `appdomain.cloud` é outra opção de domínio que você pode usar. Para obter mais informações sobre como migrar para o `appdomain.cloud`, consulte [Atualizando seu domínio](/docs/apps/tutorials?topic=creating-apps-update-domain).
{: tip}

## Etapa 3. Incluir serviços (opcional)
{: #resources-webapp}

É possível incluir serviços que aprimoram seu app com o poder cognitivo do Watson, incluir serviços remotos ou serviços de segurança. Para este tutorial, inclua um local para gerenciar seus dados.

1. Na página **Detalhes do app**, clique em **Incluir serviços**.
2. Selecione o tipo de serviço desejado. Por exemplo, selecione **Dados** > **Avançar** > **Cloudant** > **Avançar**.
3. Selecione seu plano de precificação. Há uma opção grátis que pode ser usada para este tutorial.
4. Clique em **Criar**.

## Etapa 4. Criar uma cadeia de ferramentas do DevOps
{: #toolchain-webapp}

A ativação de uma cadeia de ferramentas cria um ambiente de desenvolvimento baseado em equipe para seu app. Quando você cria uma cadeia de ferramentas, o serviço de app cria um repositório Git, no qual é possível visualizar o código-fonte, clonar seu app e criar e gerenciar problemas. Você também tem acesso a um ambiente de laboratório Git dedicado e a um pipeline de entrega contínua. Eles são customizados para o destino de implementação que você escolher, seja ele [Kubernetes](/docs/containers?topic=containers-getting-started), [Cloud Foundry](/docs/cloud-foundry-public?topic=cloud-foundry-public-about-cf), [{{site.data.keyword.cfee_full_notm}}](/docs/cloud-foundry?topic=cloud-foundry-about) ou [Virtual Server (VSI)](/docs/vsi?topic=virtual-servers-getting-started-with-virtual-servers).

A entrega contínua é ativada para alguns aplicativos. É possível ativar a entrega contínua para automatizar construções, testes e implementações por meio do Delivery Pipeline e do GitHub.

Clique em **Configurar entrega contínua** na página **Detalhes do app**, selecione um destino de implementação e clique em **Criar**. O {{site.data.keyword.cloud_notm}} automaticamente cria uma cadeia de ferramentas aberta e completa com um repositório Git e um pipeline de entrega contínua.

Depois de selecionar seu destino de implementação, abra o componente de pipeline de sua nova cadeia de ferramentas para iniciar o processo de construção e implementação inicial para que você possa ver o seu novo app em minutos.

Para obter mais informações, consulte [Criando cadeias de ferramentas](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-toolchains_getting_started).

## Etapa 5. Criar e executar o app localmente
{: #build-run-webapp}

A implementação de seu app na nuvem na última etapa criou uma cadeia de ferramentas. Uma cadeia de ferramentas cria um repositório Git para seu app no qual é possível localizar o código. Siga estas etapas para acessar o repositório. É possível construir o app localmente para teste antes de enviá-lo por push para a nuvem.

1. Na página **Detalhes do app**, clique em **Fazer download do código** ou **Clonar seu repositório** para trabalhar com seu código localmente.
2. Importe o app para seu ambiente de desenvolvimento integrado.
3. Modifique o código.
4. Configure a [Autenticação Git](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-git_working#git_authentication) incluindo um token de acesso pessoal.
5. Efetue login na interface da linha de comandos do {{site.data.keyword.cloud_notm}}. Se a sua organização usar logins federados, use a opção `-sso`.

  ```bash
  ibmcloud login -sso
  ```
  {: pre}

6. Configure seus destinos de organização e espaço.

  ```bash
  ibmcloud target --cf
  ```
  {: pre}

7. Obtenha as credenciais.

  ```bash
  ibmcloud dev get-credentials
  ```
  {: pre}

8. Verifique se o Docker está executando e crie seu app em um contêiner de desenvolvimento local do diretório.

  ```bash
  ibmcloud dev build
  ```
  {: pre}

9. Execute seu app em um contêiner de desenvolvimento local.

  ```bash
  ibmcloud dev run
  ```
  {: pre}

10. Abra seu navegador para `http://localhost:3000`. Seu número de porta pode ser diferente, dependendo do tempo de execução escolhido.

## Etapa 6. Implementar seu app
{: #deploy-webapp}

### Implementar usando uma cadeia de ferramentas
{: #deploy-webapp-toolchain}

É possível implementar seu app no {{site.data.keyword.cloud_notm}} de várias maneiras, mas uma cadeia de ferramentas do DevOps é a melhor maneira de implementar apps de produção. Com uma cadeia de ferramentas do DevOps, é possível automatizar facilmente implementações para muitos ambientes e incluir rapidamente serviços de monitoramento, criação de log e alerta para ajudar a gerenciar seu app à medida que ele cresce.

Com uma cadeia de ferramentas configurada corretamente, um ciclo de construção-implementação se inicia automaticamente com cada mesclagem na ramificação Principal em seu repositório. Todas as cadeias de ferramentas criadas por meio de um painel do desenvolvedor do {{site.data.keyword.cloud_notm}} são configuradas para implementação automática.

Também é possível implementar seu app manualmente por meio de sua cadeia de ferramentas DevOps:

1. Na página **Detalhes do app**, clique em **Visualizar cadeia de ferramentas**.
2. Clique em **Delivery Pipeline**, no qual é possível iniciar construções, gerenciar a implementação e visualizar logs e histórico.

Para obter mais informações, consulte [Construindo e implementando](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-deliverypipeline_build_deploy).

### Implementar usando o {{site.data.keyword.dev_cli_short}}
{: #deploy-webapp-cli}

Para implementar seu app para o Cloud Foundry, insira o comando a seguir:
```
ibmcloud dev deploy
```
{: pre}

Para implementar seu app em um cluster do Kubernetes, insira o comando a seguir:
```
ibmcloud dev deploy --target <container>
```
{: pre}

## Etapa 7. Verificar se o app está em execução
{: #verify-webapp}

Após você implementar o seu app, o Delivery Pipeline ou a linha de comandos apontará a você a URL para o seu app.

1. Na cadeia de ferramentas do seu DevOps, clique em **Delivery Pipeline** e, em seguida, selecione **Implementar estágio**.
2. Clique em **Visualizar logs e histórico**.
3. No arquivo de log, localize a URL do aplicativo:

    No término do arquivo de log, procure a palavra `urls` ou `view`. Por exemplo, é possível que você veja uma linha no arquivo de log que seja semelhante a `urls: my-app-devhost.mybluemix.net` ou `View the application health at: http://<ipaddress>:<port>/health`.

4. Acesse a URL em seu navegador. Se o app estiver em execução, uma mensagem que incluirá `Parabéns` ou `{"status":"UP"}` será exibida.

Se você estiver usando a linha de comandos, execute o comando [`ibmcloud dev view`](/docs/cli/idt?topic=cloud-cli-idt-cli#view) para visualizar a URL de seu app. Em seguida, acesse a URL em seu navegador.
