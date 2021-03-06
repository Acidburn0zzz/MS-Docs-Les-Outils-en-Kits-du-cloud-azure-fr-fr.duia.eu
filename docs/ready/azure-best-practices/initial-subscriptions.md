---
title: Créer vos abonnements Azure initiaux
description: Commencez votre adoption d’Azure en créant vos abonnements initiaux.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 975248025ff170ff872fdd5970f548a8fc83c953
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83215396"
---
# <a name="create-your-initial-azure-subscriptions"></a>Créer vos abonnements Azure initiaux

Commencez votre adoption d’Azure en créant un ensemble initial d’abonnements. Découvrez les abonnements avec lesquels vous devez commencer en fonction de vos exigences initiales.

## <a name="your-first-two-subscriptions"></a>Vos deux premiers abonnements

Commencez par créer deux abonnements :

- Créez un abonnement Azure pour contenir vos charges de travail de production.
- Créez un deuxième abonnement qui servira d’environnement hors production (dev/test), dans le cadre d’une [offre Azure Dev/Test](https://azure.microsoft.com/pricing/dev-test) à un tarif inférieur.

![Modèle d’abonnement initial montrant des clés à côté de cases intitulées « production » et « hors production »](../../_images/ready/initial-subscription-model.png)

<!-- docsTest:ignore Dev/Test -->

Cette approche présente de nombreux avantages :

- L’utilisation d’abonnements distincts pour vos environnements de production et de non-production crée une limite qui simplifie et sécurise la gestion de vos ressources.
- Les offres d’abonnement Azure Dev/Test sont disponibles pour les charges de travail hors production. Ces offres fournissent des tarifs réduits sur les services et licences de logiciels Azure.
- Vos environnements de production et de non-production auront probablement différents ensembles de stratégies Azure. L’utilisation d’abonnements différents facilite l’application de chaque stratégie distincte au niveau de l’abonnement.
- Vous pouvez autoriser certains types de ressources Azure dans votre abonnement de non-production à des fins de test. Vous pouvez activer ces fournisseurs de ressources dans votre abonnement de non-production sans les rendre disponibles dans votre environnement de production.
- Vous pouvez utiliser les abonnements de développement/test comme des environnements de bac à sable isolés. Ces bacs à sable permettent aux administrateurs et aux développeurs de générer et de désactiver rapidement des ensembles complets de ressources Azure. Cette isolation peut également aider à résoudre les problèmes de sécurité et de protection des données.
- Les seuils de coût acceptables que vous définissez varieront probablement suivant les abonnements de production et de développement/test.

## <a name="sandbox-subscriptions"></a>Abonnements de bac à sable (sandbox)

Si votre stratégie d’adoption du cloud comprend des objectifs d’innovation, envisagez de créer un ou plusieurs abonnements sandbox. Vous pouvez appliquer des stratégies de sécurité pour que ces abonnements de test soient isolés de vos environnements de production et de non-production. Les utilisateurs peuvent facilement tester les fonctionnalités Azure dans ces environnements isolés. Utilisez une offre Dev/Test Azure pour créer ces abonnements.

![Modèle d’abonnement initial montrant des clés à côté de cases intitulées « production », « hors production » et « sandbox »](../../_images/ready/initial-subscription-model-with-sandboxes.png)

## <a name="shared-services-subscription"></a>Abonnement de services partagés

Si vous envisagez d’héberger **plus de 1 000 machines virtuelles ou instances de calcul dans le cloud d’ici 24 mois**, créez un autre abonnement Azure pour héberger les services partagés. Cela vous préparera à l’avance à la prise en charge de l’architecture d’entreprise finalisée.

![Modèle d’abonnement initial montrant des clés à côté de cases intitulées « production » et « services partagés »](../../_images/ready/initial-subscription-model-with-shared-services.png)

## <a name="next-steps"></a>Étapes suivantes

Passez en revue les raisons pour lesquelles vous pouvez vouloir [créer des abonnements Azure supplémentaires](./scale-subscriptions.md) pour répondre à vos besoins.

> [!div class="nextstepaction"]
> [Créer des abonnements supplémentaires pour mettre à l’échelle votre environnement Azure](./scale-subscriptions.md)
