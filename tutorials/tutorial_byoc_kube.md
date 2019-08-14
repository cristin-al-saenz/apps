---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-05"

keywords: apps, deploy, deploy to kubernetes, cluster, delivery pipeline, toolchain, kube, deployment, custom code, kubernetes

subcollection: creating-apps

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Deploying your own code to a Kubernetes cluster
{: #tutorial-byoc-kube}

Learn how to create an application in {{site.data.keyword.cloud}} by using your existing app repository. You can connect your existing DevOps toolchain or create one, and continuously deliver an app to a secure container in a Kubernetes cluster. This tutorial helps you set up a continuous integration DevOps pipeline so that the change is automatically built and propagated all the way to your deployed app in the Kubernetes cluster.
{: shortdesc}

When you already have a source code repository with a code base for a working backend app, {{site.data.keyword.cloud_notm}} helps you organize this asset into an aggregate view of all the assets that make up the breadth of your whole product. {{site.data.keyword.cloud_notm}} gets you up and running on a scalable DevOps workflow when you use the DevOps toolchain feature. This tutorial helps the experienced developer or DevOps engineer acquire and configure a target {{site.data.keyword.containerlong}} and configure and run a DevOps toolchain, all under the guidance of cloud best practices.

A _cluster_ is a set of resources, worker nodes, networks, and storage devices that keep apps highly available. After you create your cluster, you can deploy your apps in containers.
{: tip}

## Before you begin
{: #prereqs-byoc-kube}

* [Create an app from your own code repository](/docs/apps/tutorials?topic=creating-apps-tutorial-byoc).
* From the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}){: new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon"), click the **Menu** icon ![Menu icon](../../icons/icon_hamburger.svg), and select **Containers** to [configure a Kubernetes cluster](/docs/containers?topic=containers-getting-started).
* Confirm that your app runs in Docker. The following commands are examples, not necessarily steps that exist in your app:
  - `git clone git@github.com:yourrepo/spring-boot-hello-world.git`
  - `cd spring-boot-hello-world`
  - `mvn clean install`
  - `docker build`
  - `docker run -e "SECRET=no" -e "NOT_SECRET=yes" -p 80:8080 {docker_image_name}`
  
* Then, go to your URL, such as `http://localhost/springboothelloworld/sayhello`. Press Ctrl+C to stop the Docker run.

## Adding services to your app (optional)
{: #resources-byoc-kube}

After you create your app, you can add a service to your app from the **App details** page. {{site.data.keyword.cloud_notm}} creates the service instance for you. The provisioning process can be different for different types of services. For example, a database service creates a database, and a push notification service for mobile apps generates configuration information. {{site.data.keyword.cloud_notm}} provides the resources of a service to your app by using a service instance. A service instance can be shared across web apps.

This process provisions a service instance, creates a resource key (credentials), and binds it to your app. For more information, see [Adding a service to your app](/docs/apps?topic=creating-apps-add-resource).

After you add a service to your app, you must [copy the credentials for the service to your deployment environment](/docs/apps?topic=creating-apps-credentials_overview).

## Preparing your app for deployment
{: #deploy-byoc-kube}

In this step, you connect a DevOps toolchain to the app and configure it to be deployed to a Kubernetes cluster that is hosted in the {{site.data.keyword.containerlong}}.

The DevOps toolchain is flexible enough to allow managed execution of arbitrary stages of shell script execution. In other words, you can do nearly anything with a DevOps toolchain. The scope of this section focuses on deployment of your app on a Kubernetes cluster, while keeping in mind "future-proofing" for scaled DevOps and cloud best practices.

Establishing a link between your app, toolchain, and repo is a step toward organizing your product assets. It also helps aggregate a view of your source repository with your DevOps workflow, your running app instances, and dependent services across all of your deployment targets.

### Connecting an existing DevOps toolchain

If you already have a DevOps toolchain, complete these steps:

1. On the **App details** page, click **Configure continuous delivery**. The **Deploy my app** page is displayed.
2. Select the toolchain that you want to connect to your app, and click **Enable deployment**. The **App details** page is displayed, indicating that continuous delivery is configured.

If you don't want to create a DevOps toolchain from scratch, you can cloud-enable your existing code by using the [`ibmcloud dev enable` command](/docs/cli/idt?topic=cloud-cli-idt-cli#enable). The command generates a DevOps toolchain template that you check into your repository. Then, you use that template as the instruction set for what the DevOps toolchain creates. For more information, see the [CLI documentation](/docs/apps?topic=creating-apps-create-deploy-app-cli#byoc-cli).
{: tip}

### Creating a DevOps toolchain

If you want to fully control the creation of the DevOps toolchain with no changes in your code repository, create the toolchain from scratch. You also create all of the integrations to build your app and deploy it to Kubernetes cluster. 

1. On the **App details** page, click **Create DevOps toolchain.** The **Create a toolchain** page is displayed.
2. Select the **Build your own toolchain** template.
3. On the **Build your own toolchain** page, enter a name for your toolchain, select a region and resource group (default), and click **Create**.
4. Use the breadcrumbs in the browser window to return to the **App details** page, which indicates that continuous delivery is configured.
5. On the **App details** page, click **View toolchain** to configure your new DevOps toolchain.

### Adding a GitHub integration
{: #github-byoc-kube}

Configure the DevOps toolchain with an integration for your GitHub repo for the toolchain. This sets a webhook in your repo so that pull requests and code pushes in that repo send a POST to the toolchain.

1. In your empty DevOps toolchain template, click **Add a Tool**.
2. Select **GitHub** if your repository is on public GitHub or on Enterprise GitHub.
3. Select or enter the GitHub server URL.
4. An `Unauthorized on GitHub` message might be displayed. If so, click **Authorize**. Then, on the Authorize IBM Cloud Toolchains page, click **Authorize IBM-Cloud**, and enter your GitHub password.
5. On the Configure the Integration page, select **Existing** for the repository type so that the DevOps toolchain configures the repository with a webhook and does not make any fork or copy of your repository.
6. Enter your repository URL, for example, `https://github.com/yourrepo/spring-boot-hello-world`.
7. After a few moments, you might be prompted to authorize GitHub to grant DevOps toolchain permission to use the GitHub ReST API to configure your repo with the webhooks that are necessary to trigger the toolchain.
8.  Click **Create Integration**.

You can view the new webhook from your repo settings.

### Adding a delivery pipeline
{: #pipeline-byoc-kube}

1. Click **Add a Tool**.
2. Select **Delivery Pipeline**.
3. Enter `Continuous Integration` for the pipeline name, and click **Create Integration**.

### Configuring your pipeline stages
{: #pipelineconfig-byoc-kube}

Configure the pipeline stages to direct your input (the GitHub repo contents) to the correct destination. Because this tutorial assumes that you have a GitHub repo that produces a working Docker image and is targeting an {{site.data.keyword.containerlong}}, you create pipeline stages with inputs, shell scripts, and outputs that achieve this goal.

1. Configure your `build and publish` pipeline stage.
  1. Select the delivery pipeline that you created, and click **Add a Stage**.
  2. Click the **Input** tab and complete the fields as follows:
    * Enter `build and publish Docker image` for the stage name.
    * Select **Git repository** for the input type.
    * Select your GitHub repo.
    * Select the branch that you use for continuous integration.
  3.  Click the **Jobs** tab, then click **Add Job '+'**, and complete the fields as follows:
    * Select **Build** for the job type.
    * Enter `build and publish` for the name.
    * Select **Container Registry** for the builder type.
    * Select the region where your Kubernetes cluster is located.
    * Select **Enter an existing API key**. If you don't have an API key, see [Creating an API key](/docs/iam?topic=iam-userapikey#create_user_key). 
    * Enter the container registry namespace, which you can find by clicking the **Menu** icon ![Menu icon](../../icons/icon_hamburger.svg), and selecting **Containers** > **Registry** > **Namespaces**.
    * For the Docker image name, enter `continuous` because this pipeline build stage is for the continuous build of your repo's continuous integration branch.
    * Edit the build script by adding a line or more after the first `#!/bin/bash` line. For example, for a repo that is built by using maven, you might add a few lines similar to the following example:

      ```bash
      export JAVA_HOME=/opt/IBM/java8
      # the MAVEN_OPTS, -B flag, and stopping the phases just prior to 'install' are recommended:
      export MAVEN_OPTS="-  
      Dorg.slf4j.simpleLogger.log.org.apache.maven.cli.transfer.Slf4jMavenTransferListener=warn"
      mvn -B clean verify
      ```
      {: codeblock}
  4. Click **Save**. 
2. Test your `build and publish` pipeline stage by clicking the **Play** icon until the build succeeds. A stage of green indicates that the build is successful. 
3. Configure your `deploy to cluster` pipeline stage to deploy the Docker image to your Kubernetes cluster. 
  1. On the Delivery Pipeline page, click **Add a Stage**.
  2. Click the **Input** tab and complete the fields as follows:
    * Enter `deploy to cluster` for the name.
    * Select **Build artifacts** for the input type.
    * Select **Build & Publish Docker Image** for the stage.
    * Select **Build & Publish** for the job.
    * Because this is your continuous integration pipeline, accept the default option for the stage trigger.
  3. Click the **Jobs** tab, then click **Add Job '+'**, and complete the fields as follows:
    * Enter `deploy to continuous integration cluster` for the name.
    * Select **Kubernetes** for the deployer type.
    * Select the region where your Kubernetes cluster is located.
    * Enter your existing API key. 
  4. Click **Save**.
4. Test your `deploy to cluster` pipeline stage by clicking the **Play** icon until the build succeeds. A stage of green indicates that the build is successful.

## Verifying that your app is running
{: #verify-byoc-kube}

The Delivery Pipeline or command line points you to the URL for your app.

1. From your DevOps toolchain, click **Delivery Pipeline**, and then select **Deploy Stage**.
2. Click **View logs and history**.
3. In the log file, find the app's URL. At the end of the log file, search for the word `urls` or `view`. For example, you might see a line in the log file that's similar to `urls: my-app-devhost.mybluemix.net` or `View the application health at: http://<ipaddress>:<port>/health`.
4. Go to the URL in your browser. If the app is running, a message that includes `Congratulations` or `{"status":"UP"}` is displayed.

If you are using the command line, run the [`ibmcloud dev view`](/docs/cli/idt?topic=cloud-cli-idt-cli#view) command to open the page of a manually deployed app in your default browser.

## Related information

 * [Creating toolchains](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-toolchains_getting_started)
 * [Configuring Git repos and issue tracking](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-integrations#grit)
 * [Configuring GitHub](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-integrations#github)
 * [Configuring GitLab](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-integrations#gitlab)