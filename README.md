README pour un développeur expérimenté

Ce script PowerShell permet de configurer un serveur Windows 2022, de déployer Active Directory (AD), puis de gérer des utilisateurs dans des unités organisationnelles (OU) spécifiques. Il automatise la configuration réseau, l'installation du rôle AD DS, la création d'une forêt et d'un domaine, ainsi que l'importation d'utilisateurs depuis des fichiers CSV dans des OUs.
Déploiement d'Active Directory

    Configuration réseau : Le script commence par vérifier et configurer l'adresse IP, la passerelle et les serveurs DNS pour l'interface réseau spécifiée (Ethernet0).

    Installation de AD DS : Installe le rôle Active Directory Domain Services et promeut le serveur en contrôleur de domaine dans la forêt foret.lan.

Création des OUs

    CORE & HUMANS : L'OU CORE est créée si elle n'existe pas, puis l'OU HUMANS est créée sous CORE.

    USERS & ADMINS : Deux sous-OUs USERS et ADMINS sont créées sous HUMANS pour l'organisation des utilisateurs.

Importation et création d'utilisateurs

    Les utilisateurs sont importés depuis deux fichiers CSV distincts :

        Liste_Users.csv : pour les utilisateurs normaux, placés dans l'OU USERS.

        Liste_Admins.csv : pour les utilisateurs administrateurs, placés dans l'OU ADMINS.

Les informations de chaque utilisateur (prénom, nom, mot de passe) sont lues depuis ces CSV et un utilisateur est créé pour chaque ligne.
Fonctionnalités détaillées :

    Configuration réseau : New-NetIPAddress et Set-DNSClientServerAddress pour configurer IP statique et DNS.

    AD DS : Utilisation de Install-WindowsFeature et Install-ADDSForest pour installer et configurer AD DS.

    Création d'OU : New-ADOrganizationalUnit pour créer des OUs avec protection contre la suppression accidentelle.

    Gestion des utilisateurs : La fonction Create-UserFromCSV utilise New-ADUser pour créer les comptes à partir des CSV.

Exécution du script

    Assurez-vous d'exécuter ce script avec des privilèges d'administrateur.

    Les chemins des CSV doivent être valides, et les fichiers doivent contenir les colonnes first_name, last_name, et password.

    Ce script peut être exécuté depuis une session PowerShell sur un serveur Windows configuré pour exécuter AD.


README pour un utilisateur débutant

Ce script permet de configurer un serveur Windows en tant que contrôleur de domaine avec Active Directory (AD) et de créer des utilisateurs dans des groupes spécifiques. Il facilite l'automatisation de la configuration réseau, de l'installation d'Active Directory et de l'importation d'utilisateurs depuis des fichiers CSV.
Étapes principales :

    Configuration du serveur : Le script configure l'adresse IP, la passerelle et le DNS du serveur.

    Installation d'Active Directory : Il installe Active Directory et le configure pour créer un domaine appelé foret.lan.

    Création de dossiers pour organiser les utilisateurs : Il crée des dossiers appelés CORE et HUMANS, puis des sous-dossiers USERS et ADMINS pour organiser les utilisateurs.

    Ajout des utilisateurs : Le script ajoute les utilisateurs à ces dossiers à partir de deux fichiers CSV, un pour les utilisateurs normaux et un pour les administrateurs.

Comment ça fonctionne :

    Étape 1 : Configuration réseau : Le script configure l'adresse IP et le DNS de votre serveur afin qu'il puisse se connecter à d'autres ordinateurs du réseau.

    Étape 2 : Installation et configuration d'Active Directory : Une fois que la configuration réseau est terminée, le script installe et configure Active Directory pour que votre serveur devienne un contrôleur de domaine.

    Étape 3 : Organisation des utilisateurs : Il crée des catégories (USERS et ADMINS) sous un dossier principal appelé HUMANS, afin de mieux organiser les utilisateurs.

    Étape 4 : Importation des utilisateurs : Le script prend les informations des utilisateurs dans des fichiers CSV que vous fournissez, et crée leurs comptes dans les bonnes catégories (utilisateurs ou administrateurs).

Fichiers nécessaires :

    Liste_Users.csv : Contient les informations des utilisateurs standards (prénom, nom, mot de passe).

    Liste_Admins.csv : Contient les informations des administrateurs (prénom, nom, mot de passe).

Exemple de format CSV :

first_name,last_name,password
John,Doe,Password123
Jane,Smith,SecurePass2025

Prérequis :

    Le script doit être exécuté sur un serveur Windows configuré pour fonctionner avec Active Directory.

    Vous devez avoir les fichiers CSV correctement remplis et placés à l'emplacement spécifié dans le script.

    Vous devez avoir un accès administrateur pour exécuter ce script.

Exécution :

    Ouvrez PowerShell en tant qu'administrateur.

    Assurez-vous que les fichiers CSV sont correctement placés dans le répertoire spécifié.

    Exécutez le script. Le serveur sera configuré, Active Directory sera installé, les OUs seront créées et les utilisateurs seront ajoutés automatiquement.
