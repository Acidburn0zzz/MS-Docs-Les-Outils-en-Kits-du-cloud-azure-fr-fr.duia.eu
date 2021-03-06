---
title: Activités de préproduction pendant une migration
description: Utilisez le Cloud Adoption Framework pour Azure afin de découvrir les activités de préproduction et les livrables associés nécessaires durant une migration.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 40a0899a10e242e98ed16aa2bcbfdbd55f65afc2
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83216076"
---
# <a name="understand-staging-activities-during-a-migration"></a>Comprendre les activités de préproduction pendant une migration

Comme décrit dans l’article sur les modèles de promotion, la _préproduction_ est le point auquel les ressources ont été migrées vers le cloud. Toutefois, elles ne sont pas encore prêtes à être promues en production. Il s’agit souvent de la dernière étape du processus de migration. Après la mise en préproduction, la charge de travail est gérée par une équipe chargée des opérations informatiques ou du cloud pour la préparer à l’utilisation en production.

## <a name="deliverables"></a>Livrables

Les ressources en préproduction peuvent ne pas être prêtes à être utilisées en production. Il y a plusieurs vérifications de préparation à la mise en production qui doivent être finalisées avant que cette étape soit considérée comme terminée. La liste suivante répertorie les livrables souvent associés à l’achèvement de la préproduction des ressources.

- **Tests automatisés.** Tous les tests automatisés disponibles pour valider les performances de la charge de travail doivent être exécutés avant la conclusion du processus de préproduction. Une fois que la ressource a quitté la préproduction, la synchronisation avec le système source d’origine est terminée. Par conséquent, il est plus difficile de redéployer les ressources répliquées une fois que les ressources sont mises en préproduction pour optimisation.
- **Documentation relative à la migration.** La plupart des outils de migration peuvent générer un rapport automatisé des ressources en cours de migration. Avant de conclure l’activité de préproduction, toutes les ressources migrées doivent être documentées pour plus de clarté.
- **Documentation de la configuration.** Toute modification apportée à une ressource (pendant la correction, la réplication ou la préproduction) doit être documentée à des fins de préparation opérationnelle.
- **Documentation du backlog.** Le backlog de la migration doit être mis à jour pour refléter la charge de travail et les ressources en préproduction.

## <a name="next-steps"></a>Étapes suivantes

Une fois les ressources en préproduction testées et documentées, vous pouvez passer aux [activités d’optimisation](../optimize/index.md).

> [!div class="nextstepaction"]
> [Optimiser les charges de travail migrées](../optimize/index.md)
