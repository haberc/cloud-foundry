---

copyright:

  years: 2018
lastupdated: "2018-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Mise à jour et mise à l'échelle
{: #update-scale}

Mettez à jour l'instance de service {{site.data.keyword.cfee_full_notm}} vers la dernière version afin d'obtenir les fonctions et les correctifs les plus récents pour CFEE. Les mises à jour pour ICDEE peuvent inclure de nouvelles versions de la plateforme Cloud Foundry et du cluster Kubernetes qui prend en charge l'infrastructure CFEE. 

Les mises à jour de version CFEE se déroulent sur le plan de contrôle contenant les composants CFEE et sur les cellules. Vous pouvez également mettre à l'échelle la capacité de votre instance CFEE en ajoutant ou en supprimant des cellules d'application. 

**Remarque :** durant une mise à jour de version ou lors de l'ajout ou la suppression de cellules, certaines métriques (par exemple, la mémoire et l'UC) affichées sur les pages _Présentation_, _Utilisation des ressources_ et _Mise à jour et mise à l'échelle_ ne sont peut-être pas disponibles. 

## Mise à jour de la version CFEE
{: #update}

Les utilisateurs doivent disposer des droits suivants pour pouvoir mettre à jour une instance CFEE vers une nouvelle version :
   * Rôle _Editeur_ ou rôle de niveau supérieur sur une instance CFEE
   * Rôle _Opérateur_ ou rôle de niveau supérieur sur le cluster Kubernetes dans lequel l'instance CFEE est mise à disposition

La mise à jour de la version CFEE de votre instance CFEE est un processus en deux étapes. Tout d'abord, mettez à jour le plan de contrôle qui héberge le composant CFEE. Ensuite, mettez à jour les cellules qui hébergent vos applications.

Les règles et contraintes suivantes s'appliquent lors de la mise à jour d'une instance CFEE vers une nouvelle version :
* Le plan de contrôle doit être mis à jour en premier. Une fois le plan de contrôle mis à jour, les cellules peuvent être mises à jour. 
* Les cellules d'application ne peuvent être mises à jour que vers la version du plan de contrôle. Autrement dit, les cellules du plan de contrôle peuvent être à un niveau de version CFEE supérieur à celui des cellules d'application, mais l'inverse n'est pas possible. 

Pour mettre à jour la version CFEE de votre instance CFEE :
1. Accédez au [tableau de bord {{site.data.keyword.Bluemix_notm}} ](https://console.bluemix.net/dashboard/apps/) et ouvrez l'environnement {{site.data.keyword.cfee_full_notm}} que vous souhaitez mettre à jour. 
2. Dans l'environnement {{site.data.keyword.cfee_full_notm}}, accédez à l'entrée **Cellules** dans le panneau de navigation pour ouvrir la page des cellules. 
3. (Facultatif) Dans le tableau _Plan de contrôle_, vous pouvez développer la ligne pour voir les noeuds worker dans le plan de contrôle. 
4. Cliquez sur **Mettre à jour**.
5. Dans la boîte de dialogue de mise à jour de _plan de contrôle_, sélectionnez l'une des versions CFEE disponibles et cliquez sur **Mettre à jour**. La mise à jour dure environ 5 minutes. La description de la version mentionne les versions des composants inclus dans le package de version CFEE sélectionné, et contient un lien vers le document _Nouveautés_ qui décrit le contenu fourni dans cette version. 
6. La colonne _Statut de noeud_ affiche la progression de la mise à jour. Une fois la mise à jour terminée, la colonne _Version_ reflète la nouvelle version CFEE. 
7. Une fois la mise à jour des cellules de plan de contrôle terminée, localisez le tableau _Cellules_ et cliquez sur **Mettre à jour**.
8. Dans la boîte de dialogue de _mise à jour de plan de contrôle_, sélectionnez la version CFEE et cliquez sur *Mettre à jour*. Seule la version des cellules est disponible pour mise à jour car les cellules ne peuvent être mises à jour que vers la version du plan de contrôle. Une seule action de mise à jour met à jour toutes les cellules. 
9. Les cellules sont mises à jour de façon séquentielle. La colonne _Statut de noeud_ indique la progression de la mise à jour de chaque cellule. A mesure que les cellules sont mises à jour, leur nouvelle version apparaît dans la colonne _Version_. 

## Interruptions durant les mises à jour de version
{: #update-disruption}

La mise à jour du plan de contrôle Cloud Foundry se fait sans interruption. Cela dit, la mise à jour des cellules Cloud Foundry vers une nouvelle version CFEE peut entraîner une interruption du fonctionnement de l'environnement CFEE. La mise à jour s'effectue cellule par cellule, ainsi, les instances d'application qui s'exécutent dans une cellule sont restaurées une fois la mise à jour terminée tandis que les autres cellules sont hors service durant leur mise à jour. Quoi qu'il en soit, certaines applications et certains services qui s'exécutent dans l'instance CFEE peuvent devenir non disponibles dans certaines circonstances. Par exemple, si l'instance CFEE comporte deux cellules Cloud Foundry pour une plaine capacité, une application ne comportant qu'une seule instance sera hors service durant la mise à jour de version car l'instance d'application ne peut pas être déplacée vers une autre cellule pendant que la cellule est mise à jour, et, par conséquent, l'application deviendra non disponible.   

Durant la mise à jour de version, des différences peuvent apparaître entre les métriques de mémoire et d'UC signalées dans les jauges Noeuds de cellule affichées sur la page _Présentation_ de CFEE (qui sont générées par le cluster Kubernetes) et les mêmes métriques affichées dans le tableau de bord _Noeuds_ de Grafana (qui sont générées au niveau du système d'exploitation). 

Le statut des composants CFEE sera indiqué sur la page Diagnostic d'intégrité durant la progression de la mise à jour. Le redémarrage prend environ 45 minutes.

## Cycle de version et politique de support
{: #version-cycle}

En règle générale, le service Cloud Foundry Enterprise Environment met régulièrement en production une nouvelle version. La version du service respecte le format de gestion des versions sémantique _**Major.Minor.Patch**_ (https://semver.org/). 

La version _secondaire_ est régulièrement incrémentée (en général, une fois par mois). La version _principale_ est également incrémentée, mais moins souvent, généralement en cas de changement significatif. La mise à jour vers une version _principale_ peut entraîner une interruption durant la mise à niveau. Les _modules de correction_ fournissent un correctif et sont appliqués à la dernière version disponible.  

Pour éviter l'interruption du système, les instances CFEE ne sont autorisées à mettre à jour qu'un maximum de 2 versions _principales_ de niveau supérieur par rapport à leur version en cours. En reprenant l'exemple précédent, si la version en cours de l'instance CFEE est 3.1.2 et que la version cible est 7.0.0, l'instance CFEE doit être mise à jour d'abord vers la version 5.x.x, puis vers la version cible 7.0.0 .

Les nouvelles fonctions et les améliorations apportées aux fonctions existantes qui sont fournies régulièrement ne sont disponibles que dans la version la plus récente. Les correctifs critiques sont fournis dans la dernière édition uniquement dans les 3 dernières versions _principales_ (la dernière version et les deux versions précédentes). Par exemple, si les versions 4.x.x, 3.x.x et 2.x.x sont disponibles, les versions 1.x.x ne seront pas prises en charge (autrement dit, les correctifs ne seront pas fournis avec les correctifs des versions 1.x.x).  

Les correctifs sont distribués avec la dernière version disponible d'une version _principale_ donnée. Par exemple, si une instance CFEE exécute la version 3.1.2 mais que la dernière version disponible dans la version _principale_ 3.x.x est la version 3.3.4, les correctifs seront distribués sur la base de code de version 3.3.x, ce qui signifie que le correctif sera distribué dans une (nouvelle) version 3.3.5. L'instance CFEE avec la version 3.1.2 doit être mise à jour vers la version 3.3.5 afin de recevoir le nouveau correctif (autrement dit, la mise à jour vers la version 3.3.4 ne permettra pas de résoudre le problème traité par le correctif, lequel est distribué uniquement dans la version 3.3.5).

## Mise à l'échelle de l'infrastructure CFEE
{: #scale}

Les utilisateurs doivent disposer des droits suivants pour pouvoir ajouter ou retirer des cellules Cloud Foundry dans une instance CFEE :
* Rôle _Administrateur_ ou rôle de niveau supérieur sur une instance CFEE
* Rôle _Opérateur_ ou rôle de niveau supérieur sur le cluster Kubernetes dans lequel l'instance CFEE est mise à disposition

Pour ajouter des cellules d'application dans votre instance CFEE :
1. Accédez au [tableau de bord {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/apps/) et ouvrez l'instance {{site.data.keyword.cfee_full_notm}} dans laquelle vous souhaitez ajouter des cellules. 
2. Cliquez sur **Ajouter une cellule** en regard du tableau _Cellules_, et la page _Ajouter des cellules Cloud Foundry_ s'ouvre. 
3. Sur la page _Ajouter des cellules Cloud Foundry_, sélectionnez le nombre de cellules à ajouter. La page affiche également la géographie et l'emplacement de l'instance CFEE dans laquelle les cellules seront ajoutées. Elle affiche également le nombre en cours de cellules et la capacité des cellules qui seront ajoutées (qui est identique à la capacité des cellules en cours). Sur le panneau de droite de la page sont indiqués le coût estimé des cellules ajoutées ainsi que le nouveau coût total estimé de l'environnement. 
4. Cliquez sur **Ajouter une cellule**.  
5. Accédez à la page _Noeuds_. Une nouvelle ligne est ajoutée dans le tableau _Cellules_ pour chaque nouveau noeud. La colonne _Statut de noeud_ indique la progression de l'ajout et du déploiement de la cellule sur votre environnement CFEE. 
