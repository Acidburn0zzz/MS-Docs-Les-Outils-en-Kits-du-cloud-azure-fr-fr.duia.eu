---
title: "Bien démarrer : Débloquer la conception et la configuration de l'environnement"
description: Familiarisez-vous avec la conception et la configuration de votre environnement cloud.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 761c6c7a8bed468a7d2c9005365a815fbe48e8ae
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83752881"
---
# <a name="get-started-design-and-configuration"></a>Bien démarrer : Conception et configuration

La conception et la configuration de l'environnement sont les obstacles les plus courants aux efforts d'adoption axés sur la migration ou l'innovation. Il peut être difficile d'implémenter rapidement une conception capable de soutenir votre plan d'adoption à long terme. Cet article présente une approche et une série d'étapes à suivre pour surmonter les obstacles courants et accélérer les efforts d'adoption.

![Prise en main de la conception et de la configuration](../_images/get-started/environment-map.png)

Les efforts techniques nécessaires à l'élaboration d'une conception et d'une configuration efficaces peuvent être complexes. Ils peuvent cependant être gérés de manière à améliorer les chances de succès de l'équipe chargée de la plateforme cloud. Le principal défi est l'alignement entre les différentes parties prenantes. Certaines d'entre elles sont en mesure d'arrêter ou de freiner les efforts d'adoption. Les étapes suivantes décrivent les moyens d'atteindre rapidement les objectifs à court terme et de réussir à long terme.

## <a name="step-1-document-the-business-strategy"></a>Étape 1 : Documenter la stratégie d'entreprise

Pour éviter les points de blocage de migration courants, assurez-vous de disposer d'une stratégie d'entreprise claire et concise. L'alignement des parties prenantes sur les motivations, les résultats opérationnels attendus et la justification métier est important tout au long du processus d'adoption et de configuration de l'environnement.

Une stratégie d'entreprise claire et concise permet à l'équipe chargée de la plateforme cloud d'identifier les points importants et les priorités lors des décisions qu'elle est amenée à prendre en matière de configuration de l'environnement. Elle aide notamment les équipes à se positionner lorsqu'il leur faut faire un choix entre vitesse d'innovation et respect des contrôles.

**Livrables :**

- Utilisez le [modèle de stratégie et de plan](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) pour consigner les motivations, les résultats opérationnels souhaités et la principale justification métier.

**Conseils relatifs aux livrables :**

- [Motivations](../strategy/motivations.md) : La première étape de l’alignement stratégique consiste à s'entendre sur les motivations qui sous-tendent l’effort de migration. Commencez par identifier et classer les motivations et les thèmes communs aux différentes parties prenantes au sein des équipes commerciales et informatiques.
- [Résultats opérationnels](../strategy/business-outcomes/index.md) : Une fois les motivations alignées, il est possible de capturer les résultats métier souhaités. Ces informations fournissent des métriques claires que vous pouvez utiliser pour mesurer la transformation globale.
- [Élaboration d'une analyse de rentabilisation sur la migration vers le cloud](../strategy/cloud-migration-business-case.md) : Il s'agit d'un bon point de départ pour développer une analyse de rentabilisation sur la migration, avec des précisions sur les formules et outils qui peuvent étayer la justification métier.

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes en charge et équipes de soutien | Équipes informées |
| --- | --- | --- |
| <li> Équipe de stratégie cloud | <li> Équipe d’adoption du cloud <li> Centre d'excellence du cloud ou équipe informatique centrale | <li> Équipe de plateforme cloud |

## <a name="step-2-assess-the-digital-estate"></a>Étape 2 : Évaluer le patrimoine numérique

La découverte et l’évaluation offrent un niveau d’alignement technique plus approfondi, qui vous aide à élaborer un plan d’action que vous pouvez utiliser pour la mise en œuvre de la stratégie. Au cours de cette étape, vous validez l’analyse de rentabilité en utilisant des données sur l’état actuel de l'environnement. Ensuite, vous effectuez une analyse quantitative de ces données et une évaluation qualitative approfondie des charges de travail ayant la priorité la plus élevée.

Les résultats de l'évaluation du patrimoine numérique fournissent à l'équipe chargée de la plateforme cloud une vision claire de l'environnement final et des exigences nécessaires pour soutenir le plan d'adoption.

**Livrables :**

- Données brutes sur l'inventaire existant.
- Analyse quantitative de l'inventaire existant pour affiner la justification métier.
- Analyse qualitative des 10 premières charges de travail.
- Justification métier mise à jour dans le [modèle de stratégie et de plan](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

**Conseils relatifs aux livrables :**

- [Inventorier les systèmes existants](../digital-estate/inventory.md) : La première étape consiste à identifier l'état actuel à partir d'une approche programmatique et pilotée par les données. Recherchez et rassemblez les données pour faciliter toutes les activités d'évaluation.
- [Rationalisation incrémentielle](../digital-estate/rationalize.md#incremental-rationalization) : Rationalisez les efforts d’évaluation pour vous concentrer sur une analyse qualitative de toutes les ressources, éventuellement même pour prendre en charge l’analyse de rentabilité. Ajoutez ensuite une analyse qualitative détaillée pour les 10 premières charges de travail à migrer.

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes en charge et équipes de soutien | Équipes informées |
| --- | --- | --- |
| <li> Équipe d’adoption du cloud | <li> Équipe de stratégie cloud | <li> Équipe de plateforme cloud |

## <a name="step-3-create-a-cloud-adoption-plan"></a>Étape 3 : Élaborer un plan d'adoption du cloud

Le modèle de plan d’adoption du cloud fournit une approche accélérée pour développer un backlog du projet. Le backlog peut ensuite être modifié pour refléter les résultats de la l'évaluation, la rationalisation, les compétences nécessaires et la mise en place de partenariats.

Un examen du plan d'adoption du cloud à court terme et du backlog permet à l'équipe chargée de la plateforme cloud d'identifier les besoins de l'environnement pour les mois à venir. Ce contexte permet de renforcer la « définition de Terminé » pour les premières zones d'atterrissage.

**Livrables :**

- Déployer le modèle de backlog.
- Mettez à jour le modèle pour qu’il reflète les 10 premières charges de travail à migrer.
- Mettez à jour les personnes et la vélocité (temps des personnes) pour estimer le calendrier des mises en production.
- Risques liés au calendrier :
  - Une connaissance insuffisante d’Azure DevOps peut ralentir le processus de déploiement.
  - La complexité et les données disponibles pour chaque charge de travail peuvent également affecter la chronologie.

**Conseils relatifs aux livrables :**

- [Modèle de plan d'adoption du cloud](../plan/template.md) : Déployez le modèle de base.
- [Alignement des charges de travail](../plan/workloads.md) : Définissez les charges de travail dans le backlog.
- [Alignement des efforts](../plan/assets.md) : Alignez les ressources et les charges de travail dans le backlog afin de définir clairement les efforts à fournir pour les charges de travail prioritaires.
- [Alignement des personnes et du calendrier](../plan/iteration-paths.md) : Établissez l’itération, la vélocité et les mises en production relatives aux charges de travail migrées.

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes en charge et équipes de soutien | Équipes informées |
| --- | --- | --- |
| <li> Équipe d’adoption du cloud | <li> Équipe de stratégie cloud <li> Équipe de plateforme cloud | <li> Équipe de plateforme cloud |

## <a name="step-4-deploy-the-first-landing-zone"></a>Étape 4 : Déployer votre première zone d’atterrissage

Au départ, l'équipe chargée de l'adoption du cloud a besoin d'une zone d'atterrissage capable de répondre aux exigences de la première vague de charges de travail. Au fil du temps, la zone d'atterrissage est mise à l'échelle pour prendre en charge des charges de travail plus complexes. Pour le moment, contentez-vous d'une zone d'atterrissage pour l'apprentissage des équipes chargées de la plateforme cloud et de l'adoption du cloud.

**Livrables :**

- Déployez une première zone d'atterrissage pour les migrations initiales à faible risque.
- Élaborez un plan de refactorisation avec l'équipe chargée du centre d'excellence du cloud ou l'équipe informatique centrale.
- Risques liés au calendrier :
  - Les exigences de gouvernance, d’exploitation et de sécurité pour les 10 premières charges de travail peuvent considérablement ralentir ce processus. La refactorisation réelle de la première zone d’atterrissage et des zones d’atterrissage suivantes prend beaucoup plus de temps, mais doit s’effectuer parallèlement aux efforts de migration.

**Conseils relatifs aux livrables :**

- [Choisissez une zone d'atterrissage](../ready/landing-zone/first-landing-zone.md) : Utilisez cet article pour trouver la bonne approche de déploiement d'une zone d'atterrissage en fonction de votre plan d'adoption à court terme. Déployez ensuite cette base de code standardisée.
- [Développer votre zone d’atterrissage](../ready/considerations/index.md) : N'essayez pas de respecter les contraintes de gouvernance, de sécurité ou d'exploitation à long terme, sauf si elles sont nécessaires pour soutenir le plan d'adoption à court terme.

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes en charge et équipes de soutien |
| --- | --- |
| <li> Équipe de plateforme cloud | <li> Équipe d’adoption du cloud <li> Centre d'excellence du cloud ou équipe informatique centrale |

## <a name="step-5-deploy-an-initial-governance-foundation"></a>Étape 5 : Déployer une première base de gouvernance

La gouvernance est un facteur déterminant pour le succès à long terme de tout effort de migration. La vitesse de migration et l’impact sur l’activité sont importants. Mais la vitesse sans gouvernance peut être dangereuse. Votre organisation doit prendre des décisions de gouvernance alignées sur vos modèles d’adoption, et sur vos besoins en matière de gouvernance et de conformité.

À mesure que ces décisions sont prises, elles se répercutent sur les efforts parallèles de l'équipe chargée de la plateforme cloud.

**Livrables :**

- Déployer une fondation de gouvernance initiale.
- Réaliser un benchmark de gouvernance afin de planifier les futures améliorations.
- Risques liés au calendrier :
  - Les stratégies d’amélioration et l’implémentation de la gouvernance peuvent ajouter de une à quatre semaines par discipline.

**Conseils relatifs aux livrables :**

- [Approche de gouvernance](../govern/index.md) : Cette méthodologie décrit un processus de réflexion sur la stratégie et les processus de l’entreprise. Il s’agit ensuite de mettre en place les disciplines nécessaires pour assurer la gouvernance dans le cadre de vos efforts d’adoption du cloud.
- [Outil de benchmark de gouvernance](../govern/benchmark.md) : Repérez les lacunes dans votre état actuel afin de pouvoir planifier l'avenir.
- [Fondation de gouvernance initiale](../govern/guides/complex/prescriptive-guidance.md) : Identifiez la discipline Base de référence des identités, la discipline Base de référence de la sécurité et la discipline Accélération du déploiement nécessaires à la création d’un produit minimal viable de gouvernance servant de base à toute adoption.

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes en charge et équipes de soutien | Équipes consultées |
| --- | --- | --- |
| <li> Équipe de gouvernance cloud | <li> Équipe de stratégie cloud <li> Centre d'excellence du cloud ou équipe informatique centrale | <li> Équipe de plateforme cloud |

## <a name="step-6-implement-an-operations-baseline"></a>Étape 6 : Implémenter une base de référence pour les opérations

La gestion des opérations est une autre exigence pour réussir la migration. Migrer vers le cloud sans comprendre les opérations en cours est une décision risquée. Parallèlement à la migration, vous devez commencer à planifier les opérations à plus long terme.

À mesure que ces plans sont élaborés, ils se répercutent sur les efforts parallèles de l'équipe chargée de la plateforme cloud.

**Livrables :**

- Déployer une base de référence de gestion.
- Compléter le classeur de gestion des opérations.
- Identifier toutes les charges de travail qui nécessitent une évaluation Microsoft Azure Well-Architected Review.
- Risques liés au calendrier :
  - Consultez le classeur : estimation d'une heure par propriétaire d'application.
  - Effectuez l'évaluation Microsoft Azure Well-Architected Review : estimation d'une heure par application.

**Conseils relatifs aux livrables :**

- [Établir une base de référence de gestion](../manage/index.md)
- [Définir des engagements métier](../manage/considerations/business-alignment.md)
- [Développer la base de référence de gestion](../manage/best-practices.md)
- [Gagner en spécificité avec les opérations avancées](../manage/design-principles.md)

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes en charge et équipes de soutien | Équipes consultées |
| --- | --- | --- |
| <li> Équipe des opérations cloud | <li> Équipe de stratégie cloud <li> Centre d'excellence du cloud ou équipe informatique centrale | <li> Équipe de plateforme cloud |

## <a name="step-7-expand-the-landing-zone"></a>Étape 7 : Étendre la zone d’accueil

Alors que l'équipe chargée de l'adoption du cloud entame ses premières migrations, l'équipe chargée de la plateforme cloud peut commencer à développer la configuration de l'environnement final avec le soutien des équipes chargées de la gouvernance et des opérations cloud. Selon le rythme du plan d'adoption du cloud, il peut être nécessaire d'inscrire cette étape dans le cadre de mises en production itératives. Des fonctionnalités peuvent être ajoutées en plus des exigences du plan d'adoption.

**Livrables :**

- Adoptez une approche de développement piloté par les tests pour refactoriser les zones d'atterrissage.
- Améliorez la gouvernance des zones d'atterrissage.
- Développez les opérations des zones d'atterrissage.
- Implémentez la sécurité des zones d'atterrissage.

**Conseils relatifs aux livrables :**

- [Refactoriser des zones d’atterrissage](../ready/landing-zone/refactor.md)
- [Développement piloté par les tests des zones d’atterrissage](../ready/considerations/test-driven-development.md)
- [Développer la gouvernance des zones d'atterrissage](../ready/considerations/landing-zone-governance.md)
- [Développer les opérations des zones d'atterrissage](../ready/considerations/landing-zone-operations.md)
- [Développer la sécurité des zones d'atterrissage](../ready/considerations/landing-zone-security.md)

<!-- markdownlint-disable MD033 -->
<br>

| Équipe responsable | Équipes en charge et équipes de soutien |
| --- | --- |
| <li> Équipe de plateforme cloud | <li> Équipe d’adoption du cloud <li> Centre d'excellence du cloud ou équipe informatique centrale |

## <a name="value-statement"></a>Énoncé de la valeur

Les étapes décrites dans ce guide peuvent aider vos équipes à accélérer leur migration vers un environnement cloud conçu pour l'entreprise et correctement configuré.

## <a name="next-steps"></a>Étapes suivantes

Tenez compte des étapes suivantes lors d'une prochaine itération afin de tirer parti de vos efforts initiaux :

- [Parcours d'apprentissage de la préparation technique de l'environnement](../ready/suggested-skills.md)
- [Check-list de planification de l'environnement de migration](../migrate/migration-considerations/prerequisites/planning-checklist.md)
