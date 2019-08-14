---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-03"

keywords: apps, Mendix, starter kit, developer tools, Mendix app, create mendix app

subcollection: creating-apps

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note .note}

# Creating apps with Mendix
{: #create-mendix}

Mendix is a low-code development environment and toolset that helps you deliver multi-device applications faster, with fewer development resources, that run on {{site.data.keyword.cloud}}. By selecting a Mendix low-code starter kit, you're guided to set up your account on Mendix Platform, start your project, and select your deployment target of Cloud Foundry or your Kubernetes cluster.
{: shortdesc}

## Selecting a starter kit
{: #starterkit-mendix}

1. From the [{{site.data.keyword.cloud_notm}} App Service dashboard](https://{DomainName}/developer/appservice/dashboard){: new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon"), click **Get Started**.
2. Select a Mendix low-code starter kit from one of the following categories:
  * [Mobile](https://{DomainName}/developer/appservice/starter-kits/mendix-mobile-app){: new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon")
  * [Watson Web or Mobile App](https://{DomainName}/developer/appservice/starter-kits/mendix-web-or-mobile-app-with-watson){: new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon")
  * [Web App](https://{DomainName}/developer/appservice/starter-kits/mendix-web-app){: new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon")
3. Click **Create app**.
4. On the **App details** page, name your app and optionally provide tags to classify your app. For more information, see [Working with tags](/docs/resources?topic=resources-tag).
5. Click **Create**.

## Authorizing IBM to create your project on Mendix and link accounts
{: #link-mendix-account}

If you're not using Mendix with {{site.data.keyword.cloud_notm}} yet, you are guided to the Mendix Platform to sign up and authorize {{site.data.keyword.cloud_notm}} to create a new project on Mendix Platform in your behalf. This project is linked to {{site.data.keyword.cloud_notm}}, so deployments are automatically directed to {{site.data.keyword.cloud_notm}}.

1. If you see this message, click **Link Account**.
  ```
  "To complete app creation, a Mendix user account is required. Would you like to link your account now?"
  ```
  {: screen}

2. On the Mendix confirmation page, select **I agree to the Mendix Privacy Policy and Terms**, and click **Confirm**.
3. When prompted, provide your email address, password, and country, and then click **Create**.
4. On the **Authorize access to your Mendix account** page, click **Authorize**.

After the authorization is complete, your browser returns to the Mendix app that you're creating. The **Select a deployment target** page is displayed.

## Selecting a deployment target for your Mendix app
{: #select-deployment}

1. On the **Select a deployment target** page, select Cloud Foundry or one of your Kubernetes clusters that is running on {{site.data.keyword.cloud_notm}}. If your account has access to {{site.data.keyword.cfee_full_notm}}, you can select a Cloud Foundry deployer type of either **[Public Cloud](/docs/cloud-foundry-public?topic=cloud-foundry-public-about-cf)** or **[Enterprise Environment](/docs/cloud-foundry-public?topic=cloud-foundry-public-cfee)**, which you can use to create and manage isolated environments for hosting Cloud Foundry apps exclusively for your enterprise.
2. Optional. If you don't have a Kubernetes cluster, you can create one now.
3. On the **Configure toolchain** page, select your region and resource group, and then click **Create**.

A DevOps toolchain is created. The toolchain integrates your Mendix project within the Mendix Platform in your {{site.data.keyword.cloud_notm}} environment. A default app is deployed to your deployment target so that you can verify that the app was successfully deployed upon completion of the DevOps toolchain.

Mendix Cloud Foundry deployments require the PostGRES database service, which doesn't have a lite tier. If you want to evaluate the Mendix starter kits by using a lite account, you can target a trial Kubernetes cluster.
{: tip}

If you selected a Kubernetes cluster for deployment, see the [Mendix Kubernetes tutorial](/docs/apps/tutorials?topic=creating-apps-deploy-mendix-kube) to learn how to configure your cluster for production use.

## Continuing the Mendix development and deployment lifecycle
{: #dev-lifecycle-mendix}

Mendix is a low-code authoring environment. The development lifecycle requires you to open your project in the Mendix Modeler desktop app.

1. From your {{site.data.keyword.cloud_notm}} app, click **Edit on Mendix**.
2. In the Mendix web portal, click **Edit in Desktop Modeler**.
  The Mendix app is opened in the desktop modeler.
3. Edit your Mendix app, and save your changes.
4. Use the Mendix Desktop Modeler app's **Run** menu, and select the **Run** option.
  The deployment package is created and uploaded to Mendix. After the deployment package is created, you can deploy your app to {{site.data.keyword.cloud_notm}}.
5. To deploy your Mendix app, go back to your **App details** page on {{site.data.keyword.cloud_notm}}, and click **Deploy**.
  This action starts your app's DevOps toolchain, which pulls the latest deployment from Mendix and deploys it to your target environment. After the deployment is complete, the latest version of your app automatically starts and becomes available.

All Mendix apps are to be deployed to {{site.data.keyword.cloud_notm}} by clicking **Configure continuous delivery** in the **App details** page on {{site.data.keyword.cloud_notm}}. Don't manually invoke Mendix toolchains through the IBM DevOps interface. Launching toolchains manually through the DevOps interface might result in a failed deployment due to a lack of required metadata that is critical for Mendix deployments. Depending on the state of your app, either a failure during the DevOps toolchain launch, or an error in the deployed app, might occur.

If you manually launch a toolchain and experience a failure, you can restore your app deployment by clicking **Configure continuous delivery** in the **App details** page on {{site.data.keyword.cloud_notm}}. This action triggers a complete DevOps flow for the Mendix app, which includes the required metadata.
{: tip}

## Optional: Configuring {{site.data.keyword.cos_full_notm}} 
{: #mendix-cos}

Some users might want to configure their deployed Mendix app to use {{site.data.keyword.cos_full}} for persistent storage and file uploads. {{site.data.keyword.cos_full_notm}} is an S3-compatible object storage service. To take advantage of S3-compatible file storage, Mendix apps must define the following environment variables to access a {{site.data.keyword.cos_full_notm}} instance, after they have configured continuous delivery:

* `S3_ACCESS_KEY_ID` - the S3 Key, which is part of {{site.data.keyword.cos_full_notm}} credentials
* `S3_SECRET_ACCESS_KEY` - the S3 secret key, which is part of {{site.data.keyword.cos_full_notm}} credentials
* `S3_BUCKET_NAME` - the S3 storage bucket
* `S3_ENDPOINT` - the S3 storage endpoint
* `S3_USE_V2_AUTH` - the value is `true`

For more information about {{site.data.keyword.cos_full_notm}} buckets and keys, see the [{{site.data.keyword.cos_full_notm}} API documentation](/docs/services/cloud-object-storage?topic=cloud-object-storage-gs-dev). For more information about regional and cross-regional endpoint values, see the [{{site.data.keyword.cos_full_notm}} docs](/docs/services/cloud-object-storage?topic=cloud-object-storage-endpoints). For more information about Mendix support for S3-compatible storage, see the [Mendix buildpack documentation](https://github.com/mendix/cf-mendix-buildpack#s3-settings){: new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon").

### {{site.data.keyword.cos_full_notm}} settings for Cloud Foundry apps
{: cos-cfapps}

Complete these steps for Cloud Foundry deployments:

1. Set these environment variables on Cloud Foundry deployments by using the `cf set-env` command:

  ```
    ibmcloud cf set-env <YOUR_APP> S3_ACCESS_KEY_ID <YOUR_KEY>
    ibmcloud cf set-env <YOUR_APP> S3_SECRET_ACCESS_KEY <YOUR_SECRET_KEY>
    ibmcloud cf set-env <YOUR_APP> S3_BUCKET_NAME <YOUR_BUCKET>
    ibmcloud cf set-env <YOUR_APP> S3_ENDPOINT s3.us-south.cloud-object-storage.appdomain.cloud
    ibmcloud cf set-env <YOUR_APP> S3_USE_V2_AUTH true
  ```

2. After you specify all of these values, restage your Cloud Foundry app for the new values to be applied.

  ```
    ibmcloud cf restage <YOUR_APP>
  ```

### {{site.data.keyword.cos_full_notm}} settings for Kubernetes apps
{: #cos-kubeapps}

Complete these steps for Kubernetes deployments:

1. Set the `S3_ACCESS_KEY_ID` and `S3_SECRET_ACCESS_KEY` environment variables as Kubernetes secret values in the cluster. For more information about creating Kubernetes secrets, see the [{{site.data.keyword.containershort_notm}} documentation](/docs/containers?topic=containers-service-binding#adding_app).

2. In addition to any existing values, specify the environment variables as additional environment variables in the `mendix-app.yaml` file inside of the Git repo's `chart/<appname>/templates` folder. The secret names must match the names that were created in the previous step.

  ```
    env:
      - name: S3_ACCESS_KEY_ID
        valueFrom:
          secretKeyRef:
            name: "mendix-s3-key"
            key: db-endpoint
      - name: S3_SECRET_ACCESS_KEY
        valueFrom:
          secretKeyRef:
            name: "mendix-s3-secret-key"
            key: db-endpoint
      - name: S3_ENDPOINT
        value: "s3.us-south.cloud-object-storage.appdomain.cloud"
      - name: S3_USE_V2_AUTH
        value: "true"
  ```

3. After the Kubernetes changes are applied, redeploy your app by navigating to the **App details** page and clicking **Deploy**. 

## Next steps 
{: #next-steps-mendix}

To deploy your app to the {{site.data.keyword.containerlong_notm}}, configure your app for production deployment. For more information, see the [Mendix Kubernetes tutorial](/docs/apps/tutorials?topic=creating-apps-deploy-mendix-kube). 
