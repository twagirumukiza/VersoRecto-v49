# Changelog

## V48.0.0
- reconstruction depuis la V45 fournie ;
- abandon de la V47 défectueuse ;
- lancement de partie protégé avec diagnostic visible ;
- Victory Planner porté à 5 demi-coups en duel ;
- recherche multi-joueurs renforcée ;
- priorité aux victoires immédiates et aux blocages ;
- conservation des 5 816 configurations gagnantes ;
- conservation de la rotation d'ouverture des 7 pions ;
- anti-répétition et pénalités de stagnation ;
- lecture du son de déplacement avec repli Web Audio ;
- mémoire locale migrée en V48 ;
- export des parties en JSON et CSV ;
- workflow GitHub Pages et test automatique.

## v48.2 — Correctif de sécurité (revue de code)
- **Faille XSS corrigée** : les noms de joueurs (et les entrées d'historique/salle) étaient insérés tels quels via `innerHTML` dans `game.js`, `online-v37/38/39.js` et `online-lab.js`. Un nom du type `<img src=x onerror=...>` s'exécutait dans le navigateur de quiconque affichait la partie — y compris les autres participants d'un salon en ligne synchronisé par Firebase. Ajout d'une fonction `escapeHtml()` appliquée systématiquement à toutes les données affichées provenant de la saisie utilisateur.
- Ajout d'une fonction `sanitizePlayerName()` (retrait des caractères de contrôle, longueur limitée à 24 caractères) appliquée à la création des joueurs, en complément de l'échappement à l'affichage (défense en profondeur).
- Ajout de `maxlength="24"` sur les champs de nom dans l'interface locale.
- Vérifié : aucune autre valeur utilisateur non échappée trouvée dans les fichiers `learning-v41.js` et `experience-v44/45/48.js` (données internes uniquement).
- Aucune régression : `tests/smoke-test.js` repasse, et la syntaxe de tous les fichiers modifiés a été revérifiée.

## v48.1 — Correctif mémoire
- Correction de la page Expérience qui appelait par erreur `VR45Memory` au lieu de `VR48Memory`.
- Ajout d’un alias de compatibilité V45.
- Sauvegarde temporaire des coups dans `sessionStorage` jusqu’à la fin de partie.
- Ajout d’un cache-busting pour forcer GitHub Pages à charger le script corrigé.

## v48.3 — Correctif fin de partie multijoueur
- Correction d’une `ReferenceError` au dernier coup dans `online-v39.js` : `currentRoomCode` n’existait pas et a été remplacé par `roomCode`.
- L’enregistrement de la mémoire est désormais protégé par `try/catch` afin qu’une erreur locale ne bloque jamais la fin de partie ni la synchronisation Firebase.
- Utilisation prioritaire de `VR48Memory`, avec compatibilité `VR45Memory` et `VR44Memory`.
- Conversion correcte de l’objet des joueurs en tableau avant l’enregistrement du résultat.
