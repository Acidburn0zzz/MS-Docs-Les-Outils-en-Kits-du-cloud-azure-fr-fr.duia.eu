---
title: Métriques et indicateurs de tolérance au risque liée à la discipline Accélération du déploiement
description: Utilisez le Framework d’adoption du cloud pour Azure pour quantifier la tolérance au risque métier liée à la discipline Accélération du déploiement.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 1ab0d2c8657889a8f4ee16bd4dd9ca4f631b32c2
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83754972"
---
# <a name="risk-tolerance-metrics-and-indicators-in-the-deployment-acceleration-discipline"></a>Métriques et indicateurs de tolérance au risque liée à la discipline Accélération du déploiement

Apprenez à quantifier la tolérance aux risques de l’entreprise associée à la discipline Accélération du déploiement. La définition de mesures et d’indicateurs vous aide à créer une étude de rentabilité pour investir dans la maturité de cette discipline.

## <a name="metrics"></a>Mesures

L’Accélération du déploiement se concentre sur les risques liés à la configuration, au déploiement, à la mise à jour et à la maintenance des ressources cloud. Les informations suivantes sont utiles lors de l'adoption de la discipline Accélération du déploiement :

- **Échecs de déploiement :** Pourcentage de déploiements qui échouent ou qui débouchent sur des ressources mal configurées.
- **Temps de déploiement :** Il s’agit du temps nécessaire pour déployer des mises à jour sur un système existant.
- **Ressources non conformes :** Il s’agit du nombre ou du pourcentage de ressources non conformes avec les stratégies définies.

## <a name="risk-tolerance-indicators"></a>Indicateurs de tolérance au risque

Les risques liés à l’accélération du déploiement dépendent en grande partie du nombre et de la complexité des systèmes cloud qui sont déployés pour votre entreprise. Plus votre patrimoine cloud s’agrandit, plus le nombre de systèmes déployés et la fréquence de mise à jour de vos ressources cloud augmentent. Avec les dépendances entre les ressources, il est de plus en plus important de veiller à ce que les ressources soient correctement configurées et de concevoir des systèmes capables de résilience, particulièrement lorsqu’une ou plusieurs ressources subissent des temps d’arrêt imprévus.

L’organisation informatique classique des entreprises sépare souvent les équipes chargées des opérations, de la sécurité et du développement. Bien souvent, ces équipes ne collaborent pas ou sont même hostiles les unes envers les autres. C’est en reconnaissant ces défis au tout début du processus et en intégrant les parties prenantes principales de chacune des équipes que vous pouvez favoriser l’agilité dans votre adoption du cloud, tout en gardant la main sur la sécurité et la gouvernance. Ainsi, envisagez d’adopter une culture organisationnelle de type DevOps ou [DevSecOps](https://www.microsoft.com/devsecops) au tout début de votre parcours d’adoption du cloud.

Collaborez avec votre équipe DevSecOps et les parties prenantes de l’entreprise pour identifier les [risques commerciaux](./business-risks.md) liés à la configuration, puis déterminez une ligne de base acceptable pour configurer la tolérance au risque. Cette section des instructions du Framework d’adoption du cloud fournit des exemples, mais les risques et les bases de référence détaillés pour votre entreprise ou vos déploiements risquent d’être différents.

Une fois que vous avez une base de référence, établissez des seuils minimaux représentant une augmentation inacceptable de vos risques identifiés. Ces seuils font office de déclencheurs lorsque vous devez prendre des mesures pour corriger ces risques. Voici quelques exemples montrant comment des métriques liées à la configuration, comme celles décrites ci-dessus, peuvent justifier un investissement accru dans la discipline Accélération du déploiement.

- **Déclencheurs relatifs aux dérives de configuration :** Lorsque les principaux composants système d’une entreprise subissent des changements de configuration inattendus, des défaillances lors du déploiement ou des mises à jour de système, l’entreprise doit investir dans la discipline Accélération du déploiement pour identifier les causes racine et définir les actions correctives.
- **Déclencheurs relatifs à la non-conformité :** Si le nombre de ressources non conformes dépasse un seuil défini (soit un nombre total de ressources ou un pourcentage), l’entreprise doit investir dans les améliorations de la discipline Accélération du déploiement pour garantir que la configuration des ressources reste conforme tout au long du cycle de vie des ressources en question.
- **Déclencheurs relatifs au calendrier du projet :** Si le temps de déploiement des ressources et des applications d’une entreprise dépasse souvent un seuil défini, l’entreprise doit investir dans ses processus Accélération du déploiement pour introduire des déploiements automatisés appliqués à la cohérence et à la prévisibilité, ou bien les améliorer. Les temps de déploiement qui sont mesurés en jours ou en semaines indiquent généralement qu’une stratégie Accélération du déploiement n’est pas optimale.

## <a name="next-steps"></a>Étapes suivantes

Utilisez le [modèle de discipline Accélération du déploiement](./template.md) pour documenter les métriques et indicateurs de tolérance qui correspondent au plan d’adoption du cloud actuel.

Considérez les exemples de stratégies d’accélération du déploiement comme des points de départ permettant de développer vos propres stratégies qui répondent à des risques métier spécifiques, dans la continuité de vos plans d’adoption du cloud.

> [!div class="nextstepaction"]
> [Examiner les exemples de stratégies](./policy-statements.md)
