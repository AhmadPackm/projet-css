# Respawn Expo

Site vitrine d'un salon du jeu vidéo fictif (13–14 mars 2027, Lens). Projet du module CSS avancé.

- **Auteur** : AIT AMY Ahmad
- **Dépôt** : https://github.com/AhmadPackm/projet-css
- **Convention de nommage** : BEM (`.bloc__element--variante`), utilitaires préfixés `u-`

## Localisation des exigences et choix techniques

| Exigence | Élément | Fichier:ligne | Pourquoi |
|---|---|---|---|
| 1. Architecture | Ordre des `@layer` | `css/main.css:14` | Déclaré une seule fois avant les `@import` : l'ordre des layers règle les conflits, donc aucun `!important`. |
| 1. Architecture | Tokens primitifs | `css/tokens.css:16` | Palette, espacements, rayons, durées : les valeurs brutes, jamais utilisées directement dans les composants. |
| 1. Architecture | Tokens sémantiques | `css/tokens.css:65` | Rôles (`--color-surface`, `--color-accent`…) : changer de thème = changer ces tokens, pas les composants. |
| 1. Architecture | Nesting natif | `css/components.css:300` | Un composant = un bloc, 3 niveaux max, avec `@media` et `@container` imbriqués pour garder tout au même endroit. |
| 2. Mise en page | `grid-template-areas` | `css/layout.css:99` | Programme : jours empilés en mobile, côte à côte en desktop en ne changeant que les zones. Aussi le hero et la FAQ. |
| 2. Mise en page | `subgrid` | `css/layout.css:175` | Les cartes partagent les lignes de la grille : images, noms, bios et liens restent alignés malgré des bios de longueurs différentes. |
| 2. Mise en page | Flexbox | `css/layout.css:50` | Pour les éléments sur un seul axe (en-tête, navigation, boutons) avec `gap` et `flex-wrap`. Grid pour le 2D. |
| 3. Responsive | Media query mobile-first | `css/layout.css:78` | Styles de base pensés pour 320 px, puis `width >= 48rem` et `64rem` pour élargir. |
| 3. Responsive | Typographie fluide `clamp()` | `css/tokens.css:90` | Toute l'échelle typographique est fluide et rangée dans les tokens. |
| 3. Responsive | Container query | `css/components.css:336` | La carte passe à l'horizontale si son conteneur dépasse 36rem. Deux contextes : bandeau invitée d'honneur (`css/layout.css:157`) et encart contact de la FAQ (`css/layout.css:216`). Pas de conteneur sur la grille des cartes, car `container-type` désactive le `subgrid`. |
| 3. Responsive | 320 px sans défilement | `css/layout.css:166` | `min(100%, 15rem)` empêche une colonne de dépasser l'écran ; images fluides et `overflow-wrap` dans le reset. |
| 4. Sélecteurs | `:has()` | `css/components.css:416` | L'offre qui contient un badge est mise en avant toute seule, sans classe en plus. |
| 4. Sélecteurs | `:is()` / `:where()` | `css/base.css:31` | `:where()` a une spécificité nulle : les styles de base des titres sont faciles à surcharger. |
| 5. Thème | `light-dark()` + `color-scheme` | `css/tokens.css:69` | Le thème suit le système ; chaque couleur sémantique a sa version claire et sombre. |
| 5. Thème (bonus) | Bascule CSS-only | `css/tokens.css:126` | La case à cocher inverse le thème en changeant `color-scheme`, sans JavaScript. |
| 6. Animations | Transition 1 | `css/components.css:151` | Boutons qui se soulèvent au survol (`translate`, peu coûteux). |
| 6. Animations | Transition 2 | `css/components.css:526` | Icône « + » de la FAQ qui tourne à l'ouverture. |
| 6. Animations | `@keyframes` | `css/components.css:588` | Apparition du titre, « Insert coin » qui clignote 4 fois seulement, réponse de FAQ qui glisse. |
| 6. Animations | `prefers-reduced-motion` | `css/components.css:117` | Tout mouvement est écrit dans `no-preference` : rien ne bouge si l'utilisateur l'a demandé, et rien ne reste invisible. |
| 6. Animations (bonus) | Animation au scroll | `css/components.css:621` | Dans `@supports` : sous Firefox, les éléments s'affichent simplement normalement. |
| 7. Accessibilité | Landmarks et titres | `index.html:25` | `header`, `nav`, `main`, `aside`, `footer`, un seul `h1`, lien d'évitement, FAQ en `<details>`. |
| 7. Accessibilité | `:focus-visible` | `css/base.css:73` | Contour vert de 3 px sur tous les éléments interactifs. |
| 7. Accessibilité | Contrastes AA | `css/tokens.css:72` | Texte 16,9:1 (clair) et 18:1 (sombre), accent 6,3:1 et 6,8:1. |
| 7. Accessibilité | Images avec `alt` | `index.html:148` | `alt` descriptif sur les portraits, `alt=""` sur la manette décorative. |
| 8. Qualité | `!important` | — | Aucun. |

## Autres choix

- **Identité visuelle** : univers « arcade » (police pixel, néons rose et cyan, ombres décalées) pour coller au thème jeu vidéo.
- **Une seule police externe** (Pixelify Sans pour les titres), police système pour le texte : plus léger et plus lisible.
- **Images en SVG pixel art** : très légères, nettes à toutes les tailles, pas de droits à gérer.
- **Aucun JavaScript** : FAQ en `<details>`, bascule de thème en `:has()`.

## Validateur W3C

Avertissements possibles sur les syntaxes récentes (nesting, `light-dark()`, `@container`, `subgrid`, `text-wrap`, `animation-timeline`) : elles sont valides et supportées par les navigateurs récents.

## Utilisation de l'IA

Claude (Anthropic) a été utilisé pour générer une première version du code HTML/CSS, des textes fictifs et des illustrations SVG, ainsi que pour vérifier les contrastes et le rendu à 320, 800 et 1440 px.

## Crédits

- Police Pixelify Sans (Google Fonts, licence SIL OFL)
- Illustrations pixel art SVG créées pour le projet
