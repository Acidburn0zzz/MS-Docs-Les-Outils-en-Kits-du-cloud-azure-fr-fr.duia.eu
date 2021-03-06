---
title: Inventaire et visibilité dans Azure
description: Découvrez ce qui doit être géré (inventaire) et la façon dont les charges de travail et ressources gérées évoluent dans le temps (visibilité).
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: b3c963341e7e13020cb4e67fca29db14569fa6b3
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223947"
---
# <a name="inventory-and-visibility-in-cloud-management"></a>Inventaire et visibilité en gestion cloud

La gestion opérationnelle dépend clairement des données. Une gestion cohérente nécessite une compréhension de ce qui est géré (inventaire) et de la façon dont ces charges de travail et ressources managées évoluent dans le temps (visibilité). Des insights clairs de l’inventaire et de la visibilité donnent à l’équipe les moyens de gérer efficacement l’environnement. Les autres activités et processus de gestion opérationnelle s’appuient sur ces deux niveaux.

Quelques phrases classiques sur l’importance des mesures donnent le ton de cet article :

- Gérer ce qui est important.
- Vous pouvez uniquement gérer ce que vous pouvez mesurer.
- Si vous ne pouvez pas le mesurer, c’est que ça n’a probablement pas d’importance.

La discipline d’inventaire et de visibilité s’appuie sur ces phrases universelles. Avant de mettre en place des processus de gestion opérationnelle efficaces, il est important de recueillir des données et de créer le niveau de visibilité adapté à chaque équipe concernée.

## <a name="common-customer-challenges"></a>Difficultés fréquemment rencontrées

Si les processus d’inventaire et de visibilité ne sont pas appliqués de manière cohérente, les équipes chargées de la gestion des opérations peuvent subir un plus grand nombre d’interruptions et des temps de récupération plus longs. En outre, elles doivent fournir des efforts beaucoup plus importants pour résoudre et trier les problèmes. Comme les modifications ont un impact négatif sur les applications de priorité élevée et sir un plus grand nombre de ressources, chacune de ces métriques augmente encore plus rapidement.

Ces difficultés sont liées à un petit nombre de questions auxquelles il n’est possible de répondre qu’avec des données (ou données de télémétrie) cohérentes :

- Comment les performances de l’état actuel diffèrent-elles des données de télémétrie concernant les performances opérationnelles standard ?
- Quelles sont les ressources qui sont à l’origine des interruptions au niveau de la charge de travail ?
- Quelles ressources doivent être corrigées pour que les performances de cette charge de travail ou de ce processus métier redeviennent acceptables ?
- À quel moment l’écart est-il devenu visible ? Qu’est-ce qui l’a déclenché ?
- Quelles modifications ont été apportées aux ressources sous-jacentes ? Par qui ?
- Les modifications étaient-elles intentionnelles ? Malveillantes ?
- Comment les modifications ont-elles affecté les données de télémétrie concernant les performances ?

Il est difficile, sinon impossible, de répondre à ces questions sans disposer d’une source de données riche et centralisée où se trouvent des journaux et des données de télémétrie. Pour permettre la gestion cloud en garantissant la configuration cohérente requise pour la centralisation des données, le service de base de référence doit commencer par définir les processus. Ces processus doivent capturer la manière dont une telle configuration applique la collecte des données afin de prendre en charge les composants de l’inventaire et de la visibilité dans la section suivante.

## <a name="components-of-inventory-and-visibility"></a>Composants de l’inventaire et de la visibilité

L’obtention de la visibilité sur une plateforme cloud nécessite quelques composants clés :

- Responsabilité et visibilité
- Inventaire
- Journalisation centralisée
- Suivi des modifications
- Données de télémétrie sur les performances

### <a name="responsibility-and-visibility"></a>Responsabilité et visibilité

Lorsque vous créez des engagements pour chaque charge de travail, la [responsabilité de la gestion](./commitment.md#management-responsibility) est un facteur clé. La responsabilité déléguée crée un besoin de visibilité déléguée. La première étape vers l’inventaire et la visibilité consiste à garantir que les parties responsables ont accès aux données appropriées. Avant d’implémenter des outils cloud natifs pour la visibilité, vérifiez que chaque outil de supervision a été configuré avec un accès et une étendue adaptés à chaque équipe chargée des opérations.

### <a name="inventory"></a>Inventaire

Si personne ne sait qu’une ressource existe, il sera difficile de la gérer. Pour qu’une ressource ou une charge de travail puisse être gérée, elle doit être inventoriée et classifiée. La première étape technique pour obtenir des opérations stables consiste à valider et à classifier l’inventaire.

### <a name="central-logging"></a>Journalisation centralisée

La journalisation centralisée est essentielle pour obtenir la visibilité dont les équipes en charge de la gestion des opérations quotidiennes ont besoin au quotidien. Toutes les ressources déployées dans le cloud doivent enregistrer les journaux dans un emplacement central. Dans Azure, cet emplacement central est Log Analytics. La centralisation de la journalisation permet de créer des rapports sur la gestion des modifications, l’intégrité des services, la configuration et la plupart des autres aspects des opérations informatiques.

L’utilisation cohérente de la journalisation centralisée est la première étape permettant de mettre en place des opérations reproductibles cohérentes. L’application peut être effectuée par le biais d’une stratégie d’entreprise. Toutefois, lorsque cela est possible, l’application doit être automatisée pour garantir la cohérence.

### <a name="change-tracking"></a>Suivi des modifications

Le changement est une constante dans les environnements technologiques. Pour obtenir des opérations fiables, il est essentiel de connaître et de comprendre les modifications qui sont apportées aux charges de travail. Toutes les solutions de gestion cloud doivent inclure un moyen de comprendre quand, comment et pourquoi le changement technique a eu lieu. Sans ces points de données, les efforts de correction sont considérablement entravés.

### <a name="performance-telemetry"></a>Données de télémétrie sur les performances

Les engagements métier concernant la gestion cloud sont dictés par les données. Pour maintenir ses engagements, l’équipe chargée des opérations cloud doit d’abord comprendre les données de télémétrie relatives à la stabilité, aux performances, aux opérations de charge de travail, ainsi qu’aux ressources qui prennent en charge la charge de travail.

L’intégrité et les opérations actuelles du réseau, du DNS, des systèmes d’exploitation et d’autres aspects fondamentaux de l’environnement, sont des points de données critiques qui sont pris en compte dans l’intégrité globale de toutes les charges de travail.

## <a name="processes"></a>Processus

Les processus de gestion cloud sont encore plus importants que les fonctionnalités de la plateforme de gestion cloud, car ils permettent de réaliser des engagements opérationnels avec l’entreprise. Toutes les méthodologies de gestion cloud doivent inclure au minimum les processus suivants :

- **Supervision réactive :** Lorsque des écarts affectent les opérations métier, qui est chargé de les résoudre ? Quelles sont les mesures prises pour résoudre ces écarts ?
- **Surveillance proactive :** Lorsque des écarts sont détectés, mais que les opérations métier ne sont pas affectées, comment ces écarts sont-ils résolus et par qui ?
- **Création de rapports sur les engagements :** Comment le respect des engagements métier est-il communiqué aux parties prenantes ?
- **Révisions budgétaires :** Quel processus a été mis en place pour réviser ces engagements par rapport aux coûts budgétés ? Quel est le processus d’ajustement de la solution déployée ou des engagements qui est utilisé pour obtenir l’alignement ?
- **Chemins d’escalade :** Quels sont les chemins d’escalade disponibles lorsque l’un des processus précédents ne répond pas aux besoins de l’entreprise ?

Il existe plusieurs autres processus liés à l’inventaire et à la visibilité. La liste précédente est conçue pour faire réfléchir l’équipe chargée des opérations. La réponse à ces questions aide à développer certains des processus nécessaires ainsi que, probablement, à provoquer de nouvelles questions, plus approfondies.

## <a name="responsibilities"></a>Responsabilités

Lorsque vous développez des processus pour la supervision opérationnelle, il est tout aussi important de déterminer les responsabilités pour les opérations quotidiennes et la prise en charge habituelle de chaque processus.

Dans une organisation appliquant l’informatique centralisée, le service informatique fournit une expertise opérationnelle. L’entreprise est naturellement consultée lorsqu’il faut remédier à des problèmes.

Dans une organisation appliquant la méthode CCoE, les opérations métier offrent une expertise et sont responsables de la gestion de ces processus. Le service informatique se concentre sur l’automatisation et l’assistance aux équipes, puisque ce sont elles qui font fonctionner l’environnement.

Toutefois, il s’agit de responsabilités communes. Les organisations ont souvent besoin de plusieurs responsabilités pour répondre aux engagements métier.

## <a name="act-on-inventory-and-visibility"></a>Agir au niveau de l’inventaire et de la visibilité

Quelle que soit la plateforme cloud, les cinq composants de l’inventaire et de la visibilité sont utilisés pour gérer la plupart des processus opérationnels. Toutes les disciplines suivantes seront basées sur les données capturées. Les articles suivants de cette série expliquent comment utiliser ces données et intégrer d’autres sources de données.

### <a name="share-visibility"></a>Partager la visibilité

Les données non utilisées ne permettent pas de retour intéressant. La gestion cloud peut s’étendre au-delà des outils et des processus natifs du cloud. Pour prendre en charge des processus plus larges, il peut être nécessaire d’améliorer une base de référence de gestion cloud pour y inclure la création de rapports, l’intégration de la gestion des services informatiques ou la centralisation des données. La gestion cloud devra peut-être inclure un ou plusieurs des éléments suivants au cours des différentes phases de maturité opérationnelle.

### <a name="report"></a>Rapport

Les processus et la communication hors connexion concernant les engagements envers les parties prenantes nécessitent souvent des rapports. La création de rapports en libre-service ou la création de rapports périodiques peuvent être nécessaires à l’amélioration de la base de référence de gestion.

### <a name="it-service-management-itsm-integration"></a>Intégration de la gestion des services informatiques (ITSM)

L’intégration ITSM est souvent le premier exemple d’action entreprise pour l’inventaire et la visibilité. Lorsque des écarts sont détectés par rapport aux modèles de performances attendus, l’intégration ITSM utilise les alertes de la plateforme cloud pour déclencher des tickets dans un outil de gestion de service distinct, afin de déclencher des activités de correction. Certains modèles opérationnels peuvent avoir besoin de l’intégration ITSM pour la base de référence de gestion améliorée.

### <a name="data-centralization"></a>Centralisation des données

Une entreprise peut avoir besoin plusieurs locataires au sein d’un même fournisseur cloud pour différentes raisons. Dans ces scénarios, la centralisation des données est un composant obligatoire de la base de référence de gestion améliorée, car elle peut fournir une visibilité de chacun de ces locataires ou environnements.

## <a name="next-steps"></a>Étapes suivantes

La conformité opérationnelle s’appuie sur les fonctionnalités d’inventaire, en appliquant l’automatisation et les contrôles de gestion. Découvrez comment la [conformité opérationnelle](./operational-compliance.md) peut s’adapter à vos processus.

> [!div class="nextstepaction"]
> [Planifier la conformité opérationnelle](./operational-compliance.md)
