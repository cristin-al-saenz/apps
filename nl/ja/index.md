---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-15"

keywords: apps, create apps, add resources, deploy apps

subcollection: creating-apps

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 入門チュートリアル
{: #tutorial-getting-started}

{{site.data.keyword.cloud}} で企業向けのモバイル・アプリケーションおよび Web アプリケーションを作成でき、{{site.data.keyword.cloud_notm}} でホストされているクラウド拡張機能を利用できます。 開始する方法にはいくつかあります。 プロセスを管理してくれるスターター・キットを使用してアプリを作成するか、または、何が必要かが分かっている場合は、必要なリソースと共に最初からアプリを作成するか、既存のリポジトリーを使用して独自のコードを持ち込みます。
{: shortdesc}

## 始める前に
{: #prereqs-getting-started}

アプリの作成は、{{site.data.keyword.cloud_notm}} コンソールまたはコマンド・ライン・インターフェース (CLI) を使用して行うことができます。 CLI を使用する場合は、[インストール手順](/docs/cli?topic=cloud-cli-ibmcloud-cli)を参照してください。

## ステップ 1. アプリの作成
{: #create-getting-started}

以下のエントリー・ポイントのいずれかを選択して、アプリを作成します。
* [スターター・キット](/docs/apps/tutorials?topic=creating-apps-tutorial-starterkit): ユーザーのためにプロセスを管理してくれるアプリ・サービス・スターター・キットのいずれかを選択してアプリを作成します。
* [カスタム](/docs/apps/tutorials?topic=creating-apps-tutorial-scratch): 何が必要なのかが分かっている場合、ブランクのスターター・キットを使用して、必要なリソースと共にカスタム・アプリを最初から作成します。
* [独自のコードの持ち込み](/docs/apps/tutorials?topic=creating-apps-tutorial-byoc): 既存の独自のコンテンツ・リポジトリーにリンクすることによって、独自のコードを持ち込みます。 アプリと Docker イメージは同じリポジトリー内に配置する必要があります。
* [CLI](/docs/apps?topic=creating-apps-create-deploy-app-cli): CLI および開発者ツールを使用して、カスタム・アプリまたはスターター・キット・アプリを作成してデプロイします。
* [コード・パターン](/docs/apps/tutorials?topic=creating-apps-tutorial-codepattern): アプリを作成するためのベースとして IBM 開発者コード・パターンを使用します。
* [{{site.data.keyword.cloud_notm}} カタログ ](https://cloud.ibm.com/catalog){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン"): カタログを参照または検索して、今日作成して使用を開始できるアプリおよびサービスを見つけます。

## ステップ 2. リソースの追加
{: #resources-getting-started}

スターター・キットを使用してアプリを作成する場合、サービスは自動的に作成されます。 コンソールで**「アプリの詳細」**ページの**「サービスの追加」**をクリックすることによって、さらにサービスをアプリに関連付けることができます。

CLI を使用してサービスを追加するには、サービスをアプリに追加するために次のコマンドを実行します。 ご使用のアカウントで既に使用可能になっている既存のサービスを選択することも、新規サービスを追加することもできます。 
```
ibmcloud dev edit
```
{: codeblock}

詳しくは、[アプリへのサービスの追加](/docs/apps?topic=creating-apps-add-resource)を参照してください。

## ステップ 3. アプリのデプロイ
{: #deploy-getting-started}

コンソールまたはコマンド・ラインを使用してアプリをデプロイできます。

### コンソールの使用
{: #console-getting-started}

コンソールを使用してアプリをデプロイするには、以下の手順を実行します。

1. **「アプリの詳細」**ページで**「継続的デリバリーの構成 (Configure continuous delivery)」**をクリックします。
2. デプロイメント・ターゲットを選択し、ツールチェーン設定を選択してから**「作成」**をクリックします。{{site.data.keyword.cloud_notm}} は、Git リポジトリーと継続的デリバリー・パイプラインを備えたオープン・ツールチェーンを自動的に作成します。
3. 新しいツールチェーンのパイプライン・ステージを開いて、ビルドとデプロイメントのプロセスを表示すると、数分後に新しいアプリが表示されます。

詳しくは、『アプリのデプロイと統合』セクションで、さまざまなデプロイメントについてのトピックの目次を参照してください。

### コマンド・ラインの使用
{: #cli-getting-started}

コマンド・ラインを使用してアプリをデプロイするには、`ibmcloud dev deploy` コマンドを実行します。 詳しくは、[CLI を使用したアプリの作成およびデプロイ](/docs/apps?topic=creating-apps-create-deploy-app-cli)を参照してください。

これで、反復型開発と継続的デリバリーのための設定ができました。
