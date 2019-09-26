---
title: 'Guide pour les entreprises standard : Stratégie d’entreprise initiale sous-tendant la stratégie de gouvernance'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guide pour les entreprises standard : Stratégie d’entreprise initiale sous-tendant la stratégie de gouvernance'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 4da4899038ca86bec2f1d003f9eaaee293119a09
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032241"
---
# <a name="standard-enterprise-guide-initial-corporate-policy-behind-the-governance-strategy"></a>Guide pour les entreprises standard : Stratégie d’entreprise initiale sous-tendant la stratégie de gouvernance

La stratégie d’entreprise suivante définit une position de gouvernance initiale qui constitue le point de départ de ce guide. Cet article définit les risques à un stade précoce, les déclarations de stratégie initiales et les processus à mettre en œuvre dès le début pour appliquer des déclarations de stratégie.

> [!NOTE]
>La stratégie d’entreprise n’est pas un document technique, mais oriente de nombreuses décisions techniques. Le MVP de gouvernance décrit dans cette [vue d’ensemble](./index.md) découle de cette stratégie. Avant d’implémenter un MVP de gouvernance, votre organisation doit développer une stratégie d’entreprise basée sur ses propres objectifs et risques.

## <a name="cloud-governance-team"></a>Équipe de gouvernance cloud

Dans ce scénario, l’équipe de gouvernance cloud est composée de deux administrateurs système qui ont reconnu le besoin de gouvernance. Au cours des prochains mois, ils seront chargés d’assainir la gouvernance de la présence cloud de la société, ce qui leur vaudra le titre d’_opérateurs du cloud_. Dans les itérations ultérieures, ce titre pourrait changer.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Indicateurs de tolérance

La tolérance au risque actuelle est élevée et l’envie d’investir dans la gouvernance de cloud est faible. Par conséquent, les indicateurs de tolérance agissent comme un système d’avertissement précoce pour déclencher des investissements de temps et d’énergie. Si les indicateurs suivants sont observés, vous devez améliorer de façon itérative la stratégie de gouvernance.

- **Gestion des coûts :** La mise à l’échelle du déploiement dépasse 100 ressources dans le cloud, ou les dépenses dépassent 1 000 USD par mois.
- **Base de référence de la sécurité :** Inclusion de données protégées dans des plans définis d’adoption du cloud.
- **Cohérence des ressources :** Inclusion de toutes les applications stratégiques dans des plans définis d’adoption du cloud.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Étapes suivantes

Cette stratégie d’entreprise prépare l’équipe de gouvernance cloud à implémenter le MVP de gouvernance, qui constituera la base de l’adoption. L’étape suivante consiste à implémenter ce MVP.

> [!div class="nextstepaction"]
> [Instructions normatives expliquées](./prescriptive-guidance.md)