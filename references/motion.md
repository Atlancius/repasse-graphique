# Animation : niveaux, outils et règles

Ouvrir aux étapes 2, 4 et avant la première animation de l'étape 6.

## Niveau d'animation

| Niveau | Ce qu'on fait |
|---|---|
| 0 Sobre | Micro-interactions et états (survol, focus, chargement) ; aucune animation au scroll |
| 1 Vivant | Révélations CSS au scroll, entrée du hero, transitions de composants |
| 2 Expressif | Une séquence orchestrée par page (GSAP), texte découpé, parallaxe d'un calque, transition de page |
| 3 Cinématique | Pin et scrub, séquence d'images pilotée par le scroll, shader ou 3D, curseur custom ; desktop seulement, repli mobile |

Le niveau est un plafond, pas un quota d'effets. Chaque effet garde un pourquoi lié au récit ; un niveau 3 se mérite par des performances mesurées sur mobile.

## Traduire les mots vagues

« Premium », « époustouflant », « niveau agence » ne sont pas des critères. Les traduire en décisions visibles :

- un objet principal qui traverse la page ;
- trois transformations mémorables au plus, reliées au message ;
- une typographie maîtrisée (deux familles, une échelle) ;
- une palette stable avec un seul accent qui raconte ;
- un vrai travail de profondeur (calques, ombres, lumière) ;
- une signature de marque réellement animée, qui finit nette et lisible.

## Quel outil pour quoi

- **CSS d'abord** : survol, focus, toast, skeleton, marquee, révélation au scroll par `animation-timeline: view()` sous `@supports`. Zéro JS.
- **GSAP + ScrollTrigger** : timeline, stagger orchestré, pin, scrub, SplitText. Sites vitrines et de marque.
- **Motion** (`motion/react`) : gestes, layout, sorties d'éléments dans une app React (dashboards).
- **Lenis** (smooth scroll) : desktop seulement, chargé dynamiquement, coupé sous 768 px et en mouvement réduit.
- **3D** : React Three Fiber + drei, ou Spline ; chargé côté client en import dynamique, jamais dans le bundle initial d'une page publique sans mesurer le LCP mobile.
- **Compteur** : `requestAnimationFrame` sur une valeur finale déjà rendue côté serveur.

## Faire

- Avant une animation signature : une référence de même mécanique ([inspiration.md](inspiration.md)), reprise en valeurs (easing, durées, déclencheurs).
- React + GSAP : `useGSAP(() => …, { scope: ref })` de `@gsap/react` dans un composant client ; `gsap.registerPlugin(useGSAP, ScrollTrigger)` une seule fois dans un module partagé.
- Mouvement réduit : `gsap.matchMedia()` avec `(prefers-reduced-motion: reduce)`, ou retour anticipé ; le contenu reste visible dans son état final.
- Animer seulement `transform`, `opacity`, `filter`.
- Effet lourd (canvas, 3D, shader) derrière une garde : ≥ 768 px, pointeur fin, pas de mouvement réduit, image statique en repli, montage après le premier affichage.
- Texte découpé lettre par lettre : garder une copie lisible (`sr-only`) et marquer la version découpée `aria-hidden`.
- Durées et easings dans des tokens (`lib/animation-tokens.ts` : `duration`, `ease`, `stagger`), une courbe d'easing accordée à la marque.
- Une seule séquence orchestrée par page.

## Ne jamais

- Smooth scroll (Lenis ou maison) sans le relier à ScrollTrigger (`lenis.on('scroll', ScrollTrigger.update)` + `gsap.ticker`) : sections figées à `opacity: 0`.
- Smooth scroll JS sur mobile : le défilement natif suffit et le JS charge le thread principal.
- `opacity: 0` initial sur un contenu dont l'animation peut ne pas jouer : masquer seulement sous `@supports (animation-timeline: view())` et `prefers-reduced-motion: no-preference`.
- Un `IntersectionObserver` par section quand le CSS suffit.
- Animer `width`, `height`, `top`, `left`, `margin`, `padding` ; `transition: all` ; minuter par `setTimeout` ; CSS et GSAP sur la même propriété.
- Même durée et même fondu partout.
