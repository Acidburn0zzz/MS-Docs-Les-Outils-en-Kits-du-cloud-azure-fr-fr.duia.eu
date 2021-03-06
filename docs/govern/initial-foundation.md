---
title: Établir une fondation de gouvernance cloud initiale
description: Utilisez Cloud Adoption Framework pour Azure afin de démarrer avec la gouvernance cloud en établissant une fondation de gouvernance cloud initiale.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5c3dbc530ff2e1f28c0927cead3a761463295c4d
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/14/2020
ms.locfileid: "83399622"
---
# <a name="establish-an-initial-cloud-governance-foundation"></a>Établir une fondation de gouvernance cloud initiale

L’établissement d’une gouvernance cloud est un vaste effort itératif. Il est difficile de trouver un juste équilibre entre vitesse et contrôle, en particulier pendant l’exécution des premières méthodologies de l’adoption du cloud. Les instructions de gouvernance dans le Framework d’adoption du cloud contribuent à fournir cet équilibre par le biais d’une approche agile de l’adoption.

Cet article présente deux options permettant d’établir une fondation initiale pour la gouvernance. Les deux options permettent d’adapter et de développer les contraintes de gouvernance à mesure que le plan d’adoption est implémenté et que les besoins deviennent plus clairement définis. Par défaut, la fondation initiale suppose une position d’isolation et de contrôle. Par ailleurs, elle porte davantage sur l’organisation des ressources que sur la gouvernance des ressources. Ce point de départ léger est appelé _produit minimum viable_ (MVP, Minimum Viable Product) pour la gouvernance. L’objectif du MVP est de réduire les obstacles à l’établissement d’une position de gouvernance initiale, puis de permettre une maturation rapide de la solution pour répondre à une variété de risques tangibles.

## <a name="already-using-the-cloud-adoption-framework"></a>Framework d’adoption du cloud déjà en cours d’utilisation

Si vous avez suivi le Cloud Adoption Framework, vous avez peut-être déjà déployé un MVP de gouvernance. La gouvernance est un aspect fondamental de tout modèle d’exploitation. Elle est présente dans chaque méthodologie du cycle de vie de l’adoption du cloud. Ainsi, le [Framework d’adoption du cloud](../index.yml) fournit des instructions qui injectent de la gouvernance dans les activités liées à l’implémentation de votre [plan d’adoption du cloud](../plan/index.md). Un exemple de l’intégration de cette gouvernance consiste à utiliser des blueprints pour déployer une ou plusieurs zones d’atterrissage présentes dans les instructions de [Méthodologie Ready](../ready/index.md). Voici un autre exemple d’instruction pour l’[application d’un scale-out aux abonnements](../ready/azure-best-practices/scale-subscriptions.md). Si vous avez suivi l’une de ces recommandations, les sections suivantes du MVP sont simplement une révision de vos décisions de déploiement existantes. Après un examen rapide, passez directement à [Améliorer la solution de gouvernance initiale et appliquer des contrôles des meilleures pratiques recommandés](./foundation-improvements.md).

## <a name="establish-an-initial-governance-foundation"></a>Établir une fondation de gouvernance initiale

Voici deux exemples de fondations de gouvernance initiales (également appelées MVP de gouvernance) illustrant l’application d’une solide fondation pour la gouvernance à des déploiements nouveaux ou existants. Choisissez le MVP qui correspond le mieux aux besoins de votre entreprise pour commencer :

- [Guide de gouvernance standard](./guides/standard/index.md) : Guide pour la plupart des organisations basées sur le modèle à deux abonnements initial recommandé, conçu pour les déploiements dans plusieurs régions, mais sans englober les clouds publics et souverains/gouvernementaux.
- [Guide de gouvernance pour les entreprises complexes](./guides/complex/index.md) : Guide pour les entreprises qui sont gérées par plusieurs unités commerciales informatiques indépendantes ou qui englobent des clouds publics et souverains/gouvernementaux.

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Étapes suivantes

Une fois qu’une fondation de gouvernance est en place, appliquez les recommandations appropriées pour améliorer la solution et vous protéger contre les risques tangibles.

> [!div class="nextstepaction"]
> [Améliorer la fondation de gouvernance initiale](./foundation-improvements.md)
