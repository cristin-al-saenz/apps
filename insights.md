---

copyright:
  years: 2019
lastupdated: "2019-05-09"

keywords: developer tools, building apps, developer entry point, DevOps, toolchain, insights

subcollection: creating-apps

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}

# DevOps Insights
{: #insights-overview}

{{site.data.keyword.DRA_full}} is a cloud-based solution that provides comprehensive insights from continuous integration and continuous delivery tools to increase the speed, quality, and control of your applications. You can add the {{site.data.keyword.DRA_short}} tool integration to your DevOps toolchain.
{: shortdesc}

{{site.data.keyword.DRA_short}} collects and analyzes the results from unit tests, functional tests, and code coverage tools to determine whether your code meets predefined criteria at specified gates in your deployment process. If your code does not meet or exceed the criteria, the deployment is stopped to prevent risks from being released. You can use DevOps Insights as a safety net for your continuous delivery environment or as a way to implement and improve quality standards.

This tool integration is available only on the public {{site.data.keyword.cloud_notm}}. It is preconfigured and does not require any configuration parameters. You can't reconfigure this tool integration.
{: note}

To add the {{site.data.keyword.DRA_short}} tool integration to your DevOps toolchain, complete these steps:

1. [Create your app](/docs/apps?topic=creating-apps-tutorial-getting-started#create-getting-started).
2. On App details page, click **Configure continuous delivery** and follow the steps for configuring a DevOps toolchain. The steps vary, depending on which deployment target that you select.
3. When you see the "Configured" message on the App details page, click **View toolchain**.
4. On the toolchain's Overview page, click **Add a Tool**.
5. In the Tool Integrations section, select **{{site.data.keyword.DRA_short}}**.
6. Click **Create Integration**. {{site.data.keyword.DRA_short}} is added to your toolchain.
7. Click the **{{site.data.keyword.DRA_short}}** tile to open the Overview page where you can start using **{{site.data.keyword.DRA_short}}**.

For more information, see the [{{site.data.keyword.DRA_short}} Getting started tutorial](/docs/services/DevOpsInsights?topic=DevOpsInsights-getting-started).
