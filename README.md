# A-Frame

**A-Frame** est un framework Web open-source basé sur JavaScript pour la création de scènes de réalité virtuelle (VR) et augmentée (AR) dans le navigateur.

Développé par Mozilla, il repose sur la puissance de WebGL et de Three.js, tout en simplifiant leur utilisation grâce à une structure basée sur HTML.
S'appuyant sur l'API WebXR, il est compatible avec tous les smartphones récents et la majorité des casques de réalité virtuelle disponibles.

A-Frame permet de créer des scènes 3D interactives en quelques lignes de code, sans avoir à manipuler directement WebGL ou Three.js.

Basé sur la technologie Web, toutes les applications créées avec A-Frame peuvent être hébergées sur un serveur Web et consultées à l'aide d'un navigateur Web.

## Table des matières

1. [A-Frame SetUp](#1-a-frame-setup)
   - [Installation](#11-installation)
   - [Installation locale](#12-installation-locale)
2. [Création de scènes A-Frame](#2-création-de-scènes-a-frame)
   - [Structure de base](#21-structure-de-base)
   - [Visual Inspector](#22-visual-inspector)
   - [Exercice](#23-exercice)
3. [Modélisation 3D](#3-modélisation-3d)
   - [Les Primitives](#31-les-primitives-)
   - [Primitives géométriques](#32-primitives-géométriques)
   - [Sous le capot a-entity](#33-sous-le-capot-a-entity-)
   - [La caméra (a-camera)](#34-la-caméra-a-camera)
   - [Transformations géométriques](#35-transformations-géométriques)
   - [Hiérarchie d'objets](#36-hiérarchie-dobjets)
   - [Exercice](#37-exercice)
   - [Textes](#38-textes)
   - [Images](#39-images)
   - [Chargement de modèles 3D](#310-chargement-de-modèles-3d)
   - [Exercice](#311-exercice)
4. [Apparence](#4-apparence)
   - [Couleur](#41-couleur)
   - [Propriétés optiques](#42-propriétés-optiques)
   - [Textures](#43-textures)
5. [Lumières](#5-lumières)
   - [Types de lumières](#51-types-de-lumières)
   - [Ombres portées](#52-ombres-portées)
   - [Exercice](#53-exercice)
6. [Ciel (a-sky)](#6-ciel-a-sky)
   - [Ciel avec couleur](#61-ciel-avec-couleur)
   - [Ciel avec texture/image](#62-ciel-avec-textureimage)
   - [Propriétés avancées](#63-propriétés-avancées)
   - [Exercice](#64-exercice)
7. [FOG](#7-fog)
   - [Types de brume](#71-types-de-brume)
   - [Exercice](#72-exercice)
8. [Animation](#8-animation)
9. [Interactions et contrôles](#9-interactions-et-contrôles)
   - [Cursor](#91-cursor-interactions-basées-sur-le-regard-avec-le-composant-curseur)
   - [Exemple d'interaction avec un objet](#92-exemple-dinteraction-avec-un-objet)
   - [Raycaster](#93-raycaster)
   - [wasd-controls](#94-wasd-controls-déplacement-clavier)
   - [look-controls](#95-look-controls-contrôle-du-regard)
10. [Création de composants personnalisés](#10-création-de-composants-personnalisés)
11. [Ressources et liens utiles](#ressources-et-liens-utiles)

---

## 1. A-Frame SetUp

### 1.1 Installation

Pour commencer à utiliser A-Frame, il suffit d'inclure la librairie dans votre projet. Vous pouvez le faire en ajoutant la ligne suivante dans le `<head>` de votre fichier HTML :

```html
<head>
  <script src="https://aframe.io/releases/1.7.0/aframe.min.js"></script>
</head>
```

### 1.2 Installation locale

Il est également possible de télécharger la librairie et de l'inclure localement dans votre projet `vite.js`.

```shell
npm install aframe
```

Ensuite, dans votre fichier JavaScript principal, importez `A-Frame` :

```javascript
import AFRAME from "aframe";
```

---

## 2. Création de scènes A-Frame

### 2.1. Structure de base

Un fichier A-Frame typique ressemble à ceci :

```html
<html>
  <head>
    <title>Ma première scène A-Frame</title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <script src="https://aframe.io/releases/1.7.0/aframe.min.js"></script>
  </head>
  <body>
    <a-scene>
      <a-box position="-1 0.5 -3" rotation="0 45 0" color="#4CC3D9"></a-box>
      <a-sphere position="0 1.25 -5" radius="1.25" color="#EF2D5E"></a-sphere>
      <a-cylinder
        position="1 0.75 -3"
        radius="0.5"
        height="1.5"
        color="#FFC65D"
      ></a-cylinder>
      <a-plane
        position="0 0 -4"
        rotation="-90 0 0"
        width="4"
        height="4"
        color="#7BC8A4"
      ></a-plane>
      <a-sky color="#ECECEC"></a-sky>
      <a-camera> </a-camera>
    </a-scene>
  </body>
</html>
```

le premier élément `<a-scene>` est le conteneur principal de la scène 3D. Il contient tous les éléments de la scène, tels que les objets 3D, les lumières, les caméras, etc.

Les éléments `<a-box>`, `<a-sphere>`, `<a-cylinder>` et `<a-plane>` sont des **primitives géométriques** prédéfinies : **entités**. Chaque primitive possède des **attributs spécifiques** : **composants**, qui définissent sa géométrie, sa position, sa couleur, etc.

![Scene](./assets/docs/scene.png)

L'icône en bas à droite permet de basculer en affichage stéréoscopique sur un smartphone ou un casque de réalité virtuelle. Les mouvements sont gérés par la centrale inertielle du casque et les joysticks.

Sur ordinateur, la rotation de la caméra est contrôlée par la souris et les déplacements en translation par les flèches du clavier.

### 2.2. Visual Inspector

A-Frame met à disposition un **outil d'inspection** accesible via le raccourci clavier `ctrl + alt + i` qui permet, à l'image d'un modeleur, de modifier les paramètres des objets composant la scène de réalité virtuelle. Cela permet de visualiser en temps réel les modifications apportées à la scène.

![Visual Inspector](./assets/docs/visual-inspector.png)

_Capture d'écran du Visual Inspector de A-Frame : [1] vue 3D façon modeleur, [2] vue arborescente de la scène, [3] propriétés géométriques et optiques de l'objet sélectionné._

Les modifications appliquées au sein de l'inspecteur ne sont pas automatiquement sauvegardées dans le code HTML du document Web, celui-ci étant stocké sur le serveur Web (éventuellement local). Mais il est possible de copier le code HTML de l'élément sélectionné grâce à l'outil figurant en haut à droite de l'interface. Ce code peut ensuite être collé dans le code source de votre application de réalité virtuelle afin d'y intégrer les modifications.

### 2.3. Exercice

> [!NOTE]
>
> - Créez un `repository git` et déployer votre site sur `GitHub Pages`.
> - Testez le code ci-dessus dans un fichier HTML et ouvrez-le dans un navigateur pour visualiser la scène 3D.
> - Testez Visual Inspector.
> - Testez le avec le Quest depuis le navigateur du Quest.

---

## 3. Modélisation 3D

### 3.1. Les Primitives :

`A-Frame` propose un ensemble de **primitives** prédéfinies qui peuvent être utilisées pour créer des objets 3D de base. Ces primitives sont des éléments HTML personnalisés qui peuvent être ajoutés à la scène en tant qu'entités.

```html
<a-box></a-box>
<a-sphere></a-sphere>
<a-cylinder></a-cylinder>
<a-plane></a-plane>
<a-sky></a-sky>
<a-camera></a-camera>
...
```

### 3.2. Primitives géométriques

Les primitives géométriques sont des formes de base qui peuvent être utilisées pour créer des objets 3D simples. Elles sont définies par des attributs spécifiques qui permettent de contrôler leur apparence.

```html
<a-box color="red" width="3"></a-box>
<a-sphere radius="2"></a-sphere>
<a-cylinder radius="0.5" height="1.5" color="blue"></a-cylinder>
<a-plane width="4" height="4" color="green"></a-plane>
```

Liste des primitives géométriques :
`a-plane`
`a-triangle`
`a-box`
`a-circle`
`a-cylinder`
`a-cone`
`a-dodecahedron`
`a-icosahedron`
`a-octahedron`
`a-ring`
`a-sphere`
`a-tetrahedron`
`a-torus`
`a-torus-knot`

![Primitives géométriques](./assets/docs/prim-geo.png)

### 3.3 Sous le capot `a-entity` :

**Entités - Composants - Systeme**

Le framework A-Frame s'articule autour du principe **Entité** - **Composant** : une entité, aussi appelée primitive, peut être modifiée par un composant inséré à l'élément en tant qu'attribut. Par exemple, pour définir la couleur d'un objet, on peut ajouter l'attribut color à l'entité correspondante.

> [!WARNING] > **Entités** : Ce sont des éléments HTML définis par la balise `<a-\*>`, comme `<a-box>, <a-sphere>`, etc.
> **Composants** : Propriétés ou comportements ajoutés aux entités. Exemples : position, color, rotation.

```html
<a-sphere radius="2"></a-sphere>
```

Dans l'exemple ci-dessus, `<a-sphere>` est une entité, et `radius="2"` est un composant qui définit le rayon de la sphère.

```html
<a-box color="red" width="3"></a-box>
```

Dans cet exemple, `<a-box>` est une entité, et `color="red"` et `width="3"` sont des composants qui définissent respectivement la couleur et la largeur de la boîte.
Il est également possible de définir une entité en utilisant la balise générique `<a-entity>`, qui peut être modifiée par plusieurs composants.

```html
<a-entity geometry="primitive : box; width: 3" material="color: red"></a-entity>
```

Les deux exemples ci-dessus sont équivalents. La première syntaxe est plus concise et plus lisible, tandis que la seconde est plus modulaire et permet de définir des composants supplémentaires.

### 3.4. La caméra (`<a-camera>`)

La caméra est l'élément qui définit le point de vue de l'utilisateur dans la scène 3D. Par défaut, A-Frame crée automatiquement une caméra si aucune n'est spécifiée, mais il est recommandé de la définir explicitement pour avoir un contrôle total.

#### Position et orientation par défaut

```html
<a-camera position="0 1.6 0"></a-camera>
```

La position par défaut `0 1.6 0` correspond à la hauteur moyenne des yeux d'un utilisateur debout (1.6m).

#### Caméra avec curseur

Pour permettre les interactions avec les objets de la scène, ajoutez un curseur à la caméra :

```html
<a-camera position="0 1.6 0">
  <a-cursor color="#FF0000"></a-cursor>
</a-camera>
```

#### Caméra dans un rig (recommandé)

Pour séparer le déplacement (position) et l'orientation (rotation), utilisez un rig parent :

```html
<a-entity id="rig" position="0 0 0">
  <a-camera position="0 1.6 0"></a-camera>
</a-entity>
```

Cette approche permet d'appliquer des transformations au rig (téléportation, physique) sans affecter directement la caméra.

Rig Parent (position absolue)
└─ Caméra (position relative au rig + rotation libre)

- Le rig : contrôle la position dans le monde (X, Z pour déplacement horizontal)
- La caméra : contrôle la hauteur (Y) et la rotation (regard)

#### Paramètres de la caméra

Principaux attributs configurables :

- `fov` (field of view) : Angle de vue en degrés (défaut: 80)
- `near` : Distance minimale de rendu (défaut: 0.005)
- `far` : Distance maximale de rendu (défaut: 10000)
- `zoom` : Facteur de zoom (défaut: 1)

```html
<a-camera fov="60" near="0.1" far="1000" zoom="1.5"></a-camera>
```

#### Caméra avec contrôles

Par défaut, la caméra intègre `look-controls` et `wasd-controls`. Pour les désactiver :

```html
<a-camera
  look-controls="enabled: false"
  wasd-controls="enabled: false"
></a-camera>
```

#### Caméra fixe (cinématique)

Pour une caméra statique sans contrôles utilisateur :

```html
<a-entity
  camera="active: true"
  position="5 2 5"
  rotation="0 -45 0"
  look-controls="enabled: false"
  wasd-controls="enabled: false"
>
</a-entity>
```

#### Multiples caméras

Vous pouvez définir plusieurs caméras et basculer entre elles en changeant l'attribut `active` :

```javascript
// Basculer vers une autre caméra
document.querySelector("#camera2").setAttribute("camera", "active", true);
```

> [Documentation camera](https://aframe.io/docs/1.7.0/components/camera.html)

### 3.5 Transformations géométriques

Les **composants** `position`, `rotation` et `scale` permettent respectivement de modifier la position, l'**orientation** et la **taille d'une primitive**.

#### Position

Les 3 valeurs du composant position correspondent aux déplacements selon les axes X, Y et Z.

```html
<a-box position="2 1 -5"></a-box>
```

#### Rotation

Les 3 valeurs du composant rotation représentent les angles de rotation (exprimés en degrés) autour des axes X, Y et Z.

```html
<a-box rotation="0 45 0"></a-box>
```

#### Scale

Les 3 valeurs du composant scale correspondent aux facteurs d'échelle selon les axes X, Y et Z. La valeur par défaut est `1 1 1` (taille normale). Une valeur de `2 2 2` double la taille dans toutes les directions.

```html
<a-box scale="2 1 0.5"></a-box>
<!-- Box 2x plus large, hauteur normale, moitié moins profonde -->
```

![Coordonnées attachées à la caméra](./assets/docs/camera_axis.jpg)
_Système de coordonnées attaché à la caméra_

### 3.6 Hiérarchie d'objets

En modélisation 3D, il peut être commode de placer un objet relativement à un autre. Lorsque l'élément parent dans la hiérarchie est deplacé, tous les éléments enfants sont automatiquement affectés par cette transformation géométrique.

```html
<a-sphere position="0 2 -5">
  <a-box position="-1 2 0"></a-box>
  <a-box position="1 2 0"></a-box>
</a-sphere>
```

La position relative de la première primitive `<a-box>` par rapport à la primitive `<a-sphere>` est de "-1 2 0" mais sa position absolue est égale à "-1 4 -5"

### 3.7. Exercice

> [!NOTE]
> Créez une belle sculpture en utilisant les primitives disponibles. Vous pouvez modifier les composants position et rotation des primitives du premier exemple afin de les empiler.

### 3.8. Textes

A-Frame propose un composant `<a-text>` qui permet d'afficher du texte en 3D. Ce composant prend en charge plusieurs attributs pour personnaliser l'apparence du texte, tels que la taille, la couleur, la police, etc.

```html
<a-text value="Hello, World!" color="black" position="0 2 -5"></a-text>
```

> [doc `<a-text>`](https://aframe.io/docs/1.7.0/primitives/a-text.html#main)

Version plus complète :

```html
<a-entity
  text="value: Hello, World!; color: black; align: center; width: 5"
  position="0 2 -5"
></a-entity>
```

> [text component](https://aframe.io/docs/1.7.0/components/text.html)

### 3.9. Images

A-Frame propose un composant `<a-image>` qui permet d'afficher des images en 3D. Ce composant prend en charge plusieurs attributs pour personnaliser l'apparence de l'image, tels que la largeur, la hauteur, la position, etc.

```html
<a-scene>
  <a-assets>
    <img id="my-image" src="image.png" />
  </a-assets>

  <!-- Using the asset management system. -->
  <a-image src="#my-image"></a-image>

  <!-- Defining the URL inline. Not recommended . -->
  <a-image src="another-image.png"></a-image>
</a-scene>
```

> [doc `<a-image>`](https://aframe.io/docs/1.7.0/primitives/a-image.html#main)

### 3.10. Chargement de modèles 3D

Au delà des nombreuses primitives proposées par A-Frame, il est possible d'afficher des **modèles 3D** issus de fichiers au format `glTF` ou `OBJ`.

l'élément `a-assets` permet de rassembler toutes les ressources (images, vidéos, modèles 3D) utilisées dans la scène. Chaque ressource doit avoir un identifiant unique (attribut `id`). L'attribut `src` désigne le chemin d'accès (dossiers et nom du fichier) au modèle 3D.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>A-Frame: OBJ and glTF 3D files</title>
    <!-- A-Frame JavaScript library -->
    <script src="https://aframe.io/releases/1.7.0/aframe.min.js"></script>
  </head>
  <body>
    <a-scene>
      <!-- Assets management -->
      <a-assets>
        <!-- MODELE OBJ -->
        <!-- Fichier de géométrie : maillage triangulaire -->
        <a-asset-item id="burger-obj" src="models/Hamburger-OBJ/Hamburger.obj">
        </a-asset-item>
        <!-- Fichier de matériau : couleur, textures -->
        <a-asset-item id="burger-mtl" src="models/Hamburger-OBJ/Hamburger.mtl">
        </a-asset-item>
        <!-- MODELE GLTF -->
        <a-asset-item id="flan" src="Flan.gltf"></a-asset-item>
      </a-assets>

      <!-- Utilisation du modèle OBJ -->
      <a-obj-model
        src="#burger-obj"
        mtl="#burger-mtl"
        position="-0.8 0 0"
        scale="0.15 0.15 0.15"
      >
      </a-obj-model>
      <!-- Utilisation du modèle GLTF -->
      <a-gltf-model src="#flan" position="0.8 0 0" scale="0.1 0.1 0.1">
      </a-gltf-model>

      <a-sky color="#ECECEC"></a-sky>

      <a-camera position="0 0.8 2"></a-camera>
    </a-scene>
  </body>
</html>
```

### 3.11. Exercice

> [!NOTE]
> Ajouter du texte et une image à votre scène.
> Allez sur http://poly.pizza et ajoutez un modèle 3D au dessus de votre colonne.

---

## 4. Apparence

Il est possible de modifier l'aspect visuel d'une primitive en modifiant les **composants relatifs au matériau**.

### 4.1 Couleur

Le **composant color** permet de définir la couleur diffuse d'une primitive. En informatique, une couleur est définie à partir des quantités de rouge, de vert et de bleu selon le principe de la synthèse additive.

A-Frame utilise la même syntaxe que le langage CSS pour définir une couleur. Il est possible d'utiliser les noms de couleurs prédéfinis, les valeurs hexadécimales ou les fonctions rgb() et rgba()...

### 4.2 Propriétés optiques

Au delà de la couleur, A-Frame propose les composants `opacity`, `roughness` et `metalness` qui correspondent respectivement à l'opacité, la rugosité et l'aspect métallique d'un matériau.

**La valeur de ces trois composants varie entre 0 et 1.**

### 4.3 Textures

Une image (ou une vidéo) peut être plaquée sur la surface d'une primitive pour simuler un effet de texture. Utilisez le système de gestion des assets pour charger la texture, puis appliquez-la via l'attribut `src` du matériau.

Exemple avec une image :

```html
<a-scene>
  <a-assets>
    <img id="wood-texture" src="textures/wood.jpg" />
  </a-assets>

  <a-box
    position="0 1 -5"
    material="src: #wood-texture; roughness: 0.8"
    width="2"
    height="2"
    depth="2"
  >
  </a-box>
</a-scene>
```

Exemple avec répétition de texture (tiling) :

```html
<a-plane
  position="0 0 -4"
  rotation="-90 0 0"
  width="10"
  height="10"
  material="src: #wood-texture; repeat: 5 5"
>
</a-plane>
```

> [Documentation material](https://aframe.io/docs/1.7.0/components/material.html)

## 5. Lumières

L'ajout de **lumières** permet d'améliorer le réalisme d'une scène 3D. A-Frame propose plusieurs types de lumières.

Type Attributs
`ambient` color intensity
`directional` color intensity position
| `point` | color intensity position |
| `spot` | color intensity angle penumbra position target |

### 5.1. Types de lumières

#### Lumière ambiante

```html
<a-entity light="type: ambient; color: white; intensity: 0.3"></a-entity>
```

L'attribut `intensity` permet de régler l'intensité de la lumière ambiante. La valeur par défaut est de 0.3.

#### Lumière directionnelle

```html
<a-entity
  light="type: directional; color: white; intensity: 0.5"
  position="1 1 1"
></a-entity>
```

L'attribut `position` permet de définir la position de la lumière dans la scène (vecteur directeur des rayons).

#### Lumière ponctuelle

```htm
<a-entity
  light="type: point; color: white; intensity: 0.7"
  position="0 2 0"
></a-entity>
```

La lumière ponctuelle émet des rayons dans toutes les directions à partir d'un point donné. L'attribut `position` permet de définir la position de la lumière dans la scène.

#### Lumière projecteur

```html
<a-entity
  light="type: spot; color: white; intensity: 0.8; angle: 30; penumbra: 0.2"
  position="0 2 0"
  rotation="-90 0 0"
></a-entity>
```

La lumière projecteur émet des rayons dans une direction donnée (Ce type de lumière s'apparente à une lumière ponctuelle mais émet un cône de lumière dans une direction donnée). L'attribut `position` permet de définir la position de la lumière dans la scène, tandis que l'attribut `rotation` permet de définir la direction des rayons.

### 5.2. Ombres portées

Pour ajouter encore plus de réalisme à la scène, les lumières peuvent générer des ombres portées en ajoutant l'attribut castShadow. Chaque objet de la scène doit préciser s'il produit une ombre (`cast`) ou s'il en reçoit (`receive`). Les ombres sont calculées en fonction de la position et de l'intensité des lumières.

```html
<a-entity
  light="type: directional; color: white; intensity: 0.5; castShadow: true"
  position="1 1 1"
></a-entity>

<a-box
  position="0 1 -5"
  rotation="0 45 0"
  color="#4CC3D9"
  shadow="receive: true"
></a-box>
```

## 5.3. Exercice

> [!NOTE]
> Testez les différentes lumières sur votre scène et testez les ombres portées.

## 6. Ciel (a-sky)

L'élément **`<a-sky>`** permet de définir l'arrière-plan d'une scène A-Frame en créant une sphère qui entoure toute la scène. Il peut être utilisé pour créer un ciel de couleur unie ou pour afficher une image panoramique à 360 degrés (equirectangulaire).

### 6.1. Ciel avec couleur

La façon la plus simple d'utiliser `<a-sky>` est de définir une couleur unie pour le fond de la scène :

```html
<a-scene>
  <a-sky color="#87CEEB"></a-sky>
  <!-- Autres éléments de la scène -->
</a-scene>
```

Exemples de couleurs courantes :

- `#87CEEB` : Bleu ciel
- `#1A1A2E` : Bleu nuit
- `#FF6B6B` : Rouge/rose (coucher de soleil)
- `#ECECEC` : Gris clair

### 6.2. Ciel avec texture/image

Pour créer un environnement plus immersif, vous pouvez utiliser une image panoramique (equirectangulaire) :

```html
<a-scene>
  <a-assets>
    <img id="sky-texture" src="images/sky-panorama.jpg" />
  </a-assets>

  <a-sky src="#sky-texture"></a-sky>

  <!-- Autres éléments de la scène -->
</a-scene>
```

**Format de l'image** : L'image doit être au format equirectangulaire (rapport 2:1, par exemple 4096x2048 pixels). Ce format permet de mapper correctement l'image sur la sphère intérieure qui entoure la scène.

**Sources d'images panoramiques** :

- [Poly Haven](https://polyhaven.com/hdris) - HDRIs gratuits
- [Flickr Equirectangular](https://www.flickr.com/groups/equirectangular/)
- Créez vos propres panoramas avec des applications comme Google Street View

### 6.3. Propriétés avancées

Le composant `<a-sky>` accepte plusieurs propriétés supplémentaires :

```html
<a-sky
  src="#sky-texture"
  rotation="0 90 0"
  radius="5000"
  phi-start="0"
  phi-length="360"
  theta-start="0"
  theta-length="90"
></a-sky>
```

**Propriétés principales** :

| Propriété      | Description                          | Valeur par défaut |
| -------------- | ------------------------------------ | ----------------- |
| `color`        | Couleur du ciel                      | `#FFF`            |
| `src`          | Source de l'image (via asset ou URL) | -                 |
| `rotation`     | Rotation du ciel (x y z en degrés)   | `0 0 0`           |
| `radius`       | Rayon de la sphère du ciel           | `5000`            |
| `phi-start`    | Angle de départ horizontal (0-360)   | `0`               |
| `phi-length`   | Longueur de l'arc horizontal (0-360) | `360`             |
| `theta-start`  | Angle de départ vertical (0-180)     | `0`               |
| `theta-length` | Longueur de l'arc vertical (0-180)   | `180`             |

**Exemple avec rotation** :

```html
<a-sky src="#sky-texture" rotation="0 -90 0"></a-sky>
```

Cela permet d'ajuster l'orientation de l'image panoramique.

**Exemple de ciel partiel** (demi-sphère) :

```html
<a-sky color="#87CEEB" theta-length="90"></a-sky>
```

Cela crée un ciel qui ne couvre que la moitié supérieure de la vue.

> [Documentation a-sky](https://aframe.io/docs/1.7.0/primitives/a-sky.html)

## 6.4. Exercice

> [!NOTE]
> Testez différentes options de `<a-sky>` sur votre scène. Utilisez une image panoramique.

## 7. FOG

L'ajout de **brume** (fog) permet de simuler des effets d'atmosphère et de profondeur dans une scène 3D. A-Frame propose deux types de brume qui s'appliquent directement sur l'élément `<a-scene>`.

| Type          | Attributs        |
| ------------- | ---------------- |
| `linear`      | color, near, far |
| `exponential` | color, density   |

### 7.1. Types de brume

#### Brume linéaire

```html
<a-scene fog="type: linear; color: #AAA; near: 5; far: 20">
  <!-- Objets de la scène -->
  <a-sphere position="0 1 -10" color="red"></a-sphere>
  <a-box position="0 0.5 -15" color="blue"></a-box>
</a-scene>
```

La brume linéaire augmente de manière linéaire entre les distances `near` (début de la brume) et `far` (brume maximale). Les objets au-delà de `far` sont complètement masqués par la brume.

#### Brume exponentielle

```html
<a-scene fog="type: exponential; color: white; density: 0.05">
  <!-- Objets de la scène -->
  <a-sphere position="0 1 -10" color="red"></a-sphere>
  <a-box position="0 0.5 -15" color="blue"></a-box>
</a-scene>
```

La brume exponentielle s'intensifie exponentiellement avec la distance. L'attribut `density` (valeur entre 0 et 1) permet de contrôler la densité de la brume : plus la valeur est élevée, plus la brume est dense.

## 7.2. Exercice

> [!NOTE]
> Testez les deux types de brume sur votre scène.

---

## 8. Animation

A-Frame propose un système d'animation assez complet allant des transitions de composants jusqu'à la simulation physique. Le composant `animation` permet d'animer n'importe quelle propriété d'une entité.

Exemple de rotation continue :

```html
<a-box
  position="0 1 -3"
  animation="property: rotation; to: 0 360 0; loop: true; dur: 3000"
></a-box>
```

Exemple d'animation au survol :

```html
<a-box
  position="0 1 -3"
  animation__mouseenter="property: scale; to: 1.2 1.2 1.2; startEvents: mouseenter"
  animation__mouseleave="property: scale; to: 1 1 1; startEvents: mouseleave"
></a-box>
```

**Paramètres principaux** :

| Paramètre     | Description                                                 |
| ------------- | ----------------------------------------------------------- |
| `property`    | Propriété à animer (position, rotation, scale, color, etc.) |
| `to`          | Valeur finale                                               |
| `from`        | Valeur initiale (optionnel)                                 |
| `dur`         | Durée en millisecondes                                      |
| `loop`        | true/false ou nombre de répétitions                         |
| `easing`      | Fonction d'easing (linear, easeInOutQuad, etc.)             |
| `startEvents` | Événements déclencheurs                                     |

> [Documentation animation](https://aframe.io/docs/1.7.0/components/animation.html)

---

## 9. Interactions et contrôles

A-Frame propose un système d'événements afin de réagir aux actions de l'utilisateur à l'aide :

- d'un **curseur** qui suit la caméra
- d'un **laser** attaché à la manette
  Pour cela, il faut inclure le composant `aframe-event-set` en ajoutant le code ci-dessous dans l'entête du fichier HTML.

```html
<script src="https://unpkg.com/aframe-event-set-component@5.x.x/dist/aframe-event-set-component.min.js"></script>
```

Évènement Description
`click` émis lors d'un **clic souris** ou d'une **pression sur la gachette**
`mouseenter` émis lorsque le **curseur** ou le **laser** survole l'objet
`mouseleave` émis lorsque le **curseur** ou le **laser** quitte la surface de l'objet

### 9.1. Cursor : Interactions basées sur le regard avec le composant curseur

Le **curseur** est un élément indispensable pour interagir avec les objets de la scène. Les interactions basées sur le regard reposent sur la rotation de la tête et le regard vers les objets pour interagir avec eux.

Comme A-Frame propose par défaut des commandes par glissement de souris, les interactions basées sur le regard peuvent être utilisées sur ordinateur pour prévisualiser l'interaction en faisant glisser la rotation de la caméra.

Le curseur est généralement attaché à la caméra pour qu'il suive le regard de l'utilisateur. Voici comment ajouter un curseur à une caméra dans A-Frame :

```html
<a-scene>
  <a-camera>
    <a-cursor></a-cursor>
    <!-- Or <a-entity cursor></a-entity> -->
  </a-camera>
</a-scene>
```

Il est possible de personnaliser le curseur en modifiant sa couleur, sa taille, sa forme, etc.

```html
<a-camera position="0 1.6 0">
  <a-cursor color="#FF0000"></a-cursor>
</a-camera>
```

### 9.2. Exemple d'interaction avec un objet

```html
<script src="https://aframe.io/releases/1.7.0/aframe.min.js"></script>
<script src="https://unpkg.com/aframe-event-set-component@5.x.x/dist/aframe-event-set-component.min.js"></script>
<body>
  <a-scene>
    <a-box
      position="-1 0.5 -3"
      rotation="0 45 0"
      color="#4CC3D9"
      event-set__enter="_event: mouseenter; color: #8FF7FF"
      event-set__leave="_event: mouseleave; color: #4CC3D9"
    ></a-box>

    <a-camera>
      <a-cursor></a-cursor>
    </a-camera>
  </a-scene>
</body>
```

### 9.3. Raycaster

Le **raycaster** est un composant qui permet de détecter les objets sur lesquels le curseur pointe. Il est utilisé pour gérer les interactions avec les objets de la scène, comme le clic sur un bouton ou le survol d'une image.

```html
<a-scene cursor="rayOrigin: mouse">
  <a-entity id="rig">
    <a-entity camera look-controls wasd-controls position="0 1.6 0">
      <a-cursor raycaster fuse="true" fuseTimeout="500"></a-cursor>
    </a-entity>
  </a-entity>
</a-scene>
```

### 9.4. wasd-controls (déplacement clavier)

Le composant `wasd-controls` permet de piloter le déplacement d'une entité avec le clavier (touches W/A/S/D ou flèches). Il est souvent utilisé sur la caméra en combinaison avec `look-controls` pour permettre la rotation et la translation indépendantes (souris / casque pour la vue, clavier pour le déplacement).

### wasd-controls (déplacement clavier)

Le composant `wasd-controls` permet de piloter le déplacement d'une entité avec le clavier (touches W/A/S/D ou flèches). Il est souvent utilisé sur la caméra en combinaison avec `look-controls` pour permettre la rotation et la translation indépendantes (souris / casque pour la vue, clavier pour le déplacement).

Paramètres courants

- `acceleration` / `speed` : contrôle la vitesse du mouvement.
- `enabled` : activer/désactiver le composant.
- `fly` : si true, permet de se déplacer en 3D (sans gravité).

Exemple :

```html
<a-entity
  camera
  look-controls
  wasd-controls="acceleration: 50; fly: true"
  position="0 1.6 0"
>
  <a-cursor></a-cursor> >
</a-entity>
```

Notes pratiques :

- Pour un déplacement avec collision/gravité, combinez `wasd-controls` avec
  un système physique (ex. `aframe-physics-system`).
- Sur mobile/VR, privilégiez les contrôles de mouvement natifs WebXR ou
  les composants fournis pour les manettes (hand-controls, tracked-controls).

Documentation : https://aframe.io/docs/ (chercher "wasd-controls" pour la version utilisée)

### 9.5. look-controls (contrôle du regard)

Le composant `look-controls` gère la **rotation (orientation) de la caméra** ou d'une entité qui représente la tête du joueur. Il collecte les entrées de la souris, du pavé tactile, des capteurs mobiles (gyroscope), et, en VR, les informations d'orientation fournies par le casque (WebXR), puis met à jour l'orientation (yaw/pitch) de l'entité.

Points clés :

- Entrées supportées : souris (drag + pointer lock), touch, capteurs mobiles, HMD/WebXR.
- Usage typique : placer `look-controls` sur la caméra et `wasd-controls` sur le rig parent pour séparer rotation (regard) et translation (position).

Options/attributs courants (nom exact selon version) :

- `pointerLockEnabled` / `pointerLock` : permettre le verrouillage du pointeur pour des mouvements de souris continus (nécessite généralement un clic utilisateur pour activer).
- `enabled` : activer/désactiver le composant.
- `touchEnabled`, `mouseEnabled`, `hmdEnabled` : activer/désactiver des
  sources d'entrée spécifiques.
- limites de `pitch`/`yaw` : parfois exposées ou à implémenter via un
  composant custom pour empêcher des rotations excessives.

Exemples :

Basique :

```html
<a-entity camera look-controls position="0 1.6 0"></a-entity>
```

Avec pointer lock (click pour activer) :

```html
<a-entity
  camera
  look-controls="pointerLockEnabled: true"
  position="0 1.6 0"
></a-entity>
```

Pattern recommandé (séparer rotation et position) :

```html
<a-entity id="rig" position="0 1.6 0">
  <a-entity camera look-controls></a-entity>
</a-entity>
```

Conseils et dépannage :

- Sur mobile iOS, l'accès aux capteurs peut nécessiter une permission via
  `DeviceOrientationEvent.requestPermission()` ; vérifiez la console pour des erreurs de permission.
- Les navigateurs exigent souvent une interaction utilisateur (clic) pour
  activer pointer lock ou accéder aux capteurs.
- Si la rotation « saute », vérifiez les conflits avec d'autres scripts qui
  modifient `object3D.rotation`, ou avec des styles/événements empêchant
  les gestes (`touch-action`, `preventDefault`).
- Pour combiner avec physique, appliquez la physique au parent (rig) et
  gardez `look-controls` sur la caméra pour éviter des oscillations.

Documentation : https://aframe.io/docs/ (chercher "look-controls" pour la version utilisée)

---

## 10. Création de composants personnalisés

A-Frame permet de créer des composants pour ajouter des fonctionnalités spécifiques :

```javascript
AFRAME.registerComponent("spin", {
  schema: { speed: { type: "number", default: 1 } },
  tick: function () {
    this.el.object3D.rotation.y += this.data.speed * 0.01;
  },
});
```

Utilisation dans HTML :

```html
<a-box spin="speed: 2" position="0 1 -5" color="#4CC3D9"></a-box>
```

---

```html
<a-entity hand-controls="hand: left"></a-entity>
<a-entity hand-controls="hand: right"></a-entity>
```

---

## Ressources et liens utiles

### Documentation officielle

- [A-Frame Documentation](https://aframe.io/docs/1.7.0/introduction/) - Documentation complète
- [A-Frame School](https://aframe.io/aframe-school/) - Tutoriels interactifs
- [A-Frame Blog](https://aframe.io/blog/) - Actualités et exemples

### Composants et extensions

- [A-Frame Registry](https://aframe.io/aframe-registry/) - Catalogue de composants communautaires
- [Superframe](https://github.com/supermedium/superframe) - Collection de composants utiles
- [A-Frame Physics System](https://github.com/c-frame/aframe-physics-system) - Physique réaliste
- [A-Frame Extras](https://github.com/c-frame/aframe-extras) - Contrôles, primitives et composants supplémentaires

### Modèles 3D et assets

- [Sketchfab](https://sketchfab.com/) - Modèles 3D (chercher "downloadable" et "glTF")
- [Poly Pizza](https://poly.pizza/) - Modèles 3D low-poly gratuits
- [Google Poly Archive](https://github.com/google-ar/poly-archive) - Archive de modèles
- [Kenney Assets](https://kenney.nl/assets) - Assets 3D gratuits pour prototypage

### Outils

- [Blender](https://www.blender.org/) - Logiciel de modélisation 3D open-source
- [Glitch](https://glitch.com/) - Éditeur en ligne pour prototyper rapidement
- [A-Frame Inspector](https://github.com/aframevr/aframe-inspector) - Inspecteur visuel (intégré)

### Communauté

- [A-Frame GitHub](https://github.com/aframevr/aframe) - Code source et issues
- [A-Frame Slack](https://aframe.io/slack-invite/) - Communauté d'entraide
- [Discord A-Frame](https://discord.gg/dFJncWwHun) - Discussions en temps réel
- [Stack Overflow](https://stackoverflow.com/questions/tagged/aframe) - Questions/réponses

### Exemples et inspirations

- [A-Frame Examples](https://aframe.io/examples/) - Galerie d'exemples officiels
- [WebVR Directory](https://webvr.directory/) - Projets WebVR/WebXR
- [Made with A-Frame](https://www.madewithfusion.com/tag/a-frame) - Showcase communautaire

### Pour aller plus loin

- [Three.js Documentation](https://threejs.org/docs/) - Bibliothèque 3D sous-jacente
- [WebXR Device API](https://www.w3.org/TR/webxr/) - Spécification WebXR
- [MDN WebXR](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API) - Guide MDN sur WebXR
