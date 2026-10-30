# Gabarit de `.repasse/etat.md`

Créer à l'étape 0, mettre à jour à chaque étape avant de passer à la suivante. `-r` reprend à la première étape non cochée.

```markdown
---
etape: 0            # dernière étape terminée
mode: creation      # creation | upgrade
niveau: 1           # 0 à 3, voir references/motion.md
auto: false         # -a
direction: null     # A | B | C | mélange décrit
commit_analyse: <sha court du code analysé, ou "sans git">
---

## Fiche essence
Produit / Public / Promesse / Ton / Signature / À garder / Contraintes

## Historique design repris
Charte retenue (fichier), décisions antérieures, diagnostics précédents et leur date

## Diagnostic (upgrade)
Tableau de references/diagnostic.md, preuves comprises

## Envies
Réponses au questionnaire ou arbitrages ; défauts retenus avec -a

## Recherche
Requêtes lancées ; références retenues (URL) ; ce qui est repris et écarté

## Directions
Les trois directions, la recommandation, le choix de l'utilisateur

## Plan
Design system, blueprint par page et par section, planchers, retenu / écarté

## Validation
Par page : build, rendu 4 largeurs, a11y, Lighthouse, note ; itérations
```
