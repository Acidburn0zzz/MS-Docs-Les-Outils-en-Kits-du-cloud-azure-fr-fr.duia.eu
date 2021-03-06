---
title: Utiliser Terraform pour créer vos zones d’atterrissage
description: Apprenez à utiliser Terraform pour créer vos zones d’atterrissage.
author: arnaudlh
ms.author: arnaul
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 8eee7eeaf2406a94ee703054ed5f1b9e369bf5a2
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755657"
---
<!-- cSpell:ignore arnaudlh arnaul Arnaud vCPUs eastasia southeastasia lalogs tfvars -->

# <a name="use-terraform-to-build-your-landing-zones"></a>Utiliser Terraform pour créer vos zones d’atterrissage

Azure fournit des services natifs pour le déploiement de vos zones d’atterrissage. D’autres outils tiers peuvent également vous aider à cet effet. Terraform de HashiCorp est le type d’outil que les clients et les partenaires utilisent souvent pour déployer des zones d’atterrissage. Cette section montre comment utiliser un exemple de zone d’atterrissage pour déployer des fonctionnalités de base de gouvernance, de comptabilité et de sécurité pour un abonnement Azure.

## <a name="purpose-of-the-landing-zone"></a>Objectif de la zone d’atterrissage

La zone d’atterrissage de base du Framework d’adoption du cloud pour Terraform comporte des éléments permettant d’assurer la journalisation, la comptabilité et la sécurité. Cette zone d’atterrissage utilise des composants standard connus sous le nom de modules Terraform pour garantir la cohérence entre les ressources déployées dans l’environnement.

## <a name="use-standard-modules"></a>Utiliser des modules standard

La réutilisation des composants est un principe fondamental de l’infrastructure en tant que code. Les modules jouent un rôle déterminant dans la définition des normes et la cohérence du déploiement des ressources à l’échelle de chaque environnement. Les modules utilisés pour déployer cette première zone d’atterrissage sont disponibles dans le [registre Terraform](https://registry.terraform.io/modules/aztfmod) officiel.

## <a name="architecture-diagram"></a>Diagramme de l'architecture

La première zone d’atterrissage déploie les composants suivants dans votre abonnement :

![Zone d’atterrissage de base utilisant Terraform](../../_images/ready/foundations-terraform-landing-zone.png)

## <a name="capabilities"></a>Fonctionnalités

Les composants déployés et leur rôle comprennent ce qui suit :

<!-- markdownlint-disable MD033 -->

| Composant | Responsabilité |
|---|---|
| Groupes de ressources | Principaux groupes de ressources nécessaires pour la base |
| Journalisation de l’activité | Audit de toutes les activités d’abonnement et de l’archivage : <li> Compte de stockage <li> Hubs d'événements Azure |
| Journalisation des diagnostics | Tous les journaux d’opérations sont conservés pendant un certain nombre de jours : <li> Compte de stockage <li> Event Hubs |
| Log Analytics | Stocke tous les journaux d’opérations. Déploie des solutions courantes pour un examen approfondi des meilleures pratiques d’application : <li> Networkmonitoring <li> Adassessment <li> Adreplication <li> Agenthealthassessment <li> Dnsanalytics <li> Keyvaultanalytics |
| Azure Security Center | Envoi de mesures et d’alertes en matière d’hygiène de sécurité par e-mail et numéro de téléphone |

<!-- markdownlint-enable MD033 -->

## <a name="use-this-blueprint"></a>Utilisation du blueprint

Avant d’utiliser la zone d’atterrissage de base du Framework d’adoption du cloud, passez en revue les hypothèses, les décisions et les recommandations d’implémentation suivantes.

## <a name="assumptions"></a>Hypothèses

Les hypothèses ou contraintes suivantes ont été prises en compte lors de la définition de cette zone d’atterrissage initiale. Si ces hypothèses s’alignent sur vos contraintes, vous pouvez utiliser le blueprint pour créer votre première zone d’accueil. Le blueprint peut également être étendu pour créer un blueprint de zone d’accueil qui réponde à vos contraintes uniques.

- **Limites d’abonnement :** Il est peu probable que cet effort d’adoption dépasse les [limites d’abonnement](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits). Deux indicateurs courants sont un excès de 25 000 machines virtuelles ou 10 000 processeurs virtuels.
- **Conformité :** Aucune exigence de tiers en matière de conformité n’est requise pour cette zone d’atterrissage.
- **Complexité architecturale :** La complexité architecturale ne nécessite pas d’abonnements de production supplémentaires.
- **Services partagés :** Aucun des services partagés existants dans Azure ne nécessite que cet abonnement soit traité comme un spoke dans une architecture hub and spoke.

Si ces hypothèses correspondent à votre environnement actuel, ce blueprint peut être une bonne façon de commencer à créer votre zone d’atterrissage.

## <a name="design-decisions"></a>Choix de conception

Les décisions suivantes sont représentées dans la zone d’atterrissage Terraform :

| Composant              | Décisions                                                                                                                                                                                                                                                                | Autres approches                                                                                                                                                                                                                                          |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enregistrement et surveillance | L’espace de travail Azure Monitor Log Analytics est utilisé. Un compte de stockage de diagnostics et un Event Hub sont approvisionnés.                                                                                                                                                        |                                                                                                                                                                                                                                                                 |
| Réseau                | N/A : le réseau est implémenté dans une autre zone d'atterrissage.                                                                                                                                                                                                                    | [Décisions en matière de mise en réseau](../considerations/networking-options.md)                                                                                                                                                                                                 |
| Identité               | Il est supposé que l’abonnement est déjà associé à une instance de Azure Active Directory.                                                                                                                                                                        | [Meilleures pratiques de gestion des identités](https://docs.microsoft.com/azure/security/fundamentals/identity-management-best-practices)                                                                                                                               |
| Stratégie                 | Cette zone d’atterrissage indique actuellement qu’aucune stratégie Azure ne doit être appliquée.                                                                                                                                                                                            |                                                                                                                                                                                                                                                                 |
| Conception de l’abonnement    | N/A : conçu pour un abonnement de production unique.                                                                                                                                                                                                                     | [Créer des abonnements initiaux](../azure-best-practices/initial-subscriptions.md)                                                                                                                                                                                  |
| Groupes de ressources        | N/A : conçu pour un abonnement de production unique.                                                                                                                                                                                                                     | [Abonnements de mise à l’échelle](../azure-best-practices/scale-subscriptions.md)                                                                                                                                                                                           |
| Groupes d’administration      | N/A : conçu pour un abonnement de production unique.                                                                                                                                                                                                                     | [Organiser les abonnements](../azure-best-practices/organize-subscriptions.md)                                                                                                                                                                                     |
| Données                   | N/A                                                                                                                                                                                                                                                                      | [Choix de la bonne option SQL Server dans Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) et [instructions relatives aux magasins de données Azure](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) |
| Stockage                | N/A                                                                                                                                                                                                                                                                      | [Conseils relatifs à Stockage Azure](../considerations/storage-options.md)                                                                                                                                                                                                  |
| Normes d’attribution de noms       | Un préfixe unique est créé en même temps que la création de l’environnement. Les ressources qui requièrent un nom global unique (par exemple, les comptes de stockage) utilisent ce préfixe. Le nom personnalisé est ajouté avec un suffixe aléatoire. L’utilisation des balises est obligatoire tel que décrit dans le tableau ci-dessous. | [Meilleures pratiques en matière de nommage et de catégorisation](../azure-best-practices/naming-and-tagging.md)                                                                                                                                                                              |
| la gestion des coûts ;        | N/A                                                                                                                                                                                                                                                                      | [Coûts de suivi](../azure-best-practices/track-costs.md)                                                                                                                                                                                                        |
| Calcul                | N/A                                                                                                                                                                                                                                                                      | [Options de calcul](../considerations/compute-options.md)                                                                                                                                                                                                         |

### <a name="tagging-standards"></a>Normes de catégorisation

Cet ensemble minimal d’étiquettes doit se trouver dans toutes les ressources et tous les groupes de ressources :

| Nom de la balise          | Description                                                                                        | Clé             | Valeur d'exemple                                    |
|-------------------|----------------------------------------------------------------------------------------------------|-----------------|--------------------------------------------------|
| Unité commerciale     | Division de niveau supérieur de votre entreprise qui est propriétaire de l’abonnement ou de la charge de travail auxquels la ressource appartient. | Businessunit    | Finance, marketing, {Nom du produit}, corp, shared |
| Centre de coûts       | Centre de coût comptable associé à cette ressource.                                              | Costcenter      | Number                                           |
| Récupération d'urgence | Caractère critique pour l’entreprise de l’application, de la charge de travail ou du service.                                     | Dr              | Dr-enabled, non-dr-enabled                       |
| Environnement       | Environnement de déploiement de l’application, de la charge de travail ou du service.                                   | Env             | Prod, dev, QA, stage, test, training             |
| Nom du propriétaire        | Propriétaire de l’application, de la charge de travail ou du service.                                                    | Propriétaire           | E-mail                                            |
| Type de déploiement   | Définit la façon dont les ressources sont conservées.                                                    | Deploymenttype  | Manual, Terraform                                |
| Version           | Version du blueprint déployé.                                                                 | Version         | V0.1                                             |
| Nom de l'application  | Nom de l’application, du service ou de la charge de travail auxquels la ressource est associée.             | Applicationname | « Nom de l'application »                                       |

<!-- cSpell:ignore caf -->

## <a name="customize-and-deploy-your-first-landing-zone"></a>Personnaliser et déployer votre première zone d’atterrissage

Vous pouvez [cloner votre zone d’atterrissage de base Terraform](https://github.com/azure/caf-terraform-landingzones). Démarrez facilement avec la zone d’atterrissage en modifiant les variables Terraform. Dans notre exemple, nous utilisons **blueprint_foundations.sandbox.auto.tfvars**, de sorte que Terraform définit automatiquement les valeurs de ce fichier pour vous.

Examinons les différentes sections variables.

Dans ce premier objet, nous créons deux groupes de ressources dans la région `southeastasia`, nommés `-hub-core-sec` et `-hub-operations` avec un préfixe ajouté au moment de l’exécution.

```hcl
resource_groups_hub = {
    HUB-CORE-SEC    = {
        name = "-hub-core-sec"
        location = "southeastasia"
    }
    HUB-OPERATIONS  = {
        name = "-hub-operations"
        location = "southeastasia"
    }
}
```

Ensuite, nous spécifions les régions dans lesquelles nous pouvons définir les fondations. Ici, `southeastasia` est utilisé pour déployer toutes les ressources.

```hcl
location_map = {
    region1   = "southeastasia"
    region2   = "eastasia"
}
```

Ensuite, nous spécifions la période de rétention pour les journaux d’opérations et les journaux d’abonnement Azure. Ces données sont stockées dans des comptes de stockage distincts et un Event Hub, dont les noms sont générés de manière aléatoire, car ils doivent être uniques.

```hcl
azure_activity_logs_retention = 365
azure_diagnostics_logs_retention = 60
```

Dans le tags_hub, nous spécifions l’ensemble minimum de balises qui sont appliquées à toutes les ressources créées.

```hcl
tags_hub = {
    environment     = "DEV"
    owner           = "Arnaud"
    deploymentType  = "Terraform"
    costCenter      = "65182"
    BusinessUnit    = "SHARED"
    DR              = "NON-DR-ENABLED"
}
```

Ensuite, nous précisons le nom de l'analytique des journaux d'activité et un ensemble de solutions qui analysent le déploiement. Ici, nous avons conservé Supervision réseau, Évaluation d'Active Directory et Réplication, DNS Analytics et Key Vault Analytics.

```hcl

analytics_workspace_name = "lalogs"

solution_plan_map = {
    NetworkMonitoring = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/NetworkMonitoring"
    },
    ADAssessment = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/ADAssessment"
    },
    ADReplication = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/ADReplication"
    },
    AgentHealthAssessment = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/AgentHealthAssessment"
    },
    DnsAnalytics = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/DnsAnalytics"
    },
    KeyVaultAnalytics = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/KeyVaultAnalytics"
    }
}

```

Puis, nous avons configuré les paramètres d’alerte pour Azure Security Center.

```hcl
# Azure Security Center Configuration
security_center = {
    contact_email   = "joe@contoso.com"
    contact_phone   = "+6500000000"
}
```

## <a name="get-started"></a>Bien démarrer

Une fois que vous avez examiné la configuration, vous pouvez la déployer comme vous le feriez pour déployer un environnement Terraform. Nous vous recommandons d’utiliser le rover, qui est un conteneur Docker qui permet le déploiement à partir de Windows, Linux ou macOS. Vous pouvez commencer à utiliser les [zones d’atterrissage](https://github.com/azure/caf-terraform-landingzones).

## <a name="next-steps"></a>Étapes suivantes

La zone d’atterrissage de base constitue le fondement d’un environnement complexe de façon décomposée. Cette édition fournit un ensemble de fonctionnalités simples qui peuvent être étendues par :

- l’ajout d’autres modules au blueprint ;
- la superposition de zones d’atterrissage supplémentaires.

La superposition de zones d’atterrissage est une bonne pratique pour découpler les systèmes, gérer les versions de chaque composant que vous utilisez, et permettre une innovation rapide et une stabilité pour votre infrastructure sous forme de déploiement du code.

De futures architectures de référence démontreront ce concept pour une topologie hub-and-spoke.

> [!div class="nextstepaction"]
> [Examiner l’échantillon de la zone d’atterrissage Terraform de base](https://github.com/azure/caf-terraform-landingzones)
