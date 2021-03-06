---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Tutoriel d'initiation
{: #getting-started}

L'environnement {{site.data.keyword.cfee_full}} est une plateforme cloud pour l'hébergement d'applications et de services dans le cloud. {{site.data.keyword.cfee_full_notm}} facilite la mise à l'échelle des applications à mesure de l'augmentation de la consommation, en simplifiant le contexte d'exécution, le middleware et l'infrastructure de sorte que vous puissiez vous concentrer sur le développement d'applications.
{: shortdesc}

Ce tutoriel d'initiation montre comment créer un environnement {{site.data.keyword.cfee_full_notm}}, ajouter des utilisateurs, créer une organisation et des espaces, déployer des applications et lier ces applications à des services.

## Comprendre les droits
{: #permissions}

Pour travailler avec des instances d'{{site.data.keyword.cfee_full_notm}}, les utilisateurs du service doivent disposer des droits appropriés. Pour plus d'informations, voir [Droits](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Etape 1 : Veillez à ce que le compte {{site.data.keyword.Bluemix_notm}} puisse créer des ressources d'infrastructure
{: #accountprep-environment}

Les instances CFEE sont déployées dans des ressources d'infrastructure, qui sont des noeuds worker Kubernetes issus du service Kubernetes.  [Préparez votre compte IBM Cloud](https://console.bluemix.net/docs/cloud-foundry/prepare-account.html) de sorte qu'il puisse créer les ressources d'infrastructure nécessaires à une instance CFEE.

## Etape 2 : Créez votre instance CFEE
{: #creating-environment}

Avant de créer votre environnement CFEE, vérifiez que vous vous trouvez dans le compte {{site.data.keyword.Bluemix_notm}} sous lequel vous voulez créer l'environnement et que vous disposez des règles d'accès requises (étape 1 ci-dessus).

1.  Ouvrez le [catalogue](https://console.bluemix.net/catalog) {{site.data.keyword.Bluemix_notm}}.

2.  Recherchez le service {{site.data.keyword.cfee_full_notm}} dans le catalogue et cliquez dessus pour ouvrir la page de présentation du service.

3.  Le premier écran de la page de création présente les principales fonctions du service. Cliquez sur **Continuer**

4.  Configurez l'instance CFEE à créer comme suit :
    * Sélectionnez un plan (la disponibilité des plans peut être restreinte en phase bêta).
    * Entrez un **Nom** pour l'instance de service.
    * Sélectionnez un **Emplacement** où l'instance de service doit être mise à disposition. Consultez la liste des [emplacements et centres de données de mise à disposition disponibles](https://console.bluemix.net/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe") par zone géographique pour CFEE et les services de prise en charge. 
    * Sélectionnez le **Nombre de cellules** pour l'environnement Cloud Foundry.
    * Sélectionnez le **Type de machine**, qui détermine la taille des cellules Cloud Foundry (unité centrale et mémoire).
    * Sélectionnez un **Groupe de ressources** sous lequel l'environnement est regroupé. Seuls les groupes de ressources auxquels vous avez accès dans le compte IBM Cloud en cours sont répertoriés dans le menu déroulant _Groupes de ressources_, ce qui signifie que vous devez détenir le droit d'accès à au moins un groupe de ressources du compte pour pouvoir créer une instance CFEE.

5.  Dans les zones **Compose for PostgreSQL**, sélectionnez l'une des organisations publiques, puis choisissez l'un des espaces disponibles dans cette organisation. L'instance de l'instance Compose for PostgreSQL sera mise à disposition dans l'espace sélectionné. Le service Compose for PostgreSQL est une dépendance requise du service CFEE.

**Remarque :** seules les organisations situées à l'emplacement où vous prévoyez de mettre à disposition l'instance CFEE (voir l'étape 4 ci-dessus) et auxquelles vous avez accès sont disponibles pour la sélection.  Au sein d'une organisation spécifique, seuls les espaces pour lesquels vous disposez de droits d'accès _développeur_ sont disponibles pour la sélection. 

6.  Eventuellement, ouvrez la section **Infrastructure** pour afficher les propriétés du cluster Kubernetes qui prend en charge l'instance CFEE. Le **nombre de noeuds worker** est égal au nombre de cellules plus 2 (deux des noeuds worker Kubernetes mis à disposition prennent en charge le plan de contrôle CFEE).
Le cluster Kubernetes dans lequel l'environnement est déployé s'affiche dans le [tableau de bord {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/apps/). Pour plus d'informations, voir la [documentation du service Kubernetes](https://console.bluemix.net/docs/containers/cs_why.html#cs_ov).

**Remarque :** il est recommandé d'activer le spanning VLAN si les noeuds worker du cluster Kubernetes sont mis à disposition sur différents sous-réseaux.  Les noeuds worker présents sur différents sous-réseaux peuvent empêcher la connectivité entre eux si le spanning VLAN est désactivé.  Pour plus d'informations, voir la documentation [spanning VLAN](https://console.bluemix.net/docs/containers/cs_subnets.html#vlan-spanning).

7.  Le **Récapitulatif de la commande**, sur la droite de la page, indique le coût de l'instance CFEE et des services auxiliaires, ainsi qu'une estimation mensuelle totale.

8.  Cliquez sur **Créer** pour ouvrir le tableau de bord de l'environnement et afficher le statut et la progression de l'opération de création.

9.  Une fois la mise à disposition lancée, l'environnement est affiché dans le tableau de bord {{site.data.keyword.Bluemix_notm}} et dans le [tableau de bord des environnements Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments).  Le statut indique quand la mise à disposition est terminée.

Le processus automatisé de création de l'environnement déploie l'infrastructure dans un cluster Kubernetes et la configure de sorte qu'elle soit prête pour utilisation. Ce processus prend entre 90 et 120 minutes.

Une fois l'environnement créé, vous recevez plusieurs courriers électroniques confirmant que l'instance CFEE et les services de prise en charge ont été mis à disposition, ainsi que des courriers électroniques mentionnant le statut des commandes correspondantes.

## Etape 3: Créez des organisations et des espaces

Une fois l'environnement {{site.data.keyword.cfee_full_notm}} créé, voir [Création d'organisations et d'espaces](https://console.bluemix.net/docs/cloud-foundry/orgs-spaces.html) pour savoir comment structurer l'environnement en créant des organisations et des espaces. Dans un environnement {{site.data.keyword.cfee_full_notm}}, les applications sont limitées à des espaces spécifiques. Un espace existe lui-même au sein d'une organisation spécifique. Les membres d'une organisation se partagent un plan d'établissement des quotas, des applications, des instances de service et des domaines personnalisés.

**Remarque :** la page _Organisations Cloud Foundry_ accessible via le menu **_Gérer > Compte > Organisations Cloud Foundry_** de l'en-tête IBM Cloud du haut est conçue exclusivement pour les organisations IBM Cloud publiques, **pas pour les organisations CFEE**. Les organisations CFEE sont gérées dans la page _Organisations_ d'une instance CFEE.  Ouvrez l'interface utilisateur CFEE et cliquez sur la page **_Organisations_** pour créer et gérer des organisations pour cet environnement CFEE.

## Etape 4 : Ajoutez des utilisateurs aux organisations et espaces

[Ajoutez des utilisateurs](https://console.bluemix.net/docs/cloud-foundry/add-users.html) à ces organisations et espaces avec des affectations de rôles spécifiques qui contrôlent leur niveau d'accès.  Pour pouvoir devenir membres d'organisations et d'espaces d'un environnement CFEE, les utilisateurs doivent préalablement obtenir un droit d'accès à l'instance CFEE. Voir [Droits](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Etape 5 : Déployez et affichez des applications

Lorsque vous êtes prêt, vous pouvez [déployer l'application](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html) à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.  Affichez dans l'interface utilisateur la liste des applications déployées dans un espace CFEE spécifique ou globalement dans toutes les instances CFEE.  Vous pouvez également démarrer, arrêter ou supprimer des applications dans ces vues.

## Etape 6 : Gérez les services

[Créez des services](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#creating-services_inspace) ou [ajoutez des services existants](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#adding-services_inspace) disponibles dans le compte IBM Cloud.  Une fois qu'une instance de service est disponible dans un espace CFEE, vous pouvez la lier aux applications CFEE qui sont déployées dans cet espace.

## Etape 7 : Liez des applications à des instances de service

[Liez votre application](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#bind_services) à un alias d'instance de service afin d'utiliser les fonctions du service.

Connaissez-vous le [tableau de bord Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/overview) ? Il offre une vue consolidée de l'ensemble des applications et services de l'{{site.data.keyword.Bluemix_notm}}, _Public_ et _Enterprise_ (CFEE).  Une fois dans le tableau de bord Cloud Foundry, cliquez sur _Public_ dans le panneau de navigation de gauche pour voir les applications publiques et les services disponibles dans le compte IBM Cloud.  Cliquez sur _Enterprise_ pour voir tous les environnements CFEE, les applications déployées dans des espaces CFEE et les services disponibles pour les espaces CFEE.
{:tip}

## Etape 8 : Installez la console Stratos pour gérer les applications (facultatif)

La console Stratos est un outil Web open source qui fonctionne avec Cloud Foundry. L'application de console Stratos peut éventuellement être installée et utilisée dans un environnement CFEE spécifique afin de gérer ses organisations, ses espaces et ses applications.

Les utilisateurs dotés du rôle d'administrateur ou d'éditeur IBM Cloud dans l'instance CFEE peuvent installer l'application de console Stratos dans cette instance CFEE.

Pour installer l'application de console Stratos :

1. Ouvrez l'instance CFEE dans laquelle vous voulez installer la console Stratos.
2. Cliquez sur **Installer la console Stratos** dans la page de présentation. Le bouton ne s'affiche que pour les utilisateurs ayant des droits d'administrateur ou d'éditeur sur cette instance CFEE.
3. Dans la boîte de dialogue Installer la console Stratos, sélectionnez une option d'installation. Vous pouvez installer l'application de console Stratos sur le plan de contrôle CFEE ou dans l'une des cellules. Sélectionnez une version de la console Stratos ainsi que le nombre d'instances de l'application à installer. Si vous installez l'application de console Stratos dans une cellule, vous êtes invité à indiquer l'organisation et l'espace où déployer l'application.
4. Cliquez sur **Installer**.

L'installation de l'application prend environ 5 minutes. Une fois l'installation terminée, un bouton **Console Stratos** s'affiche dans la page de présentation à la place du bouton _Installer la console Stratos_. Le bouton _Console Stratos_ permet de démarrer la console et il est disponible pour tous les utilisateurs ayant accès à l'instance CFEE. Les affectations d'appartenance à une organisation et à un espace sont susceptibles de limiter les possibilités d'affichage et de gestion d'un utilisateur dans la console Stratos.

Pour démarrer la console Stratos :

1. Ouvrez l'instance CFEE dans laquelle la console Stratos a été installée.
2. Cliquez sur **Console Stratos** dans la page de présentation.
3. La console Stratos s'ouvre dans un onglet de navigateur distinct. A la première ouverture de la console, vous êtes invité à accepter deux avertissements consécutifs en raison de certificats autosignés.
4. Cliquez sur **Connexion** pour ouvrir la console. Aucune donnée d'identification n'est requise puisque l'application utilise vos données d'identification {{site.data.keyword.Bluemix_notm}}.

Vous trouverez des informations sur l'API CFEE dans la [documentation API](https://console.bluemix.net/apidocs/cfaas){: new_window} pour CFEE ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").
{:tip}


## Ressources supplémentaires
{: #additional-resources}

Vous pouvez effectuer des tâches d'administration dans une instance CFEE à l'aide de commandes d'interface de ligne de commande `ibmcloud CFEE`. Ces commandes vous permettent d'obtenir des informations sur une instance CFEE et de gérer ses organisations et espaces. Voir le site de [référence de commande CFEE d'interface de ligne de commande IBM Cloud](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").

Vous trouverez des vidéos contenant des discussions et des démonstrations relatives à différents sujets concernant CFEE dans la [liste de lecture des vidéos CFEE](https://ibm.biz/CFEE-Playlist){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").


Des informations relatives à l'API CFEE sont disponibles dans la [documentation API CFEE](https://console.stage1.bluemix.net/apidocs/cfaas){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").
