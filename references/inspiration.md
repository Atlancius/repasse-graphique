# Chercher des références (Scrolltide et 21st.dev)

Ouvrir à l'étape 3, et avant toute animation signature à l'étape 6. Aucun design ne part de la moyenne du modèle : on regarde de vraies réalisations, puis on fixe ses décisions en valeurs.

## Sources

| Source | Quoi | Pour |
|---|---|---|
| [scrolltide.co/templates](https://www.scrolltide.co/templates) | sites complets : hero, landing, 3D, sections | direction d'ensemble, hero, rythme de scroll |
| [scrolltide.co/components](https://www.scrolltide.co/components) | carrousels, galeries, reveals, boutons, loaders | une interaction signature |
| [scrolltide.co/sections](https://www.scrolltide.co/sections) | sections prêtes | rythme d'une page |
| [scrolltide.co/ui](https://www.scrolltide.co/ui) | écrans d'app et dashboards | UI produit |
| [scrolltide.co/shaders](https://www.scrolltide.co/shaders) | fonds animés WebGL | fond, texture, ambiance |
| [21st.dev](https://21st.dev/) | composants React + Tailwind de la communauté | brique précise : nav, pricing, texte animé, formulaire |

Compléments utiles si le besoin dépasse ces deux catalogues : [Awwwards](https://www.awwwards.com/websites/) (sites primés, filtrer par catégorie), [Godly](https://godly.website/), [Land-book](https://land-book.com/).

## Méthode

1. **Chercher** : un ou deux mots-clés, en anglais d'abord (`hero`, `video-hero`, `particles`, `shader`, `carousel`, `text-reveal`, `pricing`, `bento`, `marquee`, `parallax`, `3d`). Navigateur intégré de l'outil ou recherche web ; sur 21st.dev, la recherche du site, ou l'outil MCP `search` / `get_inspiration` si le MCP 21st.dev est branché.
2. **Retenir 2 à 4 références**, au plus une par rôle : direction d'ensemble, hero, interaction signature, brique UI.
3. **Extraire les décisions en valeurs** en regardant l'aperçu (et le code quand il est public) : palette (HEX, pipette du navigateur), polices et échelle, grille et largeur de texte, courbe d'easing et durées, déclencheurs (scroll ou chargement), ce que la référence s'interdit.
4. **Adapter à la marque** : la référence donne la mécanique et le niveau d'exigence, jamais le contenu, les noms, le logo ni la palette d'un tiers.
5. **Tracer** dans `.repasse/etat.md` : URL retenues, ce qui est repris, ce qui est écarté et pourquoi.

Regarder, décrire, reconstruire : jamais aspirer un catalogue ni copier un site entier.

## Licences

- **Scrolltide** : les aperçus sont publics ; les prompts et le code sont payants et non redistribuables. Sans abonnement, on s'inspire de l'aperçu et on reconstruit soi-même. Avec un abonnement, le code reste dans le projet de l'abonné : jamais dans un dépôt public ni un livrable partagé.
- **21st.dev** : recherche libre ; le code d'un composant suit la licence de son auteur. Garder un lien vers la page d'origine en commentaire. Pas de scraping ni de republication du catalogue.
- Toute autre source : vérifier la licence avant de reprendre du code ; une capture ou une police payante ne se réutilise pas sans droit.
