---
title: Blank page
deprecated: false
hidden: true
metadata:
  robots: index
---
> ❗️ Avertissement
>
> ceBox évolution peut être installé sur des postes fixes\
> Les PC portables ne sont pas compatible
>
> L'installation de la solution sur des générations Intel supérieur à la version 10, nécessite une validation en amont de notre équipe Support.

> ❗️ Avertissement
>
> La gestion des prises jack présente des dysfonctionnements sur certains modèles de machines, en particulier sur les versions NUC 6/7/8. Dans ce cadre, un adaptateur USB/Jack est préconisé.

> ❗️ Attention
>
> Les VM ne pourront plus utiliser le mode Full Performance (utilisation de la carte graphique native du périphérique) pour les postes qui sont supérieurs à la génération 10 des cartes mères Intel Nuc. 
>
> Dans ce contexte, il faut utiliser la procédure suivante pour l'[Installation pilote graphique VirtIO](doc:installation-pilote-graphique-virtio)

## ceBox® OS version 3.1.13

**BugFix:**

* Correction d'un bug concernant le démarrage d'une ceBox en non-igd

**Nouvelles fonctionnalités / Optimisations :**

* Action d'arrêt du WSO possible via le menu options du WSO.
* Evolution du démarrage ceBox sans internet : 
* * 3 conditions à remplir : 
    * le cache de la VM doit être à 100% **ou une connexion vers un WSO fonctionnel 100% pré-caché**
    * la licence ne doit pas être expirée 
    * la vm ne doit pas être configurée pour fonctionner en télétravail avec un POE

## ceBox® OS version 3.1.12

**BugFix:**

* Correction du module cache éviction
* Correction du module de pré cache
* Correction d'un bug récurrent empêchant la création de version
* Correction d'un bug au niveau des localisations ceBox
* Envoi d'un rapport de bug automatique en cas de dysfonctionnement  de la machine virtuelle
* Correction d'un bug empêchant le démarrage de la machine virtuelle si la licence n'est pas relâchée correctement

**Nouvelles fonctionnalités / Optimisations :**

* Amélioration des performances grâce au CPU alloué à la machine virtuelle 
* Démarrage ceBox sans internet
  * 3 conditions à remplir : 
    * le cache de la VM doit être à 100%
    * la licence ne doit pas être expirée 
    * la vm ne doit pas être configurée pour fonctionner en télétravail avec un POE
* Amélioration de la lecture des logs dans la console ceBox 
  * Les actions d'arrêts sont maintenant plus précises
  * Simplification de certains logs
* En cas d'arrêt inopiné de la ceBox, si l'option de vérification de cache est activée, celui-ci sera contrôlé et réparé avant le lancement de la machine virtuelle

## ceBox® OS version 3.1.9

**BugFix:**

* Correction d'un bug au niveau de la consommation des messages ceBox®
* Correction d'un bug concernant le TPM 
* Augmentation des tentatives de récupération d'IP pour les ceBox®, passage de 20 essaies a 40
* Mise à jour du **noyau Linux** de ceBox® OS.\*

**Nouvelles fonctionnalités / Optimisations :**

* Prise en charge d'un mode clonage d'écran en mode non-igd

* Prise en charge du mode étendu d'écran en mode non-igd (nécessite la mise à jour du QGA en 2.0.3)

* Ajout de pilote graphique non-igd (qxl, vga, virtio), le pilote par défaut est le qxl

* Il est maintenant possible d'exporter et ou d'importer des versions de master depuis un disque externe en USB (action depuis le menu du WSO)

* Intégration de la prise en charge PXE

* Limitation des connexions ceBox® à destination du cloud

* Amélioration des log d'assistance 

* Intégration d'un agent Zabbix sur WSO®

## ceBox® OS version 3.1.6

**BugFix:**

* Correction d'un bug au niveau de l'installation d'un WSO
* Correction d'un bug pouvant provoquer la perte des VM dans le menu de démarrage ceBox®

## ceBox® OS version 3.1.5

**BugFix et sécurité:**

* Mise à jour du **noyau Linux** de ceBox® OS.\*
* Meilleur gestion des accès wan
* Mise à jour du SDWAN

## ceBox® OS version 3.1.3

**BugFix et sécurité:**

* Une ceBox® et un WSO® peuvent démarrer avant les switch / routeurs
* Dans certain cas, la ceBox® pouvait rester bloquer sur "Waiting for Internet access"
* Amélioration de la montée en charge de nos infrastructure au niveau du SDWAN

## ceBox® OS version 3.1.2

> 📘 Information
>
> Prise en charge des processeurs Intel gen 11th - Rocket Lake-S\
> Uniquement en mode Non-IGD dans le cas d'utilisation d'un Master Windows

**Nouvelles fonctionnalités / Optimisations :**

* Mise à jour du module télétravail

  * permet la redondance des POE

  * sur le choix de la sortie POE, il est possible de personnaliser l'adresse MAC, le VLAN et la métrique

* Changement du logo ceBox®

* Réduction des flux nécessaires au fonctionnement ceBox/Wso®, le 6081 est maintenant optionnel en sortie

* La console peut maintenant s'enregistrer correctement sur un WSO d'un compte enfant.

* Si une ceBox® ne tunnelise pas vers un WSO®, celle-ci sera affichée dans la colonne "Unknown Optimizer" de la console (cas utilisation télétravail). Il est maintenant possible de personnaliser l'attachement d'une ceBox® en télétravail à l'aide d'une UUID

* Augmentation de la taille autorisée d'upload sur le WSO. Elle est maintenant fixée a 270Go.

* Prise en charge du NUC 11 en mode non-igd uniquement (pour le moment)

* Prise en charge des processeurs Intel gen 11th - Rocket Lake-S

* Prise en charge native du double écran en mode non-igd

* Clarification des messages affichées lors de l'installation d'un WSO®

* Prise en charge des différentes configuration clavier pour l'installation d'un WSO®

* La ceBox® utilise maintenant un DNS fourni par le DHCP en plus de ceux déjà utilisés

* Une VM peut maintenant utiliser une connexion réseau en mode NAT, dans le cas ou un DHCP ne serait pas présent sur le lan.

* Possibilité de redémarrer la ceBox® depuis la machine virtuelle

* L'installation de ceBoxOS® est améliorée avec l'utilisation d'un disque HDD

* Installation ceBox® en IP fixe améliorée :
  * Installation manuelle, saisie des adresses IP sur la ceBox
  * Installation automatique, utilisation d'un fichier avec une correspondance MAC + paramètres IP / réseau

**BugFix et sécurité:**

* L'erreur de création de version étape x/6, au niveau de l'envoi de la version ceBox® vers le WSO est maintenant corrigée.
* La création de version ceBox® --> Cloud est rétablie
* La barre de progression du cache ceBox® lors d'un reset est maintenant rétablie a zéro. 
* Mise à jour du **noyau Linux** de ceBox® OS.
* Meilleure stabilité sur l'attachement d'une ceBox® à un WSO®

## ceBox® OS version 3.0.12

**Nouvelles fonctionnalités / Optimisations :**

* Mise à jour du module SDWAN

* Démarrage optimisé en cas d'utilisation du WiFi. Si un câble ethernet est détecté, celui-ci est utilisé par défaut. 

* Evolution sur l'algorithme de choix du WSO pour les ceBox®. 

* Si une ceBox® ne tunnelise pas vers un WSO®, celle-ci sera affichée dans la colonne "Unknown Optimizer" de la console (cas utilisation télétravail)

* Meilleure prise en charge des GPO ordinateur sur ceBox®

**BugFix :**

* Correction d'un bug pouvant empêcher l'utilisation d'un VLAN lors de l'installation du WSO®
* Correction d'un bug sur le menu de démarrage ceBoxOS®

## ceBox® OS version 3.0.11

**Nouvelles fonctionnalités / Optimisations :**

* Mise à jour du module SDWAN
* Evolution sur la gestion du sflow ceBox®/WSO®
* Evolution sur la gestion interne du proxy Wisper
* Possibilité de définir une MTU personnalisée sur la machine virtuelle avec le script de routing ceBox

**BugFix :**

* Correction d'un bug pouvant dans certain cas, rendre inopérant l'auto-configuration du clientname via l'option 17 du DHCP

## ceBox® OS version 3.0.10

* Séparation des modules Chunkstore et WGE sur de nouvelles VMs de services

> 📘 IPs nécessaires au fonctionnement ceBox®
>
> Description des diverses IPs nécessaires au fonctionnement Wisper sur l'entrée DNS :\
> 6081.wg.wisper.cloud (type TXT)\
> nslookup -type=TXT 6081.wg.wisper.cloud

* SDwan:\
  Utilisation possible de POP privés définis par le client ou d'un\
  POP public Wisper, dans le but de permettre aux\
  ceBox\@home de joindre le LAN client via les POE souhaités
* Compatibilité Hyper-V
* Vérification du hostname saisi dans le menu de boot lors de\
  l’installation, seuls les caractères alphanumériques et ‘-’ sont\
  valides, si d’autres caractères sont saisis le hostname sera celui\
  par défaut : `HW-<mac>`
* Lecture automatique des messages pour les ceBox\@home\
  toutes les 5 minutes
* En cas de relance du menu de démarrage suite à un crash, si la\
  VM n’a pas encore été sélectionnée celui ci se relance sur\
  l’onglet “bootSelector”, sinon se lance sur l’onglet “boot\
  Status”
* Remontée de l’info “power button pressed” dans les logs des ceBox®
* Bugfix\
  Support carte graphique native nuc5i5\
  Suppression du pointeur souris visible en double en\
  mode d’utilisation VM non native

## ceBox® OS version 3.0.9

* Les nouveaux hardwares sont vus avec un hostname préfixé par @!, la console limite le\
  champ d'action sur ces postes
* Intégration des briques de base pour gérer le mode byod2
* Nouveau mode détection réseau

## ceBox® OS version 3.0.8

**Nouvelles fonctionnalités / Optimisations :**

**Création de version sans WSO**

Il est possible dans la version 3.0.8 de faire évoluer votre master sans l'utilisation de votre WSO. Pour cela il faut faire l'intégration d'une clé d'autorisation sur la ceBox® pour permettre l'envoie vers le cloud.\
La version est créée directement sur la ceBox®.

**Mode "Prepare"**

Nouveau mode d'utilisation de ceBox® en Streaming Mode Prepare / make media Cache\
Ce mode permet d'avoir le téléchargement d'un environnement qui a été préparé par l'administrateur de la solution avant le démarrage de la VM.\
Ce mode de déploiement est privilégié et conseillé par la R\&D

**BugFix et securité :**

* Évolution de la gestion des patchs pour permettre la gestion des patchs sur version différente
* Synchronisation média utilisée optimisation
* Correctif cache information
* Correction problèmes d'installation divers

## ceBox® OS version 3.0.5

**Nouvelles fonctionnalités / Optimisations :**

**Amélioration de l'interface utilisateur sur la partie ceBox®**

* Visuel amélioré / refonte graphique
* Configuration du WIFI simplifié
* Configuration ceBox® / @Home
* Simplification au niveau de la configuration d'une ceBox\@Home®
* Sélection de la machine virtuelle après démarrage de ceBoxOS

**Machine virtuelle ceBox® :**

* Amélioration des performances au niveau de l'utilisation des machines virtuelles
* Amélioration du système de pré-cache
* Agent permettant la remontée d'informations ceBox® → machine virtuelle

**Améliorations ceBox\@Easy® :**

* Maintenant ceBox\@OS détermine automatiquement les périphériques à rediriger vers la machine virtuelle\
  &#x9;	(Chipset graphique, USB, webcam, etc.)
* Support des processeurs Intel et AMD

**Ajout du support ceBox\@BYOD®**

* ceBox\@BYOD® (Bring your own device) permet l'installation de la solution ceBoxOS sur un ordinateur personnel tout en conservant le système d'exploitation déjà présent.

  [https://fr.wikipedia.org/wiki/Bring\_your\_own\_device](https://fr.wikipedia.org/wiki/Bring_your_own_device)

**Améliorations ceBox\@Home**® :

* Gestion de la MTU automatique

* Possibilité d'utiliser un CDN mondial pour le streaming du média 

  [https://fr.wikipedia.org/wiki/Réseau\_de\_diffusion\_de\_contenu](https://fr.wikipedia.org/wiki/Réseau_de_diffusion_de_contenu)

**Évolution du module de chiffrement :**

* L'activation du chiffrement sur un token USB va générer un nouvel uuid ceBox® visible dans la console. Une configuration/route sera alors associée au token USB.\
  &#x9;	Ce token USB permet d'avoir une portabilité de l'environnement sur toute machine compatible ceBox®.

**Module de licence :**

* Ajout du support de pool de licence\
  &#x9;	(un pool de licence peut être attribué à un client, le pool pourra être utilisé pour l'ensemble des comptes associés au client)\
  &#x9;

**BugFix et securité :**

Make media version with shutdown : 

* La création d'une version avec arrêt de la ceBox® est optimisée. La création de la version ne nécessite plus le redémarrage du poste. 

Mise à jour du kernel

## ceBox® OS version 2.3.6

**Nouvelles fonctionnalités / Optimisations :**\
Module ceBox\@home :

* Amélioration de l'enregistrement des ceBox\@home

**BugFix :**

Correction ceBox® :

* Correction d'un bug empêchant l'utilisation d'un nom VM comportant un '\_' et/ou '-'

Corrections WSO® :

* Correction du module @home, dans certains cas, la ceBox\@home ne pouvait pas tunneliser vers le WSO®

Installation :

* Correction sur le nom d'hôte du WSO pendant l'installation. Celui-ci est maintenant pris en compte correctement

Module de chiffrage :

* La création d'un MFA est maintenant possible si la ceBox® n'a pas été configurée avec un fichier de configuration (installation standard)

Création de version :

* Correction d'un bug pouvant provoquer la perte d'affichage du WSO®
* Correction d'un bug pouvant faire échouer une création de version

## ceBox® OS version 2.3.4

**BugFix et securité :**

* Linux Kernel LTS 5.4.x
* Ajout de plugins de surveillance
  * tunnelisation, virtualisation
* Correction du module de cache ceBox®

**Nouvelles fonctionnalités / Optimisations :**

* Modèle de licences flottantes
* Mode eraser SSD et HDD plus rapide / réinstallation automatique
* Optimisation pour le support des disques Sata
* WebConfigurator : interface de configuration des ceBox®\
  (Configuration du wifi, du @home et de la double authentification MFA)
* Pre-cache : 3 modes de precaching
  * Before (avant démarrage de la machine virtuelle)
  * Live (pendant l’utilisation de la machine virtuelle)
  * **After (au moment de l'arrêt de la ceBox®)** 

> 📘 Information
>
> Le mode "after" est celui utilisé par défaut sur la ceBox®.  Il peut être modifié dans la console.

**ceBox\@Home® :**

Chiffrement du disque avec  support double authentification

* Deux modes disponibles :
  * Avec Token USB + Double facteur d'authentification
  * Token dans le disque ceBox® + Double facteur d'authentification

> 📘 Information
>
> L'utilisation du double facteur d'authentification nécessite un appareil pouvant exploiter le protocole TOTP. 
>
> Android : [https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2\&hl=fr](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2\&hl=fr)\
> Android : [https://play.google.com/store/apps/details?id=com.azure.authenticator\&hl=fr](https://play.google.com/store/apps/details?id=com.azure.authenticator\&hl=fr)
>
> IOS : [https://apps.apple.com/fr/app/google-authenticator/id388497605](https://apps.apple.com/fr/app/google-authenticator/id388497605)\
> IOS : [https://apps.apple.com/us/app/microsoft-authenticator/id983156458](https://apps.apple.com/us/app/microsoft-authenticator/id983156458)

* Support wifi pour les modèles : 
  * NUC 5-6-7-8-10
  * Asus pn61
* Tunnelisation des flux réseaux de la machine virtuelle vers le système d'information Lan via une couche Vxlan

**ceBox\@Easy® :**

* Support des machines :
  * Dell 3050/3040/3070 
  * Asus pn61

## ceBox® OS version 2.2.7

**Nouvelle fonctionnalité :**

* Ajout des VMware Tools pour le WSO

**Corrections bugs :**

* Correction du mode "réparation automatique" lorsqu'une ceBox® s'éteint anormalement
* Correction de bug concernant des fonctionnalités du @home :
  * Correction Firewall du Static Tunneling
  * Correction d'un bug empêchant dans certain cas, le démarrage d'une ceBox\@home

## ceBoxOS® version 2.2.6

**Correction bug :**

* Correction d'un bug empêchant l'utilisation de la fonction "connect" sans script de routing

## ceBox® OS version 2.2.5

**Nouvelles fonctionnalités :**

* Vérification d'arrêt correct de la ceBox®. En cas d'arrêt anormal, au prochain démarrage, la ceBox® supprime ses fichiers de synchronisation (templates, scripts...) et les resynchronise. Cette opération prend 5 mn. 
* Simplification au niveau de la création de route
* Refonte du chiffrement de la ceBox® avec utilisation d'un token USB
* Ajout d'un mode de synchronisation des versions sur le WSO
* Sécurisation du mode @home 

**Corrections bugs :**

* Corrections des bugs connus 

## ceBox® OS version 2.2.2

**Nouvelles fonctionnalités :**

* Ajout d'un espace disque persistant de 50 Go pour les machines virtuelles. Ce disque additionnel interne à ceBox®OS peut être utilisé avec un template spécifique. 
* Remplacement de l'affichage "Gotop" du WSO par un menu d'administration avancé\
  Plusieurs options disponibles :
* Mettre à jour les scripts et templates provenant du cloud sur le WSO
* Vérifier l'intégrité du cache WSO
* Obtenir l'ensemble des tunnels établis sur le WSO
* Lister les IP des consoles d'administration ceBox® enregistrées sur le WSO
* Réaliser un test de connexion sur les serveurs cloud Wisper
* Modifier la configuration réseau (cette option doit être utilisée uniquement si la configuration réseau ne peut être modifiée avec la console d'administration ceBox®) 
* Envoyer l'ensemble des logs du WSO au support Wisper 
* Redémarrer le WSO® 

**Modifications :**

* La période de rétention est maintenant conservée même en cas d'anomalie (hors reset)
  * Dorénavant, toute modification apportée au routing ne sera appliquée qu'à la fin de la période de rétention. (changement tag, script routing, etc.)
* Modification sur la gestion interne des tunnels ceBox® OS

**Corrections bugs :**

* Correction du module Encryption de ceBox® OS
* Correction du module de réception des messages entre les serveurs Cloud --> ceBox®/WSO®
* Mise à jour du kernel

## ceBox® OS version 2.2.1

**Nouvelles fonctionnalités :**

* Évolution du produit pour l'utilisation de ceBox® **@home**
* Ajout d'un mode télétravail/itinérant
* Permet à vos collaborateurs d'emporter une ceBox® et de travailler à domicile tout en accédant aux ressources de l'entreprise avec le VPN intégré à solution ceBox®
* Évolution du produit pour l'utilisation de ceBox® **@onPremise**
* Le stockage Cloud Amazon AWS est maintenant compatible avec d'autres solutions de Cloud privé
* Sécurisation de la solution ceBox® :
* Firewall intégré
* Static Tunneling, permet la gestion des tunnels sur l'ensemble d'un parc ceBox®

**Performances améliorées :**

* Amélioration de la gestion des tunnels entre ceBox®/WSO/cloud
* Maintenant tous les flux entre les ceBox® et le WSO® passent par le tunnel via le port 6081 (aucune modification réseau est nécessaire)
* Fermeture des ports non utilisés par la ceBox®
* Optimisation des requêtes HTTPS sur un parc ceBox® important > 500 ceBox®
* Optimisation du système de cache
* Meilleure lecture des données sur les ceBox®
* Meilleure répartition de charge, dorénavant, les ceBox® pourront s'échanger des données entres elles
* Optimisation du démarrage de ceBox® OS
* Optimisation sur la création de version
* Mise à jour des templates ceBox
* Meilleure gestion des doubles disques,
* Optimisation sur la création du snapshot
* Optimisation d'utilisation des processeurs Intel Nuc
* Amélioration du cache d'écriture de la VM

**Corrections bugs :**

* Vérification et correction du cache à l'arrêt de la ceBox®
* Ajout d'une vérification des fichiers de configuration à l'arrêt
* Optimisation du produit ceBox® sur les Intel NUC 8
* Correction du reset ceBox® (le reset pouvait dans certain cas rendre la carte son inactive au redémarrage)
* Correction sur les agents de surveillances ceBox®
* Correction d'un bug d'écran noir sur la machine virtuelle Windows, la ceBox® vérifie maintenant que la carte graphique IGD est correctement installée avant de créer son snapshot. Nécessite la dernière version des Wisper Utilities

## ceBox® OS version 2.1.2

* Amélioration du mode d' installation d'une ceBox® avec deux disques
* **Corrections bugs**
  * Mise à jour du kernel
  * Amélioration du tunnel interne (pour les comptes utilisant un WSO principal gérant des WSO secondaires)

## ceBox® OS version 2.1.1

* Amélioration de la rapidité sur la machine virtuelle en cas de pré-cache à 100% de la ceBox®
* Optimisation sur la gestion des tunnels

## ceBox® OS version 2.1.0

* Ajout d'un agent de surveillance des ceBox® et WSO®
* Ajout d'une date de début de la période de rétention sous forme de crontab 
* Nouveau type de routing
  * Ajout des options "add", "overwrite", "replace" 
* Amélioration du démarrage ceBox® OS et de la machine virtuelle
* Amélioration du système de snapshot
  * Live snapshot (Service vss et qemu-ga doivent être actifs)

> ❗️ Attention
>
> Pour un master Windows, le service qemu-guest-agent doit être en mode "démarrage automatique début différé" pour assurer un fonctionnement optimal.\
> La version 1.19 des utilitaires ceBox apporte cette modification.

* Changement de service de stockage des messages échangés entre console et ceBox®/WSO®
* Amélioration lecture des logs ceBox®/WSO® 
* Réinstallation ceBox® /WSO®  à distance par le support Wisper
* Ping d'une ceBox® possible

Synchronisation et application du fichier routing uniquement pendant la phase d'extinction de la ceBox®. 

* **Corrections bugs**
  * Corrections apportées sur l'agent d'état VM
  * Mise à jour de securité  (packages) 
  * Mise à jour du kernel

## ceBox® OS version 2.0.8

* Passage du cache streaming en mode non compressé pour optimiser la rapidité de lecture des blocks
* Ajout d'un agent de surveillance des VM ( verification du renomage, que la vm est operationnelle) avec restart/rescue automatique de la cebox®
* Nouveau module de synchronization des blocs de data (wso → cloud et cloud ← wso) 
* Compatibilité Nuc 8 (seul le i3 est pre qualifié)
* Modification des messages de log dans la console
* affichage des informations de cache au niveau Wso / affichage lors des synchronization
* amélioration de la gestion du demarrage sans reseau
* **Corrections bugs**
* sur la gestion des tunnels en mode ha
* problème de synchronisation selon les latences reseaux
* upgrade securité  (packages) 
* upgrade kernel
* precache media 

## ceBox® OS version 2.0

* **Amélioration du système de cache**
* Démarrage plus rapide
* Stabilité accrue
* Système plus fluide
* Gestion disque améliorée (déduplication) 
* **Refonte de la gestion des masters**
* Plus de différenciation entre VM ReadOnly et VM ReadWrite
* Les versions sont dorénavant indépendantes des unes des autres
* Clonage amélioré
* Possibilité de trier les versions par ordre alphabétique ou par date de création
* Création de master directement via la console
* Création de version à la volée (Live Version)
* Création de tag personnalisé
* \*\*Cache Auto Allocation : pré-cache de version
* \*\*Cache Auto Eviction : suppression automatique des blocs disques non utilisés
* \*\*Retention Period  : permet de garder les modifications d'une VM sur un temps défini

## ceBox® OS version 1.0.34

**Cloud Wisper :**

* **Amélioration du cloisonnement des espaces de stockage** des médias dans l’infrastructure Cloud Wisper.
* **Amélioration de la sécurité de la tunnelisation** entre le Cloud Wisper et les sites clients (chiffrement).
* **Ajout d’une QoS et d’un Firewall** dédié à chaque client dans le Cloud.
* **Renforcement de la sécurité au niveau des postes ceBox®** qui détiennent aujourd’hui des accès beaucoup plus limités au niveau du Cloud.

## ceBox® OS version 1.0.33

* **Compatibilité avec l'Intel NUC Kabylake** i5 et i7

## ceBox® OS version 1.0.32

* **Amélioration du mode IGD** avec les nouveaux pilotes Intel
* **Mise à jour des scripts** d'**entrée dans le domaine** avec le nouveau mode Read Only
* **Amélioration** du **mode Rescue des WSO**
* **Optimisation** du nouveau **mode Read Only**

## ceBox® OS version 1.0.31

* **Amélioration de la gestion des ceBox** dans la console d'Administration
* **Optimisation des ressources système** : Diminution de la fréquence des tâches système
* Meilleure gestion des **disques SSD de type NVME**

## ceBox® OS version 1.0.30

* **Accélération de la prise en compte des messages de configuration** par les ceBox® (arrêt, redémarrage, changement de Version, etc).

* **Mise en place de la QOS sur les ceBox®** (débits entre les ceBox®, leur WSO et le Cloud Wisper) **et les WSO** (débits entre le WSO et le Cloud Wisper), configurable via la console.

* **Mise en place d’un Monitoring avancé** sur les WSO et les ceBox®, accessible via un navigateur.   

* **Mise en place d’un Flow Monitor**, visualisation des flux réseaux des ceBox®, distinction des flux de la ceBox® et de la VM (Applications). 

* **Nouveau système de VM Read Only** sur les ceBox® : le mode RO débute après le premier redémarrage de la machine virtuelle. Il est toutefois possible de revenir à l’ancien système via la console, dans la configuration des ceBox®. En savoir plus dans la documentation : **Gestion PCV Read-Only**

* Mise à jour du **noyau Linux** de ceBox® OS.

* **Amélioration du système de cache** des ceBox®.

* **Amélioration de la stabilité de la solution** ceBox® (hostname control, prise en charge du clavier Qwerty, amélioration du mode HA des WSO). 

  *Les fonctionnalités ci-après sont disponibles**à partir de la version 117 de la console ceBox** :*

* **Configuration avancée des ceBox®** dans la console : QOS, Monitoring des flux, MTU. 

* **Configuration avancée des WSO** dans la console : QOS, Monitoring des flux, MTU, Auto Upload des Masters. 

* **Affichage des tailles des Médias** (Master et Versions) dans la console ceBox®. 

* **La fonction « Check » de la console a été enrichie**, elle permet d’afficher la liste des routes des ceBox® (ceBox → Master → Version). 

## ceBox® OS version 1.0.29

* **Test de performance disque des WSO** lors de l'installation.
* Amélioration de la **haute disponibilité** en cas de défaillance WAN.

## ceBox® OS version 1.0.28

* **Optimisation de la gestion des tunnels entre les ceBox® et le Cloud** Wisper.
* Amélioration des performances de la **haute disponibilité des ceBox®**, quelques correctifs.
* Mise en place d’une **gestion de la bande passante** utilisée par les **WSO**.
* Possibilité d'agrandir la taille des Images Maître (Masters).

## ceBox® OS version 1.0.27

* **Reprise de la synchronisation des Médias** en Upload en cas de défaillance réseau.

## ceBox® OS version 1.0.26

* Mise à jour du **noyau Linux** de ceBox® OS.
* **Qualification de l’Intel NUC Kabylake**, sans prise en charge de l’IGD pour le moment.
* **Amélioration de la stabilité générale** de la solution, notamment sur la partie Clonage des Images Maîtres  et mises à jour des Images Maîtres.
* **Amélioration du mode HA** ainsi que de la gestion des tunnels.
* **Optimisation de la bande passante** des services Cloud.
* **Gestion d’un second disque persistant** sur les machines virtuelles pour les boitiers Intel NUC 3’’2 (SSD / SAS).