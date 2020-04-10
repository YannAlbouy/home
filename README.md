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

![Exercice-1-Redim](/Exercice-1-redim.gif "resultat-1-redim")

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

![Exercice-2-1-Resultat](/Exercice-2-1.png "resultat-2-1")

## Exercice 2-2 Script d'animation

+ Introduction des commandes *sleep* et *translate*

Le script que l'on utilisera ici sera :

```diff
- (script (space color white)(robi color red)(robi translate 10 0)(space sleep 100)(robi translate 0 10)(space sleep 100)(robi (translate -10 0)(space sleep 100)(robi translate 0 -10) )
```
**Resultat de l'execution du script**

![Exercice-2-2-Resultat](/Exercice-2-2.gif "resultat-2-2")

*******************
## Exercice 3 Introduction des commandes
Dans cet exercice il a fallut mettre en place les classes qui mettent en œuvre l'interface *Command*.

Aucune difficulté n'a été rencontré lors de cet exercice.

Quatres classes on donc été ajouté : 
  * RobiChangeColor
  * RobiTranslate
  * SpaceChangeColor
  * SpaceSleep
  
**Classe RobiChangeColor**
```
public class RobiChangeColor implements Command{
	Color newColor;
	GRect robi;
	public RobiChangeColor(Color c, GRect r)
	{
		this.newColor = c;
		this.robi = r;
	}
	@Override
	public void run()
	{
		/*Changer la couleur de robi*/
		robi.setColor(newColor);
	}
}
```

**Classe RobiTranslate**

```
public class RobiTranslate implements Command{
	int x;
	int y;
	GRect robi;
	public RobiTranslate(int x, int y, GRect r)
	{
		this.x = x;
		this.y = y;
		this.robi = r;
	}
	@Override
	public void run()
	{
		/*Faire bouger robi */
		robi.translate(new Point(x,y));
	}
}
```

**Classe SpaceChangeColor**

```
public class SpaceChangeColor implements Command{
	Color newColor;
	GSpace space;
	public SpaceChangeColor(Color newColor, GSpace s) {
		this.newColor = newColor;
		this.space = s;
	}
	@Override
	public void run() {
		/*Changer la couleur du fond */
		space.setColor(newColor);
	}
}
```

**Classe SpaceSleep**
```
public class SpaceSleep implements Command{
	int temps;
	public SpaceSleep(int temps)
	{
		this.temps = temps;
	}
	@Override
	public void run() {
		/*Faire un temps de pause*/
		Tools.sleep(temps);
	}
}
```
**Script à executer**

```diff
-(script (space sleep 10000)(space color blue) (robi color green) (robi translate 10 0) (space sleep 100) (robi translate 0 10) (space sleep 100) (robi translate -10 0) (space sleep 100) (robi translate 0 -10) )
```

**Resultat de l'execution du script**

![Exercice-3-Resultat](/Exercice-3.gif "resultat-3")
*******************
## Exercice 4 Selection et execution des commandes

Ajout d'un interpreteur pour faciliter l'utilisation du programme

Aucune difficulté n'a été rencontré lors de cet exercice, mis a part un petit blocage lors ddu 4.4, cependant il à été reussi.

## Exercice 4-1 Réferencement des objets et enregistrement des commandes
Ajout des classes *References* et *Environment*, avec les differentes methodes.
* Reference
	* getCommandByName
	* addCommand
	* Expr run
* Environment
	* addReference
	* delReference
	* getReferenceByName

**Methode Run de Reference**

Permet de referencer l'objet graphique à un ensemble de commande
```
public Expr run(ExprList e) {
		String selector = e.get(1).getValue();
		Command c = this.getCommandByName(selector);
		if (c == null) return null;
		return c.run(this, e);
	}
```

**Exécution d'un script de test**

```diff
-(space sleep 1000)!(robi setColor green)(space sleep 500)(space setColor white)(space sleep 500)(robi setColor blue)(space setColor yellow)(robi translate 30 30) 
```

![Exercice-4-1-Resultat](/Exercice4-1.gif "resultat-4-1")

## Exercice 4-2 Ajout et suppression dynamique d'éléments graphiques
Pour cette partie il a fallu créer plusieurs classes :
* AddElement
* DelElement
* NewImage
* NewString
* NewElement

**Execution d'un script et resultat**
```diff
-(space add robi (rect.class new)) (robi translate 130 50)(robi setColor yellow)(space add momo (oval.class new))(momo setColor red)(momo translate 80 80)(space add pif (image.class new alien.gif))(pif translate 100 0)(space add hello (label.class new "Hello world"))(hello translate 10 10)(hello setColor black)
```
![Exercice-4-2-Resultat](/Exercice4-2.png "resultat-4-2")

## Exercice 4-3 Ajouter des éléments à des conteneurs

Modification pour que nos GContainer puissent contenir des éléments. Il suffit d'autoriser les GContainer à contenir des éléments.

**Script exécuter**

```
"(space add robi (rect.class new))!"
"(space.robi setDim 300 300)!"
"(space.robi setColor yellow)!"
"(space.robi add ala (rect.class new))!"
"(space.robi.ala setDim 200 200)!"
"(space.robi.ala setColor white)!"
"(space.robi.ala add hello (label.class new \"Hello world\"))!"
"(space.robi.ala.hello translate 10 10)!"
"(space.robi.ala.hello setColor black)!"
"(space.robi.ala add pif (image.class new test.jpg))!"
"(space.robi.ala.pif translate 100 0)!"
"(space.robi.ala.pif del pif)!"
"(space del robi)"
```

**Resultat lors de l'execution du script**

![Exercice-4-3-Resultat](/Exercice4-3-test.gif "resultat-4-3")

## Exercice 4-4 Création et exécution de scripts

Dans cette partie il fallait pouvoir créer et enregistrer des scripts afin de pouvoir les ré-utiliser quand on le souhaite.

J'ai rencontré des difficultés pour l'execution des scripts.

Pour gerer les scripts, le choix à été porter sur la classe *Environment* plutot que *Reference* car cela simplifie le code et l'interpreteur ne subit pas trop de modification.

Pour cela il a fallut ajouter plusieurs classes :
* AddScript
* DelScript

Ainsi qu'apporter des modifications dans la classe :
* Environment

+ **Test d'exécution d'un script pour le 4.4**

Le programme de test commence par ajouter les differents scripts, puis ils s'exécutent automatiquement. Puis il y a la suppression des scripts. Une fois le script supprimer, l'utilisateur ne pourra plus refaire la commande d'exécution, il devra tout d'abord re-ajouter le script.

**Script exécuter**

```
(space addScript addImage((self filename name)(self add w (Image new filename))))
(space addScript addRect (( self name w c )( self add name ( Rect new ) )( self.name setColor c )( self.name setDim w w ) ) )
(space addScript addOval (( self name w c )( self add name ( Oval new ) )( self.name setColor c )( self.name setDim w w ) ) )
(space addScript addLabel (( self text name)( self add w ( Label new text ) ) ) )
(space addScript delElement ( ( self filename )( self del filename ) ) )
(space addScript trslt (  (self filename w c ) (self translate w c )  ) )
(space addImage france.png france)
(space trslt france 10 5 )
(space addImage test.jpg test)
(space addRect robi 30 yellow )
(space addOval momo 60 red )
(space addLabel \"blabla\" lab1)
(space addLabel \"Bonsoir\" lab2)
(space delElement robi)
(space delElement momo)
(space delElement lab1)
(space delElement test)
(space delElement france)
(space delElement lab2)
(space delScript addRect)
(space delScript addImage)
(space delScript addOval)
(space delScript label)
```
**Resultat de l'exécution*
![Test-Exercice-4-4](/Exercice4-4-exec.gif "execution-4-4")

