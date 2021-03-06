---
title: Gestion de l’accès aux ressources dans Azure
description: Appréhendez les concepts de gestion d’accès aux ressources Azure comme Azure Resource Manager, les abonnements, les groupes de ressources et les ressources.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 9bcd4fb4a516062c053322932e1de878f4ec9095
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83756173"
---
# <a name="resource-access-management-in-azure"></a>Gestion de l’accès aux ressources dans Azure

La rubrique [Méthodologie de gouvernance](../index.md) présente les Cinq disciplines de la gouvernance du cloud, ce qui inclut la gestion des ressources. La rubrique [Présentation de la gouvernance des accès aux ressources](./index.md) explique comment la gestion de l’accès aux ressources s’inscrit dans la discipline de gestion des ressources. Avant de découvrir comment concevoir un modèle de gouvernance, il est important de comprendre les contrôles de gestion des accès aux ressources dans Azure. La configuration de ces contrôles de gestion des accès aux ressources constitue la base de votre modèle de gouvernance.

Commencez par examiner de plus près le déploiement des ressources dans Azure.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-an-azure-resource"></a>Qu’est-ce qu’une ressource Azure ?

Dans Azure, le terme _ressource_ fait référence à une entité gérée par Azure. Par exemple, les machines virtuelles, les réseaux virtuels et les comptes de stockage sont tous considérés comme des ressources Azure.

![Diagramme d’une ressource](../../_images/govern/design/governance-1-9.png)
_Figure 1 : Une ressource._

## <a name="what-is-an-azure-resource-group"></a>Qu’est-ce qu’un groupe de ressources Azure ?

Chaque ressource dans Azure doit appartenir à un [groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/management/overview#resource-groups). Un groupe de ressources est simplement une construction logique qui regroupe plusieurs ressources afin qu’elles puissent être gérées en tant qu’entité unique _en fonction du cycle de vie et des aspects de sécurité_. Par exemple, des ressources qui partagent un cycle de vie similaire, tels que les ressources d’une [application multi-niveau](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier), peuvent être créées ou supprimées en tant que groupe. En d’autres termes, toutes les ressources créées ensemble, gérées ensemble et dépréciées ensemble sont regroupées dans un groupe de ressources.

![Diagramme d’un groupe de ressources contenant une ressource](../../_images/govern/design/governance-1-10.png)
_Figure 2 : Un groupe de ressources contient une ressource._

Les groupes de ressources et les ressources qu’ils contiennent sont associés à un **abonnement** Azure.

## <a name="what-is-an-azure-subscription"></a>Qu’est-ce qu’un abonnement Azure ?

Un abonnement Azure est similaire à un groupe de ressources : il s’agit d’une construction logique qui regroupe des groupes de ressources et leurs ressources. Un abonnement Azure est également associé aux contrôles utilisés par Azure Resource Manager. Examinez plus en détail Azure Resource Manager pour en savoir plus sur sa relation avec un abonnement Azure.

![Diagramme d’un abonnement Azure](../../_images/govern/design/governance-1-11.png)
_Figure 3 : Un abonnement Azure._

## <a name="what-is-azure-resource-manager"></a>Qu’est-ce qu’Azure Resource Manager ?

Dans [Fonctionnement d’Azure](../../get-started/what-is-azure.md), vous avez découvert qu’Azure comprend un front-end avec de nombreux services qui orchestrent toutes les fonctions d’Azure. L’un de ces services, [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager), héberge l’API RESTful utilisée par les clients pour gérer les ressources.

![Diagramme d’Azure Resource Manager](../../_images/govern/design/governance-1-12.png)
_Figure 4 : Azure Resource Manager._

La figure suivante montre trois clients : [PowerShell](https://docs.microsoft.com/powershell/azure/overview), le [Portail Azure](https://portal.azure.com) et l’[interface CLI Azure](https://docs.microsoft.com/cli/azure) :

![Diagramme de clients Azure se connectant à l’API Azure Resource Manager](../../_images/govern/design/governance-1-13.png)
_Figure 5 : Les clients Azure se connectent à l’API RESTful Azure Resource Manager._

Bien que ces clients se connectent à Azure Resource Manager à l’aide de l’API RESTful, Azure Resource Manager n’inclut pas de fonctionnalités permettant de gérer directement les ressources. Au lieu de cela, la plupart des types de ressources Azure ont leur propre [fournisseur de ressources](https://docs.microsoft.com/azure/azure-resource-manager/management/overview#terminology).

![Fournisseurs de ressources Azure](../../_images/govern/design/governance-1-14.png)
_Figure 6 : Fournisseurs de ressources Azure._

Quand un client effectue une requête pour gérer une ressource spécifique, Azure Resource Manager se connecte au fournisseur de ressources pour ce type de ressources afin d’exécuter la requête. Par exemple, si un client effectue une requête pour gérer une ressource de machine virtuelle, Azure Resource Manager se connecte au fournisseur de ressources **Microsoft.Compute**.

![Azure Resource Manager se connectant au fournisseur de ressources Microsoft.Compute](../../_images/govern/design/governance-1-15.png)
_Figure 7 : Azure Resource Manager se connecte au fournisseur de ressources **Microsoft.Compute** pour gérer la ressource spécifiée dans la requête du client._

Azure Resource Manager exige du client qu’il spécifie un identificateur pour l’abonnement et le groupe de ressources, afin de gérer la ressource de machine virtuelle.

Maintenant que vous comprenez le fonctionnement d’Azure Resource Manager, revenez à la présentation de la façon dont un abonnement Azure est associé aux contrôles utilisés par Azure Resource Manager. Avant qu’une requête de gestion des ressources ne soit exécutée par Azure Resource Manager, plusieurs contrôles sont vérifiés.

Le premier contrôle est qu’une requête doit être effectuée par un utilisateur validé, et qu’Azure Resource Manager a une relation de confiance avec [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory) pour fournir des fonctionnalités d’identité utilisateur.

![Azure Active Directory](../../_images/govern/design/governance-1-16.png)
_Figure 8 : Azure Active Directory._

Dans Azure AD, les utilisateurs sont segmentés sous forme de **clients**. Un client est une construction logique qui représente une instance d’Azure AD dédiée et sécurisée, généralement associée à une organisation. Chaque abonnement est associé à un client Azure AD.

![Un abonné Azure AD associé à un abonnement](../../_images/govern/design/governance-1-17.png)
_Figure 9 : Un client Azure AD associé à un abonnement._

Chaque requête du client pour gérer une ressource dans un abonnement spécifique requiert que l’utilisateur dispose d’un compte dans le client Azure AD associé.

Le contrôle suivant consiste à vérifier que l’utilisateur dispose des autorisations suffisantes pour effectuer la requête. Les autorisations sont attribuées aux utilisateurs à l’aide du [contrôle d’accès en fonction du rôle (RBAC)](https://docs.microsoft.com/azure/role-based-access-control).

![Des utilisateurs affectés aux rôles RBAC](../../_images/govern/design/governance-1-18.png)
_Figure 10 : Un ou plusieurs rôles RBAC sont attribués à chaque utilisateur du client._

Un rôle RBAC spécifie un ensemble d’autorisations qu’un utilisateur peut utiliser pour une ressource spécifique. Lorsque le rôle est attribué à l’utilisateur, ces autorisations s’appliquent. Par exemple, le [rôle de **propriétaire** intégré](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) autorise un utilisateur à effectuer une action sur une ressource.

Le contrôle suivant vérifie que la requête est autorisée sous les paramètres spécifiés dans la [stratégie de ressources Azure](https://docs.microsoft.com/azure/governance/policy). Les stratégies de ressources Azure spécifient les opérations autorisées pour une ressource spécifique. Par exemple, une stratégie de ressources Azure peut spécifier que les utilisateurs sont uniquement autorisés à déployer un type spécifique de machine virtuelle.

![Stratégie de ressource Azure](../../_images/govern/design/governance-1-19.png)
_Figure 11 : Stratégie de ressource Azure._

Le contrôle suivant consiste à vérifier que la requête ne dépasse pas une [limite d’abonnement Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits). Par exemple, chaque abonnement dispose d’une limite de 980 groupes de ressources par abonnement. Si une requête pour déployer un groupe de ressources supplémentaire est reçue lorsque la limite a été atteinte, elle est refusée.

![Limites des ressources Azure](../../_images/govern/design/governance-1-20.png)
_Figure 12 : Limites des ressources Azure._

Le contrôle final vérifie que la requête est comprise dans l’engagement financier associé à l’abonnement. Par exemple, si la requête doit déployer une machine virtuelle, Azure Resource Manager vérifie que l’abonnement dispose des informations de paiement suffisantes.

![Un engagement financier associé à un abonnement](../../_images/govern/design/governance-1-21.png)
_Figure 13 : Un engagement financier est associé à un abonnement._

## <a name="summary"></a>Résumé

Dans cet article, vous avez étudié la gestion des accès aux ressources dans Azure à l’aide d’Azure Resource Manager.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous comprenez comment gérer l’accès aux ressources dans Azure, poursuivez pour en savoir plus sur la conception d’un modèle de gouvernance [pour une charge de travail simple](./governance-simple-workload.md) ou pour [plusieurs équipes](./governance-multiple-teams.md) à l’aide de ces services.

> [!div class="nextstepaction"]
> [Une vue d’ensemble de la gouvernance](../index.md)
