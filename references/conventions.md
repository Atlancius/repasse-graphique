# Conventions UI et design system

Ouvrir à l'étape 4 et avant le premier composant de l'étape 6. Écrit pour React (Next.js, TanStack Start, Vite) + Tailwind v4 ; si le projet utilise autre chose, garder ses conventions et appliquer l'esprit (tokens, composants nommés, aucune valeur en dur).

## Tokens

1. **Primitifs** dans `@theme` (CSS Tailwind v4) : couleurs de la charte en HEX, échelle d'espacement, rayons, familles de polices (`--font-display`, `--font-sans`, `--font-mono`).
2. **Sémantiques** dans `:root` : `--background`, `--surface`, `--foreground`, `--foreground-muted`, `--primary` / `--primary-foreground`, `--accent`, `--border`, `--ring`, qui référencent les primitifs. Variables qui en référencent d'autres : `@theme inline` (convention shadcn).
3. **Composant** si nécessaire : `--button-bg`, `--card-bg`… dérivés des sémantiques.
4. **Animation** : `lib/animation-tokens.ts` (`duration`, `ease`, `stagger` en `as const`).
5. **Mode sombre** : mêmes tokens redéfinis sous `.dark` (ou `@custom-variant dark`). App SaaS : clair et sombre. Site de marque : selon sa direction (sombre d'abord permis).
6. Projet Tailwind v3 avec `tailwind.config` : y mettre les tokens, ne pas migrer sans accord.

Projet sans tokens : poser primary, secondary, accent, background, foreground, muted, border **avant** le premier composant.

## Composants

| Niveau | Exemples | Emplacement |
|---|---|---|
| Atomes, molécules | Button, Input, Card, FormField | `components/ui/` |
| Organismes | Navbar, Hero, Footer | `components/sections/` |
| Gabarits | PageLayout | `components/layouts/` |

Chaque composant : export nommé, interface de props, prop `className`, variants `cva` + `cn()` (clsx + tailwind-merge) sur tokens sémantiques uniquement, accessible, responsive mobile-first, mode sombre.

## Faire

- Mobile-first, vérifié à 320, 768, 1024 et 1440 px.
- Polices chargées proprement (`next/font` ou fichiers auto-hébergés, `font-display: swap`) ; deux familles au plus, plus une mono si utile.
- Icônes d'une seule bibliothèque (Lucide par défaut).
- Images avec dimensions explicites (pas de CLS), format moderne (AVIF/WebP), `loading="lazy"` sauf l'image du hero.
- Chaque route a un état de chargement qui reproduit le vrai layout (skeleton).
- Un fait métier (prix, horaires, coordonnées) dans une constante unique, importée partout.
- Contraste texte/fond ≥ 4,5:1, focus visible sur tout élément interactif.

## Ne jamais

- Couleur ou taille arbitraire (`bg-[#1a2b3c]`, `text-[14px]`, `style={{ color }}`) : token ou échelle Tailwind.
- `<div onClick>` : `<button>` ou `<a>`.
- Emoji dans l'interface.
- Dégradé, texte en dégradé ou effet verre sans raison donnée par la direction.
- Thème basculé côté client après l'hydratation (flash et LCP dégradé) : décider le thème au rendu serveur ou par un script en tête de page.
- `Date.now()` ou `Math.random()` dans le rendu d'un composant hydraté : erreur d'hydratation.
- Faux contenus : chiffres, logos clients, témoignages ou captures inventés.
