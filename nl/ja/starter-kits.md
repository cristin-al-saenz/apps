---

copyright:
  years: 2019
lastupdated: "2019-06-03"

keywords: developer tools, building apps, developer entry point, get started coding, starter kit

subcollection: creating-apps

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# スターター・キットとは何ですか?
{: #starter-kits}

スターター・キットは、実動準備完了のパターンであり、DevOps パイプラインおよび Kubernetes クラスターに直接デプロイできる実動準備完了の資産を生成するために一連のサービスと統合できます。 スターター・キットを使用すると、ユーザーが選択した言語で、クラウドへのデプロイ準備ができたスケルトン実動アプリケーションを動的にアセンブルできます。 
{:shortdesc}

スターター・キットには、キットの内容と機能を記述するメタデータが含まれています。 生成する内容を {{site.data.keyword.cloud_notm}} に示す情報も含まれています。 出力は、実動準備完了ですぐに使用可能であり、{{site.data.keyword.cloud_notm}} のベスト・プラクティスに基づいて、反復によりさらなる機能拡張を行うことができます。 スターター・キットの内容は、デモンストレーションほど複雑ではなく、スニペットやサンプルほど単純なものではありません。 アプリは開発者の要件に基づいて動的に作成されます。

各スターター・キットには、言語、フレームワーク、および特定のユース・ケース用のパターンが含まれています。 ユーザーは、コードを作り直すのではなく、再利用できます。 スターター・キットで特定のサービスが必要な場合は、自動的にプロビジョンされたサービスを使用することにより、アプリの作成時にこれらのサービスのインスタンスが自動的に作成されます。

## スターター・キットとサンプルの違いとは?
{: #compare}

スターター・キットは、実動準備が完了しており、(例えば、Node.js および Express など) ランタイムを使用したキー・パターンの実装を示すことに重点を置いています。 場合によっては、スターター・キットは、サービスの統合を強調するためのシンプルなユーザー・エクスペリエンスを提供します。 スターター・キットが、高度なユース・ケースのカスタマイズ可能な実装を表している場合もあります。

スニペットは、IDE でよく提供される数行のコードです。 スニペットにより、開発者は、あるプログラミング言語の構文と統合したり、ある定義済みの API との統合をサポートしたりすることができます。 デモンストレーションは、一般的に品質および精度が高く、さまざまなサービスおよびインテグレーション・ポイントを使用します。 多くの場合、セットアップ時間が必要になり、ビジネスの問題の証明またはプラットフォーム・フィーチャーのデモンストレーションに使用します。 クラウド採用のステージを評価するために使用することができます。 そのコードが実動コードに含まれることがあります。 サンプルは、特定のフィーチャー、機能、サービス、またはユーザー・ジャーニーの小さな例です。 サンプルを再利用したり、実動アプリに組み込んだりすることができます。 通常、技術的な機能および技術的な問題を解決するためのアプローチの候補を示すために使用します。

## 移植可能コード
{: #portable-code}

スターター・キットからアプリを作成すると、一貫性のあるフォーマットで、ランタイムに依存しないコードが自動的に作成されます。 コードは、例えば Kubernetes または Cloud Foundry など、任意のターゲットに変更無しでデプロイすることができます。

移植可能コードには、複数のクラウド環境用のクラウド・イネーブルメント・コードが含まれています。特定の言語のベスト・プラクティスに従った、ユース・ケースに固有のコードコードを生成できます。 

* ユース・ケース・ロジックは、特定のユース・ケースのコア・ファンクションの機能を提供します。 例えば、Watson Conversation チャットボット用のコードや、モバイル視覚認識アプリ用のコードなどです。
* 言語コンポーネントは、スターター・キットで選択したプログラミング言語に固有のコード・コンポーネントおよびファイルです。 例えば、node.js のプログラマーは、依存関係管理のために package.json ファイルを必要としますが、このファイルは自動的に作成されます。
* サービス・イネーブルメントは、追加したサービスにアプリを接続し、サービスを使用できるようにするためのコードです。 サービス・イネーブルメント項目の例は、資格情報管理、初期化コード、サービス固有の SDK などです。
* クラウド・イネーブルメントは、アプリを {{site.data.keyword.cloud_notm}} 上で実行できるようにするコードです。 例えば、Helm チャートは、{{site.data.keyword.cloud_notm}} Kubernetes クラスターでアプリを実行できるようにします。

アプリの「アプリの詳細」ページで**「コードのダウンロード (Download code)」**をクリックすると、アプリ・コードを表示できます。 コードは、完全なアプリ・コード構成を含む `.zip` ファイルとしてダウンロードされます。 {{site.data.keyword.dev_cli_notm}} を使用して、ファイルを抽出し、コードをローカルで実行することができます。また、コード管理リポジトリーに追加することもできます。

各アプリには、アプリの技術的な詳細およびアプリがすぐに使用可能ではない場合にアプリを実行するために必要な手順を記載した README ファイルが含まれています。
{: tip}
