# appart : visite du T2 D201

Visite 3D, plan 2D et galerie photo d'un T2 de 47,9 m² en VEFA : programme Be Happy, ZAC de la Saulaie, Oullins-Pierre-Bénite, livraison prévue fin 2028.

**Voir la visite : https://vassilidev.github.io/appart/**

## Contenu

| Chemin | Rôle |
|---|---|
| `visite/index.html` | L'application : galerie d'accueil, plan 2D coté, maquette 3D, visite à la première personne, rendu photo par lancer de rayons. Un seul fichier ; three.js est chargé depuis jsdelivr. |
| `visite/photos/` | Photos de la galerie, dans chaque configuration (bureau, salle de bain, meublé ou vide). |
| `visite/plan-d201.png` | Calque du plan de vente, superposable au plan 2D. |
| `D201.pdf` | Plan de vente du lot, indice 0 du 16/04/2026. |
| `TMA.md` | Demandes de travaux modificatifs acquéreur, avec motif et incidence. |
| `CLAUDE.md` | Données du lot, points ouverts, conventions du modèle. |
| `HISTORIQUE.md` | Journal des demandes et des décisions. |

## Lancer en local

```
cd visite && python3 -m http.server 8765
```

puis ouvrir http://localhost:8765/.

Les images et l'aménagement sont indicatifs et non contractuels. Les cotes sont relevées sur le plan de vente raster (précision d'environ 2 cm).
