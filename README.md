# Forge +24

Simulateur de forge permettant de tester virtuellement l'amélioration d'un équipement de +11 jusqu'à +22, avec possibilité d'atteindre +23 ou +24 selon les résultats des améliorations.

Le simulateur comptabilise automatiquement le nombre de tentatives, les échecs, les baisses de niveau et le coût total en argent.

## Fonctionnalités

- Départ automatique à +11
- Tentatives d'amélioration simulées
- Chance différente selon le niveau
- Réussite pouvant faire progresser de +1 à +3 niveaux
- Baisses automatiques à certains niveaux
- Comptage des tentatives
- Comptage des échecs
- Comptage des baisses
- Calcul du coût total
- Conversion argent → or
- Arrêt automatique à +22, +23 ou +24
- Simulation de 1 000 parcours
- Calcul des moyennes et médianes
- Affichage du minimum et du maximum de tentatives
- Affichage du nombre de parcours terminés à +22, +23 et +24
- Tableau détaillé des 1 000 simulations
- Musique de fond optionnelle

## Règles de forge

Le niveau initial est +11.

Les chances de réussite sont les suivantes :

| Niveau | Chance |
|---|---:|
| +11 | 120 % |
| +12 | 40 % |
| +13 | 70 % |
| +14 | 26 % |
| +15 | 24 % |
| +16 | 10 % |
| +17 | 14 % |
| +18 | 7 % |
| +19 | 2 % |
| +20 | 1 % |
| +21 | 1,6 % |

Les niveaux +22, +23 et +24 ne possèdent pas de chance supplémentaire : dès qu'un de ces niveaux est atteint, le parcours est terminé.

## Progression

Lorsqu'une amélioration réussit, l'équipement progresse aléatoirement de 1 à 3 niveaux.

Exemples :

```text
+19 → +20
+19 → +21
+19 → +22

+20 → +21
+20 → +22
+20 → +23

+21 → +22
+21 → +23
+21 → +24
```

Cela signifie qu'un équipement peut terminer son parcours à +22, +23 ou +24.

## Échecs

Une tentative coûte 50 argent.

En cas d'échec, 140 argent supplémentaires sont ajoutés.

Le coût total d'un échec est donc :

```text
50 argent
+ 140 argent
= 190 argent
```

Lors d'un échec, l'équipement peut perdre aléatoirement de 0 à 2 niveaux.

Le niveau minimum est +11.

Exemples :

```text
+18 → +18
+18 → +17
+18 → +16
```

Un échec compte comme une tentative.

## Baisses automatiques

Certaines progressions déclenchent automatiquement une baisse de niveau.

Les niveaux concernés sont :

```text
+12
+16
+19
```

Lorsqu'un de ces niveaux est atteint après une réussite, l'équipement redescend immédiatement de 1 niveau.

Cette baisse coûte 20 argent.

Elle ne compte pas comme une tentative.

Exemple :

```text
+11 → +13
```

Aucune baisse n'est appliquée puisque +12 n'a pas été atteint directement.

En revanche :

```text
+11 → +12
```

devient :

```text
+11 → +12 → +11
```

avec un coût supplémentaire de 20 argent.

## Coûts

| Événement | Coût |
|---|---:|
| Tentative | 50 argent |
| Échec | +140 argent |
| Échec complet | 190 argent |
| Baisse automatique | 20 argent |
| Baisse volontaire | 20 argent |

Conversion utilisée :

```text
1 or = 1 000 argent
```

## Compteurs

Le simulateur affiche en temps réel :

```text
Tentatives
Meilleur niveau
Coût total
Nombre d'échecs
```

Les baisses sont également comptabilisées dans les statistiques internes et dans les simulations.

Le bouton « Remettre le compteur à 0 » remet uniquement le nombre de tentatives à zéro.

Le bouton « Recommencer » réinitialise complètement le parcours :

```text
Niveau       → +11
Tentatives   → 0
Meilleur     → +11
Coût         → 0
Échecs       → 0
Baisses      → 0
```

## Simulation × 1 000

Le simulateur peut effectuer 1 000 parcours indépendants.

Chaque parcours :

```text
+11
 ↓
Tentatives successives
 ↓
Échecs / réussites / baisses
 ↓
+22, +23 ou +24
 ↓
Fin du parcours
```

Pour chaque parcours, le programme enregistre :

```text
Nombre de tentatives
Coût total
Nombre d'échecs
Nombre de baisses
Niveau final
```

La simulation calcule ensuite :

- nombre moyen de tentatives
- coût moyen
- nombre médian de tentatives
- coût médian
- minimum de tentatives
- maximum de tentatives
- nombre de parcours terminés à +22
- nombre de parcours terminés à +23
- nombre de parcours terminés à +24

## Installation

Le projet fonctionne directement dans un navigateur.

Aucune installation de serveur ou de dépendance n'est nécessaire.

Structure minimale :

```text
forge/
├── index.html
├── fond.webp
└── song.mp3
```

Ouvre simplement `index.html` dans un navigateur.

## Personnalisation

Les paramètres principaux sont regroupés dans le JavaScript.

### Chances

```javascript
const chances = {
  11: 120,
  12: 40,
  13: 70,
  14: 26,
  15: 24,
  16: 10,
  17: 14,
  18: 7,
  19: 2,
  20: 1,
  21: 1.6
};
```

### Coûts

```javascript
const A = 50;
const F = 140;
const D = 20;
```

Avec :

```text
A = coût d'une tentative
F = coût supplémentaire d'un échec
D = coût d'une baisse
```

### Niveaux

```javascript
const START_LEVEL = 11;
const STOP_LEVEL = 22;
const MAX_LEVEL = 24;
```

`STOP_LEVEL` définit le niveau à partir duquel un parcours est considéré comme terminé.

`MAX_LEVEL` définit le niveau maximal pouvant être obtenu lors d'une réussite.

## Technologie

Le projet utilise uniquement :

- HTML
- CSS
- JavaScript natif

Aucune bibliothèque JavaScript externe n'est nécessaire.

Les simulations sont exécutées directement dans le navigateur avec `Math.random()`.

## Licence

Projet personnel de simulation.

Libre à toi de modifier les règles, les chances, les coûts, l'interface et le nombre de simulations selon ton système de forge.
