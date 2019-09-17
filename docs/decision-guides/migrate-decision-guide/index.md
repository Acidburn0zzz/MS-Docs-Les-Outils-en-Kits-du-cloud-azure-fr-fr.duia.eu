---
title: Guide de décision sur les outils de migration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Guide de décision sur les outils de migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.openlocfilehash: 17f462802a9ff5b44dfd734b299057649bbd797b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023844"
---
# <a name="migration-tools-decision-guide"></a>Guide de décision sur les outils de migration

La stratégie et les outils que vous utilisez pour effectuer la migration d’une application vers Azure dépendent en grande partie des motivations, des stratégies informatiques et des délais de l’entreprise. Ils nécessitent également une compréhension approfondie de la charge de travail réelle et des ressources (infrastructure, applications et données) en cours de migration. L’arbre de décision suivant a pour but de vous aider à sélectionner les outils les mieux adaptés en fonction de vos décisions de migration. Cet arbre de décision doit être pris comme un point de départ.

Le choix entre une migration à l’aide d’une technologie PaaS ou d’une technologie IaaS est déterminé par l’équilibre entre le coût, le temps, la dette technique existante et les rendements à long terme. La technologie IaaS est souvent le chemin le plus rapide vers le cloud et qui nécessite le moins de modifications à la charge de travail. La technologie PaaS peut nécessiter des modifications au niveau des structures de données ou du code source, mais elle génère d’importants rendements à long terme, qui se traduisent par une réduction des coûts d’exploitation et une plus grande flexibilité technique. Dans le diagramme suivant, le terme _moderniser_ est utilisé pour refléter une décision visant à moderniser une ressource pendant la migration et à effectuer sa migration vers une plateforme PaaS.

![Exemple de guide de décision sur les outils de migration](../../_images/migrate/migration-tools-decision-tree.png)

## <a name="key-questions"></a>Questions clés

En répondant aux questions suivantes, vous pourrez prendre des décisions en vous basant sur l’arbre ci-dessus.

- **La modernisation de la plateforme d’application pendant la migration est-elle un bon investissement si l’on considère le temps, l’énergie et le budget nécessaires ?** Les technologies PaaS, comme Azure App Service ou Azure Functions, peuvent améliorer la flexibilité du déploiement et réduire la complexité de la gestion des machines virtuelles qui hébergent des applications. Toutefois, les applications peuvent nécessiter une refactorisation avant de pouvoir tirer parti de ces fonctionnalités cloud natives, ce qui peut accroître le temps nécessaire à la migration ainsi que les coûts. Si votre application peut être migrée vers des technologies PaaS sans entraîner de nombreuses modifications, elle peut facilement faire l’objet d’une modernisation. Si une refactorisation étendue est nécessaire, il est sans doute préférable d’effectuer une migration à l’aide de machines virtuelles IaaS.
- **La modernisation de la plateforme de données pendant la migration est-elle un bon investissement si l’on considère le temps, l’énergie et le budget nécessaires ?** Comme pour la migration d’applications, les options de stockage managé Azure PaaS, telles qu’Azure SQL Database, Cosmos DB et Stockage Azure, offrent de nombreux avantages en termes de gestion et de flexibilité. Toutefois, la migration vers ces services peut nécessiter la refactorisation des données existantes et des applications qui utilisent ces données. Les plateformes de données nécessitent souvent beaucoup moins de refactorisation que les plateformes d’applications. Par conséquent, il est très courant que les plateformes de données soient modernisées, même si la plateforme d’application reste la même. Si vos données peuvent faire l’objet d’une migration vers un service de données managé sans nécessiter de nombreuses modifications, elles peuvent facilement faire l’objet d’une modernisation. Pour les données dont la refactorisation nécessite plus de temps et implique des coûts plus élevés pour utiliser ces services PaaS, il est sans doute préférable d’effectuer leur migration à l’aide de machines virtuelles IaaS, afin de mieux s’aligner sur les fonctionnalités d’hébergement existantes.
- **Votre application est-elle actuellement exécutée sur des machines virtuelles dédiées ou est-elle hébergée avec d’autres applications ?** Les applications exécutées sur des machines virtuelles dédiées peuvent être plus facilement migrées vers des options d’hébergement PaaS que les applications qui sont exécutées sur des serveurs partagés.
- **La migration de vos données va-t-elle dépasser la capacité de votre bande passante réseau ?** La capacité réseau entre Azure et vos sources de données locales peut représenter un goulot d’étranglement lors d’une migration de données. Si les données que vous devez transférer font face à des limitations de bande passante qui empêchent une migration efficace ou en temps voulu, vous devrez chercher des alternatives ou des mécanismes de transfert hors connexion. Dans le Framework d’adoption du cloud, l’[article sur la réplication de la migration](../../migrate/migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) explique comment les limites de réplication peuvent affecter la migration. Dans le cadre de votre évaluation de la migration, consultez vos équipes informatique pour vérifier que votre bande passante locale et WAN est capable de prendre en charge votre migration. Consultez également le [scénario de migration à cadre étendu lorsque les besoins de stockage dépassent la capacité réseau lors d’une migration](../../migrate/expanded-scope/network-capacity-exceeded.md#suggested-prerequisites).
- **Votre application utilise-t-elle un pipeline DevOps existant ?** Dans de nombreux cas, les pipelines Azure peuvent être facilement refactorisés pour déployer des applications dans des environnements d’hébergement basés sur le cloud.
- **Vos données ont-elles des exigences de stockage complexes ?** Les applications de production nécessitent généralement un stockage de données hautement disponible, qui offre toujours des fonctionnalités ainsi qu’un niveau de disponibilité et de continuité similaires. Les options de base de données Azure PaaS, telles que Azure SQL Database, Azure Database pour MySQL et Azure Cosmos DB, offrent des contrats de niveau de service avec une disponibilité de 99,99 %. À l’inverse, les instances SQL Server basées sur IaaS qui se trouvent sur des machines virtuelles Azure offrent des contrats de niveau de service à instance unique avec une disponibilité de 99,95 %. Si vos données ne peuvent pas être modernisées pour utiliser les options de stockage PaaS, la garantie d’une disponibilité IaaS plus élevée va nécessiter des scénarios de stockage de données plus complexes, comme l’exécution de clusters AlwaysOn SQL Server et la synchronisation continue des données des différentes instances. Cela peut impliquer des coûts d’hébergement et de maintenance élevés. Par conséquent, lorsque vous envisagez les différentes options de migration, il est important de trouver le juste équilibre entre exigences de disponibilité, efforts de modernisation et impact global sur le budget.

## <a name="innovation-and-migration"></a>Innovation et migration

Conformément à l’importance qui est donnée à la [migration incrémentielle](../../migrate/index.md#migration-implementation) dans le Framework d’adoption du cloud, une première décision concernant les outils et la stratégie de migration n’empêche pas de futurs efforts d’innovation afin de mettre à jour une application en vue de tirer parti des opportunités offertes par la plateforme Azure. Même si la première migration peut se concentrer principalement sur le réhébergement à l’aide d’une approche IaaS, vous devez prévoir de revisiter régulièrement votre portefeuille d’applications hébergées dans le cloud afin d’étudier les opportunités d’optimisation.

## <a name="learn-more"></a>En savoir plus

- **[Principes de base du cloud : Vue d’ensemble des options de calcul Azure](https://docs.microsoft.com/azure/architecture/guide/technology-choices/compute-overview)** . Fournit des informations sur les fonctionnalités des options de calcul Azure IaaS et PaaS.
- **[Principes de base du cloud : Choisir le bon magasin de données](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview)** . Décrit les options de stockage PaaS qui sont disponibles sur la plateforme Azure.
- **[Migration à cadre étendu : les besoins en stockage dépassent la capacité réseau lors d’une migration](../../migrate/expanded-scope/network-capacity-exceeded.md)** . Décrit les autres mécanismes de migration de données pour les cas où la migration des données est entravée par la quantité de bande passante réseau disponible.
- **[Base de données SQL : Choisir l’option SQL Server appropriée dans Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas#business-motivations-for-choosing-databases-managed-instances-or-sql-virtual-machines)** . Aborde les options et les justifications métier permettant de choisir entre une infrastructure hébergée (IaaS) ou un service hébergé (PaaS) pour héberger vos charges de travail SQL Server.