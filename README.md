# Diagramme N–Z des noyaux

Page HTML unique (sans dépendance, sans build) affichant la table des nucléides : neutrons **N** en abscisse, protons **Z** en ordonnée. Une case par noyau, déplaçable et zoomable au doigt ou à la souris.

## Utilisation

Aller sur le site : 
> https://stackoverflow-dev.github.io/nz-table/

### Navigation
- **Mobile** : un doigt pour déplacer (avec inertie), pincement pour zoomer, double-tap pour zoomer ×2.
- **Bureau** : glisser pour déplacer, molette pour zoomer.
- Boutons **+**, **−** et **cadrer** en bas à droite.
- Un tap/clic sur une case ouvre la fiche du noyau (Z, N, A, demi-vie, désintégrations, noyau fils).

### Recherche
| Saisie | Effet |
|---|---|
| `Cs-137`, `137Cs`, `cs137` | un isotope précis |
| `césium`, `U`, `uranium 238` | un élément (symbole ou nom français), éventuellement avec A |
| `Z=82`, `N=50-60`, `A>200` | filtre numérique (`=`, `>`, `<`, `>=`, `<=`, intervalle `a-b`) |
| `137` | tous les noyaux de nombre de masse 137 |

Les termes se combinent (ET). Entrée cadre la vue sur les résultats.

### Filtres
- Pastilles : **Stables**, **Radioactifs**, **β⁻**, **β⁺ / CE**, **α**, **Fission**.
- Bouton **Filtres** : intervalles A / Z / N, demi-vie, nombres magiques (2, 8, 20, 28, 50, 82, 126).

Les noyaux qui ne correspondent pas sont grisés. Le compteur en haut à droite indique le nombre de résultats.

## Lecture du diagramme

| Couleur | Mode principal |
|---|---|
| Noir / blanc (selon le thème) | stable |
| Bleu | β⁻ |
| Rouge | β⁺ / capture électronique |
| Jaune | α |
| Vert | fission spontanée |

Le coin inférieur droit d'une case indique un mode secondaire. Thème clair/sombre automatique.

## Données

- Source : jeu de données du paquet Python [`radioactivedecay`](https://pypi.org/project/radioactivedecay/) 0.6.1 (ICRP-107, AME2020 / NUBASE2020).
- Embarquées en JSON compact dans le fichier : ~1250 noyaux à l'état fondamental, dont 259 stables.
- Pour chaque noyau : Z, A, demi-vie (secondes, `-1` = stable), modes de désintégration avec leur pourcentage.

## Limites

- Z = 1 à 100 (jusqu'au fermium) : les éléments plus lourds sont absents.
- Les noyaux très éphémères et les états isomères ne sont pas représentés.
- La fiche affiche le noyau fils direct, sans chaîne de filiation.

## Structure du fichier

- `DATA` : tableau `[Z, A, demi-vie_s, "mode:%|mode:%"]`.
- Rendu sur `<canvas>` (pan/zoom par Pointer Events), interface en HTML/CSS natif.
- Modes : `B-` β⁻, `B+` β⁺/CE, `EC` capture électronique, `A` α, `SF` fission spontanée.
