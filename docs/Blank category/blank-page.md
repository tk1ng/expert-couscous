---
title: Blank page
deprecated: false
hidden: true
metadata:
  robots: index
---
## 1. Installation de l'agent

Après le téléchargement de l'exécutable, puis son lancement, vous voici face à une première fenêtre d'installation : 

<Image title="1.png" alt={762} src="https://files.readme.io/92512d4-1.png">
  Cliquer sur "Installer".
</Image>

<Image title="2.png" alt={760} src="https://files.readme.io/ef3e306-2.png">
  L'installation commence.
</Image>

Il n'y a quasiment pas d'étapes pour l'installation, une fois terminée, cette fenêtre s'ouvre : 

<Image title="3.png" alt={764} src="https://files.readme.io/aecda7c-3.png">
  Cliquer sur enregistrer la machine.
</Image>

Dès l'ouverture,vous devez voir le code d'enregistrement de la machine, vous devez le copier.

Ou si vous avez passé le popup, cliquer sur "Afficher les informations d'enregistrement".

<Image title="6.png" alt={749} src="https://files.readme.io/b225ade-6.png">
  Ce code n'est pas valable indéfiniment.
</Image>

Cela ré-affichera le popup avec le code d'enregistrement, puis cliquez sur "Enregistrer la machine", la fenêtre ci-dessous s'ouvre dans votre navigateur Web par défaut : 

<Image title="4.png" alt={897} src="https://files.readme.io/7389b79-4.png">
  Connectez-vous avec les identifiants d'administrateur Acronis.
</Image>

<Image title="5.png" alt={1917} src="https://files.readme.io/1dc3c77-5.png">
  Dans le champ "Registration code", coller le code d'enregistrement précédemment copier.
</Image>

Une fois l'installation le code renseigné, cliquer sur "CONFIRM REGISTRATION".\
/!\ ATTENTION : le temps de remonté de la machine n'est pas instantané, si cela ne fonctionne pas, persévérer./!\\ 

<Image title="7.png" alt={759} src="https://files.readme.io/fc52ec5-7.png">
  BRAVO ! Vous pouvez maintenant fermer la fenêtre en cliquant sur "FERMER" sur votre poste Windows.
</Image>

Ci-dessous, l’accueil de la dite console web : 

<Image title="8.png" alt={1912} src="https://files.readme.io/a464292-8.png">
  Si tout c'est bien passé, voici à quoi doit ressembler votre page d’accueil.
</Image>

Une fois connecté, sur votre gauche, un panneau latérale vous permettra d'avoir une vue rapide de vos tâches et leurs états : 

![250](https://files.readme.io/0671a81-7.jpg "7.jpg")

Sélectionnez "APPAREILS" sur le panneau décrit précédemment.\
Puis cliquez sur l'appareil que vous voulez gérer.

![698](https://files.readme.io/496a47e-8.jpg "8.jpg")

Mettez l'option  qui vous conviendra pour la sauvegarde des données utilisateurs.

![762](https://files.readme.io/3fd4dcc-9.jpg "9.jpg")

## 2. Déploiement/Installation de l'agent

L'installation ne peut se faire que par leur exécutable, qui ne contient aucun .MSI pouvant vous permettre un déploiement simple.\
La solution ceBox devient donc un atout pour optimiser cela.\
Une fois installé sur votre master, veuillez suivre la documentation ci-dessous.

## 3. Préparation à la masterisation

Windows OS

Acronis Backup Cloud 7.8 ou 7.9

Ouvrer un terminal de commande et naviguer dans "C:\Program Files\BackupClient:" : 

```
- cd "%ProgramFiles%\BackupClient\RegisterAgentTool"
```

Puis, entrer la commande suivante pour enregistrer la machine cliente grace au compte d'administration : 

```
- register_agent.exe -o register -t cloud -a https://cloud.acronis.com -u <compte> -p <mot-de-passe>

Ou utiliser la commande suivante pour utiliser la clé d'enregistrement : 

- "C:\Program Files\BackupClient\RegisterAgentTool\register_agent.exe" -a <votre-datacenter> 
```

\--token \<clé> -o register -t cloud

\<votre-datacenter\> est l'addresse du datacenter affiché dans votre navigateur à la connexion sur la console Acronis Backup exemple : [https://au1-cloud.acronis.com](https://au1-cloud.acronis.com) comme sur cette [précédente image](https://files.readme.io/b225ade-6.png²).

Acronis Backup Cloud 7.5 ou précédente : 

```
Ouvrer un terminal de commande et naviguer dans "C:\Program Files\BackupClient\BackupAndRecovery" : 

- cd "%ProgramFiles%\BackupClient\BackupAndRecovery"
```

Ou utiliser la commande suivante pour enregistrer le compte client:\
    register\_msp\_mms.exe register [https://cloud.acronis.com](https://cloud.acronis.com) \<compte\> \<mot-de-passe\>

Linux OS

Acronis Backup Cloud 7.8 or 7.9

```
Ouvrer un terminal Shell en tant que sudoer : 
```

Entrer la commande suivante pour enregistrer l'agent en utilisant le compte et le mot de passe:   

```
- /usr/lib/Acronis/RegisterAgentTool/RegisterAgent -o register -t cloud -a https://cloud.acronis.com -u <compte> -p <mot-de-passe>

Ou utiliser la commande suivante pour utiliser la clé d'enregistrement : 

 - /usr/lib/Acronis/RegisterAgentTool/RegisterAgent -o register -t cloud -a <votre-datacenter> --token <clé>
```

  \<votre-datacenter\> est l'addresse du datacenter affiché dans votre navigateur à la connexion sur la console Acronis Backup exemple : [https://au1-cloud.acronis.com](https://au1-cloud.acronis.com) comme sur cette [précédente image](https://files.readme.io/b225ade-6.png²). 

Acronis Backup Cloud 7.5 ou précédente : 

Ouvrer un terminal Shell en tant que sudoer :\
Entrer la commande suivante pour enregistrer l'agent : 

```
- /usr/lib/Acronis/BackupAndRecovery/AmsRegisterHelper register https://cloud.acronis.com <compte> <mot-de-passe>
```