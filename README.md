# AugmentedMobileApp

Application Web de réalité augmentée. L'idée est de créer une page html, définissant une scène de réalité augmentée qui précise un ou plusieurs marqueurs physiques sur lesquels viennent se placer à l'écran différentes informations pour augmenter la réalité.

À travers cette documentation, vous trouverez :
- le contexte du développement de cette application
- Les outils nécessaires au déploiement d'un tel dispositif
- L'explication du cas d'utilisation fourni via ce dépôt
- Les parties de code à adapter pour personnaliser votre utilisation de cet outil
## Contexte

Cette application a été réalisée dans un projet de travaux personnels encadrés par des enseignants de l'[Université de Technologie de Troyes](https://www.utt.fr/). Ce projet consiste en la réalisation d'une Toolbox de réalité augmentée, c'est à dire fournir un ensemble d'outils documentés permettant de mettre en place des dispositifs de réalité augmentée. 

L'application ici présente incarne une première partie de cette Toolbox, offrant un dispositif de perception et d'action mono-utilisateur. Une seconde partie de la Toolbox est à trouver sur le [dépôt](https://github.com/guibzy/AugmentedMapApp) concernant le dispositif de perception et d'action multi-utilisateurs.  

## Outils nécessaires

- Un serveur web connectée en https
- Un appareil équipé d'une caméra, d'un navigateur web et d'une connexion à internet
    - Smartphone et tablette (Android/iOS)
    - Ordinateur (Windows, Mac, Linux)

**/!\\** Si l'application n'est pas hébergée sur un serveur configuré https, seul le navigateur Mozilla Firefox est utilisable, les autres interdisent l'accès à la caméra. Cela exclut l'utilisation sur des appareils iOS puisque l'accès à la caméra passe par Safari en amont. 

## Cas d'utilisation fourni
- Cloner ce dépôt sur un serveur **https**
- Imprimer ou afficher sur un écran les marqueurs situés dans le dossier [marker/img/](marker/img)
- Accéder à la page [home.html](home.html) via le navigateur d'un appareil qui vous liste les différentes pages web de démonstration
    - Les pages nécessitant le marqueur [HIRO.jpg](marker/img/HIRO.jpg) :
        - [cube.html](cube.html) - *Exemple de projection d'un cube*
        - [image2d.html](image2d.html)  - *Exemple de projection d'une image 2D (logo UTT)*
        - [image3d.html](image3d.html) - *Exemple de projection d'une image 3D (avocat)*
        - [sphere.html](sphere.html) - *Exemple de projection d'une sphere*
        - [text.html](text.html) - *Exemple de projection d'un texte ("UTT")*
    - La pages nécessitant le marqueur [uttfinal-marker.png](marker/img/uttfinal-marker.png) :
        - [utt.html](utt.html) - *Exemple d'utilisation d'un marqueur personnalisé*
    - La pages nécessitant les deux marqueurs [HIRO.jpg](marker/img/HIRO.jpg) et [uttfinal-marker.png](marker/img/uttfinal-marker.png) :
        - [multi.html](multi.html) - *Exemple d'utilisation de différents marqueurs sur une scène*
- Sélectionner une page au choix, accepter d'utiliser la caméra et viser le marqueur adéquat pour voir apparaître sur l'écran une information augmentée. Sur smartphone, le rendu est plus intéressant si votre appareil est orienté en mode paysage.
        
## Code à adapter

Si vous souhaitez adapter l'outils pour votre usage, vous trouverez dans cette partie toutes les informations nécessaires.
### Structure de l'application
- assets - *Dossier contenant les fichiers de ressources permettant d'utiliser l'application*
    - glft - *Dossier contenant les images 3D que vous souhaitez utiliser. Il est nécessaire de fournir un fichier gltf v1 ou v2 avec son fichier binaire associé. Vous pouvez trouver des exemples de fichiers glft sur cette [page](https://github.com/KhronosGroup/glTF-Sample-Models)*
    - img - *Dossier contenant les images 2D que vous souhaitez utiliser*
- marker - *Dossier contenant les fichiers liées à l'usage des marqueurs*
    - img - *Dossier contenant les marqueurs au format image*
    - patt - *Dossier contenant les marqueurs au format .patt qui permet à la librairie AR.js d'interpréter et de reconnaître les marqueurs. A noter que le marqueur par défaut de la librairie est `hiro` et qu'il ne nécessite donc pas de posséder son fichier .patt*
- js - Dossier contenant le fichier `aframe-ar-1.5.0.js`, qui est une version modifiée (originale [ici](https://github.com/jeromeetienne/AR.js/tree/master/aframe/build)) par nos soins afin de pouvoir proposer des marqueurs personnalisés
- Les pages .html 

### Adaptations

#### Modéliser des informations

Pour comprendre comment fonctionne la définition d'une scène via [AR.js](https://github.com/jeromeetienne/AR.js) et le framework [A-frame](https://aframe.io/blog/arjs/), nous vous invitons à regarder le contenu de chaque page html de [démonstration](#cas-dutilisation-fourni) disponible dans ce dépôt. Elles n'excèdent pas plus de 10 lignes d'html et sont commentées précisément.

Pour un accès rapide aux différentes entités qu'il est possible de modéliser, vous trouverez ci-dessous un lien vers leurs documentations respectives. Il existent de nombreux attributs paramètrables, comme la possibilité d'effectuer un repositionnement, une rotation, ajouter de la transparence, de préciser une couleur, d'effectuer une mise à l'échelle.... Vous trouverez ici un exemple d'utilisation et la liste des attributs disponibles pour chaque entité :
- [box](https://aframe.io/docs/0.8.0/primitives/a-box.html#sidebar)
- [sphere](https://aframe.io/docs/0.8.0/primitives/a-sphere.html#sidebar)
- [cylindre](https://aframe.io/docs/0.8.0/primitives/a-cylinder.html#sidebar)
- [text](https://aframe.io/docs/0.5.0/primitives/a-text.html)
- [image](https://aframe.io/docs/0.5.0/primitives/a-image.html)
- [assets](https://aframe.io/docs/0.8.0/core/asset-management-system.html#sidebar)

Pour plus de précisions, ou de paramétrages, nous vous invitons à consulter les documentations disponibles :
- [AR.js](https://github.com/jeromeetienne/AR.js)
- [A-FRAME](https://aframe.io/blog/arjs/)

#### Générer un marqueur personnalisé

L'utilisation d'un marqueur personnalisé est décrit dans le fichier [utt.html](utt.html). Si vous aussi vous souhaitez générer un marqueur personnalisé, rendez vous sur cette page de [générateur](https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html) de marqueur, et suivez les étapes suivantes :
   1. Préparer une image de dimension carré (ex: 400x400) sur votre ordinateur, avec de préférence un fond clair (RGB : 240,240,240)
   2. Sur la page de générateur, cliquer sur upload, et choisissez l'image préparée
   3. (optionnel) Réglez le ratio à votre convenance, nous l'avons laissé à 0.5 par défaut lors de nos expérimentations
   4. Cliquez sur download Marker pour obtenir le fichier .patt à mettre sur le serveur. C'est ce fichier qui est à appeler lors de définition de scènes html.
   5. Cliquez sur download Image pour obtenir la version .png de votre marqueur, que vous pourrez par la suite imprimer ou afficher sur un écran pour l'utiliser.