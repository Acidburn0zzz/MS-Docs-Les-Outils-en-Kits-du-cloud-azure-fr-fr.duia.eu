---
title: 'Gouvernance pour les entreprises standard : Première politique de l’entreprise'
description: Utilisez le Framework d’adoption du cloud pour Azure pour définir la position de gouvernance initiale, les risques à un stade précoce, les déclarations de stratégie initiales et les processus à mettre en œuvre dès le début.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: c32193ee76899af327a2ed727de43f56f9d1ff63
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83214546"
---
# <a name="standard-enterprise-governance-guide-initial-corporate-policy-behind-the-governance-strategy"></a>Guide de gouvernance pour les entreprises standard : Stratégie d’entreprise initiale sous-tendant la stratégie de gouvernance

La stratégie d’entreprise suivante définit une position de gouvernance initiale qui constitue le point de départ de ce guide. Cet article définit les risques à un stade précoce, les déclarations de stratégie initiales et les processus à mettre en œuvre dès le début pour appliquer des déclarations de stratégie.

> [!NOTE]
>La stratégie d’entreprise n’est pas un document technique, mais oriente de nombreuses décisions techniques. Le MVP de gouvernance décrit dans cette [vue d’ensemble](./index.md) découle de cette stratégie. Avant d’implémenter un MVP de gouvernance, votre organisation doit développer une stratégie d’entreprise basée sur ses propres objectifs et risques.

## <a name="cloud-governance-team"></a>Équipe de gouvernance cloud

Dans ce scénario, l’équipe de gouvernance cloud est composée de deux administrateurs système qui ont reconnu le besoin de gouvernance. Au cours des prochains mois, les membres de l’équipe seront chargés d’assainir la gouvernance de la présence cloud de la société, ce qui leur vaudra le titre d’_opérateurs du cloud_. Dans les itérations ultérieures, ce titre pourrait changer.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Indicateurs de tolérance

La tolérance au risque actuelle est élevée et l’envie d’investir dans la gouvernance de cloud est faible. Par conséquent, les indicateurs de tolérance agissent comme un système d’avertissement précoce pour déclencher des investissements de temps et d’énergie. Si les indicateurs suivants sont observés, vous devez améliorer de façon itérative la stratégie de gouvernance.

- **Gestion des coûts :** L’échelle du déploiement dépasse les limites prédéterminées quant au nombre de ressources ou au coût mensuel.
- **Base de référence de sécurité :** Inclusion de données protégées dans des plans définis d’adoption du cloud.
- **Cohérence des ressources :** Inclusion de toutes les applications stratégiques dans des plans définis d’adoption du cloud.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Étapes suivantes

Cette stratégie d’entreprise prépare l’équipe de gouvernance cloud à implémenter le MVP de gouvernance, qui constituera la base de l’adoption. L’étape suivante consiste à implémenter ce MVP.

> [!div class="nextstepaction"]
> [Explication des bonnes pratiques](./prescriptive-guidance.md)
