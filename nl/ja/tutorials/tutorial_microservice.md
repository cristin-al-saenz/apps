---

copyright:
  years: 2016, 2019
lastupdated: "2019-03-18"

keywords: apps, microservice, developer tools, Node.js, Java, Python, DevOps toolchain, toolchain, cli

subcollection: creating-apps

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# マイクロサービスの作成
{: #tutorial-microservice}

Microservice 基本スターターからアプリケーションを作成できます。 これらのスターターを使用し、Web フレームワークを選択して Node、Java、または Python のマイクロサービス・バックエンドをビルドできます。 必要なツールをインストールして、アプリをビルドしてローカルで実行し、クラウドにデプロイする方法を確認できます。
{: shortdesc}

## ステップ 1. ツールのインストール
{: #prereqs-microservice}

* [開発者ツール](/docs/cli?topic=cloud-cli-ibmcloud-cli)をインストールします。
* Docker は開発者ツールの一部としてインストールされます。 ビルド・コマンドが機能するためには、Docker が実行中でなければなりません。 Docker アカウントを作成して、Docker アプリを実行し、サインインする必要があります。
* アプリを [{{site.data.keyword.cfee_full}}](/docs/cloud-foundry?topic=cloud-foundry-about) にデプロイする計画の場合は、[{{site.data.keyword.cloud_notm}} アカウントを準備する](/docs/cloud-foundry?topic=cloud-foundry-prepare)必要があります。

## ステップ 2. アプリの作成
{: #create-microservice}

{{site.data.keyword.cloud}} {{site.data.keyword.dev_console}}でアプリを作成します。

1. {{site.data.keyword.dev_console}}の[「スターター・キット」](https://{DomainName}/developer/appservice/starter-kits/){: new_window} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン") ページから、ご使用の言語に対応するスターター・キットを選択します。 例えば、Node.js アプリケーションの場合は、**「Express.js マイクロサービス (Express.js Microservice)」**に移動し、**「スターター・キットの選択」**をクリックします。
2. アプリ名を入力します。 このチュートリアルでは、`MicroserviceProject` を使用します。
3. 固有のホスト名 (例えば、`abc-devhost`) を入力します。このホスト名は、アプリの経路 `abc-devhost.mybluemix.net` です。
4. オプション。 アプリを分類するためのタグを指定します。 詳しくは、『[タグの処理](/docs/resources?topic=resources-tag)』を参照してください。
5. ご使用の言語とフレームワークを選択します。 一部のスターター・キットは、1 つの言語でしか使用できない場合があります。
6. 価格プランを選択します。 このチュートリアルでは無料オプションを使用できます。
7. **「作成」**をクリックします。

デフォルトの共有ドメインは `mybluemix.net` ですが、`appdomain.cloud` という別のドメインも選択できます。`appdomain.cloud` への移行について詳しくは、[ドメインの更新](/docs/apps/tutorials?topic=creating-apps-update-domain)を参照してください。
{: tip}

## ステップ 3. サービスの追加 (オプション)
{: #resources-microservice}

Watson のコグニティブ機能でアプリを拡張するサービスを追加したり、モバイル・サービスやセキュリティー・サービスを追加したりできます。 このチュートリアルでは、データを管理する場所を追加します。

1. **アプリの詳細**ページで、**「サービスの追加」**をクリックします。
2. 必要なサービスの種類を選択します。 例えば、**「データ (Data)」**>**「次へ」**>**「Cloudant」**>**「次へ」**をクリックします。
3. 価格プランを選択します。 このチュートリアルでは無料オプションを使用できます。
4. **「作成」**をクリックします。

## ステップ 4. DevOps ツールチェーンの作成
{: #toolchain-microservice}

ツールチェーンを有効にすると、アプリ用のチーム・ベースの開発環境が作成されます。 ツールチェーンの作成時に、アプリ・サービスによって Git リポジトリーが作成されます。このリポジトリーでは、ソース・コードの表示、アプリの複製、および問題の作成と管理を行うことができます。 また、専用の GitLab 環境と、継続的 Delivery Pipeline にアクセスすることもできます。 選択したデプロイメント・ターゲットが、[Kubernetes](/docs/containers?topic=containers-getting-started)、[Cloud Foundry](/docs/cloud-foundry-public?topic=cloud-foundry-public-about-cf)、[{{site.data.keyword.cfee_full_notm}}](/docs/cloud-foundry?topic=cloud-foundry-about)、または[仮想サーバー (VSI)](/docs/vsi?topic=virtual-servers-getting-started-with-virtual-servers) のどれであっても、それに合わせてこれらはカスタマイズされています。

{{site.data.keyword.cloud_notm}} 開発者ダッシュボードから作成されたツールチェーンはすべて、自動デプロイメント用に構成されています。
{: note}

1. **「アプリの詳細」**ページで**「継続的デリバリーの構成 (Configure continuous delivery)」**をクリックします。
2. デプロイメント・ターゲットを選択します。 選択した方式の説明に従って、デプロイメント・ターゲットをセットアップします。
  * **[IBM Kubernetes Service](/docs/apps/deploying?topic=creating-apps-containers-kube) にデプロイします**。 このオプションは、高可用性のアプリケーション・コンテナーをデプロイして管理するためのワーカー・ノードというホスト・クラスターを作成します。 クラスターを作成したり、既存のクラスターにデプロイしたりすることができます。
  * **Cloud Foundry にデプロイ**します。 このオプションはクラウド・ネイティブなアプリをデプロイします。基礎にあるインフラストラクチャーを管理する必要はありません。 ご使用のアカウントに {{site.data.keyword.cfee_full_notm}} へのアクセス権限がある場合、デプロイヤー・タイプとして、**[パブリック・クラウド](/docs/cloud-foundry-public?topic=cloud-foundry-public-about-cf)**または**[エンタープライズ環境](/docs/cloud-foundry-public?topic=cloud-foundry-public-cfee)**のいずれかを選択できます。エンタープライズ環境を使用すると、自社専用に Cloud Foundry アプリケーションをホスティングする隔離された環境を作成して管理できます。
  * **[仮想サーバー](/docs/apps?topic=creating-apps-vsi-deploy)にデプロイします**。 このオプションによって、仮想サーバー・インスタンスがプロビジョンされ、アプリを含むイメージがロードされ、DevOps ツールチェーンが作成され、最初のデプロイメント・サイクルが開始されます。

## ステップ 5. アプリのビルドおよびローカルでの実行
{: #build-run-microservice}

最後のステップでアプリをクラウドにデプロイしたときに、ツールチェーンが作成されています。 ツールチェーンは、アプリ用の Git リポジトリーを作成します。このリポジトリーで、コードを見つけることができます。 リポジトリーにアクセスするには、次のステップに従います。 アプリをクラウドにプッシュする前に、アプリをテスト用にローカルでビルドすることができます。

1. **「アプリの詳細」**ページで**「コードのダウンロード (Download code)」**または**「リポジトリーの複製 (Clone your repo)」**をクリックして、コードをローカルに処理します。
2. 統合開発環境にアプリをインポートします。
3. コードを変更します。
4. パーソナル・アクセス・トークンを追加して、[Git 認証](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-git_working#git_authentication)をセットアップします。
5. {{site.data.keyword.cloud_notm}} コマンド・ライン・インターフェースにログインします。 組織でフェデレーテッド・ログインを使用している場合は、`-sso` オプションを使用します。

  ```bash
  ibmcloud login -sso
  ```
  {: pre}

6. 組織とスペースのターゲットを設定します。

  ```bash
  ibmcloud target --cf
  ```
  {: pre}

7.  資格情報を取得します。

  ```bash
  ibmcloud dev get-credentials
  ```
  {: pre}

8. Docker が実行中であることを確認して、ディレクトリーからローカル開発コンテナーでアプリをビルドします。

  ```bash
  ibmcloud dev build
  ```
  {: pre}

9. ローカル開発コンテナーでアプリを実行します。

  ```bash
  ibmcloud dev run
  ```
  {: pre}

10.  ご使用のブラウザーで `http://localhost:3000` を開きます。 ご使用のポート番号は、選択したランタイムによって異なる可能性があります。

## ステップ 6. アプリのデプロイ
{: #deploy-microservice}

### ツールチェーンを使用したデプロイ
{: #deploy-microservice-toolchain}

アプリはいくつかの方法で {{site.data.keyword.cloud_notm}} にデプロイできますが、DevOps ツールチェーンが、実動アプリをデプロイする場合に最適な方法です。 DevOps ツールチェーンを使用すると、多数の環境へのデプロイメントを簡単に自動化して、成長するアプリの管理に役立つモニタリング、ロギング、およびアラートの各サービスを素早く追加することができます。

正しく構成されたツールチェーンを使用すると、リポジトリー内のマスター・ブランチへのマージが行われるたびに、ビルドとデプロイのサイクルが自動的に開始されます。 {{site.data.keyword.cloud_notm}} 開発者ダッシュボードから作成されたツールチェーンはすべて、自動デプロイメント用に構成されています。

DevOps ツールチェーンからアプリを手動でデプロイすることもできます。

1. **「アプリの詳細」**ページで**「ツールチェーンの表示」**をクリックします。

2. **「Delivery Pipeline」**をクリックします。ここで、ビルドの開始、デプロイメントの管理、およびログと履歴の表示を行うことができます。

### {{site.data.keyword.dev_cli_short}} を使用したデプロイ
{: #deploy-microservice-cli}

アプリを Cloud Foundry にデプロイするには、以下のコマンドを入力します。

```
ibmcloud dev deploy
```
{: pre}

アプリを Kubernetes クラスターにデプロイするには、以下のコマンドを入力します。

```
ibmcloud dev deploy --target <container>
```
{: pre}

## ステップ 7. アプリが実行中であることの確認
{: #verify-microservice}

アプリのデプロイ後に、Delivery Pipeline またはコマンド・ラインにアプリの URLが示されます。

1. DevOps ツールチェーンから、**「Delivery Pipeline」**をクリックし、**「デプロイ・ステージ」**を選択します。
2. **「ログおよび履歴の表示」**をクリックします。
3. ログ・ファイルで、アプリケーション URL を見つけます。

    ログ・ファイルの末尾で `urls` または `view` という語を探します。 例えば、`urls: my-app-devhost.mybluemix.net` または `View the application health at: http://<ipaddress>:<port>/health` のような行がログ・ファイル内で見つかります。

4. ご使用のブラウザーでその URL にアクセスします。 アプリが実行されている場合は、`Congratulations` または `{"status":"UP"}` を含むメッセージが表示されます。

コマンド・ラインを使用している場合は、[`ibmcloud dev view`](/docs/cli/idt?topic=cloud-cli-idt-cli#view) コマンドを実行して、アプリの URL を表示します。 次に、ブラウザーでその URL にアクセスします。
