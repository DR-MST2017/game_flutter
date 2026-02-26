# game_flutter

Compte-Rendu du TP Flutter – Fondamentaux des Widgets
Étudiant : Med Salah Tlili
Module : Développement Mobile Flutter – IAM1 2025/2026
Durée du TP : 3 heures
________________________________________
1. Objectifs du TP
L’objectif de ce TP était de se familiariser avec :
1.	La création de widgets personnalisés (StatelessWidget).
2.	La réutilisation des widgets grâce aux paramètres du constructeur.
3.	La stylisation des widgets avec Container et BoxDecoration.
4.	La compréhension de l’arbre des widgets (Widget Tree).
5.	L’utilisation d’expressions switch pour des styles conditionnels.
________________________________________
2. Déroulement du TP
2.1 Création d’un widget Tile
•	J’ai créé une classe Tile héritant de StatelessWidget.
•	Les propriétés letter et hitType sont passées via le constructeur pour rendre le widget réutilisable.
•	Initialement, le widget retournait un Container vide.
class Tile extends StatelessWidget {
  const Tile(this.letter, this.hitType, {super.key});

  final String letter;
  final HitType hitType;

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
________________________________________
2.2 Ajout des dimensions et stylisation
•	J’ai ajouté une largeur et hauteur fixes (60x60).
•	Une bordure grise est ajoutée autour de chaque Tile.
•	La couleur de fond change en fonction du HitType grâce à une expression switch :
decoration: BoxDecoration(
  border: Border.all(color: Colors.grey.shade300),
  color: switch (hitType) {
    HitType.hit => Colors.green,
    HitType.partial => Colors.yellow,
    HitType.miss => Colors.grey,
    _ => Colors.white,
  },
),
________________________________________
2.3 Ajout du texte centré
•	J’ai utilisé un Center pour centrer la lettre dans la case.
•	Le texte est toujours affiché en majuscule, avec le style titleLarge du thème Material :
child: Center(
  child: Text(
    letter.toUpperCase(),
    style: Theme.of(context).textTheme.titleLarge,
  ),
),
________________________________________
2.4 Création d’une rangée de 5 tuiles
•	J’ai utilisé un Row pour aligner horizontalement 5 Tiles représentant une ligne du jeu Wordle.
•	Entre chaque tuile, un SizedBox(width: 4) crée un espace de 4 pixels.
Row(
  mainAxisAlignment: MainAxisAlignment.center,
  children: [
    Tile('A', HitType.hit),
    const SizedBox(width: 4),
    Tile('L', HitType.partial),
    const SizedBox(width: 4),
    Tile('O', HitType.miss),
    const SizedBox(width: 4),
    Tile('R', HitType.miss),
    const SizedBox(width: 4),
    Tile('S', HitType.hit),
  ],
),
________________________________________
3. Résultat
•	Une ligne de 5 tuiles apparaît au centre de l’écran.
•	Chaque tuile affiche la lettre et la couleur correcte selon le type (hit, partial, miss).
•	La bordure est uniforme et le texte est centré.
•	Le widget Tile est réutilisable et paramétrable pour tout autre mot ou rangée.
________________________________________
4. Difficultés rencontrées
•	Au début, j’avais mis le widget Tile à l’intérieur de MainApp, ce qui causait des erreurs.
•	La gestion de la couleur dynamique via switch était nouvelle pour moi.
________________________________________
5. Conclusion
Ce TP m’a permis de comprendre :
1.	La distinction entre StatelessWidget et StatefulWidget.
2.	L’importance du constructeur pour rendre un widget réutilisable.
3.	Comment styliser un widget avec Container et BoxDecoration.
4.	L’organisation de l’UI via l’arbre des widgets (Widget Tree).
Je suis désormais capable de créer des widgets Flutter simples, stylisés et réutilisables.
<img width="965" height="628" alt="image" src="https://github.com/user-attachments/assets/f559a158-ffdc-470d-90fc-8e8407aa29d1" />

  Mise en Page (Layout)
Objectifs du TP
•	Structurer une application Flutter avec Scaffold et AppBar.
•	Organiser des widgets verticalement et horizontalement avec Column et Row.
•	Générer dynamiquement des widgets à partir d’une liste de données.
•	Construire une grille de jeu 5×5 par imbrication de Column et Row.
•	Utiliser la syntaxe collection for pour créer des listes de widgets.

Étapes réalisées
1.	Création de l’application de base
o	Utilisation de MaterialApp et Scaffold.
o	Ajout d’un AppBar avec le titre “Birdle” aligné à gauche via Align.
2.	Création du widget Tile
o	Widget réutilisable pour représenter une case du jeu.
o	Propriétés :
	letter : caractère affiché.
	hitType : état de la lettre (bonne position, bonne lettre, absente, vide).
o	Container stylisé avec :
	Bordure grise fine.
	Couleur de fond conditionnelle selon HitType.
	Texte centré avec Text et style provenant de Theme.
3.	Création du widget GamePage
o	Conteneur principal du jeu contenant une instance de Game.
o	Structure : Center > Padding > Column > Row.
o	Chaque ligne (Row) contient 5 tuiles (Tile).
o	Espacement entre tuiles et lignes géré par spacing dans Column et Row.
o	collection for utilisé pour générer dynamiquement :
	5 lignes (tentatives).
	5 tuiles par ligne (lettres).
o	Grille centrée horizontalement via crossAxisAlignment: CrossAxisAlignment.center.
4.	Simulation d’une ligne de jeu
o	Utilisation de _game.guess('aback') pour simuler un essai réel.
o	Résultat : première ligne colorée selon la précision des lettres.
________________________________________
Points techniques appris
•	Column et Row permettent de gérer l’axe principal et l’axe secondaire (mainAxisAlignment, crossAxisAlignment).
•	Padding et Center permettent d’espacer et centrer les widgets facilement.
•	collection for de Dart simplifie la génération dynamique des widgets à partir de listes.
•	Tile est un exemple de widget personnalisé réutilisable et stylisé avec BoxDecoration.
•	Importance de l’ordre des widgets dans l’arbre pour le rendu et l’alignement correct.
•	Utilisation d’une seed fixe dans Game pour des tests reproductibles.
________________________________________
Résultat obtenu
•	Une grille de jeu 5×5 entièrement générée avec des tuiles blanches au départ.
•	Chaque tuile a une bordure grise fine et un espacement régulier de 5px.
•	Première ligne colorée simulée pour tester le rendu des HitType.
•	Application stable avec AppBar et contenu centré.
________________________________________
Problèmes rencontrés
•	Nécessité de gérer l’alignement du titre dans AppBar.
•	Compréhension de la génération dynamique des lignes et tuiles avec collection for.
•	Gestion de l’espacement entre widgets sans utiliser SizedBox à chaque fois grâce à spacing.
________________________________________
Conclusion
Le TP a permis de comprendre et mettre en pratique les principes de mise en page Flutter : Scaffold, AppBar, Column, Row, Padding, Center, et génération dynamique de widgets.
La création de la grille 5×5 avec Tile démontre la puissance des widgets imbriqués et de la syntaxe collection for pour un layout réactif et modulable
Affichage apres exécution 
<img width="950" height="648" alt="image" src="https://github.com/user-attachments/assets/b1b067b5-d883-411e-8381-a658d11b96ca" />

  DevTools
Objectifs atteints
1.	Découverte de DevTools :
o	Lancement via flutter run + dart devtools ou IDE.
o	Exploration des onglets : Flutter Inspector, Property Editor, Performance, CPU, Memory, Network, Logging.
o	Vérification de la connexion à l’application et navigation dans l’arbre des widgets.
2.	Widget Inspector :
o	Visualisation de l’arbre complet des widgets.
o	Identification des widgets créés : MaterialApp > Scaffold > AppBar, GamePage > Padding > Column > Row > Tile.
o	Sélection interactive d’un widget Tile pour inspection.
3.	Property Editor :
o	Modification des propriétés des widgets en temps réel :
	Container dans Tile : width, height, color.
	Column dans GamePage : spacing, crossAxisAlignment.
o	Remarque : modifications temporaires, non persistantes après hot reload.
4.	Erreur “Unbounded Constraints” :
o	Provocation volontaire : ListView dans un Column sans contrainte.
o	Diagnostic avec Widget Inspector : contrainte infinie (double.infinity) sur l’axe vertical.
o	Solutions :
1.	shrinkWrap: true sur ListView.
2.	Encapsuler ListView dans SizedBox(height: xxx) ou Expanded.
3.	Solution recommandée : ne pas utiliser ListView inutilement, la grille fixe 5×5 n’a pas besoin de défilement.
5.	Bonnes pratiques :
o	Utiliser Column pour la grille fixe.
o	Espacement avec spacing (Flutter 3.27+).
o	Centrer la grille horizontalement avec crossAxisAlignment: CrossAxisAlignment.center.
o	Observer et tester les modifications via Property Editor.
Observations clés
•	Flutter décompose chaque widget en sous-widgets internes (MediaQuery, Theme, etc.).
•	Chaque modification via Property Editor est instantanée mais non persistante.
•	Compréhension du protocole constraints go down, sizes go up, parent sets position.
•	Prévention d’erreurs fréquentes : ListView/Column imbriqués, Row dans Row, widget sans parent contraint.

