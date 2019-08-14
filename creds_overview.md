---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-04"

keywords: apps, credentials, service, add service credentials, environment, deployment

subcollection: creating-apps

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}

# Manually adding service credentials to your deployment environment
{: #credentials_overview}

You want your application logic to acquire sensitive service credentials, such as database API keys or passwords, from the environment in which your app runs. That way, you don't have to keep credentials in your source code repository.
{: shortdesc}

If you create an app by using a starter kit, the environment is prepared for you automatically. When you connect a service to your starter kit before you deploy your app, the service credentials are automatically added to your environment.

You must manually add the service credentials to your deployment environment in either of the following scenarios:

 * You bring your own code.
 * You add a service to a starter kit-based app after the app is deployed.

The process for adding the service credentials depends on your deployment target and your programming language. For more information about configuring service credentials for your deployment target, see the documentation that is specific to your hosting environment:

  * [{{site.data.keyword.containerlong}}](/docs/containers?topic=containers-service-binding#adding_app)
  * Cloud Foundry Public or {{site.data.keyword.cfee_full}}
  * Virtual server instance (local docker container)

Many languages and frameworks provide standard libraries for both app-specific and environment-specific configurations. For more information, see the following programming guides:

* [Java: Working with service credentials](/docs/java?topic=cloud-native-configuration)
* [Configuring the Node.js environment](/docs/node?topic=nodejs-configure-nodejs)
* [Configuring the Spring environment](/docs/java?topic=java-spring-configuration)
* [Configuring the Swift environment](/docs/swift?topic=swift-configuration)
* [Configuring the Go environment](/docs/go?topic=go-configure-go-env)
