---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-15"

keywords: apps, services, add service, application

subcollection: creating-apps

---

{: new_window: target="_blank"}
{:shortdesc: .shortdesc}
{: codeblock: .codeblock}
{:note: .note}

# アプリへのサービスの追加
{: #add-resource}

{{site.data.keyword.cloud}} {{site.data.keyword.dev_console}} を使用してアプリを作成した場合、アプリの詳細ページからサービスを追加することができます。 しかし、アプリのコンテキスト外部で、{{site.data.keyword.cloud_notm}} カタログからリソースを直接プロビジョンすることもできます。
{: shortdesc}

サービスのインスタンスを要求して、これをアプリとは無関係に使用することも、アプリの詳細ページからサービス・インスタンスをアプリに追加することもできます。 特定のタイプのサービスを {{site.data.keyword.cloud_notm}} カタログから直接プロビジョンできます。

## サービスの検出
{: #discover-resources}

以下の方法で、{{site.data.keyword.cloud_notm}} で使用可能なサービスをすべて表示できます。

* {{site.data.keyword.cloud_notm}} コンソールから。 {{site.data.keyword.cloud_notm}} カタログを表示します。
* コマンド・ラインから。 `ibmcloud service offerings` コマンドを使用します。
* ご使用のアプリケーションから。 [GET /v2/services Services API ](http://apidocs.cloudfoundry.org/197/services/list_all_services.html){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を使用します。

アプリケーションを開発するときに、必要なサービスを選択できます。 選択されたサービスは、{{site.data.keyword.cloud_notm}} によってプロビジョンされます。 サービスのタイプによってプロビジョンのプロセスが異なる場合があります。 例えば、データベース・サービスはデータベースを作成し、モバイル・アプリケーションのプッシュ通知サービスは構成情報を生成します。

{{site.data.keyword.cloud_notm}} は、サービス・インスタンスを使用してサービスのリソースをアプリケーションに提供します。 サービス・インスタンスは Web アプリケーション間で共有できます。

他の地域でホストされているサービスがその地域内で使用可能である場合、それらのサービスを使用することもできます。 これらのサービスはインターネットからアクセスできる必要があり、さらに API エンドポイントを持つ必要があります。 {{site.data.keyword.cloud_notm}} サービスを利用するために外部アプリケーションやサード・パーティー・ツールをコード化するのと同様に、これらのサービスを利用するにはお使いのアプリケーションを手動でコード化する必要があります。 詳しくは、[外部アプリへのサービスの接続](/docs/resources?topic=resources-externalapp)を参照してください。

## 新規サービス・インスタンスの要求
{: #request-instance}

新規サービス・インスタンスを要求するには、{{site.data.keyword.cloud_notm}} ユーザー・インターフェースまたは {{site.data.keyword.cloud_notm}} コマンド・ライン・インターフェースを使用する必要があります。

サービス名を指定するときは、英字と数字のみを使用してください。英字と数字以外を使用すると、予測できない結果が生じる可能性があります。
{: note}

{{site.data.keyword.cloud_notm}} ユーザー・インターフェースを使用してサービス・インスタンスを要求する場合、以下のステップを実行します。

1. {{site.data.keyword.cloud_notm}} カタログで、追加するサービスのタイルをクリックします。 サービス詳細ページが開きます。

2. **「サービス名」**フィールドに名前を入力します。 デフォルト名が表示されます。 このフィールドで名前を変更できますし、変更せずにそのままにすることもできます。

3. 追加のフィールドまたは選択に入力してから、**「作成」**をクリックします。

{{site.data.keyword.cloud_notm}} コマンド・ライン・インターフェースを使用してサービス・インスタンスを要求する場合、アプリをローカルにダウンロードし、コマンド・ラインを開いて、アプリ・ディレクトリーに移動します。

1. 次のコマンドを実行して、サービスをアプリに追加します。 ご使用のアカウントで既に使用可能になっている既存のサービスを選択することも、新規サービスを追加することもできます。

  ```bash
  ibmcloud dev edit
  ```
  {: pre}

2. プロンプトに従って、リソース・グループを選択し、新しいデータ関連サービスを作成してアプリケーションに接続します (Cloudant など)。 サービスの地域とプランを選択する必要がある場合があります。
3. サービスが作成されるときに、サービスをアプリケーションに統合するのに役立つよう、資格情報を含め、いくつかのファイルがアプリケーション・ディレクトリーに追加されます。 任意のファイルを手動でマージすることも、今はこのステップをスキップすることもできます。

サービス・インスタンスは、同じスペースまたは組織内のアプリ・インスタンスにのみバインド可能です。ただし、外部アプリと同じように他のスペースまたは組織からサービス・インスタンスを使用できます。 バインディングを作成する代わりに、資格情報を使用してアプリ・インスタンスを直接構成します。 外部アプリが {{site.data.keyword.cloud_notm}} サービスを使用する方法について詳しくは、[『外部アプリが {{site.data.keyword.cloud_notm}} サービスを使用できるようにする』](/docs/resources?topic=resources-externalapp#externalapp)を参照してください。

## アプリケーションの構成
{: #configure-app}

ご使用のアプリケーションにサービス・インスタンスをバインドした後、そのサービスと対話するようアプリケーションを構成する必要があります。

各サービスは、アプリケーションと通信するために別のメカニズムを必要とする場合もあります。 これらのメカニズムについては、アプリケーションを開発するときに、サービス定義の一部として情報が文書化されます。 一貫性のために、メカニズムは、アプリケーションがサービスと対話するために必要です。

* データベース・サービスと対話するには、ユーザー ID、パスワード、およびアプリケーションのアクセス URI など、{{site.data.keyword.cloud_notm}} が提供する情報を使用します。
* モバイル・バックエンド・サービスと対話するには、アプリケーション ID (アプリ ID)、クライアント固有のセキュリティー情報、およびアプリケーションのアクセス URI など、{{site.data.keyword.cloud_notm}} が提供する情報を使用します。 アプリケーション開発者の名前やアプリケーションを使用するユーザーなどのコンテキスト情報を一連のサービスで共有できるように、モバイル・サービスは多くの場合、互いのコンテキストで機能します。
* Web アプリケーションと、またはモバイル・アプリケーションのサーバー・サイドのクラウド・コードと対話するには、アプリケーションの *VCAP_SERVICES* 環境変数内のランタイム資格情報など、{{site.data.keyword.cloud_notm}} が提供する情報を使用します。 *VCAP_SERVICES* 環境変数の値は、JSON オブジェクトの直列化です。 変数には、アプリケーションにバインドされているサービスと対話するために必要なランタイム・データが含まれます。 データのフォーマットは、サービスごとに異なります。 期待される情報と、情報の各部分を解釈する方法について、サービスの文書を読み取る必要が生じる場合もあります。

アプリケーションにバインドしたサービスが異常終了すると、そのアプリケーションが稼動を停止したり、エラーを起こしたりする場合があります。 これらの問題からリカバリーするために {{site.data.keyword.cloud_notm}} がアプリケーションを自動的に再始動することはありません。 障害、例外、および接続失敗を識別してリカバリーするようにアプリケーションをコーディングすることを検討してください。 詳しくは、[アプリの非自動再始動](/docs/apps/troubleshoot?topic=creating-apps-managingapps#ts_apps_not_auto_restarted)を参照してください。

## 複数の {{site.data.keyword.cloud_notm}} デプロイメント環境でのサービスへのアクセス
{: #migrate_instance}

{{site.data.keyword.cloud_notm}} は多くのデプロイメント・オプションを提供します。ユーザーは、ある環境で実行中のサービスに別の環境からアクセスすることができます。 例えば、Cloud Foundry で実行されているサービスに、Kubernetes クラスターで実行されているアプリケーションからアクセスすることができます。

### 例: Kubernetes ポッドからの Cloud Foundry サービスへのアクセス

Kubernetes クラスター内のポッドから Cloud Foundry サービスにアクセスするには、サービスの資格情報を Kubernetes シークレットに保管するために、サービスをクラスターにバインドする必要があります。 次に、この情報をアプリで利用できるようにします。 
{: shortdesc}

Kubernetes シークレットに保管されているサービス資格情報は、デフォルトでは、base64 エンコードされ暗号化されて etcd に保管されます。 

**重要**: デプロイメント YAML ファイルの中で、サービス資格情報を直接参照したり公開したりしないでください。 デプロイメント YAML ファイルは、機密データを保持するように設計されておらず、デフォルトではサービス資格情報を暗号化しません。 この情報を適切に保存してアクセスするには、Kubernetes シークレットを使用する必要があります。 

1. [サービスをクラスターにバインドします](/docs/containers?topic=containers-integrations#adding_cluster)。 
2. アプリ・ポッドからサービス資格情報にアクセスするには、次のいずれかのオプションを選択します。 
   - Secret をボリュームとしてポッドにマウントする
   - 環境変数で Secret を参照する

## ユーザー提供のサービス・インスタンスの作成
{: #user_provide_services}

{{site.data.keyword.cloud_notm}} の外部で管理されているサービスが存在する場合もあります。 そうした外部サービスにインターネットからアクセスするための資格情報を持っていれば、{{site.data.keyword.cloud_notm}} のユーザー提供サービス・インスタンスを作成することによって、外部サービスを表現し、そのサービスと通信することができます。

ユーザー提供のサービス・インスタンスを作成し、それをアプリケーションにバインドするには、以下のステップを実行します。

1. `ibmcloud service user-provided-create` コマンドを使用して、ユーザー提供のサービス・インスタンスを作成します。
    * 一般的なユーザー提供のサービス・インスタンスを作成するには、**-p** オプションを使用し、パラメーター名をコンマで区切ります。 `ibmcloud` コマンド・ライン・インターフェースはその後、各パラメーターについて順にプロンプトを出します。 以下に例を示します。
        ```
        ibmcloud service user-provided-create testups1 -p "host, port, dbname, username, password"
        host> pubsub01.example.com
        port> 1234
        dbname> sampledb01
        username> pubsubuser
        password> p@$$w0rd
        Creating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * サード・パーティーのログ管理ソフトウェアに情報をドレーンするサービス・インスタンスを作成するには、`-l` オプションを使用します。 サード・パーティーのログ管理ソフトウェアが提供する宛先を指定します。 例えば次のようにします。

        ```
        ibmcloud service user-provided-create testups2 -l syslog://example.com
        Creating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

    ユーザー提供のサービス・インスタンスの 1 つ以上のパラメーターを更新する場合は、`ibmcloud service user-provided-update` コマンドを使用します。

    * 一般的なユーザー提供のサービス・インスタンスを更新するには、**-p** オプションを使用して、パラメーターのキーと値を JSON オブジェクトで指定します。 例えば次のようにします。

        ```
        ibmcloud service user-provided-update testups1 -p "{\"username\":\"pubsubuser2\",\"password\":\"p@$$w0rd2\"}"
        Updating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * サード・パーティーのログ管理ソフトウェアに情報をドレーンするサービス・インスタンスを作成するには、`-l` オプションを使用します。 例えば次のようにします。

        ```
        ibmcloud service user-provided-create testups2 -l syslog://example2.com
        Updating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

2. `ibmcloud service bind` コマンドを使用して、サービス・インスタンスをアプリケーションにバインドします。 例えば次のようにします。

	```
	ibmcloud service bind myapp testups1
	Binding service testups1 to app myapp in org my-org / space dev as user@sample.com...
	OK
	```

外部サービスを使用するようアプリケーションを構成できるようになりました。 サービスと対話するようアプリケーションを構成する方法については、[「サービスと対話するようアプリケーションを構成する」](/docs/apps?topic=creating-apps-add-resource#configure-app)を参照してください。
