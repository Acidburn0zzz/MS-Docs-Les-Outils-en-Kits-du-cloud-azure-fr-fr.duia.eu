---
title: Guide de gouvernance pour les entreprises complexes
description: Suivez une entreprise complexe fictive à différents stades de maturité de gouvernance à mesure qu’elle définit un produit minimum viable (MVP) sur la base de bonnes pratiques.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 257b915e579136e64ae88262a3debdb0b2dbb527
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220173"
---
# <a name="governance-guide-for-complex-enterprises"></a>Guide de gouvernance pour les entreprises complexes

## <a name="overview-of-best-practices"></a>Vue d’ensemble des bonnes pratiques

Ce guide de gouvernance suit les expériences d’une entreprise fictive à différents stades de maturité. Il est basé sur les expériences de clients réels. Les meilleures pratiques recommandées se fondent sur les contraintes et les besoins de l’entreprise fictive.

Comme point de départ rapide, cette présentation définit un produit minimum viable (MVP) pour la gouvernance, basé sur les meilleures pratiques. Elle fournit également des liens vers des améliorations de gouvernance, qui ajoutent des bonnes pratiques à mesure que de nouveaux risques métier ou techniques émergent.

> [!WARNING]
> Ce MVP est un point de départ de base, qui se fonde sur un ensemble de postulats. Même cet ensemble minimal de meilleures pratiques se fonde sur des stratégies d’entreprise, qui sont axées sur des risques métier et des tolérances aux risques uniques. Pour déterminer si ces postulats s’appliquent à vous, lisez la [plus longue description](./narrative.md) qui suit cet article.

### <a name="governance-best-practices"></a>Bonnes pratiques de gouvernance

Ces bonnes pratiques servent de base sur laquelle une organisation peut s’appuyer pour ajouter de manière cohérente et rapide des garde-fous en matière de gouvernance à plusieurs abonnements Azure.

### <a name="resource-organization"></a>Organisation des ressources

Le schéma suivant montre la hiérarchie MVP de gouvernance pour organiser les ressources.

![Schéma d’organisation des ressources](../../../_images/govern/resource-organization.png)

Chaque application doit être déployée dans la zone appropriée du groupe d’administration, de l’abonnement et de la hiérarchie des groupes de ressources. Lors de la planification du déploiement, l’équipe de gouvernance cloud crée les nœuds nécessaires dans la hiérarchie pour donner aux équipes d’adoption du cloud les moyens d’agir.

1. Définissez un groupe d’administration pour chaque unité commerciale avec une hiérarchie détaillée qui reflète d’abord la géographie, puis le type d’environnement (par exemple, environnements de production ou de non-production).

1. Créez un abonnement de production et un abonnement de non-production pour chaque combinaison unique de géographie ou d’unité commerciale distincte. La création de plusieurs abonnements nécessite une attention particulière. Pour plus d’informations, consultez le [Guide de décision concernant les abonnements](../../../decision-guides/subscriptions/index.md).

1. Appliquez une [nomenclature cohérente](../../../ready/azure-best-practices/naming-and-tagging.md) à chaque niveau de cette hiérarchie de regroupement.

1. Les groupes de ressources doivent être déployés de manière à prendre en compte le cycle de vie de leur contenu. Les ressources développées, gérées et retirées ensemble appartiennent au même groupe de ressources. Pour plus d’informations sur les bonnes pratiques en matière d’utilisation de groupes de ressources, consultez [cette page](../../../decision-guides/resource-consistency/index.md).

1. Le [choix de la région](../../../migrate/azure-best-practices/multiple-regions.md) est extrêmement important, notamment pour la mise en place du réseau, de la supervision et de l’audit pour le basculement/la restauration automatique. Il convient également de vérifier que les [références SKU nécessaires](https://azure.microsoft.com/global-infrastructure/services) sont disponibles dans les régions privilégiées.

![Schéma d’organisation des ressources des grandes entreprises](../../../_images/govern/large-enterprise-resource-organization.png)

Ces modèles autorisent la croissance sans compliquer inutilement la hiérarchie.

[!INCLUDE [governance-of-resources](../../../../includes/governance-of-resources.md)]

<!-- See comments for suggestion to possibly add here -->

## <a name="incremental-governance-improvements"></a>Améliorations incrémentielles de la gouvernance

Une fois que ce MVP a été déployé, des couches supplémentaires de gouvernance peuvent être rapidement intégrées à l’environnement. Voici quelques méthodes permettant d’améliorer le MVP afin de répondre aux besoins spécifiques de l’entreprise :

- [Base de référence de sécurité pour les données protégées](./security-baseline-improvement.md)
- [Configurations des ressources pour les applications critiques](./resource-consistency-improvement.md)
- [Contrôles pour la gestion des coûts](./cost-management-improvement.md)
- [Contrôles pour l’amélioration incrémentielle multicloud](./multicloud-improvement.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>Que fournit ce guide ?

Dans le MVP, les pratiques et les outils venant de la discipline [Accélération du déploiement](../../deployment-acceleration/index.md) ont été conçus pour appliquer rapidement la stratégie d’entreprise. Plus précisément, le MVP utilise Azure Blueprints, Azure Policy et les groupes d’administration Azure pour appliquer quelques stratégies d’entreprise basiques, comme le définit le scénario pour cette entreprise fictive. Ces stratégies d’entreprise sont appliquées à l’aide de modèles Azure Resource Manager et de stratégies Azure afin d’établir une petite base de référence pour les identités et la sécurité.

![Exemple de MVP de gouvernance incrémentielle](../../../_images/govern/governance-mvp.png)

## <a name="incremental-improvements-to-governance-practices"></a>Amélioration incrémentielle des pratiques de gouvernance

Au fil du temps, ce MVP de gouvernance servira à améliorer de façon incrémentielle les pratiques de gouvernance. À mesure que le processus d’adoption avance, les risques métier augmentent. Différentes disciplines au sein du modèle de gouvernance du Framework d’adoption du cloud s’adapteront pour gérer ces risques. D’autres articles de cette série traitent des changements de la stratégie d’entreprise et de son impact sur l’entreprise fictive. Ces changements se produisent dans quatre disciplines :

- Base de référence des identités, à mesure que les dépendances de migration changent dans le scénario.
- La gestion des coûts, à mesure que l’adoption avance.
- La base de référence de la sécurité, à mesure que les données protégées sont déployées.
- La cohérence des ressources, à mesure que les opérations informatiques commencent à gérer les charges de travail critiques.

![Exemple de MVP de gouvernance incrémentielle](../../../_images/govern/governance-improvement-large.png)

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous connaissez le MVP de gouvernance et les changements de gouvernance à venir, lisez le scénario correspondant pour en savoir plus.

> [!div class="nextstepaction"]
> [Lire le scénario correspondant](./narrative.md)
