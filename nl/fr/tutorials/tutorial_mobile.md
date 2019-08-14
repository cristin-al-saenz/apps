---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-18"

keywords: apps, mobile, mobile application, starter kit, developer tools, DevOps toolchain, toolchain, cli

subcollection: creating-apps

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Création d'une application mobile à l'aide d'un kit de démarrage
{: #tutorial-mobile}

{{site.data.keyword.cloud}} inclut des kits de démarrage mobiles vous permettant de créer plus facilement et plus rapidement une application mobile. Sélectionnez une langue, une infrastructure et des outils dans les kits de démarrage de service d'application afin de commencer à utiliser une application personnalisée préconfigurée. Dans ce tutoriel, vous allez apprendre à installer les outils dont vous avez besoin, générer et exécuter l'application localement et la déployer dans le cloud.
{: shortdesc}

## Etape 1. Avant de commencer
{: #prereqs-mobile}

* Installez [{{site.data.keyword.dev_cli_short}}](/docs/cli?topic=cloud-cli-ibmcloud-cli).
* Docker est installé en tant qu'outil de développement. Pour que les commandes de génération fonctionnent, Docker doit être en cours d'exécution. Vous devez créer un compte Docker, exécuter l'application Docker et vous connecter.
* Si vous envisagez de déployer votre application dans [{{site.data.keyword.cfee_full}}](/docs/cloud-foundry?topic=cloud-foundry-about), vous devez [préparer votre compte {{site.data.keyword.cloud_notm}}](/docs/cloud-foundry?topic=cloud-foundry-prepare).

## Etape 2. Créer une application en utilisant {{site.data.keyword.dev_console}}
{: #create-mobile}

1. Créez une application {{site.data.keyword.dev_console}} dans {{site.data.keyword.cloud_notm}}.
2. Sur la page [Kits de démarrage ](https://{DomainName}/developer/appservice/starter-kits/){: new_window} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe") dans {{site.data.keyword.dev_console}}, sélectionnez un kit de démarrage correspondant aux fonctions dont vous avez besoin. Par exemple, pour une application Watson Language, sélectionnez **Swift Kitura**.
3. Entrez le nom de votre application. Pour ce tutoriel, utilisez `WatsonApp`.
4. Facultatif. Créez des étiquettes pour classer votre application. Pour plus d'informations, voir [Utilisation d'étiquettes](/docs/resources?topic=resources-tag).
5. Sélectionnez votre plateforme de langage. Pour ce tutoriel, utilisez `Swift`.
6. Sélectionnez votre langage et votre infrastructure. Certains kits de démarrage peuvent être disponibles dans un seul langage.
7. Sélectionnez votre plan de tarification. Il existe une option gratuite que vous pouvez utiliser pour ce tutoriel.
8. Cliquez sur **Créer**.

## Etape 3. Ajouter des services (facultatif)
{: #resources-mobile}

Vous pouvez ajouter des services qui améliorent votre application avec la puissance cognitive de Watson, ajoutent des services mobiles ou des services de sécurité. Pour ce tutoriel, ajoutez un emplacement pour gérer vos données.

1. Sur la page **Détails de l'application**, cliquez sur **Ajouter un service**.
2. Sélectionnez le type de service souhaité. Par exemple, sélectionnez **Données** > **Suivant** > **Cloudant** > **Suivant**.
3. Sélectionnez votre plan de tarification. Il existe une option gratuite que vous pouvez utiliser pour ce tutoriel.
4. Cliquez sur **Créer**.

## Etape 4. Créer une chaîne d'outils DevOps
{: #toolchain-mobile}

L'activation d'une chaîne d'outils permet de créer un environnement de développement basé sur une équipe pour votre application. Lorsque vous créez une chaîne d'outils, le service d'application crée un référentiel Git dans lequel vous pouvez afficher le code source, cloner votre application, créer et gérer des problèmes. Vous avez également accès à un environnement de lab dédié Git et à un pipeline de distribution continue. Ces éléments sont personnalisés en fonction de la cible de déploiement choisie, [Kubernetes](/docs/containers?topic=containers-getting-started), [Cloud Foundry](/docs/cloud-foundry-public?topic=cloud-foundry-public-about-cf), [{{site.data.keyword.cfee_full_notm}}](/docs/cloud-foundry/index.html) ou [Virtual Server (VSI)](/docs/vsi?topic=virtual-servers-getting-started-with-virtual-servers).

Toutes les chaînes d'outils créées à partir d'un tableau de bord de développeur {{site.data.keyword.cloud_notm}} sont configurées pour un déploiement automatique.
{: note}

1. Sur la page **Détails de l'application**, cliquez sur **Configurer la distribution continue**.
2. Sélectionnez une cible de déploiement. Configurez votre cible de déploiement en fonction des instructions qui s'appliquent à la cible que vous sélectionnez :
  * **Déployer dans [IBM Kubernetes Service](/docs/apps/deploying?topic=creating-apps-containers-kube)**. Cette option crée un cluster d'hôtes, appelé noeuds worker, afin de déployer et de gérer des conteneurs d'application à haute disponibilité. Vous pouvez créer un cluster ou effectuer un déploiement sur un cluster existant.
  * **Déployer dans Cloud Foundry**. Cette option déploie votre application cloud native sans qu'il soit nécessaire de gérer l'infrastructure sous-jacente. Si votre compte a accès à {{site.data.keyword.cfee_full_notm}}, vous pouvez sélectionner un déployeur de type **[Public Cloud](/docs/cloud-foundry-public?topic=cloud-foundry-public-about-cf)** ou **[Enterprise Environment](/docs/cloud-foundry-public?topic=cloud-foundry-public-cfee)**, que vous pouvez utiliser pour créer et gérer des environnements isolés pour l'hébergement de vos applications Cloud Foundry exclusivement pour votre entreprise.
  * **Déployer sur un [serveur virtuel](/docs/apps?topic=creating-apps-vsi-deploy)**. Cette option met à disposition une instance de serveur virtuel qui inclut votre application, créer une chaîne d'outils DevOps et initie pour vous le premier cycle de déploiement.

## Etape 5. Générer et exécuter l'application localement
{: #build-run-mobile}

Le déploiement de votre application dans le cloud effectué lors de la dernière étape a créé une chaîne d'outils. Cette dernière crée un référentiel Git pour votre application dans lequel vous pouvez trouver le code. Procédez comme suit pour accéder à votre référentiel. Vous pouvez générer l'application localement à des fins de test avant de la placer dans le cloud.

1. Sur la page **Détails de l'application**, cliquez sur **Télécharger le code** ou **Cloner votre référentiel** pour utiliser votre code localement.
2. Importez l'application dans votre environnement de développement intégré.
3. Modifiez le code.
4. Configurez l'[authentification Git](/docs/services/ContinuousDelivery?topic=ContinuousDelivery-git_working#git_authentication) en ajoutant un jeton d'accès personnel.
5. Connectez-vous à l'interface de ligne de commande {{site.data.keyword.cloud_notm}}. Si votre entreprise utilise des connexions fédérées, utilisez l'option `-sso`.

  ```bash
  ibmcloud login -sso
  ```
  {: pre}

6. Configurez vos cibles d'organisation et d'espace.

  ```bash
  ibmcloud target --cf
  ```
  {: pre}

7.  Obtenez les données d'identification.

  ```bash
  ibmcloud dev get-credentials
  ```
  {: pre}

8. Assurez-vous que Docker est en cours d'exécution et générez votre application dans un conteneur de développement local à partir du répertoire.

  ```bash
  ibmcloud dev build
  ```
  {: pre}

9. Exécutez votre application dans un conteneur de développement local.

  ```bash
  ibmcloud dev run
  ```
  {: pre}

10.  Ouvrez votre navigateur dans `http://localhost:3000`. Votre numéro de port peut être différent en fonction de l'environnement d'exécution choisi.

### Exécution de votre application Swift dans Xcode
{: #run_swift}

1. Ouvrez le fichier `README.md` dans un visualiseur Markdown afin de passer en revue les étapes nécessaires pour configurer votre application.
2. Ouvrez votre terminal et accédez au dossier de votre application, puis exécutez les commandes suivantes :
    1. Exécutez `pod setup` si vous devez configurer votre référentiel CocoaPods.
    2. Exécutez `pod update` si vous devez mettre à jour vos pods existants.
    3. Exécutez `pod install` pour installer les pods de votre application.
3. Ouvrez votre espace de travail Xcode `<appname>.xcworkspace`.
4. Exécutez votre application.

### Exécution de votre application Cordova dans Xcode
{: #run_cordova_xcode}

Si vous avez choisi d'utiliser Cordova comme langage d'implémentation, suivez les instructions ci-dessous :

1. Ouvrez le fichier `README.md` dans un visualiseur Markdown pour configurer votre application.
2. Ouvrez votre application `platforms/ios` dans Xcode.
3. Exécutez votre application.

### Exécution de votre application Cordova dans Android Studio
{: #run_cordova_studio}

Utilisez cette section si vous avez choisi d'utiliser Cordova comme plateforme de votre application mobile.

1. Décompressez le fichier `BasicProject-Cordova.zip`.
2. Ouvrez le fichier `README.md` dans un visualiseur Markdown pour configurer votre application.
3. Ouvrez votre application `platforms/android` dans Android Studio.
4. Exécutez votre application.

### Exécution de votre application Android dans Android Studio
{: #run_android}

Utilisez cette section si vous avez choisi d'utiliser Android comme plateforme de votre application mobile.

1. Ouvrez le fichier `README.md` dans un visualiseur Markdown pour configurer votre application.
2. Ouvrez votre application `BasicProject-Android` dans Android Studio.
3. Exécutez votre application.

## Etape 6. Déployer votre application
{: #deploy-mobile}

### Déploiement à l'aide d'une chaîne d'outils
{: #deploy-mobile-toolchain}

Vous pouvez déployer votre application dans {{site.data.keyword.cloud_notm}} de différentes manières. Mais l'utilisation d'une chaîne d'outils DevOps reste le meilleur moyen de déployer des applications de production. A l'aide d'une chaîne d'outils DevOps, vous pouvez facilement automatiser un grand nombre de déploiements et ajouter rapidement des services de surveillance, de journalisation et d'alerte afin de gérer plus facilement votre application à mesure de sa croissance.

Avec une chaîne d'outils correctement configurée, un cycle de génération-déploiement démarre automatiquement avec chaque fusion vers la branche principale de votre référentiel. Toutes les chaînes d'outils créées à partir d'un tableau de bord de développeur {{site.data.keyword.cloud_notm}} sont configurées pour un déploiement automatique.

Vous pouvez également déployer manuellement votre application depuis votre chaîne d'outils DevOps :

1. Sur la page **Détails de l'application**, cliquez sur **Afficher la chaîne d'outils**.

2. Cliquez sur **Delivery Pipeline**. Vous pouvez alors démarrer des générations, gérer le déploiement et afficher les journaux et l'historique.

### Déploiement en utilisant {{site.data.keyword.dev_cli_short}}
{: #deploy-mobile-cli}

Pour déployer votre application sur Cloud Foundry, entrez la commande suivante :

```
ibmcloud dev deploy
```
{: pre}

Pour déployer votre application sur un cluster Kubernetes, entrez la commande suivante :

```
ibmcloud dev deploy --target <container>
```
{: pre}

## Etape 7. Vérifier que votre application est en cours d'exécution
{: #verify-mobile}

Une fois votre application déployée, Delivery Pipeline ou la ligne de commande indique l'URL de votre application.

1. Dans votre chaîne d'outils DevOps, cliquez sur **Delivery Pipeline** puis sélectionnez **Etape de déploiement**.
2. Cliquez sur **Afficher les journaux et l'historique**.
3. Dans le fichier journal, recherchez l'URL de l'application :

    A la fin du fichier journal, recherchez le mot `urls` ou `view`. Ainsi, une ligne similaire à `urls: my-app-devhost.mybluemix.net` ou à `View the application health at: http://<ipaddress>:<port>/health`.

4. Accédez à l'URL dans votre navigateur. Si l'application est en cours d'exécution, un message qui inclut `Congratulations` ou `{"status":"UP"}` s'affiche.

Si vous utilisez la ligne de commande, exécutez la commande [`ibmcloud dev view`](/docs/cli/idt?topic=cloud-cli-idt-cli#view) pour afficher l'URL de votre application. Accédez ensuite à l'URL dans votre navigateur.
