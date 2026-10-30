---
name: repasse-graphique
description: "Repasse graphique, up graphique, refonte visuelle, site sans design, niveau Awwwards : donne à un site ou une app web un graphisme de premier plan, de la compréhension du produit au code vérifié, à partir de références réelles (Scrolltide, 21st.dev). Utiliser pour créer ou relever le design d'un site existant."
argument-hint: "[-a] [-r] [--mode creation|upgrade] [--niveau 0|1|2|3] [url-deployee]"
---

# Repasse graphique

Fonctionne dans Claude Code et Codex. Question à l'utilisateur : AskUserQuestion ou question dans le chat. Sous-agent : outil Agent ou `spawn_agent` ; sans sous-agents, enchaîner les volets soi-même. Suivi : liste de tâches de l'outil (TodoWrite, `update_plan`).

Amène le graphisme d'un site ou d'une app web au meilleur niveau, qu'il n'existe pas encore (mode **création**) ou qu'il faille le relever (mode **upgrade**). Le skill comprend l'essence du produit, cadre les envies, cherche de vraies références, fait choisir une direction, puis implémente et prouve. Il ne part jamais de la « moyenne » d'un modèle : chaque décision visuelle s'appuie sur une référence et se fixe en valeurs.

```
/repasse-graphique                     → projet courant, mode détecté
/repasse-graphique https://exemple.fr  → idem + audits sur l'URL déployée
/repasse-graphique -a --niveau 2       → enchaîne avec les recommandations, niveau d'animation 2
/repasse-graphique -r                  → reprend depuis .repasse/etat.md
```

- `-a` (auto) : prend les options recommandées sans poser de question, **sauf la porte de l'étape 5**.
- `-r` (reprise) : relit `.repasse/etat.md` et repart de la première étape non cochée.
- `--niveau` : plafond d'animation, voir [references/motion.md](references/motion.md).

## Checklist

Copier dans le suivi et cocher :

```
- [ ] 0. Contexte, mode (création ou upgrade), reprise
- [ ] 1. Essence du produit écrite ; diagnostic noté en upgrade
- [ ] 2. Envies cadrées : questionnaire (création) ou propositions (upgrade)
- [ ] 3. Recherche : références Scrolltide / 21st.dev, 3 directions distinctes, choix
- [ ] 4. Plan : design system, blueprint par page et par section, planchers
- [ ] 5. Porte : plan validé explicitement par l'utilisateur
- [ ] 6. Implémentation page par page, boucle de validation après chaque page
- [ ] 7. Note finale, itération (2 max) ou verdict ; livraison
```

État et décisions dans `.repasse/etat.md` à la racine du projet, selon [references/etat.md](references/etat.md). Avec `-r`, vérifier d'abord que le code n'a pas changé depuis le commit noté (`git log`), sinon refaire l'étape 0.

## 0. Contexte et mode

- **Charte de marque** : chercher dans le projet une charte, un `STYLE-GUIDE.md`, un `DESIGN.md`, un dossier `brand/` ou des logos fournis. Une charte existante (HEX, polices, ton) prime sur toute référence. Pas de charte et marque floue : demander à l'utilisateur avant de choisir des couleurs.
- **Historique design** : lire les décisions de design déjà écrites (`docs/**`, ADR, `.repasse/` d'un passage précédent) et partir de leurs notes plutôt que de les refaire.
- **Projet** : stack, routes, composants, tokens (`@theme` du CSS Tailwind v4 ou `tailwind.config`), conventions ; lire `package.json`, `components/**`, le CSS global.
- **Mode**, sauf `--mode` : **création** si le projet n'a ni tokens propres, ni polices choisies, ni direction visible (thème par défaut de Tailwind ou shadcn, CSS minimal, contenus provisoires) ; sinon **upgrade**. Annoncer le mode détecté et sa preuve (fichier, ligne).
- Créer `.repasse/etat.md` ; noter le commit analysé.

## 1. Comprendre l'essence

Lire le code et les contenus (pages, textes, métadonnées, README, cahier des charges, données) puis écrire la fiche essence dans `.repasse/etat.md` :

```
Produit     : ce que c'est, en une phrase
Public      : qui, dans quel contexte d'usage
Promesse    : ce que le visiteur obtient
Ton         : trois adjectifs justifiés par le contenu
Signature   : l'élément propre au sujet qui peut devenir le moment mémorable
À garder    : ce qui fonctionne déjà (upgrade)
Contraintes : performance, accessibilité, pages critiques, délais
```

Mode upgrade : diagnostic noté en parallèle, en lecture seule, selon [references/diagnostic.md](references/diagnostic.md). Chaque note cite sa preuve ; sans preuve, écrire « non mesuré ».

## 2. Cadrer les envies

- **Création** : poser le questionnaire de [references/questionnaire.md](references/questionnaire.md), deux lots de quatre questions au plus, options tirées de la fiche essence, recommandation en premier.
- **Upgrade** : présenter les améliorations classées par impact et effort (tableau : amélioration, pourquoi, preuve du diagnostic, niveau d'animation requis, coût de performance) et ne demander que les vrais arbitrages : niveau d'animation, éléments à garder, audace acceptée.

Avec `-a` : retenir les recommandations et les consigner.

## 3. Rechercher et choisir une direction

1. Chercher des références selon [references/inspiration.md](references/inspiration.md) pour chaque rôle : direction d'ensemble, hero, interaction signature, briques UI. Requêtes courtes, un ou deux mots-clés en anglais (`hero`, `particles`, `shader`, `carousel`, `text-reveal`, `pricing`, `bento`, `scroll`, `3d`) ; une phrase entière ne trouve rien. Dix requêtes au plus, tirées de la fiche essence et des réponses.
2. Construire **trois directions vraiment différentes** (mise en page, mouvement et matière, pas seulement la palette), au format de [references/directions.md](references/directions.md). Chacune cite ses références (URL) et ce qu'elle en reprend.
3. Optionnel, sur accord de l'utilisateur : une image de hero par direction avec l'outil de génération d'images dont il dispose. Jamais de service payant sans son accord.
4. Faire choisir une direction (ou un mélange explicite). Avec `-a` : la recommandée.

## 4. Plan

1. **Design system** selon [references/conventions.md](references/conventions.md) : tokens Tailwind v4 (primitifs, sémantiques), palette en HEX exacts de la charte ou de la direction, deux familles de polices et une échelle, tokens d'animation.
2. **Blueprint par page** : sections dans l'ordre ; pour chacune le composant existant, la référence reprise (licence et lien d'origine), le contenu réel. Jamais de faux chiffres, faux témoignages ni fausses captures.
3. **Blueprint motion**, pour chaque section : technique, outil, durée, easing, déclencheur, rendu en mouvement réduit, coût mobile. Une seule séquence orchestrée par page, plafonnée par le niveau d'animation ([references/motion.md](references/motion.md)). Granularité attendue :

   ```markdown
   #### Hero
   - Entrée : titre découpé par mots, power3.out, stagger 0.03 s ; mouvement réduit : texte final
   - Fond : shader en dégradé maillé, statique sous 768 px
   - Scroll : parallaxe d'un seul calque (scrub), desktop seulement
   ```

4. **Planchers**, toujours exigés : chaque largeur dessinée (320, 768, 1024, 1440 px) ; mode sombre si le type de projet l'exige (app SaaS : clair et sombre) ; LCP ≤ 2,5 s, INP ≤ 200 ms, CLS ≤ 0,1 sur mobile ; WCAG 2.2 AA, focus visible, `prefers-reduced-motion`.
5. Écrire ce qui est retenu et ce qui est écarté, avec la raison.

## 5. Porte

Présenter fiche essence, direction retenue et plan. **Aucun code avant un accord explicite de l'utilisateur, même avec `-a`.**

## 6. Implémenter et valider

Ordre : tokens et styles globaux → layout (navigation, pied de page) → atomes et leurs états → hero → sections par priorité → micro-interactions → transitions de page → finitions.

Lire [references/conventions.md](references/conventions.md) avant le premier composant et [references/motion.md](references/motion.md) avant la première animation. API d'une bibliothèque (GSAP, Motion, Tailwind, Next.js…) : vérifier la doc officielle à jour (Context7 si branché, sinon le site officiel) plutôt que de deviner. Sous-agents d'implémentation en parallèle seulement sur des fichiers disjoints ; vérifier soi-même ce qu'ils déclarent.

Après chaque page, boucle jusqu'au vert :

1. Build et typecheck avec le gestionnaire du lockfile (`npm`, `pnpm`, `bun`, `yarn`).
2. Rendu réel aux quatre largeurs (navigateur intégré de l'outil, sinon Playwright) : clavier, mouvement réduit, mode sombre ; captures avant/après.
3. Accessibilité : skill d'audit a11y si installé, sinon `npx @axe-core/cli <url>` ou l'onglet Accessibilité de Lighthouse.
4. Lighthouse mobile (`npx lighthouse <url> --form-factor=mobile` ou DevTools) : régression au-delà des planchers → corriger avant la page suivante.
5. Auto-revue sur la grille de [references/diagnostic.md](references/diagnostic.md), preuve à l'appui.

## 7. Note finale et livraison

Reprendre la grille en colonnes Avant / Après / Cible (création : Après / Cible), puis les transformations appliquées et les fichiers modifiés. Critique finale par un sous-agent qui ne voit que les captures et la grille (sinon relecture froide par soi-même, captures seules). Dimension sous la cible : correctifs ciblés, revalidation. **Deux itérations au plus**, puis verdict à l'utilisateur : score atteint, écarts restants, cause.

Ne jamais déclarer « fini » sans preuve : build vert, captures, mesures. Commit seulement si l'utilisateur le demande ; ce skill ne déploie pas.
