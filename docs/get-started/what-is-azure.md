---
title: Fonctionnement d’Azure
description: Découvrez les principes de base de la structure interne et du fonctionnement de la plateforme cloud Azure et de la virtualisation cloud.
author: alexbuckgit
ms.author: abuck
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: governance
ms.openlocfilehash: 00d5709aeb0a922b8f8c5efd26abafe70d70a237
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755155"
---
<!-- cSpell:ignore PDU -->

<!-- markdownlint-disable MD026 -->

# <a name="how-does-azure-work"></a>Fonctionnement d’Azure

Azure est la plateforme de cloud public de Microsoft. Azure offre une grande collection de services, y compris la plateforme en tant que service (PaaS), l’infrastructure en tant que service (IaaS), la base de données gérée en tant que service (DBaaS). Mais ce qu’est -ce qu’Azure exactement et comment fonctionne-t-il ?

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2ixGo]

Azure, comme les autres plateformes de cloud, s’appuie sur une technologie appelée _virtualisation_. Le matériel informatique peut être, en général, émulé dans le logiciel, car il s’agit simplement d’un ensemble d’instructions encodées de façon permanente ou semi-permanente en silicium. À l’aide d’une couche d’émulation qui mappe les instructions du logiciel pour obtenir des instructions de matériel, le matériel virtualisé peut s’exécuter dans le logiciel comme s’il s’agissait du matériel réel lui-même.

Fondamentalement, le cloud est un ensemble de serveurs physiques dans un ou plusieurs centres de données qui exécutent un matériel virtualisé pour le compte de clients. Ainsi, comment le cloud crée, démarre, arrête et supprime-t-il simultanément des millions d’instances d’un matériel virtualisé pour des millions de clients ?

Pour le comprendre, examinons l’architecture du matériel dans le centre de données. Dans chaque centre de données se trouve une collection de serveurs dans les racks de serveurs. Chaque rack de serveurs contient de nombreuses **lames** de serveurs ainsi qu’un commutateur de réseau fournissant une connectivité réseau et une unité de distribution de l’alimentation (PDU) fournissant l’électricité. Les racks sont parfois regroupés en unités plus grandes appelées _clusters_.

Dans chaque rack ou cluster, la plupart des serveurs sont désignés pour exécuter ces instances du matériel virtualisé au nom de l’utilisateur. Mais certains serveurs exécutent le logiciel de gestion du cloud connu sous le nom de contrôleur de structure. Le _contrôleur de structure_ est une application distribuée avec beaucoup de responsabilités. Il alloue des services, analyse l’intégrité du serveur et les services qui y sont exécutés et répare des serveurs en cas d’échec.

Chaque instance du contrôleur de structure est connectée à un autre ensemble de serveurs exécutant le logiciel d’orchestration du cloud, généralement appelé _frontal_. Le serveur frontal héberge les services web, les API RESTful et les bases de données Azure internes utilisés pour toutes les fonctions exécutées par le cloud.

Par exemple, le serveur frontal héberge les services qui gèrent les demandes clients pour allouer des ressources Azure telles que des [machines virtuelles](https://docs.microsoft.com/azure/virtual-machines) et des services tels qu'[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction). Tout d’abord, le serveur frontal valide l’utilisateur et vérifie que l’utilisateur est autorisé à allouer les ressources demandées. Dans ce cas, le serveur frontal consulte une base de données pour localiser un rack de serveurs avec une capacité suffisante, puis fait en sorte que le contrôleur de structure sur ce rack alloue la ressource.

Azure est tout simplement une vaste collection de serveurs et de matériel réseau qui exécutent un ensemble complexe d’applications distribuées qui orchestrent la configuration et l’opération du matériel et des logiciels virtualisés sur ces serveurs. C’est cette orchestration qui fait toute la puissance d’Azure : les utilisateurs ne sont plus responsables du suivi, ni de la mise à niveau du matériel, Azure effectuant tout cela en arrière-plan.

## <a name="next-steps"></a>Étapes suivantes

Découvrez plus en détail l’adoption du cloud avec [Microsoft Cloud Adoption Framework pour Azure](../index.yml).

> [!div class="nextstepaction"]
> [En savoir plus sur Microsoft Cloud Adoption Framework pour Azure](../index.yml)
