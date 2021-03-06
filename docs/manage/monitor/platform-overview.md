---
title: Vue d’ensemble des plateformes de supervision cloud
description: Consultez une vue d'ensemble générale de deux plateformes de supervision pour mieux comprendre la façon dont chacune d'elles fournit des fonctionnalités de supervision de base.
author: mgoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: abe6fb81a1108e291d0a4f12382172a5f6b39e4d
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83861478"
---
<!-- cSpell:ignore opsman ITSM -->

# <a name="cloud-monitoring-guide-monitoring-platforms-overview"></a>Guide de supervision du cloud : Vue d’ensemble des plateformes de supervision

Microsoft fournit une gamme de fonctionnalités de supervision dans deux produits : System Center Operations Manager, qui a été conçu pour un environnement local, puis étendu au cloud, et Azure Monitor, qui a été conçu pour le cloud, mais qui peut également superviser des systèmes locaux. Ces deux offres fournissent des services de supervision essentiels, comme les alertes, le suivi du temps d’activité des services, et la supervision, les diagnostics et l’analytique de l’intégrité des applications et de l’infrastructure.

De nombreuses organisations adoptent les pratiques les plus récentes pour l’agilité DevOps et les innovations du cloud pour gérer leurs environnements hétérogènes. Ils se préoccupent également de leur capacité à prendre des décisions appropriées et responsables concernant la façon de superviser ces charges de travail.

Cet article fournit une vue d’ensemble générale de nos plateformes de supervision, pour vous aider à comprendre comment elles fournissent toutes deux des fonctionnalités de supervision essentielles.

## <a name="the-story-of-system-center-operations-manager"></a>Histoire de System Center Operations Manager

En 2000, nous sommes entrés dans le domaine de la gestion des opérations avec Microsoft Operations Manager (MOM) 2000. En 2007, nous avons introduit une version remaniée du produit, nommée System Center Operations Manager. Il a évolué au-delà de la simple supervision d’un serveur Windows, et s’est concentré sur la supervision robuste et de bout en bout des services et des applications, notamment des plateformes hétérogènes, des périphériques réseau et d’autres dépendances des services ou des applications. Il s’agit d’une plateforme de supervision de niveau entreprise pour les environnements locaux, dans la même classe qu’IBM Tivoli ou HP Operations Manager sur le marché. Il a évolué pour prendre en charge la supervision des ressources de calcul et de plateforme s’exécutant dans Azure, Amazon Web Services (AWS) et d’autres fournisseurs cloud.

## <a name="the-story-of-azure-monitor"></a>Histoire d’Azure Monitor

Lors de la publication d’Azure en 2010, la supervision des services cloud était fournie avec l’agent Azure Diagnostics, qui offrait un moyen de collecter des données de diagnostic auprès des ressources Azure. Cette fonctionnalité était considérée comme un outil de supervision général, plutôt que comme une plateforme de supervision de niveau d’entreprise.  

Application Insights a été introduit pour évoluer avec les modifications du secteur, où la prolifération des appareils cloud, mobiles et IoT était en augmentation, et l’introduction de pratiques DevOps. Il est passé de la supervision des performances des applications dans Operations Manager à un service dans Azure, où il offre une supervision détaillée des applications web écrites dans différents langages. En 2015, la préversion d’Application Insights pour Visual Studio a été annoncée et plus tard, elle a été appelée simplement Application Insights. Elle collecte des détails sur les performances, les demandes et les exceptions, et les traces.

En 2015, Azure Operational Insights a été rendu disponible publiquement. Il fournissait le service d’analyse Log Analytics, qui collectait et effectuait des recherches dans les données provenant de machines dans des environnements Azure et locaux, ou dans d’autres environnements cloud, et se connectait à System Center Operations Manager. Des Intelligence Packs étaient proposés, qui fournissaient une variété de configurations de gestion et de supervision prépackagées, contenant une collection de logiques de requête et d’analytique, des visualisations et des règles de collecte de données pour des scénarios comme l’audit de sécurité, les évaluations de l’intégrité et la gestion des alertes. Plus tard, Azure Operational Insights est devenu Log Analytics.  

En 2016, la préversion de Azure Monitor a été annoncée lors de la conférence Microsoft Ignite. Il offrait une infrastructure commune pour collecter les métriques de la plateforme, les journaux de diagnostic des ressources et les événements du journal d’activité au niveau de l’abonnement provenant de n’importe quel service Azure qui commençait à utiliser l’infrastructure. Auparavant, chaque service Azure avait sa propre méthode de supervision.

Lors de la conférence Microsoft Ignite de 2018, nous avons annoncé que la marque Azure Monitor s’étendait pour inclure plusieurs services différents développés à l’origine avec des fonctionnalités indépendantes :

- Le **Azure Monitor** d’origine permet de collecter des métriques de plateforme, des journaux de diagnostic des ressources et des journaux d’activité seulement pour les ressources de la plateforme Azure.
- **Application Insights**, pour la supervision des applications.
- **Log Analytics**, comme emplacement principal pour la collecte et l’analyse des données de journal.
- Un nouveau **service d’alerte unifié** qui regroupait les mécanismes d’alerte de chacun des autres services mentionnés précédemment.  
- **Azure Network Watcher** pour la supervision, le diagnostic et l’affichage des métriques pour les ressources d’un réseau virtuel.

## <a name="the-story-of-operations-management-suite-oms"></a>Histoire d’Operations Management Suite (OMS)

De 2015 à avril 2018, Operations Management Suite (OMS) était un regroupement des services de gestion Azure suivants pour la gestion des licences :

- Application Insights
- Azure Automation
- Sauvegarde Azure
- Operational Insights (renommé par la suite en Log Analytics)
- Site Recovery

Les fonctionnalités des services qui faisaient partie d’OMS n’ont pas changé quand OMS a été arrêté. Elles ont été réalignées sous Azure Monitor.

## <a name="infrastructure-requirements"></a>Exigences de l’infrastructure

### <a name="operations-manager"></a>Operations Manager

Operations Manager nécessite une infrastructure et une maintenance significatives pour prendre en charge un groupe d’administration, qui est une unité de fonctionnalités de base. Au minimum, un groupe d’administration se compose d’un ou plusieurs serveurs d’administration, d’une instance serveur SQL Server hébergeant la base de données de l’entrepôt de données opérationnelles et celles utilisées pour les rapports, et d’agents. La complexité de la conception d’un groupe d’administration dépend de plusieurs facteurs, comme l’étendue des charges de travail à superviser, et du nombre d’appareils ou d’ordinateurs qui prennent en charge les charges de travail. Si vous avez besoin d’une haute disponibilité et de la résilience du site, comme c’est généralement le cas avec les plateformes de supervision d’entreprise, les exigences en matière d’infrastructure et la maintenance associée peuvent croître considérablement.

![Diagramme d’un groupe d’administration Operations Manager](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor étant une offre SaaS (Software as a Service), son infrastructure sous-jacente s’exécute dans Azure et est gérée par Microsoft. Elle assure la supervision, l’analytique et les diagnostics à la bonne échelle. Elle est disponible sur tous les clouds nationaux. Les éléments principaux de l’infrastructure (collecteurs, magasins de métriques et de journaux, analytique) sur lesquels repose Azure Monitor sont gérés par Microsoft.  

![Diagramme d’Azure Monitor](./media/monitoring-management-guidance-cloud-and-on-premises/azure-monitor-greyed-optimized.svg)

## <a name="data-collection"></a>Collecte de données

<!-- markdownlint-disable MD024 -->

### <a name="operations-manager"></a>Operations Manager

#### <a name="agents"></a>Agents

Operations Manager collecte seulement les données directement à partir d’agents installés sur des [ordinateurs Windows](https://docs.microsoft.com/system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#windows-agent). Il peut accepter des données provenant du SDK Operations Manager, mais cette approche est généralement utilisée pour les partenaires qui étendent le produit avec des applications personnalisées, et non pas pour la collecte des données de supervision. Il peut collecter des données auprès d’autres sources, comme des [ordinateurs Linux](https://docs.microsoft.com/system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#linuxunix-agent) et des périphériques réseau, en utilisant des modules spéciaux qui s’exécutent sur l’agent Windows à distance pour accéder à ces autres périphériques.

![Diagramme de l’agent Operations Manager](./media/monitoring-management-guidance-cloud-and-on-premises/data-collection-opsman-agents-optimized.svg)

L’agent Operations Manager peut collecter auprès de plusieurs sources de données sur l’ordinateur local, comme le journal des événements, les journaux personnalisés et les compteurs de performance. Il peut également exécuter des scripts, qui peuvent collecter des données auprès de l’ordinateur local ou de sources externes. Vous pouvez écrire des scripts personnalisés pour collecter des données qui ne peuvent pas être collectées par d’autres moyens, ou auprès de différents appareils distants qui ne peuvent pas être supervisés autrement.

#### <a name="management-packs"></a>Packs d’administration

Operations Manager effectue toute la supervision avec des workflows (règles, moniteurs et découverte d’objets). Ces workflows sont regroupés dans un [pack d’administration](https://docs.microsoft.com/system-center/scom/manage-overview-management-pack?view=sc-om-2019) et déployés sur des agents. Les packs d’administration sont disponibles pour un large éventail de produits et de services, qui incluent des règles et des moniteurs prédéfinis. Vous pouvez également créer votre propre pack d’administration pour vos propres applications et vos scénarios personnalisés.

#### <a name="monitoring-configuration"></a>Configuration de la supervision

Les packs d’administration peuvent contenir des centaines de règles, de moniteurs, et de règles de découverte d’objets. Un agent exécute tous ces paramètres de supervision provenant de tous les packs d’administration qui s’appliquent, qui sont déterminés par des règles de découverte. Chaque instance de chaque paramètre de supervision s’exécute indépendamment et agit immédiatement sur les données qu’elle collecte. C’est ainsi qu’Operations Manager peut obtenir des alertes en quasi temps réel et l’état d’intégrité actuel des ressources supervisées.

Par exemple, un moniteur peut échantillonner un compteur de performance à des intervalles de quelques minutes. Si ce compteur dépasse un seuil, il définit immédiatement l’état d’intégrité de son objet cible, ce qui déclenche immédiatement une alerte dans le groupe d’administration. Une règle planifiée peut surveiller la création d’un événement particulier, puis déclencher immédiatement une alerte quand cet événement est créé dans le journal des événements local.

Comme ces paramètres de supervision sont isolés les uns des autres et qu’ils fonctionnent à partir des sources de données individuelles, Operations Manager a des difficultés à corréler les données entre plusieurs sources. Il est également difficile de réagir aux données une fois qu’elles ont été collectées. Vous pouvez exécuter des workflows qui accèdent à la base de données Operations Manager, mais ce scénario n’est pas courant et il est généralement utilisé pour un nombre limité de workflows ayant des objectifs spéciaux.

![Diagramme d’un groupe d’administration Operations Manager](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

#### <a name="data-sources"></a>Sources de données

Azure Monitor collecte des données auprès de différentes sources, notamment des ressources d’infrastructure et de plateforme Azure, des agents sur des ordinateurs Windows et Linux, et des données de supervision collectées dans Stockage Azure. Un client REST peut écrire des données de journal dans Azure Monitor en utilisant une API, et vous pouvez définir des métriques personnalisées pour vos applications web. Certaines données de métriques peuvent être routées vers différents emplacements, en fonction de leur utilisation. Par exemple, vous pouvez utiliser les données pour des alertes « aussi rapides que possible » ou pour une analyse de tendances à long terme en combinaison avec d’autres données des journaux.

#### <a name="monitoring-solutions-and-insights"></a>Solutions de supervision et insights

Les solutions de supervision utilisent la plateforme de journaux dans Azure Monitor pour assurer la supervision d’une application ou d’un service particulier. Ils définissent généralement la collecte des données auprès d’agents ou de services Azure, et fournissent des requêtes et des vues de journaux pour analyser ces données. En règle générale, elles ne fournissent pas de règles d’alerte, ce qui signifie que vous devez définir vos propres critères d’alerte en fonction des données collectées.

Les insights, comme Azure Monitor pour conteneurs et Azure Monitor pour machines virtuelles, utilisent la plateforme de journaux et de métriques d’Azure Monitor afin de fournir une expérience de supervision personnalisée pour une application ou un service dans le portail Azure. Ils peuvent fournir des conditions de supervision et d’alerte d’intégrité, en plus d’analyses personnalisées des données collectées.

#### <a name="monitoring-configuration"></a>Configuration de la supervision

Azure Monitor sépare la collecte de données et les actions effectuées sur ces données, et prend en charge les microservices distribués dans un environnement cloud. Il consolide les données provenant de plusieurs sources en une plateforme de données commune, et fournit des fonctionnalités d’analyse, de visualisation et d’alerte basées sur les données collectées.

Les données collectées par Azure Monitor sont stockées sous forme de journaux ou de métriques, auxquels font appel différentes fonctionnalités d’Azure Monitor. Les métriques contiennent les valeurs numériques de séries chronologiques bien adaptées aux alertes en quasi temps réel et à la détection rapide des problèmes. Les journaux contiennent des données texte ou numériques qui peuvent faire l’objet de requêtes au moyen d’un langage puissant particulièrement utile pour effectuer des analyses complexes.

Comme Azure Monitor dissocie la collecte de données des actions sur ces données, il est possible qu’il ne puisse pas fournir des alertes en quasi temps réel dans de nombreux cas. Pour alerter sur les données des journaux, les requêtes sont exécutées selon une planification périodique définie dans l’alerte. Ce comportement permet à Azure Monitor de corréler facilement les données de toutes les sources supervisées, et vous pouvez analyser les données de façon interactive de différentes manières. Ceci est particulièrement utile pour effectuer une analyse des causes racines et pour identifier l’endroit où un problème peut survenir.

## <a name="health-monitoring"></a>Surveillance de l’intégrité

### <a name="operations-manager"></a>Operations Manager

Dans Operations Manager, les packs d’administration incluent un modèle de service qui décrit les composants de l’application supervisée et leurs relations. Les moniteurs identifient l’état d’intégrité actuel de chaque composant en fonction des données et des scripts de l’agent. Les états d’intégrité sont agrégés pour vous permettre de voir rapidement l’état d’intégrité récapitulatif des ordinateurs et des applications supervisés.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor ne fournit pas de méthode définissable par l’utilisateur pour implémenter un modèle de service ou des moniteurs qui indiquent l’état d’intégrité actuel des composants des services. Comme les solutions de supervision sont basées sur les fonctionnalités standard d’Azure Monitor, elles ne fournissent pas de supervision au niveau des états. Les fonctionnalités suivantes d’Azure Monitor peuvent être utiles :

- **Application Insights :** Crée une carte composite de votre application web et fournit un état d’intégrité pour chaque composant ou dépendance de l’application. Ceci inclut l’état des alertes et l’exploration de diagnostics plus détaillés de votre application.

- **Azure Monitor pour machines virtuelles :** Fournit une expérience de supervision de l’intégrité pour les machines virtuelles Azure invitées, de façon similaire à Operations Manager, lors de la supervision de machines virtuelles Windows et Linux. Il évalue l’intégrité des composants clés des systèmes d’exploitation du point de vue de la disponibilité et des performances, afin de déterminer l’état d’intégrité actuel. Quand il détermine que la machine virtuelle invitée connaît une utilisation soutenue des ressources, un problème de capacité d’espace disque ou un problème lié aux fonctionnalités de base du système d’exploitation, il génère une alerte pour attirer votre attention sur cet état.

- **Azure Monitor pour conteneurs :** supervise les performances et l’intégrité d’Azure Kubernetes Service et d’Azure Container Instances. Cela collecte des métriques sur la mémoire et le processeur à partir des contrôleurs, des nœuds et des conteneurs qui sont disponibles dans Kubernetes via l’API Metrics. Il collecte également les journaux des conteneurs, et les données d’inventaire sur les conteneurs et leurs images. Des critères d’intégrité prédéfinis basés sur les données de performances collectées vous permettent de déterminer s’il existe un goulot d’étranglement des ressources ou un problème de capacité. Vous pouvez également comprendre les performances globales, ou les performances d’un type d’objet Kubernetes spécifique (pod, nœud, contrôleur ou conteneur).

## <a name="analyze-data"></a>Analyser des données

### <a name="operations-manager"></a>Operations Manager

Operations Manager fournit quatre méthodes de base pour analyser les données après leur collecte :

- **Explorateur d’intégrité :** Vous aide à découvrir les moniteurs qui identifient un problème d’état d’intégrité, et passer en revue les informations sur le moniteur et les causes possibles des actions qui lui sont associées.

- **Views :** Offre des visualisations prédéfinies des données collectées, comme un graphique des données de performances, ou une liste de composants supervisés et leur état d’intégrité actuel. Les vues de diagramme présentent visuellement le modèle de service d’une application.

- **Rapports :** Vous permettent de récapituler les données d’historique stockées dans l’entrepôt de données d’Operations Manager. Vous pouvez personnaliser les données sur lesquelles les vues et les rapports sont basés. Cependant, il n’existe pas de fonctionnalité permettant une analyse complexe ou interactive des données collectées.

- **Interface de commande d’Operations Manager :** Étend Windows PowerShell avec un ensemble supplémentaire d’applets de commande, et peut interroger et visualiser les données collectées. Ceci inclut des graphiques et d’autres visualisations, en mode natif avec PowerShell, ou avec la console web HTML d’Operations Manager.

### <a name="azure-monitor"></a>Azure Monitor

Avec le moteur d’analyse puissant d’Azure Monitor, vous pouvez travailler de manière interactive avec les données des journaux, et de les combiner avec d’autres données de supervision pour la recherche de tendances et d’autres analyses de données. Les vues et les tableaux de bord vous permettent de visualiser les données de requête de différentes façons à partir du portail Azure, et de les importer dans Power BI. Les solutions de supervision incluent des requêtes et des vues pour présenter les données qu’elles collectent. Les insights comme Application Insights, Azure Monitor pour machines virtuelles et Azure Monitor pour conteneurs incluent des visualisations personnalisées permettant la prise en charge de scénarios de supervision interactifs.

## <a name="alerting"></a>Génération d’alertes

### <a name="operations-manager"></a>Operations Manager

Operations Manager crée des alertes en réponse à des événements prédéfinis, quand un seuil de performance est atteint et quand l’état d’intégrité d’un composant supervisé change. Il comprend une gestion complète des alertes, ce qui vous permet de définir leur résolution et de les affecter à différents opérateurs ou ingénieurs système. Vous pouvez définir des règles de notification qui spécifient les alertes qui vont envoyer des notifications proactives.

Les packs d’administration incluent différentes règles d’alerte prédéfinies pour différentes conditions critiques dans l’application supervisée. Vous pouvez ajuster ces règles ou créer des règles personnalisées pour les besoins spécifiques de votre environnement.

### <a name="azure-monitor"></a>Azure Monitor

Avec Azure Monitor, vous pouvez créer des alertes basées sur une métrique qui dépasse un seuil ou sur le résultat d’une requête planifiée. Bien que les alertes basées sur des métriques puissent obtenir des résultats en quasi temps réel, les requêtes planifiées ont un temps de réponse plus long, en fonction de la vitesse d’ingestion et d’indexation des données. Au lieu d’être limitées à un agent spécifique, les alertes de requête de journal dans Azure Monitor vous permettent d’analyser des données parmi toutes les données stockées dans plusieurs espaces de travail. Ces alertes incluent également les données provenant d’une application Application Insights spécifique via l’utilisation d’une requête portant sur plusieurs espaces de travail.

Les solutions de supervision peuvent inclure des règles d’alerte, mais en général, vous les créez en fonction de vos propres besoins.

## <a name="workflows"></a>Workflows

### <a name="operations-manager"></a>Operations Manager

Les packs d’administration d’Operations Manager contiennent des centaines de workflows individuels, et déterminent les données à collecter et l’action à effectuer avec ces données. Par exemple, une règle peut échantillonner un compteur de performances à un intervalle de quelques minutes, en stockant ses résultats pour analyse. Un moniteur peut échantillonner le même compteur de performances et comparer sa valeur à un seuil pour déterminer l’état d’intégrité d’un objet supervisé. Une autre règle peut exécuter un script pour collecter et analyser des données sur un ordinateur d’agent, et déclencher une alerte s’il retourne une valeur particulière.

Les workflows dans Operations Manager sont indépendants les uns des autres, rendant donc difficile l’analyse portant sur plusieurs objets supervisés. Ces scénarios de supervision doivent être basés sur les données une fois qu’elles ont été collectées, ce qui est possible mais peut être difficile, et n’est donc pas courant.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor sépare la collecte des données, et les actions et l’analyse effectuées à partir de ces données. Les agents et d’autres sources de données écrivent les données de journal dans un espace de travail Log Analytics, et écrivent les données de métriques dans la base de données des métriques, sans aucune analyse de ces données ni connaissance de la façon dont elles peuvent être utilisées. Azure Monitor génère des alertes et effectue d’autres actions à partir des données stockées, ce qui vous permet d’effectuer des analyses sur des données provenant de toutes les sources.

## <a name="extend-the-base-platform"></a>Étendre la plateforme de base

### <a name="operations-manager"></a>Operations Manager

Operations Manager implémente toute la logique de supervision dans un pack d’administration, que vous créez vous-même, ou que vous obtenez auprès de nous ou d’un partenaire. Quand vous installez un pack d’administration, il découvre automatiquement les composants de l’application ou du service sur différents agents, et déploie les règles et les moniteurs appropriés. Le pack d’administration contient des définitions d’intégrité, des règles d’alerte, des règles de performances et de collecte d’événements, et des vues, afin de fournir une analyse complète prenant en charge le service ou l’application de l’infrastructure.

Le SDK Operations Manager permet à Operations Manager de s’intégrer à des plateformes de supervision de tiers ou à des logiciels de gestion des services informatiques (ITSM). Le SDK est également utilisé par certains packs d’administration de partenaires pour prendre en charge la supervision des périphériques réseau et pour fournir des expériences de présentation personnalisées, comme le tableau de bord Squared Up HTML5 ou l’intégration à Microsoft Office Visio.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor collecte les métriques et les journaux auprès de ressources Azure, avec peu ou pas de configuration. Les solutions de supervision ajoutent une logique pour la supervision d’une application ou d’un service, mais fonctionnent néanmoins toujours dans les requêtes et les vues de journaux standards d’Azure Monitor. Des insights, comme Application Insights et Azure Monitor pour machines virtuelles, utilisent la plateforme Azure Monitor pour la collecte et le traitement des données. Ils fournissent également des outils supplémentaires pour visualiser et analyser les données. Vous pouvez combiner des données collectées par des insights avec d’autres données, en utilisant des fonctionnalités de base d’Azure Monitor, comme les requêtes de journal et les alertes.

Azure Monitor prend en charge plusieurs méthodes pour collecter des données de supervision ou de gestion auprès d’Azure ou de ressources externes. Vous pouvez ensuite extraire et transférer des données de la métrique ou des magasins de journaux vers vos outils ITSM ou d’analyse. Sinon, vous pouvez effectuer des tâches d’administration à l’aide de l’API REST Azure Monitor.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Supervision des modèles de déploiement cloud](./cloud-models-monitor-overview.md)
