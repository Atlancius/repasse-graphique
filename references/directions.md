# Trois directions à faire choisir

Ouvrir à l'étape 3. Trois directions diffèrent par la mise en page, le mouvement et la matière ; trois palettes sur la même maquette ne font pas trois directions.

## Format d'une direction

```markdown
### Direction A — <nom évocateur>

<Une phrase : ce que ressent le visiteur et pourquoi c'est juste pour ce produit.>

- Références : <URL> — on prend <mécanique, valeurs> ; on laisse <...>
- Palette : <fond HEX>, <texte HEX>, <accent HEX> (accent sur 4 éléments par écran au plus)
- Typographie : <display> + <texte> (+ <mono> si utile), échelle en clamp()
- Mise en page : <grille, largeur de texte, rythme des sections, ce qui casse la grille>
- Moment mémorable : <l'élément propre au sujet et comment il bouge>
- Motion : niveau <0-3>, une courbe d'easing, durées types, déclencheurs ; repli en mouvement réduit
- Coût : <poids JS, 3D ou vidéo, risque LCP mobile> ; <ce qui est désactivé sous 768 px>
- Pages concernées : <toutes, ou lesquelles et dans quel ordre>
- Risque : <ce qui peut mal tourner et comment le vérifier>
- Écarté : <ce que cette direction refuse volontairement, et pourquoi>
```

## Recommandation

Terminer par la direction recommandée et sa raison en deux lignes, rattachée à la fiche essence (public, promesse, ton). Une direction qui contredit la charte de marque est écartée avant d'être présentée. Vérifier le contraste texte/fond de chaque palette (4,5:1 minimum pour le texte courant).

## Reprendre une référence par ses valeurs

Une référence se reprend par ses décisions, pas par son apparence : HEX, familles et échelle de polices, interlignage et largeur de texte (≈ 62 caractères), courbe d'easing unique, décalages et durées (exemple : entrée en translation de 16 px sur 750 ms, décalage 60 ms entre éléments), déclencheurs liés au scroll plutôt qu'à un minuteur, interdits explicites, grain ou texture et leur intensité.
