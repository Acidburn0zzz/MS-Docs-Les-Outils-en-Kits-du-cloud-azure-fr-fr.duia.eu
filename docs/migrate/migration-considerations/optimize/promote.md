---
title: Qu’est-ce qui est nécessaire pour promouvoir une ressource migrée vers la production ?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Un processus au sein d’une migration cloud qui se concentre sur les tâches de migration des charges de travail vers le cloud.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: eb025eacb7743f470b15e2714ed65a05c21034a1
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836619"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-required-to-promote-a-migrated-resource-to-production"></a>Qu’est-ce qui est nécessaire pour promouvoir une ressource migrée vers la production ?

La promotion vers la production marque la fin de la migration d’une charge de travail vers le cloud. Une fois que la ressource et toutes ses dépendances sont promues, le trafic de production est redirigé. La redirection du trafic rend obsolètes les ressources locales, ce qui leur permet d’être désactivées.

Le processus de promotion varie en fonction de l’architecture de la charge de travail. Toutefois, il existe plusieurs prérequis cohérents et quelques tâches courantes. Cet article décrit chacune d’entre elles et sert de check-list de prépromotion.

## <a name="prerequisite-processes"></a>Processus préalables

Chacun des processus suivants doit être exécuté, documenté et validé avant le déploiement de production :

- **[Évaluation](../assess/index.md) :** La compatibilité de la charge de travail avec le cloud a été évaluée.
- **[Construction](../assess/architect.md) :** La structure de la charge de travail a été correctement construite pour s’aligner sur le fournisseur de services cloud choisi.
- **[Réplication](../migrate/replicate.md) :** Les ressources ont été répliquées dans l’environnement cloud.
- **[Intermédiaire](../migrate/stage.md) :** Les ressources répliquées ont été restaurées dans une instance intermédiaire de l’environnement cloud.
- **[Tests d’entreprise](./business-test.md) :** La charge de travail a été entièrement testée et validée par les utilisateurs professionnels.
- **[Plan des changements opérationnels](./business-change-plan.md) :** L’entreprise a partagé un plan portant sur les modifications à apporter, conformément à la promotion de production. Cela doit inclure un plan d’adoption par les utilisateurs, des modifications des processus métier, des utilisateurs qui nécessitent une formation et des chronologies pour différentes activités.
- **[Prêt](./ready.md) :** En règle générale, une série de modifications techniques doivent être apportées avant la promotion.

## <a name="best-practices-to-execute-prior-to-promotion"></a>Meilleures pratiques à exécuter avant la promotion

Les modifications techniques suivantes devront probablement être terminées et documentées dans le cadre du processus de promotion :

- **Alignement de domaine.** Certaines stratégies d’entreprise nécessitent des domaines distincts pour la mise en lots et la production. Assurez-vous que toutes les ressources sont jointes au domaine approprié.
- **Routage des utilisateurs.** Vérifiez que les utilisateurs accèdent à la charge de travail via des itinéraires réseau appropriés. Vérifiez également la cohérence des attentes de niveaux de performance.
- **Alignement des identités.** Vérifiez que les utilisateurs qui sont redirigés vers l’application disposent des autorisations appropriées au sein du domaine pour héberger l’application.
- **Niveau de performance.** Effectuez une validation finale du niveau de performance des charges de travail pour réduire les surprises.
- **Validation de la continuité d’activité et de la reprise d’activité.** Vérifiez que les processus de sauvegarde et de récupération appropriés fonctionnent comme prévu.
- **Classification des données.** Validez la classification des données pour vous assurer que les stratégies et protections appropriées ont été implémentées.
- **Vérification du responsable de la sécurité des systèmes d’information.** Vérifiez que le responsable de la sécurité des systèmes d’information a passé en revue la charge de travail, les risques commerciaux, la tolérance aux risques et les stratégies d’atténuation des risques.

## <a name="final-step-promote"></a>Dernière étape : Promouvoir

Les charges de travail nécessiteront différents niveaux de processus détaillés de révision et de promotion. Toutefois, le réalignement réseau constitue la dernière étape commune à toutes les versions de promotion. Lorsque tout le reste est prêt, mettez à jour les enregistrements DNS ou les adresses IP pour acheminer le trafic vers la charge de travail migrée.

## <a name="next-steps"></a>Étapes suivantes

La promotion d’une charge de travail signale la fin d’une mise en production. Toutefois, parallèlement à la migration, les ressources hors service doivent être [désactivées](./decommission.md), les mettant ainsi hors service.

> [!div class="nextstepaction"]
> [Désactiver les ressources hors service](./decommission.md)