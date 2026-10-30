# Diagnostic noté et grille de revue

Ouvrir aux étapes 1 (upgrade), 6 et 7. Barème inspiré d'Awwwards : Design 40 %, Usability 30 %, Creativity 20 %, Content 10 % ; une mention honorable commence vers 6,5/10.

## Volets (un sous-agent par volet si possible, lecture seule)

| Volet | Comment | Sortie |
|---|---|---|
| Design system | lire tokens (`@theme`, `:root`), composants, charte | cohérent / partiel / absent, écarts à la charte |
| Motion existant | chercher `gsap`, `motion`, `framer-motion`, `@keyframes`, `animation-timeline`, `transition`, `three`, `lenis` | niveau 0-3 atteint, techniques, nombre de courbes d'easing |
| Accessibilité | skill a11y si installé, sinon `npx @axe-core/cli <url>` | violations WCAG 2.2 AA par sévérité |
| Rendu réel | navigateur intégré, sinon Playwright | captures 320, 768, 1024, 1440 px ; erreurs console |
| Performance | [PageSpeed Insights](https://pagespeed.web.dev/) si URL publique, sinon Lighthouse mobile | LCP, INP (TBT en labo), CLS |
| SEO de base | title, meta description, h1 unique, alt, Open Graph | manques par page |

Sans URL déployée : lancer le serveur de développement du projet (commande du `package.json`) et mesurer en local, en le précisant. Impossible de démarrer → « non mesuré ».

## Grille

| Dimension | Note /10 | Cible | Preuve |
|---|---|---|---|
| Design (direction, typo, couleur, mise en page) | | 8 | |
| Usability (navigation, mobile, accessibilité) | | 8 | |
| Creativity (interactions, récit, moment mémorable) | | 8 | |
| Content (textes, cohérence de marque) | | 8 | |
| Motion et micro-interactions | | 7 | |
| Responsive | | 9 | |
| Performance | | 9 | |
| SEO | | 8 | |

Note estimée = 0,4 × Design + 0,3 × Usability + 0,2 × Creativity + 0,1 × Content ; les quatre dernières lignes sont des planchers techniques. Chaque note cite sa preuve (sortie d'audit, capture, mesure). Ensuite : les écarts majeurs avec leur impact, et les pages à transformer (page, priorité, complexité, technique principale).

## Étalonnage

| Note | Ce qu'on voit |
|---|---|
| 4 | Thème par défaut du framework, contenu provisoire, rien de propre au sujet |
| 6 | Propre et cohérent, mais interchangeable avec un autre site du secteur |
| 8 | Direction identifiable, un moment mémorable, finitions tenues sur toutes les largeurs |
| 10 | Niveau « Site of the Day » : idée forte et exécution sans défaut mesurable |

Motion : noter le niveau atteint sur l'échelle 0-3 de [motion.md](motion.md), quelle que soit la technique, puis sa qualité.

## Signes d'un graphisme générique, à corriger en priorité

- Palette et typographie par défaut du framework ; dégradé violet, texte en dégradé, panneaux en verre sans raison.
- Hero « titre centré + deux boutons + capture » sans élément propre au sujet.
- Tout apparaît en fondu au scroll ; même durée et même easing partout.
- Cartes identiques en grille pour chaque section ; aucune variation de rythme.
- Icônes décoratives à la place de vrais visuels ; fausses captures ; chiffres inventés.
- Emojis dans l'interface.
