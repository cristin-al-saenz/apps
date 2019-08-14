---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-18"

keywords: apps, Mendix, starter kit, developer tools, Mendix app

subcollection: creating-apps

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 使用 Mendix 创建应用程序
{: #create-mendix}

Mendix 是一种低代码开发环境和工具集，可以帮助您使用较少的开发资源更快地交付在 {{site.data.keyword.cloud}} 上运行的多设备应用程序。当您选择 Mendix 低代码入门模板工具包后，系统会指导您在 Mendix Platform 上设置帐户，启动项目，并从 Cloud Foundry 或 Kubernetes 集群中选择部署目标。
{: shortdesc}

## 选择入门模板工具包
{: #starterkit-mendix}

1. 在 [{{site.data.keyword.cloud_notm}} App Service 仪表板 ](https://{DomainName}/developer/appservice/dashboard){: new_window} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标") 中，单击**入门**。
2. 从以下类别中选择一个 Mendix 低代码入门模板工具包：
  * [移动 ](https://{DomainName}/developer/appservice/starter-kits/mendix-mobile-app){: new_window} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")
  * [Watson Web 或移动应用程序 ](https://{DomainName}/developer/appservice/starter-kits/mendix-web-or-mobile-app-with-watson){: new_window} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")
  * [Web 应用程序 ](https://{DomainName}/developer/appservice/starter-kits/mendix-web-app){: new_window} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")
3. 单击**创建应用程序**。
4. 在**应用程序详细信息**页面上，对应用程序命名，并可选择性提供标记来对应用程序分类。有关更多信息，请参阅[使用标记](/docs/resources?topic=resources-tag)。
5. 单击**创建**。


## 授权 IBM 在 Mendix 上创建项目并链接帐户
{: #link-mendix-account}

如果您尚未将 Mendix 与 {{site.data.keyword.cloud_notm}} 配合使用，系统会引导您前往 Mendix Platform 进行注册并授权 {{site.data.keyword.cloud_notm}} 代表您在 Mendix Platform 上创建新项目。此项目会链接到 {{site.data.keyword.cloud_notm}}，因此部署会自动定向到 {{site.data.keyword.cloud_notm}}。

1. 如果您看到以下消息：“要完成应用程序的创建，需要使用 Mendix 用户帐户。要立即链接您的帐户吗？”，请单击**链接帐户**。
2. 在 Mendix 确认页面上，选择**我同意 Mendix 的隐私策略和条款**，然后单击**确认**。
3. 出现提示时，提供您的电子邮件地址、密码和国家/地区，然后单击**创建**。
4. 在**授权访问您的 Mendix 帐户**页面上，单击**授权**。

授权完成后，您的浏览器将返回到您正在创建的 Mendix 应用程序。此时将显示**选择部署目标**页面。

## 选择 Mendix 应用程序的部署目标
{: #select-deployment}

1. 在**选择部署目标**页面上，选择 Cloud Foundry 或在 {{site.data.keyword.cloud_notm}} 上运行的其中一个 Kubernetes 集群。如果您的帐户有权访问 {{site.data.keyword.cfee_full_notm}}，那么可以选择 Cloud Foundry 部署程序类型**[公共云](/docs/cloud-foundry-public?topic=cloud-foundry-public-about-cf)**或**[企业环境](/docs/cloud-foundry-public?topic=cloud-foundry-public-cfee)**，可使用这些类型来创建和管理隔离的环境，以用于专门为您的企业托管 Cloud Foundry 应用程序。
2. 可选。如果您没有 Kubernetes 集群，可以立即创建一个。
3. 在**配置工具链**页面上，选择您的区域和资源组，然后单击**创建**。

这将创建 DevOps 工具链。该工具链会在 {{site.data.keyword.cloud_notm}} 环境中的 Mendix Platform 内集成 Mendix 项目。系统会将缺省应用程序部署到部署目标中，以便您可以在完成 DevOps 工具链后验证应用程序是否已成功部署。

Mendix Cloud Foundry 部署需要 PostGRES 数据库服务，但该服务没有轻量层。如果您想要使用轻量帐户评估 Mendix 入门模板工具包，可以部署到试用版 Kubernetes 集群。
{: tip}

如果选择了 Kubernetes 集群来进行部署，请参阅 [Mendix Kubernetes 教程](/docs/apps/tutorials?topic=creating-apps-deploy-mendix-kube)来了解如何配置集群以便用于生产环境。


## 继续 Mendix 部署和部署生命周期
{: #dev-lifecycle-mendix}

Mendix 是一个低代码编写环境。开发生命周期要求您在 Mendix Modeler 桌面应用程序中打开项目。

1. 在 {{site.data.keyword.cloud_notm}} 应用程序中，单击**在 Mendix 上编辑**。
2. 在 Mendix Web 门户网站中，单击**在 Desktop Modeler 中编辑**。这会在 Desktop Modeler 中打开 Mendix 应用程序。
3. 编辑 Mendix 应用程序，并保存更改。
4. 使用 Mendix Desktop Modeler 应用程序的**运行**菜单，选择**运行**选项。这会创建部署软件包并将其上传到 Mendix。当部署软件包创建完成后，您可以将应用程序部署到 {{site.data.keyword.cloud_notm}}。
5. 要部署 Mendix 应用程序，请返回到 {{site.data.keyword.cloud_notm}} 上的**应用程序详细信息**页面，然后单击**部署**。此操作会启动应用程序的 DevOps 工具链，该工具链会从 Mendix 中拉出最新部署并将其部署到目标环境。当部署完成后，最新版本的应用程序会自动启动并可供使用。

单击 {{site.data.keyword.cloud_notm}} 上**应用程序详细信息**页面中的**配置持续交付**后，所有 Mendix 应用程序都将部署到 {{site.data.keyword.cloud_notm}} 上。不要通过 IBM DevOps 界面手动调用 Mendix 工具链。通过 DevOps 界面手动启动工具链可能会导致部署失败，因为缺少对 Mendix 部署至关重要的必需元数据。可能会在 DevOps 工具链启动期间发生问题，或在部署的应用程序中发生错误，具体取决于应用程序的状态。如果在手动启动工具链时遇到问题，可以复原应用程序部署，方法是单击 {{site.data.keyword.cloud_notm}} 上**应用程序详细信息**页面中的**配置持续交付**。此操作会触发 Mendix 应用程序的完整 DevOps 流程，其中包含必需的元数据。
{: tip}

## 后续步骤 
{: #next-steps-mendix}

要将应用程序部署到 {{site.data.keyword.containerlong_notm}}，请针对生产部署配置您的应用程序。有关更多信息，请参阅 [Mendix Kubernetes 教程](/docs/apps/tutorials?topic=creating-apps-deploy-mendix-kube)。 
