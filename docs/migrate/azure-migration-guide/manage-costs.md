---
title: Mécanismes de contrôle des coûts axés sur la migration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Découvrez comment configurer les budgets et les paiements, et comprenez les factures pour vos ressources Azure.
author: bandersmsft
ms.author: banders
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 294a426aef047bb7acd418c19574a4fd7e0b2320
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905636"
---
# <a name="migration-focused-cost-control-mechanisms"></a>Mécanismes de contrôle des coûts axés sur la migration

Le cloud introduit quelques changements dans la façon dont nous travaillons, quel que soit notre rôle dans l’équipe technologique. Le coût est un excellent exemple de cette évolution. Dans le passé, seuls les responsables financiers et informatiques étaient concernés par le coût des ressources informatiques (infrastructure, applications et données). Le cloud permet à tous les membres de l’équipe informatique de prendre des décisions qui améliorent le support de l’utilisateur final et d’agir en conséquence. Toutefois, ce pouvoir s’accompagne de la responsabilité d’être conscient des coûts lors de la prise de décision.

Cet article présente les outils qui peuvent vous aider à prendre des décisions judicieuses en matière de coûts avant, pendant et après une migration vers Azure.

Les outils de cet article sont les suivants :

> - Azure Migrate
> - Calculatrice de prix Azure
> - Calculatrice du coût TCO Azure
> - Gestion des coûts Azure
> - Azure Advisor

Les processus décrits dans cet article peuvent également nécessiter un partenariat avec les responsables informatiques, les services financiers ou les propriétaires d’applications métier. Pour obtenir de l’aide concernant les partenariats avec ces rôles, consultez l’article du Framework d’adoption du cloud sur la mise en place d’une organisation sensible au coûts (disponible au 3e trimestre 2019).

<!-- markdownlint-disable MD024 MD025 -->

# <a name="estimate-vm-costs-prior-to-migrationtabestimatevmcosts"></a>[Estimer les coûts d’une machine virtuelle avant la migration](#tab/EstimateVMCosts)

Avant la migration de toute ressource (infrastructure, application ou données), il est possible d’estimer les coûts et d’affiner le dimensionnement en fonction des critères de performance observés pour ces ressources. L’estimation des coûts a deux objectifs : elle permet de contrôler les coûts et fournit un point de contrôle pour s’assurer que les budgets actuels tiennent compte des exigences de niveaux de performance nécessaires.

## <a name="cost-calculators"></a>Calculatrices de coûts

Pour les calculs de coûts manuels, il existe deux calculatrices pratiques qui peuvent fournir une estimation rapide des coûts en fonction de l’architecture de la charge de travail à migrer.

- La [calculatrice de tarification](https://azure.microsoft.com/pricing/calculator) Azure fournit des estimations de coûts qui s’appuient sur les produits Azure entrés manuellement.
- Parfois, les décisions requièrent une comparaison des coûts futurs du cloud et des coûts locaux actuels. La [calculatrice du coût total de possession (TCO)](https://azure.microsoft.com/pricing/tco/calculator) peut fournir cette comparaison.

Ces calculatrices de coûts manuels peuvent être utilisées de manière autonome pour prévoir les dépenses et les économies potentielles. Elles peuvent également être utilisées conjointement avec les outils de prévision des coûts d’Azure Migrate pour ajuster les attentes en matière de coûts selon les architectures alternatives ou les contraintes de niveaux de performance.

## <a name="azure-migrate-calculations"></a>Calculs d’Azure Migrate

**Configuration requise :** Le reste de cet onglet part du principe que le lecteur a déjà rempli Azure Migrate avec une collection de ressources (infrastructure, applications et données) à migrer. L’article précédent relatif aux évaluations fournit des instructions sur la collecte des données initiales. Une fois les données remplies, suivez les étapes suivantes pour estimer les coûts mensuels en fonction des données collectées.

Azure Migrate calcule les **estimations de coût mensuel** en fonction des données capturées par le collecteur et la carte de service. Les étapes suivantes chargeront les estimations de coût :

1. Accédez au panneau Évaluation Azure Migrate dans le portail.
1. Dans la page **Vue d’ensemble** du projet, sélectionnez **+Créer une évaluation**.
1. Cliquez sur **Tout afficher** pour passer en revue les propriétés de l’évaluation.
1. Créez le groupe et spécifiez un nom de groupe.
1. Sélectionnez les machines que vous souhaitez ajouter au groupe.
1. Cliquez sur **Créer une évaluation** pour créer le groupe et l’évaluation.
1. Une fois l’évaluation créée, affichez-la dans Vue d’ensemble > Tableau de bord.
1. Dans la section Détails de l’évaluation de la navigation du panneau, sélectionnez **Détails des coûts**.

L’estimation obtenue, illustrée ci-dessous, identifie les coûts mensuels du calcul et du stockage, qui représentent souvent la plus grande partie des coûts du cloud.

![compute-storage-monthly-cost-estimate. png](./media/manage-costs/compute-storage-monthly-cost-estimate.png)
*Figure 1 : image du détail des coûts d’une évaluation dans Azure Migrate.*

## <a name="additional-resources"></a>Ressources supplémentaires

- [Configurer et passer en revue une évaluation avec Azure Migrate](/azure/migrate/tutorial-assess-vmware#set-up-an-assessment)
- Pour un plan plus complet relatif à la gestion des coûts sur un grand nombre de ressources (infrastructure, applications et données), consultez le [modèle de gouvernance du Framework d’adoption du cloud](../../governance/journeys/index.md). En particulier, des conseils sur la [discipline de Cost Management](../../governance/cost-management/index.md) et le [guide sur l’amélioration de Cost Management dans les grandes entreprises](../../governance/journeys/complex-enterprise/cost-management-evolution.md).

# <a name="estimate-and-optimize-vm-costs-during-and-after-migrationtabestimateoptimize"></a>[Estimer et optimiser les coûts des machines virtuelles pendant et après la migration](#tab/EstimateOptimize)

L’estimation des coûts avant la migration offre une cible solide pour les attentes en matière de coûts. Elle permet également de tenir compte des besoins de chaque ressource (infrastructure, applications et données) à migrer en matière de niveaux de performance et de coût. Toutefois, cela reste une estimation. Une fois la ressource migrée et en charge, des calculs de coûts plus précis peuvent être effectués, en fonction de la charge réelle ou synthétisée.

## <a name="azure-advisor-cost-recommendations"></a>Recommandations de coûts Azure Advisor

Dans les 24 heures qui suivent la migration des ressources (infrastructure, applications et données) vers Azure, Azure Advisor commence à surveiller le niveau de performances de chaque ressource pour vous fournir des commentaires sur la ressource. L’un des commentaires recueillis concerne l’équilibre entre le coût et l’utilisation.

Les étapes suivantes fournissent des recommandations de coût pour les ressources (infrastructure, applications et données) au sein de vos abonnements actuels :

1. Accédez au panneau **Azure Advisor** dans le portail. Pour ce faire, sélectionnez **Advisor** dans le volet de navigation gauche du Portail Azure. Si vous ne voyez pas Advisor dans le volet gauche, sélectionnez **Tous les services**. Dans le volet du menu de services, sous **Surveillance et gestion**, sélectionnez **Advisor**.
1. Le tableau de bord Advisor présente un résumé de vos recommandations pour tous les abonnements sélectionnés. Vous pouvez choisir les abonnements pour lesquels afficher les recommandations à l’aide de la liste déroulante de filtrage des abonnements.
1. Pour afficher les recommandations de coût, sélectionnez l’onglet Coût.

## <a name="azure-cost-management"></a>Gestion des coûts Azure

Azure Cost Management peut fournir une vision plus holistique des habitudes de dépenses, notamment un affichage détaillé des coûts et des tendances des dépenses dans le temps. Pour les migrations volumineuses ou complexes, cet affichage peut fournir les insights nécessaires pour prendre des décisions de gestion des coûts à grande échelle.

Configuration requise : Le reste de cet onglet part du principe que le lecteur a terminé la configuration d’Azure Cost Management pendant l’exécution du guide de préparation Azure. Pour plus d’informations sur la configuration d’Azure Cost Management, consultez cet [article dans le guide de préparation Azure](/azure/architecture/cloud-adoption/ready/azure-readiness-guide/manage-costs). Une fois les données remplies, suivez les étapes suivantes pour estimer les coûts mensuels en fonction des données collectées.

Les étapes suivantes chargeront les données d’analyse des coûts d’Azure Cost Management pour vos abonnements :

1. Accédez au panneau **Cost Management + facturation** dans le portail. Si vous ne voyez pas Cost Management + facturation dans le volet gauche, cliquez sur **Tous les services**. Dans le volet du menu de services, sous **Surveillance et gestion**, cliquez sur **Cost Management + facturation**.
1. Dans le panneau Cost Management + facturation, sélectionnez **Cost Management** dans la navigation de gauche pour que le panneau ouvert commence l’analyse et l’optimisation des coûts du cloud.
1. Dans le panneau Cost Management, sélectionnez **Analyse des coûts**.
    1. Utilisez le paramètre **Étendue** pour passer à une autre étendue dans l’analyse des coûts.

Cette analyse vous permettra d’examiner les coûts totaux, le budget (le cas échéant) et les coûts cumulés. Chaque calcul peut être affiché par service, par ressource et dans le temps. Plus important encore, les coûts peuvent être analysés par balise. Le nommage et la catégorisation appropriés des ressources (infrastructure, applications et données) constituent le point de départ fondamental de tous les processus de gouvernance et de gestion des coûts. Des balises appropriées permettent une meilleure gestion des coûts et des impacts plus clairs des optimisations des niveaux de performance et des coûts.

## <a name="additional-resources"></a>Ressources supplémentaires

- Pour un plan plus complet relatif à la gestion des coûts sur un grand nombre de ressources (infrastructure, applications et données), consultez le [modèle de gouvernance du Framework d’adoption du cloud](../../governance/journeys/index.md). En particulier, des conseils sur la [discipline de Cost Management](../../governance/cost-management/index.md) et le [guide sur l’amélioration incrémentielle de Cost Management dans les grandes entreprises](../../governance/journeys/complex-enterprise/cost-management-evolution.md).
- Pour plus d’informations sur Azure Advisor, consultez [Réduire les coûts de service grâce à Azure Advisor](/azure/advisor/advisor-cost-recommendations).
- Pour plus d’informations sur Azure Cost Management, consultez [Comprendre et utiliser les étendues](/azure/cost-management/understand-work-scopes) et [Explorer et analyser les coûts avec l’analyse des coûts](/azure/cost-management/quick-acm-cost-analysis).

# <a name="tips-and-tricks-to-optimize-coststabtipstricks"></a>[Astuces et conseils pour optimiser les coûts](#tab/TipsTricks)

Outre les outils mentionnés dans cet article, il existe des astuces et conseils qui peuvent vous aider à réduire rapidement les coûts globaux du cloud. Voici quelques conseils de haut niveau à connaître :

## <a name="avoid-unnecessary-spending"></a>Éviter les dépenses inutiles

La plupart des ressources (infrastructure, applications et données) dans un centre de données existant peuvent théoriquement être migrées vers le cloud. Toutefois, cela ne signifie pas qu’elles devraient l’être. Pendant l’évaluation de chaque charge de travail, vérifiez que la charge de travail doit être migrée. L’article du Framework d’adoption du cloud sur la [rationalisation incrémentielle](../../digital-estate/rationalize.md) peut aider à déterminer les ressources qui doivent être migrées.

## <a name="reduce-waste"></a>Réduire le gaspillage

Une fois que vous avez déployé votre infrastructure dans Azure, il est important de s’assurer qu’elle est utilisée. La manière la plus simple de faire des économies immédiatement consiste à passer en revue vos ressources et à supprimer celles qui ne sont pas utilisées.

## <a name="reduce-overprovisioning"></a>Réduire le surapprovisionnement

Même avec les meilleures approches en matière d’estimation, il est probable qu’il y ait des ressources (infrastructure, applications et données) surapprovisionnées et sous-exploitées. L’examen de ces ressources à l’aide des outils des deux onglets précédents permettra d’identifier les moyens potentiels de réduire le dimensionnement des ressources pour mieux répondre aux exigences de niveaux de performance et réduire les coûts.

## <a name="take-advantage-of-available-discounts"></a>Tirer parti des remises disponibles

Parlez avec le représentant de votre compte Microsoft pour comprendre comment vous pouvez tirer parti des options de remise actuelles. Voici quelques exemples de remises couramment utilisées pour réduire les coûts.

## <a name="azure-reservations"></a>Réservations Azure

Les [réservations Azure](/azure/billing/billing-save-compute-costs-reservations) vous permettent de prépayer un ou trois ans de capacité de calcul de machine virtuelle ou de SQL Database. Le prépaiement vous permet d’obtenir une remise sur les ressources que vous utilisez. Avec un engagement initial d’une durée de 1 ou 3 ans, les réservations Azure réduisent considérablement (jusqu’à 72 % par rapport au tarif du paiement à l’utilisation) les coûts de calcul de vos machines virtuelles ou de votre base de données SQL. Les réservations permettent de bénéficier d’une remise sur la facturation et n’ont aucune incidence sur l’état de runtime de vos machines virtuelles ou bases de données SQL.

## <a name="use-azure-hybrid-benefit"></a>Utiliser Azure Hybrid Benefit

Si vous avez déjà des licences Windows Server ou SQL Server dans vos déploiements locaux, vous pouvez utiliser le programme [Azure Hybrid Benefit](https://azure.microsoft.com/pricing/hybrid-benefit) pour faire des économies dans Azure. Avec l’avantage Windows Server, chaque licence couvre le coût du système d’exploitation (jusqu’à deux machines virtuelles) et vous payez uniquement les coûts liés au calcul de base. Vous pouvez utiliser des licences SQL Server existantes pour économiser jusqu’à 55 % sur les options SQL Database basées sur vCore. Parmi ces options figurent SQL Server dans Machines virtuelles Azure et SQL Server Integration Services.

## <a name="low-priority-vms-with-batch"></a>Machines virtuelles de basse priorité avec Batch

Pour les processus en arrière-plan de basse priorité, Batch offre un moyen de gérer les machines virtuelles du service en arrière-plan et de réduire les coûts. Toutefois, il est important de comprendre l’impact sur le niveau de performances des [machines virtuelles de basse priorité avec Batch](/azure/batch/batch-low-pri-vms) avant de choisir cette option avec remise.

## <a name="additional-resources"></a>Ressources supplémentaires

Pour un plan plus complet relatif à la gestion des coûts sur un grand nombre de ressources (infrastructure, applications et données), consultez le [modèle de gouvernance du Framework d’adoption du cloud](../../governance/journeys/index.md). En particulier, des conseils sur la [discipline de Cost Management](../../governance/cost-management/index.md) et le [guide de gouvernance sur l’amélioration incrémentielle de Cost Management dans les grandes entreprises](../../governance/journeys/complex-enterprise/cost-management-evolution.md).