---
title: Motivations et risques métier dans la discipline Ligne de base des identités
description: Appréhendez et découvrez des exemples de clients types qui adoptent une discipline de base de référence de la sécurité dans le cadre d’une stratégie de gouvernance cloud.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: dd4f6b58d3d8f1a1d1b6348ae83979c37c9305bc
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755873"
---
# <a name="motivations-and-business-risks-in-the-security-baseline-discipline"></a>Motivations et risques métier dans la discipline Ligne de base des identités

Cet article décrit les raisons pour lesquelles les clients adoptent une discipline Base de référence de la sécurité au sein d’une stratégie de gouvernance cloud. Des exemples sur les risques métier potentiels pouvant conduire à la rédaction d’instructions de stratégie sont également présentés.

<!-- markdownlint-disable MD026 -->

## <a name="relevance"></a>Pertinence

La sécurité est une préoccupation majeure de tous les services informatiques. Les déploiements dans le cloud sont confrontés aux mêmes risques de sécurité que les charges de travail hébergées dans des centres de données locaux classiques. La nature des plateformes de cloud public, sans propriété directe sur le matériel physique stockant et exécutant vos charges de travail, signifie que la sécurité du cloud requiert ses propres stratégies et processus.

L’un des principaux éléments qui distingue la gouvernance de la sécurité du cloud de la stratégie de sécurité traditionnelle est la facilité avec laquelle les ressources peuvent être créées, ce qui est susceptible d’ajouter des vulnérabilités si la sécurité n’est pas prise en compte avant le déploiement. La flexibilité offerte par certaines technologies comme [SDN (Software-Defined Networking)](../../decision-guides/software-defined-network/index.md) pour rapidement faire évoluer votre topologie réseau cloud peut aussi modifier votre surface d’attaque de manière imprévisible. Les plateformes cloud fournissent également des outils et des fonctionnalités capables d'améliorer vos fonctionnalités de sécurité au-delà des possibilités des environnements locaux.

Vos investissements et processus en matière de stratégie de sécurité dépendent en grande partie de la nature de votre déploiement dans le cloud. Les déploiements de tests initiaux peuvent nécessiter un minimum de stratégies de sécurité, mais une charge de travail stratégique devra répondre à des besoins de sécurité aussi complexes qu'étendus. À un certain niveau, tous les déploiements doivent respecter une certaine discipline.

La discipline Base de référence de la sécurité couvre les stratégies d'entreprise et les processus manuels que vous pouvez mettre en place pour protéger votre déploiement dans le cloud contre les risques de sécurité.

> [!NOTE]
>S'il est important de comprendre la [discipline Ligne de base des identités](../identity-baseline/index.md) dans le contexte de la discipline Ligne de base de la sécurité et de la façon dont cela se rapporte au contrôle d'accès, les [Cinq disciplines de la gouvernance du cloud](../index.md) la traitent comme une discipline à part.

## <a name="business-risk"></a>Risque métier

La discipline Base de référence de la sécurité tente de répondre aux principaux risques métier en matière de sécurité. Collaborez avec votre entreprise pour identifier ces risques et surveiller la pertinence de chacun d’entre eux lorsque vous planifiez et implémentez vos déploiements cloud.

Les risques varient d'une organisation à l'autre. Utilisez cette liste de risques courants liés à la sécurité comme point de départ pour les discussions au sein de votre équipe de gouvernance cloud :

- **Violation des données :** Une exposition par inadvertance ou la perte de données sensibles hébergées dans le cloud peut entraîner la perte de clients, des problèmes contractuels ou des conséquences juridiques.
- **Interruption de service :** Les pannes et autres problèmes de performances dus à une infrastructure non sécurisée altèrent le bon déroulement des opérations et peuvent entraîner une perte de productivité ou d'activité.

## <a name="next-steps"></a>Étapes suivantes

À l’aide du [modèle de discipline Ligne de base des identités](./template.md), documentez les risques métier susceptibles d’être introduits par le plan d’adoption du cloud actuel.

Une fois tous les risques métier réalistes appréhendés, l’étape suivante consiste à documenter la tolérance de l’activité aux risques, ainsi que les indicateurs et métriques clés permettant de surveiller cette tolérance.

> [!div class="nextstepaction"]
> [Comprendre les indicateurs, les métriques et la tolérance au risque](./metrics-tolerance.md)
