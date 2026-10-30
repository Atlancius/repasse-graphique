# Repasse graphique — skill pour Claude Code et Codex

Donne à un site ou une app web un graphisme de premier plan : l'agent comprend ton produit, te pose les bonnes questions, cherche de vraies références (Scrolltide, 21st.dev), te propose trois directions, attend ton accord, puis code et vérifie page par page.

## Installation

Copie le dossier `repasse-graphique` entier (avec `references/` et `agents/`) :

| Outil | Pour tous tes projets | Pour un seul projet |
|---|---|---|
| Claude Code | `~/.claude/skills/repasse-graphique/` | `<projet>/.claude/skills/repasse-graphique/` |
| Codex | `~/.codex/skills/repasse-graphique/` | `<projet>/.agents/skills/repasse-graphique/` |

Sous Windows, `~` = `C:\Users\<toi>`. Relance l'outil après la copie.

## Utilisation

Ouvre l'agent à la racine de ton projet, puis :

```
/repasse-graphique                     projet courant, mode détecté (création ou upgrade)
/repasse-graphique https://monsite.fr  idem + audits sur le site en ligne
/repasse-graphique -a --niveau 2       prend les recommandations, animation niveau 2
/repasse-graphique -r                  reprend là où tu t'étais arrêté
```

Dans Codex : `$repasse-graphique`.

Niveaux d'animation : 0 sobre, 1 vivant, 2 expressif, 3 cinématique.

L'agent ne code **rien** avant que tu valides le plan. Son état est sauvé dans `.repasse/etat.md` de ton projet.

## Prérequis

- Un projet web (idéalement React + Tailwind v4 ; marche aussi sur d'autres stacks).
- Node.js pour les mesures (`npx lighthouse`, `npx @axe-core/cli`).
- Recommandé : un navigateur piloté par l'agent (navigateur intégré de Claude Code, ou Playwright) pour les captures aux 4 largeurs.
- Optionnel : MCP 21st.dev, MCP Context7 (docs à jour).

## Licences des références

Scrolltide : aperçus gratuits, code payant et non redistribuable. 21st.dev : code sous la licence de chaque auteur. Le skill s'inspire et reconstruit ; il ne copie pas. Détails : `references/inspiration.md`.
