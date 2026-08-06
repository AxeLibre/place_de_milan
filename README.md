# Place de Milan — Atelier volumétrique

Outil web léger et gratuit pour proposer des scénarios d'urbanisme sur l'îlot
« place de Milan » (nord de la sortie ouest de Part-Dieu, Lyon). Chacun peut
dessiner des emprises de bâtiments, régler leur nombre d'étages, répartir les
usages par tranche (résidentiel / bureaux / commerces / hôtel / services) et
exporter une image de sa proposition — ou le fichier de projet pour que
d'autres le reprennent.

Aucun serveur, aucune base de données : tout tourne dans le navigateur
(Three.js chargé depuis un CDN). Le site se déploie tel quel sur GitHub Pages.

## Déploiement sur GitHub Pages

1. Créez un nouveau dépôt GitHub (public), par ex. `place-de-milan-3d`.
2. Déposez `index.html` à la racine du dépôt (glisser-déposer sur GitHub,
   ou en ligne de commande) :
   ```bash
   git init
   git add index.html README.md
   git commit -m "Atelier volumétrique — place de Milan"
   git branch -M main
   git remote add origin https://github.com/<votre-compte>/place-de-milan-3d.git
   git push -u origin main
   ```
3. Dans le dépôt GitHub : **Settings → Pages → Build and deployment →
   Source : Deploy from a branch**, branche `main`, dossier `/ (root)`.
   Enregistrez.
4. Au bout d'une à deux minutes, le site est accessible à l'adresse indiquée
   (généralement `https://<votre-compte>.github.io/place-de-milan-3d/`).
   Vous pouvez partager ce lien directement sur le fil SkyscraperCity.

Aucune étape de build n'est nécessaire : c'est un unique fichier HTML
autonome qui charge Three.js via CDN (`unpkg.com`) et deux polices Google
Fonts. Si votre dépôt doit fonctionner totalement hors-ligne, il faudra
héberger ces dépendances localement (voir « Aller plus loin » ci-dessous).

## Utilisation

- **+ Nouveau bâtiment** : passe en mode dessin. Cliquez sur le sol pour
  poser les sommets de l'emprise au sol du bâtiment (polygone quelconque,
  pas nécessairement rectangulaire), puis validez avec **Entrée**
  (**Échap** annule).
- Le bâtiment créé apparaît dans le panneau de droite. Vous pouvez :
  - renommer le bâtiment,
  - régler son **nombre d'étages**,
  - définir plusieurs **tranches d'usage** (« de l'étage X à l'étage Y →
    tel usage »), pour un socle commercial, des bureaux en milieu de tour
    et des logements en partie haute par exemple.
- **Fond de plan** : permet de charger une image (plan cadastral,
  capture Géoportail/Google Maps, photo aérienne...) projetée au sol.
  Un petit outil de calibration demande ensuite de cliquer deux points
  dont vous connaissez la distance réelle (ex. deux angles de rue) et de
  saisir cette distance en mètres, pour que l'échelle du plan corresponde
  à l'échelle des bâtiments (1 unité 3D = 1 mètre).
- **Grille** : affiche/masque le quadrillage de sol et le contour
  schématique indicatif de l'îlot (positionné approximativement — à
  recaler via votre propre fond de plan calibré pour plus de précision).
- **Exporter l'image (PNG)** : capture le rendu 3D actuel tel qu'affiché
  à l'écran (orientez la caméra avant d'exporter).
- **Sauver le projet / Charger** : exporte ou importe un fichier `.json`
  décrivant l'ensemble des bâtiments (emprises, étages, usages). Pratique
  pour partager une proposition modifiable avec d'autres forumeurs, ou pour
  repartir d'une proposition existante et la faire évoluer.

Un bâtiment d'exemple est chargé au démarrage à titre d'illustration —
supprimez-le (« Supprimer » dans sa fiche) pour repartir d'une page blanche.

## Notes de précision

- Le contour en pointillés orangés et l'emprise par défaut de la grille
  sont **purement indicatifs** : je n'avais pas de relevé cadastral fiable
  de l'îlot à intégrer par défaut. Pour un rendu fidèle, chargez une vraie
  capture de plan (Géoportail, cadastre.gouv.fr, Google Maps en vue
  aérienne) via « Fond de plan » et calibrez-la avec deux points de
  repère dont vous connaissez la distance réelle.
- La hauteur d'étage est fixée à 3 m (modifiable dans le code,
  constante `FLOOR_HEIGHT` en tête du `<script>`).

## Aller plus loin (pistes d'évolution)

- Fond de plan par défaut intégré (image du cadastre commitée dans le
  dépôt) pour éviter à chaque utilisateur de recharger/recalibrer.
- Export/partage de proposition via URL (encodage du JSON en paramètre
  d'URL ou en `localStorage` + bouton « copier le lien »).
- Bibliothèque de gabarits de bâtiments (immeuble haussmannien, tour,
  barre) pour démarrer plus vite.
- Cotation automatique (hauteur totale, SDP approximative par usage).
- Hébergement local de Three.js et des polices si un fonctionnement
  strictement hors-ligne est nécessaire.
