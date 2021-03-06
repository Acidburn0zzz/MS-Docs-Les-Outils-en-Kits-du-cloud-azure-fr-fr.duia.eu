---
title: 'Innovation Azure : Interagir via des appareils'
description: Découvrez comment Azure fournit un framework pour la création de solutions d’entreprise immersives et efficaces via des appareils de périphérie connectés et perceptifs.
author: umarmohamedusman
ms.author: umarm
ms.date: 10/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 0b876c402f18492b956b5ae561107ec6b57e63ee
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83862107"
---
<!-- cSpell:ignore umarmohamedusman umarm Moovit -->

::: zone target="docs"

# <a name="azure-innovation-guide-interact-through-devices"></a>Guide d’innovation Azure : Interagir par le biais des appareils

::: zone-end

::: zone target="chromeless"

# <a name="interact-through-devices"></a>Interagir par le biais des appareils

::: zone-end

Innovez avec des appareils connectés par intermittence et des appareils de périmètre perceptifs. Orchestrez des millions de ces appareils, acquérez et traitez des données illimitées et tirez parti d’un nombre croissant d’expériences multipériphériques et multicapteurs. Pour les appareils à la périphérie de votre réseau, Azure fournit une infrastructure pour la création de solutions d’entreprise immersifs et efficaces. Avec l’informatique ubiquitaire, activée par Azure et par une technologie d’intelligence artificielle (IA), vous pouvez concevoir chaque type d’application et de système intelligent que vous pouvez imaginer.

Les clients Azure utilisent un ensemble de systèmes et d’appareils connectés en perpétuelle expansion qui accumule et analyse des données&mdash;(proches de vos utilisateurs, de vos données, ou les deux). Les utilisateurs reçoivent des aperçus et des expériences en temps réel, livrées par des applications conscientes du contexte et hautement réactives. En déplaçant des parties de la charge de travail en périphérie, ces appareils peuvent passer moins de temps à envoyer des messages vers le cloud et réagir plus rapidement aux événements spatiaux.

> [!div class="checklist"]
>
> - Ressources industrielles
> - [Microsoft HoloLens 2](https://docs.microsoft.com/hololens)
> - [Azure Sphere](https://docs.microsoft.com/azure-sphere/product-overview/what-is-azure-sphere)
> - [Azure Kinect DK](https://docs.microsoft.com/azure/kinect-dk/about-azure-kinect-dk)
> - Drones
> - [Azure SQL Edge](https://docs.microsoft.com/azure/azure-sql-edge/overview)
> - [IoT Plug and Play](https://docs.microsoft.com/azure/iot-pnp/overview-iot-plug-and-play)

<!-- markdownlint-disable MD025 -->

## <a name="global-scale-iot-service"></a>[Service IoT à l’échelle mondiale](#tab/IoTHub)

<!-- markdownlint-enable MD025 -->

Concevez des solutions qui exercent une communication bidirectionnelle avec les appareils IoT à l’échelle de milliards. Utilisez les données de télémétrie transmises par les appareils au cloud prêtes à l’emploi pour comprendre l’état de vos appareils et définir des itinéraires d’acheminement de messages vers d’autres services Azure, simplement par la configuration. En tirant parti des messages du cloud vers les appareils, vous pouvez envoyer en toute confiance des commandes et des notifications à vos appareils connectés et suivez la remise des messages avec des accusés de réception. Si besoin, renvoyez automatiquement des messages aux appareils à des fins de connectivité intermittente.

Voici quelques-unes des fonctionnalités que vous trouverez :

- **Canal de communication sécurisé** pour envoyer et recevoir des données à partir d'appareils IoT.
- **Gestion intégrée des appareils** et provisionnement pour connecter et gérer les appareils IoT à grande échelle.
- **Intégration complète à Event Grid** et calcul sans serveur pour simplifier le développement d'applications IoT.
- **Compatibilité avec Azure IoT Edge** pour créer des applications IoT hybrides.

::: zone target="docs"

### <a name="learn-more"></a>En savoir plus

- [IoT Hub](https://docs.microsoft.com/azure/iot-hub)

- [Service Azure IoT Hub Device Provisioning (DPS)](https://docs.microsoft.com/azure/iot-dps)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Action

Pour créer un hub IoT :

1. Accédez à **IoT Hub**.
2. Sélectionnez **Créer un hub IoT**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FIotHubs]" submitText="Go to IoT Hub" :::

<!-- markdownlint-enable DOCSMD001 -->

Le service Azure IoT Hub Device Provisioning est un service d’assistance pour IoT Hub qui permet le provisionnement sans contact et juste-à-temps.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Action

Pour créer un service Azure IoT Hub Device Provisioning :

1. Accédez à **Services Device Provisioning**.
2. Sélectionnez **Ajouter**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FProvisioningServices]" submitText="Go to Device Provisioning Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="azure-digital-twins"></a>[Azure Digital Twins](#tab/DigitalTwins)

Créez des expériences à intelligence spatiale réutilisables et extrêmement scalables qui relient les données de streaming entre le monde numérique et le monde physique. Améliorez votre engagement client à l’aide de modèles complets d’environnements physiques. Générez des graphes d’intelligence spatiale afin de modéliser les relations et les interactions entre les personnes, les espaces et les appareils. Interrogez les données à partir d’un espace physique plutôt que des capteurs disparates.

**Modèles objet Azure Digital Twins :** Une ontologie qui décrit les régions, les lieux, les étages, les bureaux, les zones, les salles de conférence et les salles de focalisation d’un immeuble, ou diverses stations d’alimentation, sous-stations, ressources énergétiques et clients d’une grille d’énergie, peut être modelée à l’aide d’ontologies et de modèles d’objets Digital Twins.

**Graphique d’intelligence spatiale :** Graphique hiérarchique des espaces, des appareils et des personnes définis dans le modèle objet Digital Twins qui prend en charge l’héritage, le filtrage, le parcours, la mise à l’échelle et l’extensibilité. Vous pouvez gérer votre graphe spatial et interagir avec ce dernier à l’aide d’une collection d’API REST hébergées dans Azure.

::: zone target="docs"

### <a name="learn-more"></a>En savoir plus

- [Azure Digital Twins](https://docs.microsoft.com/azure/digital-twins/about-digital-twins)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Action

Pour créer Azure Digital Twins :

1. Dans le volet de gauche, sélectionnez **Créer une ressource**.
2. Recherchez **digital twins**, puis sélectionnez **Digital Twins**.
3. Sélectionnez **Créer** pour commencer le processus de déploiement.
4. Pour passer en revue les Digital Twins existants, sélectionnez ce bouton :

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.IoTSpaces%2FGraph]" submitText="Go to Digital Twins" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="location-intelligence"></a>[Intelligence géographique](#tab/AzureMaps)

En plus des fonctionnalités de localisation traditionnelles, telles que la proximité, le trafic et le routage, le service Azure Maps permet aux entreprises de créer des solutions à l’aide de l’intelligence de localisation en temps réel, alimentée par des partenaires de technologie de mobilité de classe mondiale **TomTom** et **Moovit**. Intégrez facilement des fonctionnalités avancées de localisation et de mobilité dans vos applications avec les services géospatiaux.

**Data Service (préversion) :** Chargez et stockez des données géospatiales à utiliser pour des opérations spatiales ou la composition d’images pour réduire le temps de latence, augmenter la productivité et activer de nouveaux scénarios au sein de vos applications.

**Opérations spatiales :** Améliorez votre géolocalisation avec une bibliothèque de calculs mathématiques géospatiaux courants, notamment le geofencing, le point le plus proche, la distance du grand cercle et les mises en mémoire tampon.

**Géolocalisation :** Recherchez le pays d’une adresse IP. Personnalisez le contenu et les services en fonction de l’emplacement de l’utilisateur, et obtenez des informations sur la répartition géographique des clients.

::: zone target="docs"

### <a name="learn-more"></a>En savoir plus

- [Azure Maps](https://docs.microsoft.com/azure/azure-maps)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Action

Pour utiliser l’intelligence géographique :

1. Accédez à **Comptes Azure Maps**.
2. Sélectionnez **Créer des comptes Azure Maps**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Maps%2FAccounts]" submitText="Go to Azure Maps Account" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="spatial-experiences"></a>[Expériences spatiales](#tab/spatial)

Azure Spatial Anchors permet aux développeurs de travailler sur des plateformes de réalité mixte afin de percevoir les espaces, de désigner des points d’intérêt précis et de rappeler ces mêmes points d’intérêt sur les appareils pris en charge.

**Ajoutez du contexte au monde réel :** Apportez à vos utilisateurs une meilleure compréhension de leurs données, où ils en ont besoin et quand ils en ont besoin, en plaçant et connectant votre contenu numérique à des points d’intérêt physiques.

**Partagez des hologrammes entre appareils :** Accélérez les décisions et les résultats en apportant la 3D à votre équipe et à vos clients sur les appareils de leur choix. Spatial Anchors permet à des personnes situées dans un même espace d’utiliser facilement des applications de réalité mixte multi-utilisateurs.

**Expériences d’engagement :** Connectez les ancres spatiales en créant des relations entre elles, et fournissez une expérience utilisateur qui peut inclure au moins deux points d’intérêt avec lesquels un utilisateur doit interagir pour effectuer une tâche. Votre application peut permettre à un utilisateur de placer un artefact virtuel dans le monde réel. Dans un environnement industriel, un utilisateur pourrait obtenir des informations contextuelles sur une machine en pointant vers celle-ci l’appareil photo d’un appareil pris en charge.

Azure Spatial Anchors se compose d’un service managé et de kits SDK clients pour les plateformes d’appareils prises en charge.

::: zone target="docs"

- [Azure Spatial Anchors](https://azure.microsoft.com/services/spatial-anchors)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Action

Pour utiliser les expériences spatiales :

1. Accédez à **Comptes Spatial Anchors**.
2. Sélectionnez **Créer des comptes Spatial Anchors**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.MixedReality%2FSpatialAnchorsAccounts]" submitText="Go to Spatial Anchors Accounts" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-remote-rendering"></a>[Azure Remote Rendering](#tab/RemoteRender)

Restituez du contenu 3D interactif de haute qualité et diffusez-le sur vos appareils en temps réel. Les charges de travail de rendu sont principalement utilisées pour les effets spéciaux (VFX) dans l’industrie du multimédia et du divertissement. Le rendu est également utilisé dans de nombreux autres secteurs comme la publicité, la vente au détail, le pétrole et le gaz et la fabrication.

Le processus de rendu exige beaucoup de ressources informatiques. Il peut y avoir plusieurs images ou images à produire, et la restitution de chaque image peut prendre plusieurs heures. Par conséquent, le rendu est une charge de travail idéale pour le traitement par lots qui peut utiliser Azure et Azure Batch pour exécuter plusieurs rendus en parallèle.

::: zone target="docs"

### <a name="learn-more"></a>En savoir plus

- [Azure Remote Rendering](https://azure.microsoft.com/services/remote-rendering)

- [Rendu avec Azure](https://docs.microsoft.com/azure/batch/batch-rendering-service)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Action

Pour utiliser Remote Rendering :

1. Accédez à **Comtes Batch**.
2. Sélectionnez **Créer des comptes Batch**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Batch%2FBatchAccounts]" submitText="Go to Azure Batch" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
