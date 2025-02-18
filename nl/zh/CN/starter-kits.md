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

# 什么是入门模板工具包？
{: #starter-kits}

入门模板工具包是一种生产就绪型模式，可与一组服务集成，用于生成可直接部署到 DevOps 管道和 Kubernetes 集群的生产就绪型资产。
入门模板工具包非常适合按您选择的语言来动态组合框架生产应用程序，以准备好进行云部署。
{:shortdesc}

入门模板工具包中包含描述工具包的功能和用途的元数据。此外，还包含用于告知 {{site.data.keyword.cloud_notm}} 要生成哪些内容的相关信息。输出是现成的生产就绪型内容，可基于 {{site.data.keyword.cloud_notm}} 最佳实践进行反复迭代以进一步加以改进。入门模板工具包的内容不像演示那么复杂，但也不像片段或样本那么简单。应用程序是根据开发者的需求动态创建的。

每个入门模板工具包中都具有针对特定用例的语言、框架和模式。您可以复用代码，而不用重新创建代码。
如果入门模板工具包需要特定服务，可以通过自动供应的服务，在创建应用程序时自动创建这些服务的实例。

## 入门模板工具包与样本有何不同？
{: #compare}

入门模板工具包是生产就绪型的，专注于使用运行时（例如，Node.js 和 Express）来演示关键模式实现。在某些情况下，入门模板工具包会提供简单的用户体验来着重强调服务的集成。在另一些情况下，入门模板工具包表示对复杂用例的可定制实现。

片段是一些通常在 IDE 中显示的代码行。片段可帮助开发者与编程语言语法集成，或支持与定义的 API 集成。通常，演示的质量和精确度较高，并且会使用一系列服务和集成点。演示通常需要设置时间，并用于证明业务问题或演示平台功能。您可以将演示用于评估采用云的阶段。有时，这是生产代码中所包含的代码。样本是由特定特性、功能、服务或用户旅程组成的一个小型示例。您可以复用样本或者将其包含到生产应用程序中。样本通常用于展示技术功能，以及说明用于解决技术问题的可行方法。

## 可移植代码
{: #portable-code}

通过入门模板工具包创建应用程序会自动创建与运行时无关的统一格式代码。您可以将代码原封不动地部署到所选目标中，例如 Kubernetes 或 Cloud Foundry。

可移植代码包含适用于多个云环境的云支持代码。您可以生成遵循特定语言的最佳实践且特定于用例的代码。 

* 用例逻辑提供了特定用例核心功能的代码。例如，Watson Conversation 聊天机器人的代码或移动可视识别应用程序的代码。
* 语言组件是特定于为入门模板工具包所选择的编程语言的代码组件和文件。例如，node.js 程序员需要 package.json 文件进行依赖项管理，并且会自动创建此文件。
* 服务支持是让应用程序能够连接和使用所添加服务的代码。服务支持项的示例包括凭证管理、初始化代码和特定于服务的 SDK。
* 云支持是让应用程序能够在 {{site.data.keyword.cloud_notm}} 上运行的代码。例如，让应用程序能够在 {{site.data.keyword.cloud_notm}} Kubernetes 集群上运行的 Helm 图表。

您还可以通过单击应用程序的“应用程序详细信息”页面上的**下载代码**来查看应用程序代码。代码会下载为 `.zip` 文件，其中包含完整的应用程序代码结构。您可以使用 {{site.data.keyword.dev_cli_notm}} 解压缩该文件并在本地运行代码，或者将其添加到代码管理存储库中。

每个应用程序都有一个自述文件，其中包含应用程序的技术详细信息，以及当应用程序无法即装即用时所需的运行条件。
{: tip}
