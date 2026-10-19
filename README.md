# TIPE 2025 — Réalisation d’un bras artificiel

Projet réalisé en **CPGE PT\*** à **Champagne-sur-Seine** dans le cadre de la **session TIPE 2025**.

## Présentation

Ce TIPE avait pour objectif d’étudier dans quelle mesure les connaissances acquises en classe préparatoire pouvaient permettre de **concevoir et réaliser un bras artificiel capable de reproduire certaines fonctions d’un membre supérieur humain**.

La problématique retenue était :

> **Dans quelle mesure nos connaissances acquises en classe préparatoire nous permettent-elles de concevoir un bras artificiel capable de réaliser les fonctions habituellement assurées par un bras humain ?**

Le projet associe plusieurs domaines de l’ingénierie :

- biomécanique ;
- conception mécanique ;
- modélisation 3D ;
- impression 3D ;
- électronique ;
- traitement du signal ;
- automatique et asservissement ;
- systèmes embarqués ;
- transmission de puissance ;
- communication entre microcontrôleurs ;
- programmation.

Le travail a abouti à la réalisation d’une **maquette fonctionnelle de bras artificiel**, intégrant acquisition de données, traitement de signaux, communication entre plusieurs cartes électroniques, asservissement et actionnement mécanique.

---

## Conception du prototype

L’ensemble des systèmes mécaniques spécifiques du prototype a été **conçu et designé par mes soins**.

Toutes les pièces visibles en **noir ou en gris non métallique** sur le prototype correspondent à des éléments en plastique ou en résine que j’ai :

1. conçus et modélisés en 3D ;
2. travaillés sous **SolidWorks** et **Onshape** pour la conception mécanique paramétrique ;
3. modélisés sous **Blender 3D** pour les éléments nécessitant une **modélisation surfacique par sculptage** ;
4. préparés pour la fabrication ;
5. puis **imprimés en 3D**.

L’objectif était de concevoir des pièces adaptées spécifiquement à la géométrie, aux mouvements, aux liaisons et aux contraintes mécaniques du bras artificiel, plutôt que de réaliser uniquement un assemblage de composants standards.

---

## 1. Acquisition et traitement du signal EMG

Le projet utilise un **capteur électromyographique (EMG)** afin de récupérer une information issue de la contraction musculaire de l’utilisateur.

Le signal EMG brut n’étant pas directement exploitable, une étape de **traitement et de filtrage du signal** est nécessaire avant son utilisation dans le système de commande.

L’objectif est ainsi de transformer une information physiologique issue de l’utilisateur en une donnée exploitable par la prothèse.

---

## 2. Mesure de la position du poignet

Un capteur inertiel **MPU6050 6 axes** est utilisé afin de récupérer notamment :

- les accélérations ;
- les vitesses angulaires.

Des changements de base et des traitements numériques sont ensuite utilisés afin d’exploiter ces données pour déterminer la position et l’orientation de la main relativement à l’avant-bras.

Cette partie du projet permet d’étudier la récupération des mouvements de l’utilisateur afin de les transmettre au bras artificiel.

---

## 3. Asservissement du moteur

L’actionnement du bras repose notamment sur un **moteur à courant continu équipé d’un encodeur**.

Un asservissement de position a été développé afin d’améliorer la précision du mouvement.

Pour une consigne en échelon de **90°** :

- l’erreur statique observée initialement était inférieure à **8°** ;
- après mise en place de l’asservissement et du traitement associé, l’erreur statique obtenue était d’environ **1°**.

### Conception du pont en H

Une première solution consistait à réaliser directement un **pont en H à transistors** afin de piloter le moteur.

Le principal problème rencontré lors de cette conception provenait de la **résistance interne des transistors utilisés**.

Cette résistance était trop importante pour le fonctionnement recherché et perturbait le signal de commande du moteur.

Afin de ne pas bloquer l’avancement du projet, cette réalisation discrète a finalement été remplacée par un **module L298N** pour la maquette.

Cette étape a néanmoins permis d’étudier concrètement les contraintes d’un **étage électronique de puissance**, notamment la différence entre la génération d’un signal de commande et la capacité réelle du circuit à fournir la puissance nécessaire au moteur.

---

## 4. Dimensionnement mécanique

Une étude de statique et de cinématique a été réalisée afin d’estimer le couple nécessaire au niveau de l’articulation du coude.

Le couple maximal calculé était d’environ :

**1,87 N·m**

Un objectif de dimensionnement proche de **2 N·m** a donc été retenu.

Le moteur utilisé sur la maquette était un :

**Motoréducteur Pololu 37Y3530-43.8 avec encodeur**

Le moteur retenu permettait de faire fonctionner le démonstrateur, mais ses performances restaient insuffisantes pour atteindre l’objectif de charge maximal envisagé pour une version plus proche d’une véritable prothèse.

Cette différence entre le composant idéal et le composant réellement utilisé faisait partie des compromis nécessaires pour conserver un projet réalisable dans le cadre et le budget d’un TIPE.

---

## 5. Architecture électronique — réseau entre quatre cartes

Le fonctionnement du prototype ne repose pas uniquement sur une communication ponctuelle entre deux cartes électroniques.

L’architecture a été conçue autour de **quatre cartes communiquant au sein d’un réseau en étoile**.

L’objectif était de répartir les différentes tâches du système entre plusieurs unités électroniques plutôt que de concentrer l’ensemble des traitements sur une seule carte.

Cette architecture permet notamment de séparer différentes fonctions :

- acquisition des données ;
- traitement des informations ;
- communication ;
- commande des actionneurs.

Le réseau en étoile permet également :

- de répartir la charge de calcul ;
- de structurer les échanges entre les cartes ;
- de limiter les dépendances entre les différents sous-systèmes ;
- de faciliter le développement et le débogage ;
- de conserver une architecture évolutive.

---

## 6. Conception d’une main articulée

Une extension du projet a également porté sur la réalisation d’une **main artificielle**.

Deux sous-systèmes ont notamment été étudiés.

### Exosquelette d’acquisition

Un exosquelette équipé de **potentiomètres** permet de récupérer la position des différentes phalanges de la main de l’utilisateur.

### Main artificielle

La partie mécanique de la main utilise principalement :

- des engrenages ;
- des systèmes poulies-courroies.

L’objectif était de privilégier des transmissions mécaniques permettant d’obtenir une meilleure précision et une meilleure fiabilité, tout en limitant l’utilisation de ressorts et d’élastiques.

Les pièces mécaniques spécifiques nécessaires à cette réalisation ont également été conçues et modélisées dans le cadre du projet.

---

## Résultats

Le projet a permis de développer une maquette intégrant notamment :

- acquisition de signaux musculaires EMG ;
- mesure inertielle ;
- traitement de données capteurs ;
- traitement du signal ;
- commande de moteurs ;
- asservissement de position ;
- communication entre **quatre cartes électroniques** ;
- architecture réseau en étoile ;
- transmission mécanique ;
- calcul et dimensionnement du couple moteur ;
- conception mécanique ;
- modélisation 3D ;
- impression de pièces en plastique et en résine ;
- conception d’une première main articulée.

L’objectif principal était de démontrer la **faisabilité globale d’un système capable d’acquérir les mouvements et intentions d’un utilisateur afin de les transformer en mouvements d’un bras artificiel**.

Le prototype a également permis d’identifier plusieurs limitations techniques et pistes d’amélioration pour une version plus aboutie.

---

## Perspectives

Plusieurs pistes de développement avaient été identifiées à l’issue du TIPE :

- amélioration de la main artificielle ;
- utilisation d’actionneurs offrant un couple plus important ;
- amélioration du traitement des signaux EMG ;
- augmentation de la précision des mouvements ;
- utilisation de capteurs piézoélectriques ou de capteurs de force pour contrôler la préhension ;
- utilisation de méthodes d’intelligence artificielle afin de prédire certains mouvements de l’utilisateur et améliorer la réactivité de la prothèse.

---

## Technologies et outils utilisés

### Conception mécanique et modélisation 3D

- **SolidWorks**
- **Onshape**
- **Blender 3D** — modélisation surfacique par sculptage
- modélisation 3D
- impression 3D plastique / résine
- conception mécanique
- engrenages
- systèmes poulies-courroies

### Électronique et systèmes embarqués

- Arduino / microcontrôleurs
- C / C++
- Python
- capteur EMG
- MPU6050
- moteurs à courant continu
- encodeurs
- servomoteurs
- potentiomètres
- L298N
- réseau de quatre cartes en étoile

### Automatique et traitement du signal

- acquisition de données
- traitement du signal EMG
- filtrage
- asservissement de position
- traitement de données inertielles
- transformation de repères

---

## MCOT — Mise en cohérence des objectifs du TIPE

La **MCOT** associée au projet présente le travail préparatoire ayant conduit au choix du sujet, à la problématique et aux objectifs du TIPE.

Le projet s’inscrit dans le domaine de la **biomécanique**, et plus particulièrement dans l’étude du lien possible entre l’être humain et la machine.

L’enjeu principal retenu était l’acquisition, la transmission et le traitement de différents signaux afin de produire une action correspondant à la volonté de l’utilisateur.

Les trois objectifs principaux définis dans la MCOT étaient :

1. **concevoir un bras artificiel** ;
2. **récupérer toutes les informations sur la position du bras de l’utilisateur** ;
3. **établir une communication entre le bras de l’utilisateur et le bras artificiel**.

➡️ **[Consulter la MCOT](MCOT_Arthur_Ripoll_2025.pdf)**

---

## Bibliographie commentée

La préparation du projet s’est appuyée sur une étude bibliographique portant notamment sur :

- l’électromyographie ;
- le contrôle d’exosquelettes par signaux EMG ;
- l’estimation des mouvements et des couples articulaires ;
- la motricité bio-inspirée ;
- le traitement et la modélisation des signaux électromyographiques ;
- le contrôle biomimétique de prothèses ;
- l’anatomie du membre supérieur ;
- la dynamique mécanique du bras humain.

Parmi les références utilisées figurent notamment des travaux de :

- B. Tresussart, R. Caron, F. Geffard et F. Marin ;
- Y. Koike et M. Kawato ;
- Sébastien Mick ;
- H. He et K. Kiguchi ;
- Jonathan Monsifrot ;
- Effie Ségas ;
- Frank Netter ;
- Eric J. Perreault, Robert F. Kirsch et Patrick E. Crago.

La bibliographie complète ainsi que les commentaires associés sont disponibles dans la MCOT.

---

## Documentation

### Présentation complète du TIPE

➡️ **[Consulter le diaporama complet](TIPE_Arthur_Ripoll_2025.pdf)**

Le document présente notamment :

- la démarche de conception ;
- le traitement du signal EMG ;
- la mesure inertielle ;
- l’asservissement ;
- la conception du pont en H ;
- le dimensionnement mécanique ;
- l’architecture réseau ;
- les essais expérimentaux ;
- les résultats obtenus ;
- la conception de la main ;
- les photographies du prototype ;
- les principaux programmes développés en annexes.

### MCOT et bibliographie

➡️ **[Consulter la MCOT et la bibliographie commentée](MCOT_Arthur_Ripoll_2025.pdf)**

---

## À propos de ce projet

**Note :** Ce TIPE, réalisé en 2025, constitue mon premier projet d’ingénierie complet en CPGE. La présentation est volontairement conservée proche de sa version d’origine afin de refléter le travail et les méthodes développés à cette période.

---

## Auteur

**Arthur Ripoll**  
CPGE PT\* — Champagne-sur-Seine  
Session TIPE 2025

---

> **Remarque :** ce projet a été réalisé dans un cadre académique et constitue un **prototype expérimental**. Il ne s’agit pas d’un dispositif médical certifié.
