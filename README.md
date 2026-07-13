# Verso Recto V48

Version autonome construite à partir de la V45 fonctionnelle. Aucun fichier de la V47 n’est utilisé.

## Contenu
- jeu local, IA et mode mixte de 2 à 4 participants ;
- plateau de 72 triangles et 28 pions ;
- 5 816 configurations gagnantes (2 faces pour 2 908 motifs) ;
- Victory Planner renforcé, recherche alpha-bêta et Worker avec repli local ;
- priorité aux victoires immédiates et blocage des menaces ;
- ouverture avec rotation des 7 pions, sauf urgence tactique ;
- anti-stagnation et limitation des allers-retours ;
- son de déplacement et de victoire avec solution de secours Web Audio ;
- mémoire locale V48 ;
- export JSON et CSV des parties ;
- fichiers GitHub Pages prêts à publier.

## Lancer
Ouvrir `index.html` ou servir le dossier avec un serveur statique. Pour GitHub Pages, publier la branche principale depuis la racine.

## Tests
Exécuter `node tests/smoke-test.js`.
