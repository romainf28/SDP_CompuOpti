### :pushpin: Projet CompuOpti
Projet pour le cours de Systèmes de Décision et Préférences à CentraleSupélec.

#### :page_facing_up: Description
Le sujet du projet peut être récupéré en s'identifiant avec votre compte de CentraleSupélec à partir de ce [lien](https://centralesupelec.edunao.com/pluginfile.php/291576/mod_resource/content/3/Projet_SDP_2022_23-4.pdf).

La société *CompuOpti* cherche à planifier efficacement son personnel sur les projets. Chaque projet nécessite de staffer un certain nombre de jours/hommes sur des compétences spécifiques (optimisation, gestion de projet, developpement web, ...). Ainsi, un projet peut nécessiter 6 jours/personne de compétences A, 2 jours/personne de compétences B, et 5 jours/personne de compétences C. 
On considèrera que le problème se déroule sur un horizon de temps donné (on ne considèrera que les jours ouvrés). Chaque membre du personnel de *CompuOpti* possède certaines qualifications, parmi un ensemble donné de qualifications (par exemple {A, B, C, D, E}), et des jours de congés prédéfinis intervenant durant l’horizon de temps.

Chaque qualification intervenant dans le projet est associé à un nombre de jours de travail dédié à cette qualification. Par ailleurs, chaque projet produit un gain s’il est réalisé, et la société cherche à maximiser le bénéfice total induit par les projets réalisés. Pour chaque projet, une date de livraison a été négociée avec le client, cette date ne doit pas être dépassée, sans quoi une pénalité financière par jour de retard est inscrite dans le contrat de prestation.

Il s’agit donc de définir des emplois du temps pour les membres du personnel, c’est-à-dire d’affecter chaque jour de travail d’un membre du personnel à une qualification d’un projet (ou à aucune activité). 

Le problème étudié est donc un problème de planification de personnel et d’affectation de projets.

#### :clipboard: Critères
Outre le bénéfice pour *CompuOpti*, l'entreprise veut prendre en compte d’autres aspects dans l’élaboration du planning. Voici les critères à prendre en compte :

1. Maximiser le résultat financier de l’entreprise et donc constituer un planning qui conduit à maximiser le bénéfice (incluant d’éventuelles pénalités).

2. Les collaborateurs n’aient pas à changer trop souvent de projet et, pour ce faire on s’attachera à minimiser le nombre de projets sur lesquels un quelconque collaborateur est affecté.

3. Il est important que les projets soient réalisés dans un nombre limité de jours consécutifs, ainsi on cherchera pour cela à executer le projet le plus long en un minimum de jours. 

#### 🔒 Contraintes
Dans la constitution du planning, un certain nombre de contraintes sont bien sûr à respecter :

1. Un membre du personnel ne peut être affecté à une qualification d’un projet que s’il possède cette qualification (contrainte de qualification du personnel).

2. A tout instant, un membre du personnel ne peut être affecté qu’à un seul projet et qu’à une seule qualification intervenant dans ce projet (contrainte d’unicité de l’affectation quotidienne du personnel).

3. Un membre de personnel ne peut pas être affecté à une qualification de projet un jour de congé (contrainte de congé).

4. Un projet n’est considéré réalisé que si tous les jours de travail dédiés à chacune des qualifications intervenant dans le projet ont ét;e couverts par des membres du personnel (contrainte de couverture des qualifications du projet).

5. Enfin, un projet ne peut être réalisé qu’une fois sur une période de temps donnée (contrainte d’unicité de la réalisation d’un projet).

#### :bar_chart: Jeux de données
Pour tester notre modèle, nous disposons de trois instances de taille croissante (``toy instance.json``, ``medium instance.json`` et ``large instance.json``) au format JSON.
Au delà de ces trois instances de départ, nous avons construit un générateur d’instances pour tester la performance de nos algorithmes.

#### 🎯 Objectifs
Le projet comporte deux parties. La première partie consiste à développer et mettre en oeuvre un modèle permettant de calculer la surface des solutions non-dominées du problème d’optimisation multiobjectif. La seconde partie vise à développer un modèle de préférence permettant de discriminer entre les solutions de la surface des solutions non-dominées.
Pour cela, il faudra être capable de partitionner les plannings en trois groupes : les planning inacceptables, corrects, et satisfaisants.

#### :card_index_dividers: Segmentation
Notre répertoire est segmenté en X deux fichiers markdown, un fichier .gitinore et un fichier texte pour les requirements :

```bash 
.
├── .gitignore
├── README.md
├── CONTRIBUTING.md
├── requirements.txt
├── instances
│    ├── instances_gived
│    │   ├── large_instance.json
│    │   ├── medium_instance.json
│    │   └── toy_instance.json
│    └── instances_created
│        ├── adjusted_job_length_horizon_16.json
│        └── dummy_test.json
├── trap_instances_creation.ipynb
├── pareto_surfaces
│    ├── large_instance.json
│    ├── medium_instance.json
│    └── toy_instance.json
├── save_efficient_solutions.py
├── modelisation.ipynb
├── preferences_medium_instance.ipynb
├── modelisation_instance_created.ipynb
├── display_utils.py
├── lp_utils.py
├── preferences_utils.py
├── utils.py
└── Systèmes_de_décision & préférences_Rapport.pdf 
```
 
- ``.gitignore`` contient les fichiers qui doivent être ignorés lors de l'ajout de fichiers au dépôt Git.
- ``README.md`` contient l'ensemble des informations sur le projet pour pouvoir l'installer.
- ``CONTRIBUTING.md`` contient l'ensemble des informations sur les normes et les pratiques de collaboration et de gestion du projet.
- ``requirements.txt`` contient la liste des modules et des bibliothèques Python qui doivent être installés, ainsi que leur version spécifique.
- ``instances`` contient l'ensemble des jeux de données avec deux sous-dossiers ``instances_gived``, qui comprend les jeux de données à notre disposition et ``instances_created``, qui comprend deux générations d'instances que nous avons créées.
- ``trap_instances_creation.ipynb`` permet de créer nos deux jeux d'instances ``dummy_test.json`` et ``adjusted_job_length_horizon_16.json``.
- ``pareto_surfaces`` contient l'ensemble des solutions non-dominées pour chaque instance donnée (``instances_gived`).
- ``save_efficient_solutions.py`` permet de sauvegarder les solutions non-dominées dans le dossier ``pareto_surfaces``.
- ``modelisation.ipynb`` contient l'ensemble des étapes pour construire nos deux modèles, un pour calculer la surface des solutions non-dominées et un modèle de préférence pour discriminer les solutions de la surface des solutions non-dominées (création du PL étape par étape, epsilon constraint pour les solutions non-dominées et inférence des préférences) pour l'instance ``toy_instance.json``.
- ``preferences_medium_instance.ipynb`` contient un test du programme d'inférence de préférences sur l'instance ``medium_instance.json``.
- ``modelisation_instance_created.ipynb`` est une réplique du notebook ``modelisation.ipynb`` qui permet d'avoir les résultats pour les instances créées (``adjusted_job_length_horizon_16.json``).
- Chaque fichier ``utils``, à savoir ``display_utils.py``, ``lp_utils.py``, ``preferences_utils.py`` et ``utils.py`` contient des fonctions utilitaires. Ils sont régroupés par catégorie de fonctions.
- ``Systèmes_de_décision & préférences_Rapport.pdf`` est le rapport détaillé et décrit l'ensemble de nos choix de modélisation ainsi que les résultats obtenus.

#### :wrench: Installation
Avant d'exécuter le modèle, vous devez installer [Gurobi](https://www.gurobi.com/downloads/).

Pour exécuter le modèle, nous vous recommandons sur un terminal uniquement :

1. Tout d'abord, assurez-vous que vous avez installé une version `python` supérieure à 3.9. Nous vous conseillons un environnement conda avec la commande suivante : 
```bash
conda create --name compuopti python=3.9
```
- Pour activer l'environnement :
```bash
conda activate compuopti
```
- Pour accéder au répertoire : 
```bash
cd SDP_CompuOpti
```

2. Vous devez ensuite installer tous les `requirements` en utilisant la commande suivante :
```bash
pip install -r requirements.txt
```

3. Pour exécuter les fichiers python utilisez les commandes suivantes :
```bash
python3 [nom du fichier]
```

4. Nous vous recommandons d'exécuter les notebooks et fichiers python dans l'ordre suivant : 

    1. trap_instances_creation.ipynb
    
    2. modelisation.ipynb
    
    3. preferences_medium_instance.ipynb
    
    4. modelisation_instance_created.ipynb
    
    5. save_efficient_solutions.py  

#### 🤔 Choix
Nous avons décidé d'appliquer, pour le modèle calculant la surface des solutions non-dominées, une méthode de type ε-constraint avec des pas entiers, étant donné le problème de programmation linéaire entière multiobjectif.

Pour les modèles de préférence discriminant la surface des solutions non-dominées, nous avons décidé d'implémenter un premier modèle de méthode de surclassement basée sur la comparaison d’alternatives et un deuxième modèle basé sur la théorie de l’utilité et la somme pondérée.

Un générateur d'instances a également été mis en place. Cela nous permet de tester l’influence de différents paramètres sur le classement fourni par notre système d’inférence de préférence.

#### :pencil2: Auteurs
- DELEBASSÉE Robin
- FOURNIER Romain
- MICHOT Albane
