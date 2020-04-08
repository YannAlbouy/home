# Albouy Yann Licence 3 CDA - Projet de synthese de SI 
Développement d’un langage spécifique pour des animations graphiques simples 
*******************
+ [Exercice 1 : Prise en main de la couche graphique](#exercice-1-Prise-en-main-de-la-couche-graphique)
+ [Exercice 2 : Première version d'un interpréteur de script](#exercice-2-première-version-dun-interpréteur-de-script)
  + [Exercice 2.1 : Script de configuration](#exercice-2-1-script-de-configuration)
  + [Exercice 2.2 : Script d'animation](#exercice-2-2-script-danimation)
+ [Exercice 3 : Introduction des commandes](#exercice-3-introduction-des-commandes)
+ [Exercice 4 : Selection et execution des commandes](#exercice-4-selection-et-execution-des-commandes)
  + [Exercice 4.1 : Réferencement des objets et enregistrement des commandes](#exercice-4-1-réferencement-des-objets-et-enregistrement-des-commandes)
  + [Exercice 4.2 : Ajout et suppression dynamique d'éléments graphiques](#exercice-4-2-ajout-et-suppression-dynamique-déléments-graphiques)
  + [Exercice 4.3 : Ajouter des éléments à des conteneurs](#exercice-4-3-ajouter-des-éléments-à-des-conteneurs)
  + [Exercice 4.4 : Création et exécution de scripts](#exercice-4-4-création-et-exécution-de-scripts)
*******************
## Exercice 1 Prise en main de la couche graphique
Cet exercice consistait à prendre en main la couche graphique.

__L'objet était de :__
  * Déplacer robi jusqu'au bord droit
  * Déplacement jusqu'au bord bas
  * Déplacement jusqu'au bord gauche
  * Déplacement jusqu'au bord haut
  * Changement de couleur avec une couleur aléatoire

**Résultat avec redimmensionnement**

![Exercice-1-Resultat-Redim](https://github.com/YannAlbouy/home/blob/master/Exercice-1-redim.gif "resultat-1-redim")

Aucune difficulté n'a été rencontré lors de cet exercice.
*******************
## Exercice 2 Première version d'un interpréteur de script
Dans le programme, un script est représenté come une expression parenthésée appelée S-expression.

Aucune difficulté n'a été rencontré lors de cet exercice.

## Exercice 2-1 Script de configuration

Le script que l'on utilisera ici sera :

```diff
- (script (space color black) (robi color yellow) )
```
**Resultat de l'execution du script**

![Exercice-2-1-Resultat](https://github.com/YannAlbouy/home/blob/master/Exercice-2-1.png "resultat-2-1")

## Exercice 2-2 Script d'animation

Le script que l'on utilisera ici sera :

```diff
- (script (space color white)(robi color red)(robi translate 10 0)(space sleep 100)(robi translate 0 10)(space sleep 100)(robi (translate -10 0)(space sleep 100)(robi translate 0 -10) )
```
**Resultat de l'execution du script**

![Exercice-2-2-Resultat](https://github.com/YannAlbouy/home/blob/master/Exercice-2-2.gif "resultat-2-2")

*******************
## Exercice 3 Introduction des commandes
Dans cet exercice il a fallut mettre en place les classes qui mettent en œuvre l'interface *Command*.
Quatres classes on donc été ajouté : 
  * RobiChangeColor
  * RobiTranslate
  * SpaceChangeColor
  * SpaceSleep

*******************
## Exercice 4 Selection et execution des commandes
## Exercice 4-1 Réferencement des objets et enregistrement des commandes
## Exercice 4-2 Ajout et suppression dynamique d'éléments graphiques
## Exercice 4-3 Ajouter des éléments à des conteneurs
## Exercice 4-4 Création et exécution de scripts

<p>Ceci est un paragraphe de texte.</p>

<p>Ceci est un autre paragraphe de texte !</p>
