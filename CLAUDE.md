# ImoD201 : T2 D201 en VEFA

Dossier de suivi de l'achat du lot **D201**, programme **Be Happy**, SCCV La Saulaie Îlot 4 (Eiffage Immobilier / Sogeprom, architectes Lambert Lénack), ZAC de la Saulaie, Oullins-Pierre-Bénite. L'acquéreur prépare un aménagement **brutaliste** (béton brut, béton ciré, aucune plinthe) avec un architecte, à négocier en **TMA** (travaux modificatifs acquéreur).

Répondre en français. Être factuel : distinguer ce qui vient d'un document, ce qui est mesuré sur le plan et ce qui est une hypothèse.

## Fichiers

| Chemin | Rôle |
|---|---|
| `D201.pdf` | Plan de vente du lot, A3, **indice 0 du 16/04/2026**. Raster seulement (pas de DWG). Seule source géométrique à ce jour. |
| `visite/index.html` | Application autonome : plan 2D coté (SVG), maquette 3D, visite à la première personne, rendu photo par lancer de rayons. Un seul fichier, three.js r180 via importmap jsdelivr. |
| `TMA.md` | Demandes de travaux modificatifs acquéreur, avec motif et incidence. |
| `visite/plan-d201.png` | Calque du plan promoteur (alpha), superposable au plan 2D, calé en mètres (x -0,2992, z -3,9019, 7,2901 × 13,0534 m). |

Dépôt public : https://github.com/vassilidev/appart, publié sur GitHub Pages : https://vassilidev.github.io/appart/ (la racine redirige vers `visite/`). `visite/index.html` est un document HTML complet ; pour le publier en Artifact claude.ai, retirer d'abord `<!doctype>`, `<html>`, `<head>` et `<body>`. `HISTORIQUE.md` tient le journal des demandes.

Tester en local : `cd visite && python3 -m http.server 8765`, puis `http://localhost:8765/`. Captures headless : puppeteer global, Chrome avec `--use-angle=metal --enable-gpu --ignore-gpu-blocklist` (GPU Apple M3 ; SwiftShader est 10 à 20 fois plus lent). En headless, l'affichage est limité à environ 1,5 image par seconde : pour le lancer de rayons, appeler `renderSample()` en boucle. Poignée de debug : `window.__d201`, état via `App.set(clé, valeur)`, visite via `App.goStop(id)`.

## Données du lot

### Plan de vente (D201.pdf)

| Pièce | Surface | Cotes intérieures |
|---|---|---|
| Séjour / Cuisine | 21,4 m² | 3,38 × 6,47 |
| Entrée + placard | 6,9 m² | entrée 2,90 × 1,22, dégagement 1,23, placard prof. 0,65 |
| Chambre | 12,5 m² | 2,80 × 4,46 |
| Salle de bain | 4,7 m² | 2,80 × 1,70 |
| WC | 2,4 m² | 1,60 × 1,53 |
| **Surface habitable** | **47,9 m²** | |
| Loggia (« balcon » au tableau) | 11,8 m² | ≈ 6,14 × 1,92 utiles |

- HSP 2,50 m. **Soffites ≈ 2,20 m** (hachures) : entrée, dégagement jusqu'à 0,65 m dans le séjour, salle de bain **sauf au-dessus de la baignoire** (2,50 m).
- Baignoire : ni paroi, ni barre de rideau, ni douchette dessinées.
- Baies : porte palière sur **coursive** extérieure (nord du plan), fenêtre sur allège (FA) 0,89 m dans l'entrée, PF séjour 1,64 m, PF chambre 1,63 m, toutes avec **BSO**. Aucun volet roulant.
- La salle de bain s'ouvre **sur la chambre**, pas sur le dégagement. Le WC s'ouvre sur le dégagement.
- Tableau électrique : dans le placard d'entrée (GTL côté dégagement). Gaines : angle nord-ouest de la cuisine, bloc entre WC et SdB.
- Équipements dessinés : baignoire 1,70, vasque 0,80, WC au sol, sèche-serviettes. Cuisine en L indicative : évier + LV au nord, LL / tri / cuisson / frigo à l'ouest. Emplacement LL aussi dessiné en pointillés dans le WC.
- Aucun radiateur dessiné.

### Comparateur Eiffage et notice (lecture partielle)

T2, 48 m², R+2, exposition annoncée **Est**, RE2020, livraison T4 2028. Notice : menuiseries bois ou alu double vitrage (2.4), BSO alu (2.5), équipements ménagers non prévus (2.9.1), 6 à 9 kW (2.9.3), chauffage collectif UTA YZENTIS France Air sur boucle d'eau tempérée, 19 °C / 21 °C SdB (2.9.4), pas de cave ni parking (3.1, 3.2), loggias non étanchées (3.3).

### Points ouverts

- **Orientation** : la boussole du plan met la loggia plein **sud**, le comparateur dit **est**. À faire trancher (coupes/façades).
- Diffusion du chauffage non précisée. Hypothèse : soufflage d'air via les soffites (UTA). À confirmer.
- Hauteurs d'allège et de linteau non cotées.
- Nature du vitrage de la FA d'entrée, sur coursive (clair, dépoli, feuilleté) : non précisée.
- Revêtements, références sanitaires, positions des prises : inconnus.

## Démarches

Documents à exiger (annexes obligatoires au contrat de réservation, art. R261-13 CCH) : plan coté DWG ou PDF vectoriel, notice descriptive complète contractuelle, coupes et façades du bâtiment D, surfaces habitable et utile détaillées, CCTP ou liste des prestations. Demander aussi la **procédure TMA** : date d'ouverture, périmètre, chiffrage.

Calendrier : démarrage du cloisonnement le **01/04/2028**, donc TMA à arbitrer et chiffrer **courant 2027**. Liste des demandes en cours : `TMA.md` (numérotation stable). Plinthes et revêtements : écartés des TMA à la demande de l'acquéreur (25/09/2026).

## Modèle 3D : conventions

- Repère en mètres : **x vers l'est** (droite du plan), **z vers le sud** (bas du plan), y vers le haut. Origine : angle intérieur nord-ouest du séjour. Sol fini y = 0, plafond 2,50.
- Relevé au pixel : sur le rendu 400 dpi du PDF, `x = (px − 1408,4) / 262`, `z = (py − 1782,3) / 262`. Précision ≈ ±2 cm. Les cotes affichées dans le plan 2D sont celles du promoteur.
- Toute la géométrie est dans `App.D` (script 1 de `visite/index.html`). La 3D et le plan 2D en dérivent : modifier les données, pas le dessin.
- Hypothèses du modèle : allège FA 1,00, linteau FA 2,15, PF 2,25, portes intérieures 2,04, porte palière 2,15, dalles 28 cm, contexte urbain schématique sans ombre portée (seul le bâtiment D porte ombre).
- Deux ambiances : « Livraison standard » (supposée : stratifié chêne, grès 45 × 45, faïence, plinthes) et « Brutaliste » (projet de l'acquéreur).
- La visite montre uniquement le projet de l'acquéreur : aménagement « mon projet » (porte de chambre en TMA-01), finitions béton, déco vivante. Ces trois choix sont figés, les boutons ont été retirés à sa demande (25/09/2026). Options restantes : bureau (chambre ou séjour), salle de bain (baignoire ou douche extra-plate, TMA-07), meublé ou vide, vitrage de la FA (clair ou dépoli). Données 2D dans `D.projet`, 3D dans `buildProjet`, `buildDeco`, `buildBathOptions`.

## Programme de l'acquéreur (25/09/2026)

Vit seul, peut-être à deux plus tard. Veut cuisiner souvent : cuisine complète avec lave-vaisselle, four et micro-ondes. Bureau assis-debout et fauteuil confortable, de préférence dans la chambre. Table ronde plutôt que carrée. Lave-linge quelque part (WC retenu). Loggia agréable à vivre. Porte de chambre à inverser. Déco vivante, colorée, avec des plantes et des fleurs, pas « tout blanc Ikea ». Plinthes et revêtements : pas de TMA.

