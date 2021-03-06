---
title: 'Bien démarrer : Gérer les coûts du cloud'
description: Découvrez les principes de base de la gestion des coûts associés à l’adoption du cloud.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 456d5ecbe31d23731515821943da02861144bffe
ms.sourcegitcommit: 070e6a60f05519705828fcc9c5770c3f9f986de5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83814541"
---
# <a name="get-started-manage-cloud-costs"></a>Bien démarrer : Gérer les coûts du cloud

La discipline de gouvernance cloud Gestion des coûts est axée sur l'établissement de budgets, la supervision des modèles d'allocation des coûts et l'implémentation de contrôles visant à améliorer les comportements de dépense cloud à l'échelle du portefeuille informatique. L'optimisation des coûts d'entreprise implique de nombreux autres rôles et fonctions pour réduire les coûts et équilibrer les besoins en matière de scalabilité, de performances, de sécurité et de fiabilité. Ce guide de démarrage rapide mappe ces différentes fonctions de soutien afin de contribuer à établir un alignement entre les équipes impliquées.

Toutefois, l’optimisation des coûts d’entreprise implique de nombreux autres rôles et fonctions pour réduire les coûts et équilibrer les besoins en matière de scalabilité, de performances, de sécurité et de fiabilité. Cet article mappe ces fonctions de soutien pour contribuer à établir un alignement entre les équipes impliquées.

La gouvernance est la pierre angulaire de l’optimisation des coûts au sein d’une grande entreprise. La section suivante décrit les recommandations en matière d’optimisation des coûts dans le contexte de la gouvernance. Les étapes suivantes permettent à chaque équipe de prendre des mesures qui ciblent son rôle dans le cadre de l'optimisation des coûts. Ensemble, ces étapes aideront votre organisation à s'engager sur la voie de l'optimisation des coûts.

![Bien démarrer avec la gestion des coûts d’entreprise](../_images/get-started/cost-map.png)

## <a name="step-1-optimize-enterprise-costs"></a>Étape 1 : Optimiser les coûts d'entreprise

L'équipe de gouvernance cloud est bien préparée à évaluer les dépenses excessives ou non planifiées et à agir en conséquence par le biais d'une combinaison de supervision des performances, de réduction du dimensionnement des ressources, et d'arrêt sécurisé des ressources inutilisées. L’optimisation des coûts d’entreprise commence par une compréhension d’équipe partagée des outils, des processus et des dépendances nécessaires pour agir judicieusement afin de répondre aux préoccupations en matière de coût à l’échelle de l’environnement.

**Livrables :**

- Implémenter des changements de gestion des coûts intelligents à l’échelle de l’entreprise.
- Documenter vos stratégies de gestion des coûts, vos processus et vos orientations en matière de conception dans le [Modèle de discipline Gestion des coûts](../govern/cost-management/template.md).

Ces livrables sont le résultat de quelques tâches récurrentes :

- Garantir l’alignement stratégique avec l’équipe de stratégie cloud (qui comprend les parties prenantes de la charge de travail dans le portefeuille)
- Optimiser les coûts à l'échelle de l'environnement :
  - Arrêter manuellement ou automatiquement les machines virtuelles inutilisées
  - Supprimer ou désallouer les machines virtuelles arrêtées
  - Garantir le dimensionnement approprié des ressources
  - Aligner les dépenses sur les attentes budgétaires
- Valider toute modification architecturale par le biais de Microsoft Azure Well-Architected Review pour faciliter la conversation avec les propriétaires techniques des charges de travail

**Conseils relatifs aux livrables :**

- Vérifiez que toutes les charges de travail et ressources respectent les [conventions d'affectation de noms et de balisage appropriées](../ready/azure-best-practices/naming-and-tagging.md). [Appliquez les conventions de balisage à l'aide d'Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags), avec un accent particulier sur les balises de « centre de coûts » et « propriétaire technique ».
- Examinez et appliquez régulièrement les [bonnes pratiques de gestion des coûts](../govern/cost-management/best-practices.md) afin de guider l’analyse et les améliorations au sein de l’entreprise. Voici quelques-unes des pratiques de gouvernance les plus percutantes :

  - Agissez sur les [bonnes pratiques générales en matière de coût](../govern/cost-management/best-practices.md) afin de réduire le dimensionnement et les coûts et d'arrêter les machines inutilisées.
  - Appliquez les [avantages liés à un environnement hybride](../govern/cost-management/best-practices.md#best-practice-take-advantage-of-azure-hybrid-benefit) pour réduire les coûts de licence.
  - Alignez les [instances réservées](../govern/cost-management/best-practices.md#best-practice-use-reserved-vm-instances) pour réduire les coûts liés aux ressources.
  - [Supervisez l'utilisation des ressources](../govern/cost-management/best-practices.md#best-practice-monitor-resource-utilization) pour réduire l'impact sur les performances des ressources.
  - [Réduisez les coûts de non-production](../govern/cost-management/best-practices.md#best-practice-reduce-nonproduction-costs) par le biais de stratégies visant à régir les environnements de non-production.
  - Agissez suite aux [recommandations en matière d’optimisation des coûts](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json).

- Des compromis au niveau des charges de travail peuvent être nécessaires pour implémenter des modifications d’optimisation des coûts efficaces. [Microsoft Azure Well-Architected Framework](https://docs.microsoft.com/azure/architecture/framework/cost/tradeoffs) et [Microsoft Azure Well-Architected Review](https://docs.microsoft.com/assessments/?id=azure-architecture-review) peuvent guider ces conversations avec le propriétaire technique d'une charge de travail spécifique.
- Si vous débutez en matière de gouvernance cloud, établissez des [disciplines, des processus et des stratégies de gouvernance](../govern/index.md) à l'aide de la méthodologie de gouvernance.
- Si vous débutez dans la discipline Gestion des coûts, vous pouvez consulter l'[article consacré aux améliorations de la gestion des coûts](../govern/guides/complex/cost-management-improvement.md), en vous concentrant sur la section portant sur l'[implémentation](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices).

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes responsable et de support |
| --- | --- |
| <li> Équipe de gouvernance cloud | <li> Équipe de stratégie cloud <li> Équipe d’adoption du cloud <li> Centre d’excellence du cloud ou équipe informatique centrale |

L’équipe de gouvernance peut détecter et réduire considérablement les coûts dans la plupart des entreprises. Un dimensionnement des ressources de base piloté par les données peut avoir un impact immédiat et mesurable sur les coûts.

Comme indiqué dans [Construire une organisation sensible aux coûts](../organize/cost-conscious-organization.md), l'accent mis à l'échelle de l'entreprise sur la gestion et l'optimisation des coûts peut offrir une plus grande valeur ajoutée. Les étapes suivantes montrent comment les différentes équipes peuvent vous aider à développer une organisation sensible aux coûts.

## <a name="step-2-define-a-strategy"></a>Étape 2 : Définir une stratégie

Les décisions stratégiques affectent directement les contrôles des coûts, tout au long du cycle de vie de l’adoption et jusqu’aux opérations à long terme. La clarté stratégique permet d’améliorer les efforts d’optimisation des coûts pilotés par l’équipe de gouvernance.

**Livrables :**

- Enregistrer les motivations, les résultats et les justifications métier dans le [modèle de stratégie et de plan](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).
- Créer votre premier budget à l'aide d'Azure Cost Management.

**Conseils relatifs aux livrables :**

- [Comprendre les motivations](../strategy/motivations.md). Les événements métier critiques et certaines motivations de migration ont tendance à être sensibles aux coûts, ce qui accroît l'importance du contrôle des coûts pour tous les efforts ultérieurs. D’autres motivations à long terme liées à l’innovation ou à la croissance pendant la migration peuvent être étudiées sous l’angle du chiffre d’affaires. La compréhension des motivations vous aidera à déterminer la propriété à affecter à la gestion des coûts.
- [Résultats métiers](../strategy/business-outcomes/index.md) : Certains résultats budgétaires ont tendance à être extrêmement sensibles aux coûts. Lorsque les résultats souhaités correspondent aux métriques budgétaires, vous devez investir très tôt dans la discipline de gouvernance Gestion des coûts.
- [Justification métier](../strategy/cloud-migration-business-case.md). La justification métier fait office de vue générale du plan financier pour l'adoption du cloud. Il s’agit d’une bonne source pour les efforts de budgétisation initiaux.

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes responsable et de support |
| --- | --- |
| <li> Équipe de stratégie cloud | <li> Équipe de gouvernance cloud <li> Équipe d’adoption du cloud <li> Centre d’excellence du cloud ou équipe informatique centrale |

## <a name="step-3-develop-a-cloud-adoption-plan"></a>Étape 3 : Développer un plan d’adoption du cloud

Le plan d’adoption offre une clarté quant au calendrier des activités pendant l’adoption. L’alignement du plan et de l’analyse du patrimoine numérique vous permet de prévoir la croissance mensuelle de vos dépenses. Cela aide également votre équipe de gouvernance cloud à aligner les processus et à identifier les modèles de dépense.

**Livrables :**

- Effectuer les étapes 1 à 6 de la création d’un [plan d’adoption du cloud](../plan/plan-intro.md#build-your-cloud-adoption-plan).
- Collaborer avec votre équipe de gouvernance cloud pour affiner les budgets et créer des prévisions de dépenses réalistes.

**Conseils pour la prise en charge de l’achèvement des livrables :**

- [Collecter des données d’inventaire](../digital-estate/inventory.md). Établissez une source de données pour l'analyse du patrimoine numérique avant l'adoption.
- [Meilleure pratique : Azure Migrate](../plan/contoso-migration-assessment.md). Utilisez Azure Migrate pour collecter l’inventaire.
- [Rationalisation incrémentielle](../digital-estate/rationalize.md#incremental-rationalization) : Au cours de la rationalisation incrémentielle et de l’analyse quantitative, identifiez les candidats au cloud à des fins de budgétisation.
- [Aligner les modèles de coût et les modèles de prévision](../digital-estate/calculate.md). Utilisez Azure Cost Management pour aligner les modèles de coût et de prévision en [créant des budgets](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json).
- [Créer votre plan d’adoption du cloud](../plan/plan-intro.md#build-your-cloud-adoption-plan). Créez un plan avec des détails de calendrier, de charges de travail et de ressources actionnables. Ce plan sert de base aux dépenses dans le temps (ou à la prévision des coûts). Les _dépenses dans le temps_ constituent la référence initiale pour toutes les analyses d'optimisation actionnables au sein de la discipline de gouvernance Gestion des coûts.

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes responsable et de support |
| --- | --- |
| <li> Équipe d’adoption du cloud | <li> Équipe de stratégie cloud <li> Équipe de gouvernance cloud <li> Centre d’excellence du cloud ou équipe informatique centrale |

## <a name="step-4-implement-best-practices-for-landing-zones"></a>Étape 4 : Implémenter les meilleures pratiques pour les zones d'atterrissage

La méthodologie de préparation de l'infrastructure Microsoft Cloud Adoption Framework pour Azure se concentre principalement sur le développement de zones d'atterrissage pour héberger des charges de travail dans le cloud. Pendant l'implémentation des zones d'atterrissage, l'organisation doit envisager diverses décisions pour optimiser les coûts.

**Livrables :**

- Déployer une ou plusieurs zones d'atterrissage susceptibles d'héberger des charges de travail dans le plan d'adoption à court terme.
- Vérifier que toutes les zones d'atterrissage sont conformes aux décisions d'optimisation des coûts et aux exigences de gestion des coûts.

**Conseils relatifs aux livrables :**

- [Suivre les coûts](../ready/azure-best-practices/track-costs.md#provide-the-right-level-of-cost-access). Établissez une hiérarchie d’environnement bien gérée, fournissez le niveau d’accès aux coûts approprié et utilisez des ressources de gestion des coûts supplémentaires dans chaque zone d’atterrissage.
- [Optimiser votre investissement dans le cloud](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Familiarisez-vous avec les bonnes pratiques afin d’optimiser les investissements.
- [Créer et gérer des budgets](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Familiarisez-vous avec les bonnes pratiques en matière de création et de gestion des budgets.
- [Optimiser les coûts à partir de recommandations](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Familiarisez-vous avec les bonnes pratiques en matière de respect des recommandations qui vous permettront d’optimiser les coûts.
- [Superviser l’utilisation et les dépenses](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Familiarisez-vous avec les bonnes pratiques en matière de supervision de l'utilisation et des dépenses au sein d'une zone d'atterrissage.

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes responsable et de support |
| --- | --- |
| <li> Équipe d’adoption du cloud | <li> Équipe de stratégie cloud <li> Équipe de gouvernance cloud <li> Centre d’excellence du cloud ou équipe informatique centrale |

## <a name="step-5-complete-waves-of-migration-effort"></a>Étape 5 : Terminer les vagues de l’effort de migration

La migration est un processus reproductible exécuté par l’équipe d’adoption du cloud. Tout au long de ce processus, il existe de nombreuses opportunités pour optimiser les coûts dans votre portefeuille. Une grande partie de ces décisions in-process sont appliquées à un petit groupe de charges de travail lors de chaque vague ou itération de migration.

**Livrables :**

- Créer un benchmark, tester, redimensionner et déployer une collection de charges de travail entièrement optimisées.

**Conseils relatifs aux livrables :**

- Des [mécanismes de contrôle des coûts axés sur la migration](../migrate/azure-migration-guide/manage-costs.md) fournissent des insights sur les contrôles d'optimisation des coûts natifs du cloud qui vous aideront lors de la migration.
- [Bonnes pratiques pour l'optimisation du coût des charges de travail migrées](../migrate/azure-best-practices/migrate-best-practices-costs.md) contient une check-list de 14 bonnes pratiques à respecter avant et après la migration afin d'optimiser les coûts de chaque mise en production de charge de travail.

Les coûts d'exploitation à long terme sont un thème commun dans chaque domaine d'améliorations du processus de migration. Cette liste d'améliorations du processus est organisée par phase du processus de migration :

- [Prérequis](../migrate/migration-considerations/prerequisites/index.md) fournit des informations sur la gestion des modifications et du backlog qui influencent les coûts du cloud budgétés et réels.
- [Évaluer](../migrate/migration-considerations/assess/index.md) fournit six processus spécifiques qui vont de la validation des hypothèses à la compréhension des options des partenaires. Chaque processus influence les opportunités d'optimisation du cloud.
- [Migrer](../migrate/migration-considerations/migrate/index.md) contient une suggestion de processus sur la correction des ressources. Cette suggestion offre la possibilité d'optimiser l'état configuré, en faveur d'une solution optimisée.
- [Promouvoir](../migrate/migration-considerations/optimize/index.md) se concentre fortement sur les tests, le redimensionnement, la validation et la publication des ressources migrées, ainsi que sur la désactivation des ressources hors service. Il s’agit du premier point clair auquel les prévisions et les budgets peuvent être testés par rapport aux performances et à la configuration réelles.

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes responsable et de support |
| --- | --- |
| <li> Équipe d’adoption du cloud | <li> Équipe de stratégie cloud <li> Équipe de gouvernance cloud <li> Centre d’excellence du cloud ou équipe informatique centrale |

## <a name="step-6-drive-customer-focused-innovation"></a>Étape 6 : Stimuler l’innovation axée sur le client

L'innovation et le développement de nouveaux produits nécessitent un examen architectural bien plus approfondi. Le Cloud Adoption Framework fournit des détails sur le processus d’innovation et la réflexion sur la gestion des produits. Les décisions d'optimisation des coûts concernant les nouvelles innovations sont pour la plupart hors de la portée de ce guide.

**Livrables :**

- Prendre des décisions architecturales clés sur les nouvelles innovations afin d'équilibrer les considérations de coûts et d'autres considérations critiques en matière de conception.

**Conseils relatifs aux livrables :**

- Utilisez [Microsoft Azure Well-Architected Review](https://docs.microsoft.com/assessments/?id=azure-architecture-review) pour comprendre l'équilibre entre les différentes décisions en matière d'architecture.
- Pour obtenir des conseils plus détaillés sur l'optimisation des coûts dans le cadre de l'innovation, consultez [Microsoft Azure Well-Architected Review](https://docs.microsoft.com/azure/architecture/framework).

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes responsable et de support |
| --- | --- |
| <li> Équipe d’adoption du cloud | <li> Équipe de stratégie cloud <li> Équipe de gouvernance cloud <li> Centre d’excellence du cloud ou équipe informatique centrale |

## <a name="step-7-implement-sound-operations"></a>Étape 7 : Implémenter des opérations fiables

L'établissement d'une solide base de référence vous aidera à collecter des données et à créer des alertes opérationnelles. Cet effort peut aider à détecter les opportunités d'optimisation des coûts. Il créera un équilibre entre la résilience et l'optimisation des coûts.

**Livrables :**

- Superviser votre environnement d’entreprise afin d’obtenir des recommandations d’optimisation des coûts continues, alignées sur les classifications de criticité et de résilience de chaque charge de travail.

**Conseils pour la prise en charge de l’achèvement des livrables :**

- [Créez un alignement métier](../manage/considerations/business-alignment.md) afin de clarifier la criticité et l’appétit pour les investissements de résilience.

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes responsable et de support |
| --- | --- |
| <li> Équipe des opérations cloud | <li> Équipe de stratégie cloud <li> Équipe de gouvernance cloud <li> Centre d’excellence du cloud ou équipe informatique centrale |

## <a name="value-statement"></a>Énoncé de la valeur

Les étapes suivantes peuvent vous aider à [construire une organisation sensible aux coûts](../organize/cost-conscious-organization.md). L'optimisation des coûts est plus facile à implémenter lorsqu'une organisation utilise la propriété partagée et une approche collaborative avec les bonnes équipes au bon moment.
