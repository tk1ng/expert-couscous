---
title: Blank page
deprecated: false
hidden: true
metadata:
  robots: index
---
Si vous avez un problème, voici les actions à effectuer : 

> 👍 Solution
>
> * Redémarrer la ceBox®
>
> * Éteindre la ceBox®, débrancher l'alimentation, attendre 1 minute et rebrancher l'alimentation de la ceBox®.
>
> * Supprimer la route sur la ceBox®, redémarrer la ceBox®, puis refaire la route.
>
> * [Réinstallation d'une ceBox®](https://helpcenter-cebox.wisper.io/docs/installation-dune-cebox#installation-dune-cebox) (Boot sur la clé d'installation faire un Eraser puis le redémarrage faire une installation de ceBox®)

Vous pouvez aussi utiliser l'outil ci-dessous, qui vous permettra de faire vos propres diagnostiques

<Embed url="https://www.ultimatebootcd.com/" title="Overview" favicon="https://www.ultimatebootcd.com/favicon.ico" image="https://www.ultimatebootcd.com/graphics/freewarede.jpg" provider="ultimatebootcd.com" href="https://www.ultimatebootcd.com/" />

> 🚧 Avertissement
>
> Avant de renvoyer un NUC au SAV Wisper, faire les manipulations suivantes, cela vous permettra potentiellement de gagner du temps.

> ❗️ Attention
>
> Si l'un des problèmes ci-dessous persiste, rapprochez-vous du support.

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Problème constaté
      </th>

      <th style={{ textAlign: "left" }}>
        Solution
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        Si message Bios bloquant
        "Minimal bash like line editing is supported for the first word tab list possible command completion"  

        Quand vous appuyez sur la touche "tab" vous arrivez sur une ligne de command Grub "\<grub\>"
      </td>

      <td style={{ textAlign: "left" }}>
        * [Réinstaller ceBox® OS](https://helpcenter-cebox.wisper.io/docs/installation-dune-cebox#installation-dune-cebox)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si un NUC reboot en boucle\
        Le voyant bleu clignote bleu (3 fois, pause, 3 fois, etc.)
      </td>

      <td style={{ textAlign: "left" }}>
        * Vérifier que la RAM est correctement clipsée et/ou la RAM est défectueuse
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si le NUC ne démarre pas (pas de voyant), démonter le SSD et voir si un voyant apparait au moment d'appuyer sur le Bouton
      </td>

      <td style={{ textAlign: "left" }}>
        * Vérifier avec une autre alimention électrique.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si vous constatez un problème réseau sur le NUC
      </td>

      <td style={{ textAlign: "left" }}>
        * [Réinstaller ceBox® OS](https://helpcenter-cebox.wisper.io/docs/installation-dune-cebox#installation-dune-cebox)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si Bruit au niveau du ventilateur
      </td>

      <td style={{ textAlign: "left" }}>
        * Dépoussiérer le NUC
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si un NUC reste bloqué sur la page Bios "Intel NUC"
      </td>

      <td style={{ textAlign: "left" }}>
        * Vérifier que la RAM est correctement clipsé
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si message Bios\
        Warning : CMOS Battery Failure\
        Warning : CMOS Ckecksum Error\
        Warning : CMOS Time Not Set
      </td>

      <td style={{ textAlign: "left" }}>
        Il y a un problème de Pile Bios, rapprochez-vous du support
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si pas d'affichage coté Windows
      </td>

      <td style={{ textAlign: "left" }}>
        * Vérifier en se connectant en VNC sur la machine et vérifier que les drivers sont bien installé dans le gestionnaire de tâche.  
        * Vérifier que c'est la carte Intel qui remonte dans le gestionnaire de tâche et non "Microsoft de base".  
        * Si problème de driver : [Mettre à jour les pilotes & ceBox® utility](https://helpcenter-cebox.wisper.io/docs/mettre-%C3%A0-jour-les-pilotes-cebox-utility)  
        * Vérifier que l'affichage est présent en allant sur le Bios.  
        * [Réinstaller ceBox® OS](https://helpcenter-cebox.wisper.io/docs/installation-dune-cebox#installation-dune-cebox)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si pas d'affichage coté Bios
      </td>

      <td style={{ textAlign: "left" }}>
        * Faire un test avec un autre câble vidéo et un autre écran
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si le voyant du bouton est allumé orange et que l'on appuie sur le bouton d'alimentation, rien ne se passe
      </td>

      <td style={{ textAlign: "left" }}>
        * Vérifier que la RAM et SSD sont correctement clipsés
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si le NUC s'éteint juste après avoir démarré
      </td>

      <td style={{ textAlign: "left" }}>
        * Vérifier que la RAM et SSD sont correctement clipsés
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si Plantage pendant chargement de L'OS
      </td>

      <td style={{ textAlign: "left" }}>
        * [Réinstaller Cebox® OS](https://helpcenter-cebox.wisper.io/docs/installation-dune-cebox#installation-dune-cebox)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si vous restez sur bloqué sur ClientName
      </td>

      <td style={{ textAlign: "left" }}>
        * [Réinstaller ceBox® OS](https://helpcenter-cebox.wisper.io/docs/installation-dune-cebox#installation-dune-cebox)  
        * Problème de communication avec le WSO® [Matrice de Flux ceBox®](https://helpcenter-cebox.wisper.io/docs/a-partir-de-la-3x-cebox)  
        * Changer de prise réseau et utiliser une prise où une ceBox® fonctionne.  
        * Vérifier la résolution DNS vers clientname.cblambda.neocoretech.net (en remplaçant clientname par le nom de votre compte client, transmis par Wisper).  
        * Vérifier l'ouverture des [Matrice de Flux ceBox®](https://helpcenter-cebox.wisper.io/docs/a-partir-de-la-3x-cebox) ports vers le WAN.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        Si la VM redémarre en boucle (mode rescue)
      </td>

      <td style={{ textAlign: "left" }}>
        Vérifier la configuration Bios [Configuration NUC pour WSO® & ceBox®](https://helpcenter-cebox.wisper.io/docs/configuration-nuc-pour-wso-et-cebox)
      </td>
    </tr>
  </tbody>
</Table>