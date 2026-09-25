# Historique du projet D201

Journal des demandes de l'acquéreur et des décisions prises, dans l'ordre. Session de travail du 25/09/2026 avec Claude Code. Le dossier n'était pas versionné avant la création du dépôt : ce fichier sert d'historique.

## Point de départ

- Documents disponibles : le plan de vente du lot (`D201.pdf`, indice 0 du 16/04/2026), les données du comparateur Eiffage (T2, 48 m², R+2, exposition annoncée Est, RE2020, livraison T4 2028) et une lecture partielle de la notice (menuiseries, BSO, équipements ménagers non prévus, chauffage collectif YZENTIS, pas de cave ni de parking, loggias non étanchées).
- Demande initiale : modéliser le logement en 3D réaliste et fidèle, le voir en 2D, en 3D et s'y promener. Créer un fichier de contexte (CLAUDE.md) et une mémoire.

## Relevé du plan

- Plan rendu à 400 dpi, cotes relevées au pixel (262 px/m) et recoupées avec les cotes et le tableau des surfaces du promoteur. Écart relevé < 2 cm.
- Données : séjour/cuisine 21,4 m², entrée + placard 6,9 m², chambre 12,5 m², salle de bain 4,7 m², WC 2,4 m², loggia 11,8 m². HSP 2,50 m, soffites à 2,20 m (entrée, dégagement, salle de bain hors baignoire).
- Écart repéré : la boussole du plan met la loggia au sud, le comparateur dit est. Réglage « Loggia : au sud / à l'est » pour comparer l'ensoleillement.
- Question de l'acquéreur sur une fenêtre dans le WC : c'est « LL » (emplacement lave-linge) écrit à la verticale, pas une fenêtre. Le WC et la salle de bain sont des pièces aveugles.
- Question sur les hachures : ce sont des soffites (faux plafonds à 2,20 m qui cachent les gaines), pas un revêtement de sol.

## Visite 3D, première version

- Application en un seul fichier (`visite/index.html`) : plan 2D vectoriel coté, maquette 3D, visite à la première personne, rendu photo par lancer de rayons, soleil calculé pour Lyon selon la date et l'heure, BSO orientables, deux finitions.
- Audit par 5 agents indépendants (géométrie, interactions, réalisme, code, ergonomie), environ 70 constats appliqués : portes à 82 cm de passage, tableau électrique côté dégagement, placard de 1,31 m, fenêtre d'entrée au nu intérieur (pas de tablette), cuisine en modules de 60, cloison SdB de 7 cm, bugs d'interface, lumières des lampes qui traversaient les cloisons, béton et parquet plus justes.

## Programme d'aménagement de l'acquéreur

- Vit seul, peut-être à deux plus tard. Cuisine complète (lave-vaisselle, four, micro-ondes). Table ronde plutôt que carrée. Lave-linge quelque part. Loggia agréable à vivre.
- Porte de chambre : ouverte vers la chambre, elle masquait la porte de la salle de bain. Inversée vers le séjour, paumelles côté nord, ouverture à 180° : **TMA-01**.
- Lave-linge : d'abord un modèle top 40 cm dans le WC, puis, à la demande de l'acquéreur, un frontal 60 × 60 : **TMA-02**.
- Attentes électriques de la cuisine (**TMA-03**), prises du bureau et des chevets (**TMA-04**), prise extérieure sur la loggia (**TMA-05**).
- Plinthes et revêtements : TMA **retirée** à la demande de l'acquéreur.
- Entrée : banc sous la fenêtre, patères, porte de placard miroir, applique. Vitrage de la fenêtre sur coursive non précisé : option clair ou dépoli.
- Salle de bain : le plan ne prévoit ni paroi ni barre de rideau. Paroi fixe côté robinetterie, renfort dans la cloison (**TMA-06**). Option douche extra-plate de 3 cm à la place de la baignoire (**TMA-07**), entrée centrale pour ne pas buter sur la vasque. Panier à linge.
- Bureau assis-debout : d'abord petit, puis grand bureau pour 2 écrans et une tour. Deux variantes : au séjour à la place du canapé (par défaut, téléviseur fixé au-dessus des écrans, canapé contre la cloison face au bureau) ou dans la chambre à la place du dressing (penderie reportée au mur sud, lit reculé).
- Déco : d'abord « béton », puis demande d'une déco vivante (plantes, fleurs, couleurs, affiches, pas « tout blanc Ikea »), puis **murs peints propres sans béton**. Les réglages Scénario, Finitions et Déco ont été retirés : le projet est figé. Restent Bureau, Bain, Meublé/Vide.
- Dégagement rendu plus joyeux : galerie de cadres sur tablette, tapis, plafonnier ambré, porte d'entrée peinte en terracotta côté intérieur.
- Table rapprochée de la cuisine, en Ø 80, pour dégager la porte de chambre et garder 1 m devant les plans de travail.
- WC : dérouleur, rouleaux de réserve, balayette.

## Qualité et navigation

- Lumière d'ambiance captée pièce par pièce (cubemap, rebonds successifs, harmoniques sphériques) et mélangée en continu aux portes et aux baies, pour supprimer les sauts de lumière entre pièces signalés par l'acquéreur. Exposition automatique continue.
- Vrais miroirs (réflexion plane) dans la salle de bain et sur la porte du placard.
- Navigation : clic au sol avec calcul d'itinéraire (grille de 8 cm, A*), qui contourne chaises et meubles et ouvre les portes sur le trajet. Visite guidée animée de pièce en pièce. Sensibilité mobile réduite.
- Performances : ombres recalculées seulement quand la scène change, miroir allégé, sélection limitée au logement.
- Deuxième vérification par 3 agents (dégagements, fonctions, rendu), constats appliqués : chaise rangée sous le bureau en chambre, pare-baignoire de 70 cm, butées de portes, porte du WC fermée par défaut, meubles de loggia recalés.

## Galerie et publication

- Page d'accueil façon annonce d'agence : galerie photo avec filtres (bureau séjour ou chambre, baignoire ou douche, meublé ou vide), puis bouton « Lancer la visite 3D ».
- Photos calculées en rendu temps réel suréchantillonné (le lancer de rayons, plus réaliste, coûte environ une seconde par passe sur cette scène).
- Publication demandée sur GitHub Pages, dépôt public `vassilidev/appart`, avec tout l'historique et toutes les informations.
