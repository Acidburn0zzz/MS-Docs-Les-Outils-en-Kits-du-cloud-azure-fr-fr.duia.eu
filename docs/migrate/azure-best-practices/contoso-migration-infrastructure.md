---
title: Déployer une infrastructure de migration
description: Découvrez comment Contoso configure une infrastructure Azure pour la migration vers Azure.
author: deltadan
ms.author: abuck
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: cf026f32e52f5742525e655cd904e152e849bcd6
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83861971"
---
<!-- cSpell:ignore deltadan CSPs untrust CIDR RRAS CONTOSODC sysvol ITIL NSGs ASGs -->

# <a name="deploy-a-migration-infrastructure"></a>Déployer une infrastructure de migration

Cet article explique comment la société fictive Contoso prépare son infrastructure locale pour la migration, configure une infrastructure Azure en vue de la migration et exécute les activités dans un environnement hybride. Lorsque vous utilisez cet exemple pour vous aider à planifier vos propres efforts de migration d’infrastructure, gardez les points suivants à l’esprit :

- L’exemple d’architecture présenté est spécifique à Contoso. Passez en revue les besoins commerciaux et les exigences techniques et structurelles de votre organisation lorsque vous prenez d’importantes décisions en matière d’infrastructure concernant la conception des abonnements ou l’architecture réseau.
- Votre stratégie de migration détermine si vous avez besoin de tous les éléments décrits dans l’article. Par exemple, si vous créez uniquement des applications cloud en mode natif dans Azure, vous aurez peut-être besoin d’une structure de mise en réseau moins complexe.

## <a name="overview"></a>Vue d’ensemble

Avant de pouvoir effectuer la migration vers Azure, Contoso doit impérativement préparer une infrastructure Azure. Généralement, Contoso doit prendre en compte six points essentiels :

> [!div class="checklist"]
>
> - **Étape 1 : Abonnements Azure.** comment acheter Azure, et interagir avec la plateforme et les services Azure ?
> - **Étape 2 : Identité hybride.** comment gérer et contrôler l’accès aux ressources locales et Azure après la migration ? Comment étendre ou transférer la gestion des identités vers le cloud ?
> - **Étape 3 : Récupération d’urgence et résilience.** comment garantir la résilience des applications et de l’infrastructure en cas de pannes et de sinistres ?
> - **Étape 4 : Mise en réseau.** comment concevoir une infrastructure réseau et établir la connectivité entre le centre de données local et Azure ?
> - **Étape 5 : Sécurité.** Comment le déploiement Azure ou hybride sera-t-il sécurisé ?
> - **Étape 6 : Gouvernance.** comment garder le déploiement en phase avec les exigences de gouvernance et de sécurité ?

## <a name="before-you-start"></a>Avant de commencer

Avant de commencer à examiner l'infrastructure, pensez à lire quelques informations générales sur les fonctionnalités Azure pertinentes :

- Plusieurs options sont disponibles pour l’achat d’un accès Azure, notamment le paiement à l’utilisation, les Contrats Entreprise (EA), les licences Open de revendeurs Microsoft ou de Partenaires Microsoft appelés fournisseurs de solutions cloud (CSP). En savoir plus sur les [options d’achat](https://azure.microsoft.com/pricing/purchase-options) et la façon dont les [abonnements Azure sont organisés](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).
- Obtenez une vue d’ensemble de la [gestion de l'identité et de l'accès](https://www.microsoft.com/security/business/identity) Azure. En particulier, découvrez [Azure AD et l’extension d’Active Directory local vers le cloud](https://docs.microsoft.com/azure/active-directory/identity-fundamentals). Il existe un livre électronique téléchargeable très utile sur la [gestion de l’identité et de l’accès (IAM) dans un environnement hybride](https://azure.microsoft.com/resources/hybrid-cloud-identity).
- Azure fournit une infrastructure réseau fiable avec des options de connectivité hybride. Obtenez une vue d’ensemble de la [mise en réseau et du contrôle d’accès réseau](https://docs.microsoft.com/azure/security/security-network-overview).
- Lisez la [présentation de la sécurité Azure](https://docs.microsoft.com/azure/security/fundamentals/overview) et apprenez à créer un plan de [gouvernance Azure](https://docs.microsoft.com/azure/governance).

## <a name="on-premises-architecture"></a>Architecture locale

Voici un diagramme montrant l’infrastructure locale actuelle de Contoso.

 ![Architecture de Contoso](./media/contoso-migration-infrastructure/contoso-architecture.png)

- Contoso dispose d'un centre de données principal situé dans la ville de New York, dans l'Est des États-Unis.
- Il y a trois branches locales supplémentaires aux États-Unis.
- Le centre de données principal est connecté à Internet avec une connexion Ethernet Fiber Metro (500 Mbits/s).
- Chaque branche est connectée localement à Internet via des connexions de qualité professionnelle, avec des tunnels VPN IPSec vers le centre de données principal. Cette approche permet au réseau entier d’être connecté en permanence et optimise la connexion Internet.
- Le centre de données principal est entièrement virtualisé avec VMware. Contoso a deux hôtes de virtualisation ESXi 6.5 gérés par vCenter Server 6.5.
- Contoso utilise Active Directory pour la gestion des identités, et des serveurs DNS sur le réseau interne.
- Les contrôleurs de domaine du centre de données s’exécutent sur des machines virtuelles VMware. Les contrôleurs de domaine au niveau des branches locales s’exécutent sur des serveurs physiques.

## <a name="step-1-buy-and-subscribe-to-azure"></a>Étape 1 : Acheter et s’abonner à Azure

Contoso doit savoir comment acheter Azure, créer des abonnements et obtenir une licence pour les services et les ressources.

### <a name="buy-azure"></a>Acheter Azure

Contoso s’inscrit dans un [Contrat Entreprise (EA)](https://azure.microsoft.com/pricing/enterprise-agreement). Ce contrat implique un engagement financier initial en faveur d’Azure, permettant à Contoso d’obtenir d’importants avantages, notamment des options flexibles de facturation et des tarifs optimisés.

- Contoso a estimé ses dépenses Azure annuelles. Quand l’entreprise a signé le contrat, Contoso a payé la première année en totalité.
- Contoso doit utiliser tous les services dans l’année, sous peine de perdre les sommes versées.
- Si, pour une raison quelconque, Contoso dépasse son engagement et dépense plus que prévu, Microsoft facture la différence.
- Les coûts qui dépassent cet engagement sont calculés aux mêmes taux que ceux stipulés dans le contrat. Aucune pénalité n’est appliquée en cas de dépassement.

### <a name="manage-subscriptions"></a>Gérer les abonnements

Après avoir payé pour Azure, Contoso doit déterminer comment gérer les abonnements. Comme Contoso a signé un Contrat Entreprise, l’entreprise peut configurer autant d’abonnements Azure qu’elle le souhaite.

- L’inscription d’une entreprise Azure définit la forme et l’utilisation des services Azure en son sein et la structure de gouvernance principale.
- Dans un premier temps, Contoso a déterminé une structure (appelée structure d’entreprise) pour l’accord de mise en œuvre d’entreprise. Contoso s’est appuyé sur la [structure d’entreprise Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance) pour mieux comprendre comment concevoir une structure.
- Pour l’instant, Contoso a décidé d’utiliser une approche fonctionnelle pour gérer ses abonnements.
  - Dans l’entreprise, un seul service informatique contrôle le budget Azure. Ce sera le seul groupe avec des abonnements.
  - Contoso étendra ce modèle à l’avenir pour que d’autres groupes d’entreprise (services) puissent être ajoutés dans l’inscription de l’entreprise.
  - Au sein du service informatique, Contoso a structuré deux abonnements, Production et Développement.
  - Si Contoso a besoin de nouveaux abonnements à l’avenir, l’entreprise devra gérer l’accès, les stratégies et la conformité de ces abonnements. Elle peut le faire en introduisant des [groupes d’administration Azure](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview), sous forme de couche supplémentaire au-dessus des abonnements.

  ![Structure de l’entreprise](./media/contoso-migration-infrastructure/enterprise-structure.png)

### <a name="examine-licensing"></a>Examiner les licences

Une fois les abonnements configurés, Contoso peut examiner les licences Microsoft. La stratégie de licence dépendra des ressources que Contoso souhaite migrer vers Azure, et de la manière dont les machines virtuelles et les services seront sélectionnés et déployés dans Azure.

#### <a name="azure-hybrid-benefit"></a>Azure Hybrid Benefit

Lors du déploiement de machines virtuelles dans Azure, les images standard incluent une licence qui facture Contoso à la minute pour le logiciel utilisé. Toutefois, Contoso est un client Microsoft de longue date qui a conservé des Contrats Entreprise et des licences avec Software Assurance (SA).

Azure Hybrid Benefit est une méthode de migration rentable qui permet à Contoso de réaliser des économies sur les machines virtuelles Azure et les charges de travail SQL Server en convertissant ou en réutilisant les licences Windows Server Datacenter et Standard couvertes par la Software Assurance. Cela permet à Contoso de payer un taux de calcul de base inférieur pour les machines virtuelles et SQL Server. Pour plus d’informations, consultez [Azure Hybrid Benefit](https://azure.microsoft.com/pricing/hybrid-benefit).

#### <a name="license-mobility"></a>Mobilité de licence

Mobilité de licence à travers la Software Assurance octroie aux clients de licences en volume Microsoft comme Contoso la flexibilité de déployer des applications serveur éligibles grâce à l'activation de SA sur Azure. Cela élimine la nécessité d’acheter de nouvelles licences. Comme cette mobilité n’engendre aucuns frais, les licences existantes peuvent être facilement déployées dans Azure. Pour plus d’informations, consultez [License Mobility via Software Assurance sur Azure](https://azure.microsoft.com/pricing/license-mobility).

#### <a name="reserve-instances-for-predictable-workloads"></a>Réserver des instances pour les charges de travail prévisibles

Les charges de travail prévisibles sont celles qui doivent toujours être disponibles avec des machines virtuelles en cours d’exécution. Par exemple, les applications métier telles qu’un système ERP SAP. En revanche, les charges de travail imprévisibles sont celles qui sont variables, telles que les machines virtuelles qui sont activées en période de forte demande et désactivées lorsque la demande est faible.

![Instance réservée](./media/contoso-migration-infrastructure/reserved-instance.png)

En contrepartie de l’utilisation d’instances réservées pour des instances de machine virtuelle spécifiques qui doivent être gérées sur de longues périodes, Contoso peut bénéficier à la fois d’une remise et d’une capacité hiérarchisée. L'utilisation d'[instances réservées Azure](https://azure.microsoft.com/pricing/reserved-vm-instances) avec Azure Hybrid Benefit peut permettre à Contoso d'économiser jusqu'à 82 % sur les prix habituels du paiement à l'utilisation (à partir d'avril 2018).

## <a name="step-2-manage-hybrid-identity"></a>Étape 2 : Gérer l’identité hybride

L’octroi et le contrôle de l’accès utilisateur à des ressources Azure avec une gestion des identités et des accès (IAM) constituent une étape importante dans la mise en place de votre infrastructure Azure.

- Contoso décide d’étendre son annuaire Active Directory local dans le cloud plutôt que de créer un système distinct dans Azure.
- L’entreprise crée pour cela un annuaire Active Directory basé sur Azure.
- Comme Contoso n’a pas Office 365, l’entreprise doit provisionner un nouveau Azure AD.
- Office 365 utilise Azure AD pour la gestion des utilisateurs. Si Contoso utilisait Office 365, l’entreprise aurait déjà un locataire Azure AD pouvant servir de répertoire principal.
- En savoir plus sur [Azure AD pour Office 365](https://docs.microsoft.com/office365/enterprise/about-office-365-identity).
- Apprenez à [ajouter un abonnement à un locataire Azure AD existant](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory).

### <a name="create-an-azure-ad-directory"></a>Création d’un répertoire Azure AD

Contoso utilise l’édition Azure Active Directory Free incluse avec un abonnement Azure. Les administrateurs de Contoso créent un répertoire Azure AD :

1. Dans le [portail Azure](https://portal.azure.com), ils accèdent à **Créer une ressource** > **Identité** > **Azure Active Directory**.
2. Dans **Créer un répertoire**, ils spécifient le nom du répertoire, un nom de domaine initial et la région dans laquelle le répertoire doit être créé.

    ![Création d’un répertoire Azure AD](./media/contoso-migration-infrastructure/azure-ad-create.png)

    > [!NOTE]
    > Le format du nom de domaine initial du répertoire créé est le suivant : `domain-name.onmicrosoft.com` Ce nom ne peut pas être changé ni supprimé. Au lieu de cela, Contoso doit ajouter son nom de domaine inscrit à Azure AD.

### <a name="add-the-domain-name"></a>Ajouter le nom de domaine

Pour utiliser le nom de domaine standard, les administrateurs de Contoso doivent l’ajouter en tant que nom de domaine personnalisé dans Azure AD. Cette option leur permet d’attribuer des noms d’utilisateur connus. Par exemple, un utilisateur peut se connecter avec l'adresse e-mail `billg@contoso.com`au lieu de `billg@contosomigration.microsoft.com`.

Pour configurer un nom de domaine personnalisé, il l'ajoute à l'annuaire, ajoute une entrée DNS, puis vérifie le nom dans Azure AD.

1. Dans **Noms de domaine personnalisés** > **Ajouter un domaine personnalisé**, elle ajoute le domaine.
2. Pour utiliser une entrée DNS dans Azure, elle doit l’inscrire auprès du bureau d’enregistrement de domaines.

    - Dans la liste **Noms de domaines personnalisés**, elle note les informations DNS pour le nom. L’entreprise utilise une entrée MX.
    - Pour cela, elle doit accéder au serveur de noms. Les administrateurs se connectent au domaine `contoso.com` et créent un enregistrement MX pour l'entrée DNS fournie par Azure AD, en utilisant les informations indiquées.

3. Une fois les enregistrements DNS propagés, ils sélectionnent **Vérifier** dans les détails du domaine pour vérifier le nom de domaine personnalisé.

     ![DNS Azure AD](./media/contoso-migration-infrastructure/azure-ad-dns.png)

### <a name="set-up-on-premises-and-azure-groups-and-users"></a>Configurer les utilisateurs et groupes Azure et locaux

Maintenant que le répertoire Azure AD est établi, les administrateurs de Contoso doivent ajouter des employés à des groupes Active Directory locaux synchronisés avec Azure AD. Ils doivent utiliser des noms de groupe local correspondant aux noms des groupes de ressources dans Azure. Cela facilite l’identification des correspondances à des fins de synchronisation.

#### <a name="create-resource-groups-in-azure"></a>Créer des groupes de ressources dans Azure

Les groupes de ressources Azure rassemblent des ressources Azure. Un ID de groupe de ressources permet à Azure d’effectuer des opérations sur les ressources au sein du groupe.

- Un abonnement Azure peut comporter plusieurs groupes de ressources. Un groupe de ressources n'est rattaché qu'à un seul abonnement.
- En outre, un même groupe de ressources peut comporter plusieurs ressources. Une ressource appartient à un seul groupe de ressources.

Les administrateurs de Contoso configurent des groupes de ressources Azure comme le montre le tableau suivant.

<!-- markdownlint-disable MD033 -->

| Resource group | Détails |
| --- | --- |
| `ContosoCobRG` | Ce groupe contient toutes les ressources liées à la continuité des activités. Il inclut les coffres que Contoso utilise pour le service Azure Site Recovery et le service Sauvegarde Azure. <br><br> Il inclut également les ressources utilisées pour la migration, notamment Azure Migrate et Azure Database Migration Service. |
| `ContosoDevRG` | Ce groupe contient des ressources de développement et de test. |
| `ContosoFailoverRG` | Ce groupe sert de zone d’accueil pour les ressources basculées. |
| `ContosoNetworkingRG` | Ce groupe contient toutes les ressources de mise en réseau. |
| `ContosoRG` | Ce groupe contient les ressources associées aux bases de données et aux applications de production. |

<!-- markdownlint-disable MD026 -->

Contoso crée les groupes de ressources comme suit :

1. Dans le portail Azure > **Groupes de ressources**, elle ajoute un groupe.
2. Pour chaque groupe, elles spécifient un nom, l’abonnement auquel appartient le groupe, et la région.
3. Les groupes de ressources s’affichent dans la liste **Groupes de ressources**.

  ![Groupes de ressources](./media/contoso-migration-infrastructure/resource-groups.png)

##### <a name="scale-resource-groups"></a>Mettre à l’échelle des groupes de ressources

Plus tard, Contoso ajoutera des groupes de ressources en fonction des besoins. Par exemple, les administrateurs peuvent définir un groupe de ressources pour chaque application ou service, pour pouvoir les gérer et les sécuriser séparément.

#### <a name="create-matching-security-groups-on-premises"></a>Créer des groupes de sécurité locaux correspondants

1. Dans l’annuaire Active Directory local, les administrateurs de Contoso configurent des groupes de sécurité avec des noms correspondant aux noms des groupes de ressources Azure.

    ![Groupes de sécurité Active Directory locaux](./media/contoso-migration-infrastructure/on-prem-ad.png)

2. À des fins de gestion, elle crée un groupe supplémentaire qui sera ajouté à tous les autres groupes. Ce groupe disposera d’un droit d’accès à tous les groupes de ressources dans Azure. Un nombre limité d’administrateurs généraux sera ajouté à ce groupe.

### <a name="synchronize-active-directory"></a>Synchroniser Active Directory

Contoso souhaite fournir une identité commune pour accéder aux ressources locales et dans le cloud. Pour cela, l’entreprise intègre l’annuaire Active Directory local à Azure AD. Avec ce modèle :

- Les utilisateurs et les organisations peuvent profiter d’une identité unique pour accéder à des applications locales et des services cloud comme Office 365, ou des milliers d’autres sites sur Internet.
- Les administrateurs peuvent utiliser les groupes dans Active Directory pour implémenter le [contrôle d’accès en fonction du rôle (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) dans Azure.

Pour faciliter l’intégration, Contoso se sert de [l’outil Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). Lorsque vous installez et configurez l'outil sur un contrôleur de domaine, il synchronise les identités Active Directory locales avec Azure AD.

### <a name="download-the-tool"></a>Télécharger l’outil

1. Dans le portail Azure, les administrateurs de Contoso accèdent à **Azure Active Directory** > **Azure AD Connect** et téléchargent la dernière version de l’outil sur le serveur utilisé pour la synchronisation.

    ![Téléchargez Azure AD Connect](./media/contoso-migration-infrastructure/download-ad-connect.png)

2. Ils lancent l'installation de `AzureADConnect.msi` à l'aide des **Paramètres Express**. Il s'agit de l'installation la plus courante, et elle peut être utilisée pour une topologie à forêt unique avec synchronisation de hachage de mot de passe pour l'authentification.

    ![Assistant Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz1.png)

3. Dans **Connexion à Azure AD**, Contoso spécifie les informations d’identification pour se connecter à Azure AD (dans le formulaire `admin@contoso.com` ou `admin@contoso.onmicrosoft.com`).

    ![Assistant Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz2.png)

4. Dans **Connexion à AD DS**, Contoso spécifie les informations d'identification de l'instance locale d'Active Directory (sous la forme `CONTOSO\admin` ou `contoso.com\admin`).

     ![Assistant Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz3.png)

5. Dans **Prêt pour la configuration**, Contoso sélectionne **Démarrer le processus de synchronisation une fois la configuration terminée** pour démarrer immédiatement la synchronisation. Elle lance ensuite l’installation.

    Notez les points suivants :
  
    - Contoso dispose d’une connexion directe à Azure. Si votre instance locale d'Active Directory se trouve derrière un proxy, consultez [Résoudre les problèmes de connectivité liés à Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-troubleshoot-connectivity).

    - Après la première synchronisation, les objets Active Directory locaux sont visibles dans le répertoire Azure AD.

      ![Répertoire Active Directory local dans Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

    - Le service informatique de Contoso est représenté dans chaque groupe, en fonction de son rôle.

      ![Membres Active Directory locaux dans Azure](./media/contoso-migration-infrastructure/on-prem-ad-group-members.png)

### <a name="set-up-rbac"></a>Configurer le RBAC

Le [contrôle d’accès en fonction du rôle (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) Azure permet une gestion précise de l’accès pour Azure. L’utilisation de RBAC vous permet d’accorder uniquement les droits d’accès dont les utilisateurs ont besoin pour effectuer leur travail. Vous affectez le rôle RBAC approprié aux utilisateurs, groupes et applications au niveau d’une étendue. L’étendue d’une attribution de rôle peut être une seule ressource, un groupe de ressources ou un abonnement.

Les administrateurs de Contoso attribuent ensuite des rôles aux groupes Active Directory synchronisés localement.

1. Dans le groupe de ressources `ControlCobRG`, ils sélectionnent **Contrôle d'accès (IAM)**  > **Ajouter une attribution de rôle**.
2. Dans **Ajouter une attribution de rôle** > **Rôle** > **Contributeur**, ils sélectionnent le groupe `ContosoCobRG` dans la liste. Le groupe apparaît alors dans la liste **Membres sélectionnés**.
3. Ils répètent cette procédure avec les mêmes autorisations pour les autres groupes de ressources (à l'exception de `ContosoAzureAdmins`), en ajoutant les autorisations `Contributor` au compte qui correspond au groupe de ressources.
4. Pour le groupe de `ContosoAzureAdmins`, ils attribuent le rôle `Owner`.

    ![Membres Active Directory locaux dans Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

## <a name="step-3-design-for-resiliency"></a>Étape 3 : Conception pour la résilience

### <a name="set-up-regions"></a>Configurer des régions

Les ressources Azure sont déployées dans des régions.

- Les régions sont organisées en zones géographiques et Azure garantit que les exigences en matière de résidence de données, de souveraineté, de conformité et de résilience sont respectées dans les limites géographiques.
- Une région est composée d’un ensemble de centres de données. Ces centres de données sont déployés dans un périmètre avec une latence définie et connectés via un réseau régional dédié à faible latence.
- Chaque région Azure est associée à une autre région pour assurer la résilience.
- En savoir plus sur les [régions Azure](https://azure.microsoft.com/global-infrastructure/regions) et comprendre [comment les régions sont jumelées](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

Contoso a choisi d'utiliser `East US 2` (en Virginie) comme région primaire et `Central US` (dans l'Iowa) comme région secondaire pour plusieurs raisons :

- Le centre de données Contoso se trouve à New York, et Contoso a voulu limiter la latence avec le centre de données le plus proche.
- `East US 2` dispose de tous les services et produits dont Contoso a besoin. Toutes les régions Azure ne proposent pas les mêmes produits et services. Pour plus d’informations, consultez les [Produits Azure par région](https://azure.microsoft.com/global-infrastructure/services).
- `Central US` est la région Azure jumelée avec `East US 2`.

Dans la perspective d’un environnement hybride, Contoso doit prévoir la mise en place d’une stratégie de résilience et de reprise d’activité dans la conception de la région. De manière générale, les stratégies vont du déploiement dans une seule région, qui s'appuie sur les caractéristiques de la plateforme Azure telles que les domaines d'erreur et le jumelage régional pour la résilience, à un modèle actif-actif complet dans lequel les services cloud et la base de données sont déployés et desservent les utilisateurs de deux régions.

Contoso a opté pour une solution intermédiaire. L’entreprise va déployer des applications et des ressources dans une région primaire, en conservant une copie complète de l’infrastructure dans la région secondaire afin d’avoir une sauvegarde complète si une défaillance totale d’une application ou à l’échelle d’une région se produit.

### <a name="set-up-availability"></a>Configurer la disponibilité

**Groupes à haute disponibilité :**

Les groupes à haute disponibilité contribuent à protéger les applications et les données d’une panne matérielle locale et de mise en réseau au sein d’un centre de données.

- Les groupes à haute disponibilité distribuent des machines virtuelles Azure sur différents matériels physiques au sein d’un centre de données.
- Les domaines d’erreur représentent un matériel sous-jacent ayant une source d’alimentation et un commutateur réseau communs dans le centre de données. Les machines virtuelles d’un groupe à haute disponibilité sont réparties sur différents domaines d’erreur pour réduire les pannes dues à une seule défaillance matérielle ou réseau.
- Les domaines de mise à jour représentent les matériels sous-jacents qui peuvent faire l’objet d’une opération de maintenance ou être redémarrés en même temps. Les groupes à haute disponibilité distribuent également des machines virtuelles dans plusieurs domaines de mise à jour pour s’assurer qu’au moins une instance s’exécute à tout moment.

Contoso implémentera des groupes à haute disponibilité chaque fois que les charges de travail des machines virtuelles nécessitent une haute disponibilité. Pour plus d’informations, consultez [Gérer la disponibilité des machines virtuelles Windows dans Azure](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability).

**Zones de disponibilité :**

Les zones de disponibilité contribuent à protéger les applications et les données contre les défaillances affectant l’ensemble d’un centre de données dans une région.

- Chaque zone de disponibilité représente un emplacement physique unique dans une région Azure.
- Chaque zone de disponibilité est composée d’un ou de plusieurs centres de données équipés d’une alimentation, d’un système de refroidissement et d’un réseau indépendants.
- Il y a un minimum de trois zones distinctes dans toutes les régions activées.
- La séparation physique des zones dans une région protège les applications et les données des défaillances du centre de données.

Contoso va déployer des zones de disponibilité en fonction des besoins des applications en termes de scalabilité, de haute disponibilité et de résilience. Pour plus d'informations, consultez [Régions et zones de disponibilité dans Azure](https://docs.microsoft.com/azure/availability-zones/az-overview).

### <a name="configure-backup"></a>Configurer une sauvegarde

**Sauvegarde Azure :**

Sauvegarde Azure vous permet de sauvegarder et de restaurer des disques de machines virtuelles Azure.

- Sauvegarde Azure permet de sauvegarder automatiquement des images de disque de machine virtuelle, stockées dans le stockage Azure.
- Les sauvegardes sont cohérentes avec les applications, garantissant la cohérence transactionnelle des données sauvegardées et le démarrage des applications après leur restauration.
- Sauvegarde Azure prend en charge le stockage localement redondant (LRS) pour répliquer plusieurs copies de vos données de sauvegarde au sein d’un centre de données si une défaillance matérielle locale se produit.
- Si une panne régionale se produit, Sauvegarde Azure prend également en charge le stockage géoredondant (GRS) en répliquant vos données de sauvegarde dans une région secondaire jumelée.
- Sauvegarde Azure chiffre les données en transit à l'aide d'AES 256. Les données sauvegardées au repos sont chiffrées à l'aide de [Storage Service Encryption (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption).

Contoso utilisera Sauvegarde Azure avec GRS sur toutes les machines virtuelles de production pour veiller à ce que les données de charge de travail soient sauvegardées et puissent être restaurées rapidement en cas de panne ou autre interruption. Pour plus d’informations, consultez [Vue d’ensemble de Sauvegarde Azure](https://docs.microsoft.com/azure/backup/backup-overview).

### <a name="set-up-disaster-recovery"></a>Configurer une récupération d'urgence

**Azure Site Recovery :**

Azure Site Recovery permet d’assurer la continuité de l’activité en maintenant l’exécution des charges de travail et applications métier lors des interruptions régionales.

- Azure Site Recovery réplique continuellement les machines virtuelles Azure d'une région primaire vers une région secondaire, garantissant ainsi la présence de copies fonctionnelles aux deux emplacements.
- En cas de panne dans la région primaire, votre application ou service bascule vers la région secondaire à l’aide d’instances de machines virtuelles répliquées dans celle-ci, ce qui réduit les interruptions potentielles.
- Lorsque les opérations reviennent à la normale, vos applications ou services peuvent effectuer une restauration automatique vers des machines virtuelles dans la région primaire.

Contoso implémente [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) pour toutes les machines virtuelles de production utilisées dans les charges de travail stratégiques, ce qui garantit une interruption minimale en cas de panne dans la région primaire.

## <a name="step-4-design-a-network-infrastructure"></a>Étape 4 : Concevoir une infrastructure réseau

Une fois la conception des régions définie, Contoso peut élaborer une stratégie de mise en réseau. L’entreprise doit réfléchir à la façon dont le centre de données local et Azure se connectent et communiquent entre eux, et à la façon de concevoir l’infrastructure réseau dans Azure. Plus précisément, Contoso doit :

- **Planifier la connectivité d’un réseau hybride.** déterminer comment connecter les réseaux locaux et Azure.
- **Concevoir une infrastructure réseau Azure.** déterminer comment déployer des réseaux sur les régions. Comment les réseaux vont-ils communiquer dans une même région et entre régions ?
- **Concevoir et configurer des réseaux Azure.** configurer les réseaux et sous-réseaux Azure, et choisir les données qui y résideront.

### <a name="plan-hybrid-network-connectivity"></a>Planifier la connectivité du réseau hybride

Contoso a étudié [plusieurs architectures](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking) pour créer un réseau hybride entre Azure et le centre de données local. Pour plus d'informations, consultez [Choisir une solution pour connecter un réseau local à Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations).

Pour rappel, l’infrastructure du réseau local de Contoso se compose actuellement du centre de données à New York et de branches locales dans la moitié est des États-Unis. Tous les emplacements disposent d’une connexion Internet de qualité professionnelle. Chacune des branches est ensuite connectée au centre de données via un tunnel VPN IPSec sur Internet.

![Réseau Contoso](./media/contoso-migration-infrastructure/contoso-networking.png)

Voici comment Contoso a décidé d’implémenter une connectivité hybride :

1. Configurer une nouvelle connexion VPN de site à site entre le centre de données Contoso de New York et les deux régions Azure USA Est 2 et USA Centre.
2. Le trafic des branches pour les réseaux virtuels dans Azure sera acheminé via le principal centre de données Contoso.
3. À mesure que Contoso étend son déploiement Azure, l’entreprise établit une connexion ExpressRoute entre le centre de données et les régions Azure. Dans ce cas, Contoso conserve la connexion VPN de site à site pour le basculement uniquement.
    - En savoir plus sur le [choix entre une solution hybride ExpressRoute et VPN](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations).
    - Vérifiez les [emplacements ExpressRoute et la prise en charge](https://docs.microsoft.com/azure/expressroute/expressroute-locations-providers).

**VPN uniquement :**

![VPN Contoso](./media/contoso-migration-infrastructure/hybrid-vpn.png)

**VPN et ExpressRoute :**

![Contoso VPN/ExpressRoute](./media/contoso-migration-infrastructure/hybrid-vpn-expressroute.png)

### <a name="design-the-azure-network-infrastructure"></a>Concevoir l’infrastructure réseau Azure

Contoso doit veiller à ce que sa configuration réseau autorise un déploiement hybride sécurisé et scalable. Pour cela, Contoso adopte une approche à long terme et conçoit des réseaux virtuels résilients et prêts pour l'entreprise. Pour plus d'informations, consultez [Planifier des réseaux virtuels](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm).

Pour connecter les deux régions, Contoso implémente un modèle de réseau de hub à hub :

- Dans chaque région, Contoso utilisera un modèle hub-and-spoke.
- Pour connecter des réseaux et des hubs, Contoso utilisera le Peering de réseau Azure.

#### <a name="network-peering"></a>Peering de réseau

L'[appairage de réseaux virtuels](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) d'Azure connecte les réseaux virtuels et les hubs. Le peering mondial permet d’établir des connexions entre les réseaux virtuels ou les hubs de différentes régions. Le peering local connecte des réseaux virtuels d’une même région. Le peering de réseaux virtuels offre plusieurs avantages :

- Le trafic réseau entre les réseaux virtuels homologués est privé.
- Le trafic entre les réseaux virtuels reste sur le réseau principal de Microsoft. Aucun chiffrement et aucune connexion Internet publique, ni passerelle ne sont nécessaires pour que les réseaux virtuels communiquent.
- Le peering fournit une connexion par défaut à faible latence et haut débit entre les ressources de différents réseaux virtuels.

#### <a name="hub-to-hub-across-regions"></a>Déploiement « hub à hub » entre les régions

Contoso déploiera un hub dans chaque région. Un hub est un réseau virtuel d'Azure qui centralise la connectivité à votre réseau local. Les réseaux virtuels de hubs se connectent à l’aide d’un peering de réseaux virtuels global. Le peering de réseaux virtuels global connecte des réseaux virtuels entre des régions Azure.

- Le hub de chaque région est jumelé à son hub partenaire dans l’autre région.
- Le hub est jumelé à chaque réseau dans sa région et peut se connecter à toutes les ressources réseau.

    ![Peering global](./media/contoso-migration-infrastructure/global-peering.png)

#### <a name="hub-and-spoke-model-within-a-region"></a>Modèle hub-and-spoke au sein d’une région

Dans chaque région, Contoso déploiera des réseaux virtuels à différentes fins, sous forme de réseaux spoke à partir du hub de région. Les réseaux virtuels d’une région utilisent le peering pour se connecter à leur hub et entre eux.

#### <a name="design-the-hub-network"></a>Concevoir le réseau hub

Dans le modèle « hub et spoke » que Contoso a choisi, l’entreprise doit réfléchir au routage du trafic provenant de son centre de données local et d’Internet. Voici comment Contoso a décidé de gérer le routage pour les hubs `East US 2` et `Central US` :

- Contoso crée un réseau qui autorise le trafic à partir d’Internet et de son réseau d’entreprise à l’aide d’un VPN vers Azure.
- L’architecture réseau a deux limites, une zone de périmètre frontend non approuvée et une zone backend approuvée.
- Un pare-feu disposera d’une carte réseau dans chaque zone afin de contrôler l’accès aux zones de confiance.
- À partir d'Internet :
  - Le trafic Internet atteindra une adresse IP publique avec équilibrage de charge sur le réseau de périmètre.
  - Ce trafic est acheminé via le pare-feu et soumis aux règles du pare-feu.
  - Une fois les contrôles d’accès au réseau mis en place, le trafic est transféré vers l’emplacement approprié dans la zone de confiance.
  - Le trafic sortant du réseau virtuel sera acheminé vers Internet à l’aide d’itinéraires définis par l’utilisateur. Le trafic est forcé via le pare-feu et inspecté conformément aux stratégies de Contoso.
- À partir du centre de données Contoso :
  - Le trafic entrant via le VPN site à site ou ExpressRoute accède à l'adresse IP publique de la passerelle VPN Azure.
  - Le trafic est acheminé via le pare-feu et soumis aux règles du pare-feu.
  - Après application des règles de pare-feu, le trafic est transféré vers un équilibreur de charge interne (référence SKU standard) sur le sous-réseau de la zone interne de confiance.
  - Le trafic sortant du sous-réseau approuvé vers le centre de données local via le VPN est acheminé via le pare-feu, où les règles sont appliquées, avant d’atteindre la connexion de site à site VPN.

### <a name="design-and-set-up-azure-networks"></a>Concevoir et configurer des réseaux Azure

Avec un réseau et une topologie de routage en place, Contoso est prêt à configurer les réseaux et sous-réseaux Azure.

- Contoso implémentera un réseau privé de classe A dans Azure (`10.0.0.0/8`). Cette solution fonctionne, car son infrastructure locale actuelle dispose d'un espace d'adressage privé de classe B (`172.160.0.0/16`) pour éviter tout risque de chevauchement entre les plages d'adresses.
- Contoso va déployer des réseaux virtuels à la fois dans les régions primaire et secondaire.
- Contoso utilise une convention d'affectation de noms qui inclut le préfixe `VNET` et l'abréviation de région `EUS2` ou `CUS`. Conformément à cette norme, les réseaux hub sont nommés `VNET-HUB-EUS2` (dans la région `East US 2`) et `VNET-HUB-CUS` (dans la région `Central US`).

#### <a name="virtual-networks-in-east-us-2"></a>Réseaux virtuels dans `East US 2`

`East US 2` est la région primaire que Contoso utilisera pour déployer des services et des ressources. Voici comment Contoso concevra des réseaux dans cette région :

- **Hub :** le réseau virtuel hub de la région `East US 2` est considéré comme la connectivité principale au centre de données local.
- **Réseaux virtuels :** les réseaux virtuels spoke de la région `East US 2` peuvent être utilisés pour isoler des charges de travail si nécessaire. En plus du réseau virtuel hub, Contoso disposera de deux réseaux virtuels spoke dans la région `East US 2` :
  - `VNET-DEV-EUS2`. Ce réseau virtuel fournit à l’équipe de développement et de test un réseau entièrement fonctionnel pour ses projets de développement. Il sert de zone de production pilote et s’appuie sur l’infrastructure de production pour fonctionner.
    - `VNET-PROD-EUS2`. les composants de production Azure IaaS seront placés dans ce réseau.
  - Chaque réseau virtuel possède son propre espace d’adressage unique, sans chevauchement. Contoso veut configurer le routage sans NAT.
- **Sous-réseaux :**
  - Il y aura un sous-réseau dans chaque réseau pour chaque niveau d’application.
  - Chaque sous-réseau du réseau de production aura un sous-réseau correspondant dans le réseau virtuel de développement.
  - En outre, le réseau de production comporte un sous-réseau pour les contrôleurs de domaine.

Le tableau suivant récapitule les réseaux virtuels de `East US 2`.

| **Réseau virtuel** | **Plage** | **Homologue** |
| --- | --- | --- |
| `VNET-HUB-EUS2` | `10.240.0.0/20` | `VNET-HUB-CUS2`, `VNET-DEV-EUS2`, `VNET-PROD-EUS2` |
| `VNET-DEV-EUS2` | `10.245.16.0/20` | `VNET-HUB-EUS2` |
| `VNET-PROD-EUS2` | `10.245.32.0/20` | `VNET-HUB-EUS2`, `VNET-PROD-CUS` |

![Modèle hub-and-spoke dans la région primaire](./media/contoso-migration-infrastructure/primary-hub-peer.png)

#### <a name="subnets-in-the-east-us-2-hub-network-vnet-hub-eus2"></a>Sous-réseaux du réseau `East US 2 Hub` (`VNET-HUB-EUS2`)

| Sous-réseau/zone | CIDR | Adresses IP utilisables |
| --- | --- | --- |
| `IB-UntrustZone` | `10.240.0.0/24`  | 251 |
| `IB-TrustZone`   | `10.240.1.0/24`  | 251 |
| `OB-UntrustZone` | `10.240.2.0/24`  | 251 |
| `OB-TrustZone`   | `10.240.3.0/24`  | 251 |
| `GatewaySubnets` | `10.240.10.0/24` | 251 |

#### <a name="subnets-in-the-east-us-2-development-network-vnet-dev-eus2"></a>Sous-réseaux du réseau de développement `East US 2` (`VNET-DEV-EUS2`)

Le réseau virtuel de développement est utilisé par l’équipe de développement comme zone de production pilote. Il comporte trois sous-réseaux.

| Subnet | CIDR | Adresses | Dans un sous-réseau |
| --- | --- | --- | --- |
| `DEV-FE-EUS2` | `10.245.16.0/22` | 1019 | Machines virtuelles frontales/de couche web |
| `DEV-APP-EUS2` | `10.245.20.0/22` | 1019 | Machines virtuelles de niveau application |
| `DEV-DB-EUS2` | `10.245.24.0/23` | 507 | Machines virtuelles de base de données |

#### <a name="subnets-in-the-east-us-2-production-network-vnet-prod-eus2"></a>Sous-réseaux du réseau de production `East US 2` (`VNET-PROD-EUS2`)

Les composants IaaS Azure sont situés dans le réseau de production. Chaque niveau application a son propre sous-réseau. Les sous-réseaux correspondent à ceux du réseau de développement, avec ajout d’un sous-réseau pour les contrôleurs de domaine.

| Subnet | CIDR | Adresses | Dans un sous-réseau |
| --- | --- | --- | --- |
| `PROD-FE-EUS2` | `10.245.32.0/22` | 1019 | Machines virtuelles frontales/de couche web |
| `PROD-APP-EUS2` | `10.245.36.0/22` | 1019 | Machines virtuelles de niveau application |
| `PROD-DB-EUS2` | `10.245.40.0/23` | 507 | Machines virtuelles de base de données |
| `PROD-DC-EUS2` | `10.245.42.0/24` | 251 | Machines virtuelles de contrôleur de domaine |

![Architecture réseau du hub](./media/contoso-migration-infrastructure/azure-networks-eus2.png)

#### <a name="virtual-networks-in-central-us-secondary-region"></a>Réseaux virtuels de la région `Central US` (région secondaire)

La région `Central US` est la région secondaire de Contoso. Voici comment Contoso va structurer les réseaux :

- **Hub :** le réseau virtuel hub de la région `Central US` est considéré comme le point de connectivité secondaire vers le centre de données local, et les réseaux virtuels spoke de la région `Central US` peuvent, si nécessaire, être utilisés pour isoler des charges de travail gérées séparément des autres spokes.
- **Réseaux virtuels :** Contoso dispose de deux réseaux virtuels dans la région `Central US` :
  - `VNET-PROD-CUS`: Ce réseau virtuel est un réseau de production et peut être considéré comme un hub secondaire.
  - `VNET-ASR-CUS`: Ce réseau virtuel servira d’emplacement dans lequel les machines virtuelles sont créées après le basculement depuis le site local, ou d’emplacement pour les machines virtuelles Azure qui ont basculé de la région principale vers la région secondaire. Ce réseau est similaire aux réseaux de production, mais il ne comporte aucun contrôleur de domaine.
  - Chaque réseau virtuel de la région possède son propre espace d’adressage, sans chevauchement. Contoso configure le routage sans NAT.
- **Sous-réseaux :** les sous-réseaux seront conçus de la même façon que ceux de la région `East US 2`.

Le tableau suivant récapitule les réseaux virtuels de `Central US`.

| Réseau virtuel | Plage | Homologue |
| --- | --- | --- |
| **VNET-HUB-CUS** | 10.250.0.0/20 | VNET-HUB-EUS2, VNET-ASR-CUS, VNET-PROD-CUS |
| **VNET-ASR-CUS** | 10.255.16.0/20 | VNET-HUB-CUS, VNET-PROD-CUS |
| **VNET-PROD-CUS** | 10.255.32.0/20 | VNET-HUB-CUS, VNET-ASR-CUS, VNET-PROD-EUS2 |

![Modèle hub-and-spoke dans une région jumelée](./media/contoso-migration-infrastructure/paired-hub-peer.png)

#### <a name="subnets-in-the-central-us-hub-network-vnet-hub-cus"></a>Sous-réseaux du réseau hub USA Centre (VNET-HUB-CUS)

**Sous-réseau** | **CIDR** | **Adresses IP utilisables**
--- | --- | ---
**IB-UntrustZone** | 10.250.0.0/24 | 251
**IB-TrustZone** | 10.250.1.0/24 | 251
**OB-UntrustZone** | 10.250.2.0/24 | 251
**OB-TrustZone** | 10.250.3.0/24 | 251
**GatewaySubnet** | 10.250.2.0/24 | 251

#### <a name="subnets-in-the-central-us-production-network-vnet-prod-cus"></a>Sous-réseaux du réseau de production de la région USA Centre (VNET-PROD-CUS)

Parallèlement au réseau de production dans la région principale USA Est 2, il existe un réseau de production dans la région secondaire USA Centre.

| **Sous-réseau** | **CIDR** | **Adresses** | **Dans un sous-réseau** |
| --- | --- | --- | --- |
| **PROD-FE-CUS** | 10.255.32.0/22 | 1019 | Machines virtuelles frontales/de couche web |
| **PROD-APP-CUS** | 10.255.36.0/22 | 1019 | Machines virtuelles de niveau application |
| **PROD-DB-CUS** | 10.255.40.0/23 | 507 | Machines virtuelles de base de données |
| **PROD-DC-CUS** | 10.255.42.0/24 | 251 | Machines virtuelles de contrôleur de domaine |

#### <a name="subnets-in-the-central-us-failoverrecovery-network-in-central-us-vnet-asr-cus"></a>Sous-réseaux du réseau de basculement et de récupération de la région USA Centre (VNET-ASR-CUS)

Le réseau VNET-ASR-CUS est utilisé à des fins de basculement entre les régions. Site Recovery servira à répliquer et à basculer les machines virtuelles Azure entre les régions. Il fonctionne également comme un centre de données Contoso vers le réseau Azure pour les charges de travail protégées qui restent sur site, mais basculent vers Azure pour la récupération d’urgence.

VNET-ASR-CUS est le même sous-réseau de base que le sous-réseau virtuel de production de la région USA Est 2, mais sans sous-réseau de contrôleur de domaine.

| **Sous-réseau** | **CIDR** | **Adresses** | **Dans un sous-réseau** |
| --- | --- | --- | --- |
| **ASR-FE-CUS** | 10.255.16.0/22 | 1019 | Machines virtuelles frontales/de couche web |
| **ASR-APP-CUS** | 10.255.20.0/22 | 1019 | Machines virtuelles de niveau application |
| **ASR-DB-CUS** | 10.255.24.0/23 | 507 | Machines virtuelles de base de données |

![Architecture réseau du hub](./media/contoso-migration-infrastructure/azure-networks-cus.png)

#### <a name="configure-peered-connections"></a>Configurer des connexions jumelées

Le hub de chaque région sera être jumelé au hub de l’autre région et à tous les réseaux virtuels au sein de la région du hub. Les hubs peuvent ainsi communiquer et afficher tous les réseaux virtuels au sein d’une région. Notez les points suivants :

- Le peering crée deux connexions : une à partir de l’homologue initial sur le premier réseau virtuel, et une autre sur le second réseau virtuel.
- Dans un déploiement hybride, le trafic qui transite entre des pairs doit être visible depuis la connexion VPN entre le centre de données local et Azure. Pour cela, quelques paramètres spécifiques doivent être définis sur les connexions jumelées.

Pour toutes les connexions depuis les réseaux virtuels spoke via le hub et jusqu’au centre de données local, Contoso doit autoriser le transfert du trafic et traverser les passerelles VPN.

##### <a name="domain-controller"></a>Contrôleur de domaine

Pour les contrôleurs de domaine du réseau VNET-PROD-EUS2, Contoso souhaite que le trafic passe entre le réseau hub/production EUS2 et sur la connexion VPN vers le site local. Pour ce faire, les administrateurs de Contoso doivent autoriser ce qui suit :

1. **Autoriser le trafic transféré** et **autoriser les configurations de transit par passerelle** sur la connexion jumelée. Dans notre exemple, il s’agit de la connexion VNET-HUB-EUS2 vers VNET-PROD-EUS2.

    ![Peering](./media/contoso-migration-infrastructure/peering1.png)

2. **Autoriser le trafic transféré** et **Utiliser des passerelles distantes** sur l’autre côté du peering, sur la connexion VNET-PROD-EUS2 vers VNET-HUB-EUS2.

    ![Peering](./media/contoso-migration-infrastructure/peering2.png)

3. Localement, ils configurent une route statique qui achemine le trafic local au réseau virtuel via le tunnel VPN. La configuration est terminée sur la passerelle qui fournit le tunnel VPN de Contoso vers Azure. Ils utilisent RRAS pour cela.

    ![Peering](./media/contoso-migration-infrastructure/peering3.png)

##### <a name="production-networks"></a>Réseaux de production

Un réseau homologue spoke ne peut pas voir un réseau homologue spoke d’une autre région via un hub.

Pour que les réseaux de production Contoso des deux régions puissent se voir, les administrateurs de Contoso doivent établir une connexion jumelée directe pour VNET-PROD-EUS2 et VENT-PROD-CUS.

![Peering](./media/contoso-migration-infrastructure/peering4.png)

### <a name="set-up-dns"></a>Configurer le DNS

Lorsque vous déployez des ressources dans des réseaux virtuels, vous avez deux options pour la résolution du nom de domaine. Vous pouvez utiliser la résolution de noms fournie par Azure, ou fournir des serveurs DNS pour la résolution. Le type de résolution de noms que vous utilisez dépend de la manière dont vos ressources doivent communiquer entre elles. [Plus d’informations](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#azure-provided-name-resolution) sur le service Azure DNS.

Les administrateurs de Contoso ont décidé que le service Azure DNS n’est pas un bon choix dans l’environnement hybride. Ils préfèrent plutôt utiliser les serveurs DNS locaux.

<!-- docsTest:ignore "on premises" -->

- Comme il s’agit d’un réseau hybride, toutes les machines virtuelles locales et dans Azure doivent être capables de résoudre les noms afin de fonctionner correctement. Cela signifie que des paramètres DNS personnalisés doivent être appliqués à tous les réseaux virtuels.
- Actuellement, Contoso a déployé des contrôleurs de domaine dans ses centres de données et ses filiales. Ses serveurs DNS principaux sont CONTOSODC1 (172.16.0.10) et CONTOSODC2 (172.16.0.1).
- Une fois que les réseaux virtuels sont déployés, les contrôleurs de domaine locaux sont configurés comme serveurs DNS dans les réseaux.
- Si un DNS personnalisé facultatif est spécifié pour le réseau virtuel, l’adresse IP virtuelle `168.63.129.16` pour les programmes de résolution récursifs dans Azure doit être ajoutée à la liste. Pour cela, Contoso configure les paramètres du serveur DNS sur chaque réseau virtuel. Par exemple, les paramètres du DNS personnalisé pour le réseau virtuel VNET-HUB-EUS2 se présenteraient ainsi :

    ![Système DNS personnalisé](./media/contoso-migration-infrastructure/custom-dns.png)

En plus des contrôleurs de domaine locaux, Contoso implémente quatre contrôleurs de domaine supplémentaires pour prendre en charge les réseaux Azure, deux pour chaque région. Voici les éléments que Contoso déploie dans Azure.

| **Région** | **DC** | **Réseau virtuel** | **Sous-réseau** | **Adresse IP** |
| --- | --- | --- | --- | --- |
| EUS2 | CONTOSODC3 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.4 |
| EUS2 | CONTOSODC4 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.5 |
| CUS | CONTOSODC5 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4 |
| CUS | CONTOSODC6 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4 |

Après avoir déployé les contrôleurs de domaine locaux, Contoso doit mettre à jour les paramètres DNS sur les réseaux de chaque région afin d’inclure les nouveaux contrôleurs de domaine dans la liste de serveurs DNS.

#### <a name="set-up-domain-controllers-in-azure"></a>Configurer des contrôleurs de domaine dans Azure

Après la mise à jour des paramètres du réseau, les administrateurs de Contoso peuvent installer les contrôleurs de domaine dans Azure.

1. Dans le portail Azure, elle déploie une nouvelle machine virtuelle Windows Server sur le réseau virtuel approprié.
2. Ils [créent des groupes à haute disponibilité](https://docs.microsoft.com/azure/virtual-machines/windows/tutorial-availability-sets) à chaque emplacement pour la machine virtuelle. Les ensembles de disponibilité effectuent les tâches suivantes :

    - Vérifier que la structure Azure sépare les machines virtuelles dans différentes infrastructures dans la région Azure.
    - Permet à Contoso de bénéficier d’un contrat SLA à 99,95 % pour les machines virtuelles dans Azure.

    ![Groupe de disponibilité](./media/contoso-migration-infrastructure/availability-group.png)

3. Une fois la machine virtuelle déployée, ils ouvrent l’interface réseau pour la machine virtuelle. Ils définissent l’adresse IP privée sur statique et spécifient une adresse valide.

    ![Carte réseau de machine virtuelle](./media/contoso-migration-infrastructure/vm-nic.png)

4. Elle attache maintenant un nouveau disque de données à la machine virtuelle. Ce disque contient la base de données Active Directory et le partage sysvol.
    - La taille du disque déterminera le nombre d’IOPS pris en charge.
    - Au fil du temps, la taille du disque devra éventuellement être augmentée à mesure que l’environnement se développe.
    - Le lecteur ne doit pas être défini en lecture-écriture pour la mise en cache de l’hôte. Les bases de données Active Directory ne prennent pas en charge cette configuration.

     ![Disque Active Directory](./media/contoso-migration-infrastructure/ad-disk.png)

5. Une fois le disque ajouté, Contoso se connecte à la machine virtuelle via le Bureau à distance puis ouvre le Gestionnaire de serveur.

6. Ensuite, dans **Services de fichiers et de stockage**, elle exécute l’Assistant Nouveau volume, en s’assurant que le lecteur reçoit la lettre F: ou une lettre supérieure sur la machine virtuelle locale.

     ![Assistant Nouveau volume](./media/contoso-migration-infrastructure/volume-wizard.png)

7. Dans le Gestionnaire de serveur, Contoso ajoute le rôle **Active Directory Domain Services**. Ensuite, elle configure la machine virtuelle comme un contrôleur de domaine.

      ![Rôle du serveur](./media/contoso-migration-infrastructure/server-role.png)

8. Une fois la machine virtuelle configurée comme un contrôleur de domaine et redémarrée, Contoso ouvre le Gestionnaire DNS et configure le programme de résolution d’Azure DNS comme un redirecteur. Ainsi, le contrôleur de domaine peut transférer les requêtes DNS qu’il ne peut pas résoudre dans Azure DNS.

    ![Redirecteur DNS](./media/contoso-migration-infrastructure/dns-forwarder.png)

9. Maintenant, ils mettent à jour les paramètres DNS personnalisés pour chaque réseau virtuel avec le contrôleur de domaine approprié pour la région du réseau virtuel. Elle inclut les contrôleurs de domaine locaux de la liste.

### <a name="set-up-active-directory"></a>Configurer Active Directory

Active Directory est un service essentiel pour la mise en réseau et doit être correctement configuré. Les administrateurs de Contoso génèrent des sites Active Directory pour le centre de données Contoso et pour les régions EUS2 et CUS.

1. Ils créent deux nouveaux sites (`AZURE-EUS2` et `AZURE-CUS`), ainsi que le site du centre de données (`ContosoDatacenter`).
2. Après avoir créé ces sites, Contoso crée des sous-réseaux dans les sites pour qu’ils correspondent aux réseaux virtuels et au centre de données.

    ![Sous-réseaux DC](./media/contoso-migration-infrastructure/dc-subnets.png)

3. Contoso crée ensuite deux liens de sites pour connecter tous les éléments. Les contrôleurs de domaine doivent être déplacés vers leur emplacement.

    ![Liens DC](./media/contoso-migration-infrastructure/dc-links.png)

4. Une fois que tout est configuré, la topologie de réplication Active Directory est en place.

    ![Réplication DC](./media/contoso-migration-infrastructure/ad-resolution.png)

5. Lorsque tout est terminé, une liste des contrôleurs de domaine et des sites apparaît dans le centre d’administration Active Directory local.

    ![Centre d'administration Active Directory](./media/contoso-migration-infrastructure/ad-center.png)

## <a name="step-5-plan-for-governance"></a>Étape 5 : Planifier pour la gouvernance

Azure fournit une gamme de contrôles de gouvernance pour les services et la plateforme Azure. Pour plus d'informations, consultez la page [Options de gouvernance Azure](https://docs.microsoft.com/azure/security/governance-in-azure).

Comme elle configure l’identité et le contrôle d’accès, Contoso a déjà commencé à mettre en place certains aspects de la gouvernance et de la sécurité. Globalement, il existe trois domaines à prendre en compte :

- **Stratégie :** Azure Policy applique des règles et des effets sur vos ressources afin que ces dernières restent conformes aux exigences de l’entreprise et aux contrats de niveau de service.
- **Verrous :** Azure vous permet de verrouiller des abonnements, des groupes de ressources et d’autres ressources, afin que ces éléments puissent être modifiés seulement par les personnes autorisées à le faire.
- **Balises :** les ressources peuvent être contrôlées, auditées et gérées à l’aide d’étiquettes. Les balises associent des métadonnées aux ressources pour fournir des informations sur les ressources ou les propriétaires.

### <a name="set-up-policies"></a>Configurer les stratégies

Le service Azure Policy évalue vos ressources, en analysant celles qui ne sont pas conformes avec les définitions de stratégie mises en place. Par exemple, une stratégie peut autoriser uniquement certains types de machines virtuelles, ou nécessiter des ressources comportant une étiquette spécifique.

Les stratégies spécifient une définition de stratégie, tandis qu’une attribution de stratégie spécifie l’étendue à laquelle une stratégie doit être appliquée. L’étendue peut aller d’un groupe d’administration à un groupe de ressources. [En savoir plus](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage) sur la création et la gestion des stratégies.

Contoso souhaite commencer avec deux stratégies :

- L’entreprise veut une stratégie pour garantir que les ressources peuvent être déployées seulement dans les régions EUS2 et CUS.
- Elle veut limiter les références de machine virtuelle aux références approuvées uniquement. L’objectif est de s’assurer qu’aucune référence (SKU) de machine virtuelle coûteuse n’est utilisée.

#### <a name="limit-resources-to-regions"></a>Limiter des ressources à des régions

Contoso utilise la définition de stratégie intégrée **Emplacements autorisés** pour limiter les régions de ressources.

1. Dans le Portail Azure, sélectionnez **Tous les services**, puis recherchez **Policy**.
2. Sélectionnez **Attributions** > **Attribuer une stratégie**.
3. Dans la liste des stratégies, sélectionnez **Emplacements autorisés**.
4. Définissez l’**étendue** sur le nom de l’abonnement Azure, puis sélectionnez les deux régions dans la liste autorisée.

    ![Régions autorisées par la stratégie](./media/contoso-migration-infrastructure/policy-region.png)

5. Par défaut, la stratégie est définie sur **Deny** (Refuser), ce qui signifie que si quelqu'un lance un déploiement dans l’abonnement ne figurant pas dans la région EUS2 ou CUS, ce déploiement échoue. Voici ce qui se passe si un utilisateur dans l’abonnement Contoso tente de configurer un déploiement dans la région USA Ouest.

    ![Stratégie ayant échoué](./media/contoso-migration-infrastructure/policy-failed.png)

#### <a name="allow-specific-vm-skus"></a>Autoriser des références (SKU) de machines virtuelles spécifiques

Contoso utilise la définition de stratégie intégrée `Allow virtual machine SKUs` pour limiter les types de machines virtuelles qui peuvent être créées dans l'abonnement.

![Référence (SKU) de stratégie](./media/contoso-migration-infrastructure/policy-sku.png)

#### <a name="check-policy-compliance"></a>Vérifier la conformité de la stratégie

Les stratégies prennent effet immédiatement, et Contoso peut vérifier la conformité des ressources.

1. Dans le Portail Azure, sélectionnez le lien **Conformité**.
2. Le tableau de bord de conformité s’affiche. Vous pouvez explorer ce tableau de bord pour obtenir plus de détails.

    ![Conformité à la stratégie](./media/contoso-migration-infrastructure/policy-compliance.png)

### <a name="set-up-locks"></a>Configurer des verrous

Contoso utilise depuis longtemps l’infrastructure ITIL pour la gestion de ses systèmes. Un des aspects les plus importants de cette infrastructure est le contrôle des modifications, et Contoso veut s’assurer que ce contrôle des modifications est implémenté dans le déploiement Azure.

Contoso [verrouille les ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) comme suit :

- Tout composant de production ou de basculement doit figurer dans un groupe de ressources comportant un verrou ReadOnly. Cela signifie que pour modifier ou supprimer des éléments de production, le verrou doit être supprimé.
- Les groupes de ressources hors production auront des verrous CanNotDelete. Cela signifie que les utilisateurs autorisés peuvent lire ou modifier une ressource, mais ne peuvent pas la supprimer.

### <a name="set-up-tagging"></a>Configurer le marquage

Pour suivre les ressources à mesure qu’elles sont ajoutées, il sera de plus en plus important pour Contoso d’associer des ressources à un service, client et environnement approprié.

En plus de fournir des informations sur les ressources et les propriétaires, les balises permettront à Contoso d’agréger et de regrouper des ressources, et d’utiliser ces données à des fins de facturation interne.

Contoso doit visualiser ses ressources Azure de façon pertinente pour l’entreprise, comme par rôle ou département. Notez que les ressources ne doivent pas nécessairement appartenir au même groupe de ressources pour partager une balise. Contoso créera une taxonomie d’étiquette afin que tout le monde utilise les mêmes étiquettes.

| **Nom de la balise** | **Valeur** |
| --- | --- |
| `CostCenter` | 12345 : doit être un centre de coût valide de SAP. |
| `BusinessUnit` | Nom de l’unité commerciale (de SAP). Correspond à `CostCenter`. |
| `ApplicationTeam` | Alias de messagerie de l’équipe propriétaire de la prise en charge de l’application. |
| `CatalogName` | Nom de l'application ou `ShareServices`, selon le catalogue de services pris en charge par la ressource. |
| `ServiceManager` | Alias de messagerie du Gestionnaire de services ITIL pour la ressource. |
| `COBPriority` | Priorité définie par l’entreprise pour BCDR. Valeurs de 1 à 5. |
| `ENV` | `DEV`, `STG` et `PROD` sont les valeurs autorisées ; elles représentent le développement, la mise en lots et la production. |

Par exemple :

 ![Balises Azure](./media/contoso-migration-infrastructure/azure-tag.png)

Après avoir créé la balise, Contoso reviendra en arrière pour créer de nouvelles définitions et attributions de stratégie et appliquer l’utilisation des balises requises dans toute l’organisation.

## <a name="step-6-consider-security"></a>Étape 6 : Prendre en compte la sécurité

La sécurité est cruciale dans le cloud, et Azure fournit un large éventail de fonctionnalités et outils de sécurité. Ces éléments vous aident à créer des solutions sécurisées sur la plateforme Azure sécurisée. Consultez la section [Faites confiance au cloud approuvé](https://azure.microsoft.com/overview/trusted-cloud) pour en savoir plus sur la sécurité Azure.

Contoso doit prendre en compte quelques aspects :

- **Azure Security Center :** [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) fournit une gestion unifiée de la sécurité et une protection avancée contre les menaces pour l'ensemble des charges de travail cloud hybrides. Utilisez-le pour appliquer des stratégies de sécurité à l'ensemble de vos charges de travail, pour limiter votre exposition aux menaces, ainsi que pour détecter les attaques et y répondre.
- **Groupes de sécurité réseau :** Un [groupe de sécurité réseau (NSG)](https://docs.microsoft.com/azure/virtual-network/security-overview) filtre le trafic réseau en fonction d'une liste de règles de sécurité qui autorisent ou refusent le trafic réseau vers des ressources connectées à des réseaux virtuels Azure.
- **Chiffrement des données :** [Azure Disk Encryption](https://docs.microsoft.com/azure/security/fundamentals/encryption-atrest) est une fonctionnalité qui vous permet de chiffrer les disques de vos machines virtuelles IaaS Windows et Linux.

### <a name="work-with-the-azure-security-center"></a>Utiliser le Centre de sécurité Azure

Contoso recherche le moyen d’obtenir un aperçu de la sécurité de son nouveau cloud hybride et plus précisément de ses charges de travail Azure. Par conséquent, Contoso a décidé d’implémenter Azure Security Center en commençant par les fonctionnalités suivantes :

- Gestion de stratégie centralisée.
- Évaluation continue.
- Recommandations exploitables.

#### <a name="centralize-policy-management"></a>Gestion de stratégie centralisée

Avec la gestion de stratégie centralisée, Contoso assure la conformité aux exigences de sécurité en gérant de façon centralisée les stratégies de sécurité dans l’ensemble de l’environnement. L’entreprise peut implémenter facilement et rapidement une stratégie qui s’applique à toutes les ressources Azure.

![Stratégie de sécurité](./media/contoso-migration-infrastructure/security-policy.png)

#### <a name="assess-and-action"></a>Évaluation et action

Contoso tirera parti de l’évaluation continue de la sécurité, qui surveille la sécurité des machines, réseaux, stockages, données et applications, pour découvrir d’éventuels problèmes de sécurité.

- Security Center analyse l’état de sécurité des ressources de calcul, d’infrastructure et de données de Contoso, et celui des services et applications Azure.
- L’évaluation continue aide l’équipe des opérations Contoso à découvrir d’éventuels problèmes de sécurité, comme les systèmes avec des mises à jour de sécurité manquantes ou des ports réseau exposés.
- Contoso souhaite en particulier s’assurer que toutes les machines virtuelles sont protégées. Security Center facilite cette opération en vérifiant l’intégrité des machines virtuelles et en proposant des recommandations classées par priorité, permettant de résoudre les failles de sécurité avant qu’elles ne soient exploitées.

![Surveillance](./media/contoso-migration-infrastructure/monitoring.png)

### <a name="work-with-nsgs"></a>Utiliser des groupes de sécurité réseau

Contoso peut limiter le trafic réseau vers les ressources d’un réseau virtuel à l’aide de groupes de sécurité réseau.

- Un groupe de sécurité réseau contient une liste de règles de sécurité qui autorisent ou refusent le trafic réseau entrant ou sortant en fonction de l’adresse IP source ou de destination, du port et du protocole.
- Quand elles sont appliquées à un sous-réseau, les règles sont appliquées à toutes les ressources dans le sous-réseau. En plus des interfaces réseau, cela inclut des instances de services Azure déployées dans le sous-réseau.
- Les groupes de sécurité d’application permettent de configurer la sécurité réseau comme un prolongement naturel de la structure de l’application, et donc de regrouper les machines virtuelles et définir des stratégies de sécurité réseau basées sur ces groupes.
  - Les groupes de sécurité d’application permettent à Contoso de réutiliser la stratégie de sécurité à grande échelle, sans maintenance manuelle d’adresses IP explicites. La plateforme gère la complexité des adresses IP explicites et plusieurs ensembles de règles, ce qui vous permet de vous concentrer sur la logique métier.
  - Contoso peut spécifier un groupe de sécurité d’application en tant que source et destination dans une règle de sécurité. Après avoir défini une stratégie de sécurité, Contoso peut créer des machines virtuelles et affecter des cartes réseau de machines virtuelles à un groupe.

Contoso implémentera une combinaison de groupes de sécurité réseau et de groupes de sécurité d’application. Contoso se préoccupe de la gestion des groupes de sécurité réseau. L’entreprise se soucie également de l’utilisation abusive des NSG et de la complexité supplémentaire pour le personnel chargé des opérations. Voici ce que fera Contoso :

- L’intégralité du trafic vers et depuis tous les sous-réseaux (Nord-Sud) sera soumise à une règle de groupe de sécurité réseau, à l’exception de GatewaySubnets dans les réseaux hub.
- Tous les pare-feu ou contrôleurs de domaine seront protégés à la fois par les groupes de sécurité réseau et les groupes de sécurité réseau de la carte réseau.
- Des groupes de sécurité d’application seront appliqués à toutes les applications de production.

Contoso a créé un modèle montrant le résultat potentiel pour ses applications.

![Sécurité](./media/contoso-migration-infrastructure/asg.png)

Les groupes de sécurité réseau associés aux groupes de sécurité d’application seront configurés avec des privilèges minimum pour s’assurer que seuls les paquets autorisés peuvent circuler d’une partie du réseau vers leur destination.

| Action | Nom | Source | Cible | Port |
| --- | --- | --- | --- | --- |
| `Allow` | `AllowInternetToFE` | `VNET-HUB-EUS1`/`IB-TrustZone` | `APP1-FE` | 80, 443 |
| `Allow` | `AllowWebToApp` | `APP1-FE` | `APP1-APP` | 80, 443 |
| `Allow` | `AllowAppToDB` | `APP1-APP` | `APP1-DB` | 1433 |
| `Deny`  | `DenyAllInbound` | Quelconque | Quelconque | Quelconque |

### <a name="encrypt-data"></a>Chiffrer les données

Azure Disk Encryption est intégré à Azure Key Vault, ce qui permet de contrôler et de gérer les clés et les secrets de chiffrement de disque dans un abonnement Key Vault. Elle garantit que toutes les données sur les disques des machines virtuelles sont chiffrées au repos dans le stockage Azure.

- Contoso a déterminé que des machines virtuelles spécifiques exigent un chiffrement.
- Contoso va appliquer un chiffrement aux machines virtuelles contenant des données client, confidentielles ou PPP.

## <a name="conclusion"></a>Conclusion

Dans cet article, Contoso a configuré une infrastructure Azure et une stratégie pour l’abonnement Azure, l’identité hybride, la reprise d’activité, la mise en réseau, la gouvernance et la sécurité.

Les étapes effectuées ici ne sont pas toutes indispensables pour une migration cloud. Dans ce cas, Contoso avait prévu une infrastructure réseau capable de gérer tout type de migration tout en étant sécurisée, résiliente et scalable.

Avec cette infrastructure, la société Contoso est prête à passer à l’étape suivante et à tester la migration.

## <a name="next-steps"></a>Étapes suivantes

Après la configuration de son infrastructure Azure, Contoso est prête à commencer la migration des charges de travail vers le cloud. Consultez la section relative à la [vue d’ensemble des modèles et exemples de migration](./contoso-migration-overview.md#windows-server-workloads) pour découvrir une sélection de scénarios utilisant cet exemple d’infrastructure comme cible de migration.
