# Claude Code — Commande de correction
## Article : Le Paradoxe du Transfert
## Fichier cible : `frontend/article-paradoxe-transfert.html`
## Référence design : `design.md` (ODL v1.0)

---

## Contexte à lire avant d'agir

```
Lis dans l'ordre :
1. CLAUDE.md                              → conventions globales du projet
2. design.md                              → ODL v1.0, source de vérité design
3. frontend/article-paradoxe-transfert.html → fichier à corriger
```

---

## Mission

Appliquer **trois corrections précises** sur `frontend/article-paradoxe-transfert.html`.
Ne modifier aucun autre fichier. Ne toucher à aucune logique éditoriale.
Conserver intégralement la structure HTML, le contenu textuel, et les styles existants.

---

## CORRECTION 1 — Date dynamique (priorité haute)

### Problème
La date de publication est statique ou absente.
Sur un article de référence cité académiquement, une date figée nuit à la crédibilité.

### Ce que tu dois faire

Localise le bloc JavaScript en bas du fichier (avant `</body>`).
Remplace ou complète la fonction de date par exactement ceci :

```javascript
// ── DATE DYNAMIQUE — ODL règle 07 ──────────────────────────
(function() {
  const now = new Date();

  // Format long FR : "28 avril 2026"
  const dateLongFR = now.toLocaleDateString('fr-FR', {
    day: 'numeric',
    month: 'long',
    year: 'numeric'
  });

  // Format long EN : "April 28, 2026"
  const dateLongEN = now.toLocaleDateString('en-GB', {
    day: 'numeric',
    month: 'long',
    year: 'numeric'
  });

  // Format court pour footer : "Avril 2026"
  const dateShortFR = now.toLocaleDateString('fr-FR', {
    month: 'long',
    year: 'numeric'
  });

  // Injection dans le DOM
  const elPubDate    = document.getElementById('pub-date');
  const elFooterDate = document.getElementById('footer-date');
  const elCoverDate  = document.getElementById('cover-date');

  if (elPubDate)    elPubDate.textContent    = dateLongFR;
  if (elFooterDate) elFooterDate.textContent = dateShortFR;
  if (elCoverDate)  elCoverDate.textContent  = dateLongFR;
})();
```

### Cibles HTML à vérifier / ajouter si absentes

```html
<!-- Dans le byline header -->
<span class="byline-date" id="pub-date"></span>

<!-- Dans le SVG cover (textContent ne fonctionne pas sur SVG <text>) -->
<!-- Si présent, remplacer par un <text> avec id="cover-date-svg"
     et injecter via setAttribute ou textContent -->

<!-- Dans le footer -->
<span id="footer-date"></span>
```

### Règle de validation
Après correction, ouvre le fichier dans un navigateur.
La date affichée doit correspondre à la date du jour réel — jamais une date en dur.
Vérifie avec : `document.getElementById('pub-date').textContent` dans la console.

---

## CORRECTION 2 — Design moderne LinkedIn (priorité haute)

### Problème identifié sur le screenshot
- Fond trop sombre → illisible dans le feed LinkedIn (contexte clair)
- Marges latérales trop larges → contenu écrasé sur mobile
- Typographie trop dense → fatigue de lecture sur écran

### Ce que tu dois faire

#### 2.1 — Fond et surface

Dans le bloc `:root`, vérifie et impose ces valeurs exactes :

```css
:root {
  --bg:       #f7f3ec;   /* crème chaud — jamais #000 ni #111 */
  --bg-warm:  #efe9de;
  --bg-deep:  #e6ddd0;
  --surface:  #faf7f2;
}
```

Vérifie que `body { background: var(--bg); }` est bien appliqué.
Si `background` est surchargé ailleurs (sections, wrappers), supprime les surcharges sombres.

#### 2.2 — Marges et largeur de colonne

```css
.article-wrap {
  max-width: 740px;      /* pas plus — lisibilité LinkedIn desktop */
  margin: 0 auto;
  padding: 0 24px 100px; /* 24px latéral — pas 60px ni 70px */
}
```

Sur mobile (`max-width: 680px`) :
```css
@media (max-width: 680px) {
  .article-wrap {
    padding: 0 16px 80px;
  }
}
```

#### 2.3 — Interlignes et taille de corps

```css
.article-body p {
  font-size: 1.02rem;
  line-height: 1.9;      /* respiration — pas moins de 1.8 */
  margin-bottom: 22px;
  text-align: justify;
  hyphens: auto;
}
```

#### 2.4 — Nav sticky lisible sur fond clair

```css
.site-nav {
  background: rgba(247,243,236,0.92);  /* translucide chaud */
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(139,100,30,0.15);
}
```

#### 2.5 — Contraste texte (WCAG AA minimum)

Vérifie que les couleurs de texte respectent ces valeurs ODL :
```css
--ink:      #1a1410;   /* titres */
--text:     #4a3c28;   /* corps */
--text-mid: #7a6a52;   /* secondaire */
--text-dim: #a89880;   /* metadata — ne jamais utiliser seul sur fond clair */
```

### Règle de validation
Ouvre le fichier dans un onglet. Rétrécis la fenêtre à 375px de large (iPhone SE).
Le texte doit être lisible sans zoom, les marges visibles des deux côtés.

---

## CORRECTION 3 — Bandeau image de couverture (priorité haute)

### Problème
L'article n'a pas de bandeau visuel en haut.
LinkedIn extrait automatiquement la première image `<meta og:image>` ou le premier visuel prominent de la page pour la prévisualisation du lien partagé.

### Ce que tu dois faire

#### 3.1 — Vérifier le SVG cover existant

Le fichier contient déjà un bloc `.cover` avec un SVG composé.
Vérifie qu'il est positionné **immédiatement après `</nav>`**, avant `<div class="article-wrap">`.

Structure attendue :
```html
</nav>

<div class="cover">          ← doit être ici
  <svg viewBox="0 0 1200 420" ...>
    ...
  </svg>
</div>

<div class="article-wrap">  ← article commence ici
```

Si le bloc `.cover` est absent ou mal positionné, le déplacer à cet endroit.

#### 3.2 — Dimensions et ratio du cover

```css
.cover {
  width: 100%;
  aspect-ratio: 1200 / 420;   /* ratio LinkedIn recommandé : ~2.85:1 */
  max-height: 420px;
  background: var(--forest);   /* #1e4a28 — fallback si SVG ne charge pas */
  overflow: hidden;
  position: relative;
}

.cover svg {
  width: 100%;
  height: 100%;
  display: block;
}
```

Sur mobile :
```css
@media (max-width: 680px) {
  .cover {
    aspect-ratio: auto;
    min-height: 200px;
    max-height: 260px;
  }
}
```

#### 3.3 — Contenu obligatoire du SVG cover

Le SVG doit contenir dans cet ordre :
1. Fond dégradé `--forest` → `#0d1a0f`
2. Grille de fond subtile (pattern)
3. Glows radiaux (or + vert)
4. Texte : kicker `OIVE · DÉCOUVERTE CENTRALE · 2025` (JetBrains Mono, or atténué)
5. Texte : titre `Le Paradoxe du` + `Transfert` en italic gold (Playfair Display)
6. Texte : sous-titre `Pourquoi 1€ visible cache 6 à 8€ invisibles`
7. Graphique ratio : `1€` (rouge) · `×6–8` (gold) · `6–8€` (vert)
8. Signature : `PAR NJENG PIERRE-YVES · SOKOHOST.COM`
9. `<text id="cover-date-svg" ...></text>` — date injectée par JS

Pour injecter la date dans le SVG (le SVG est inline, donc accessible au DOM) :
```javascript
const coverDateSvg = document.getElementById('cover-date-svg');
if (coverDateSvg) coverDateSvg.textContent = dateLongFR;
```

#### 3.4 — Meta og:image

Ajouter dans le `<head>` :
```html
<meta property="og:image" content="https://sokohost.com/og/paradoxe-transfert.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="420">
<meta property="og:image:alt" content="Le Paradoxe du Transfert — OIVE · Njeng Pierre-Yves">
<meta property="twitter:image" content="https://sokohost.com/og/paradoxe-transfert.png">
```

Note pour le déploiement : générer le PNG de l'image OG depuis le SVG avec
`node scripts/generate-og.js` (script à créer séparément).

---

## Séquence d'exécution pour Claude Code

```
1. Lire CLAUDE.md
2. Lire design.md
3. Lire frontend/article-paradoxe-transfert.html en entier
4. Appliquer CORRECTION 1 (date dynamique)
5. Vérifier console : document.getElementById('pub-date').textContent
6. Appliquer CORRECTION 2 (design clair, marges, contraste)
7. Tester visuellement à 375px de large
8. Appliquer CORRECTION 3 (bandeau cover + og:image)
9. Vérifier structure : nav → cover → article-wrap
10. Lancer : npx html-validate frontend/article-paradoxe-transfert.html
11. Si erreurs → corriger → relancer
12. Commit : "fix(article): date dynamique + design LinkedIn + bandeau cover"
```

---

## Tests de validation post-correction

```bash
# Ouvrir dans le navigateur
open frontend/article-paradoxe-transfert.html

# Vérifier dans la console DevTools
document.getElementById('pub-date').textContent
# → doit afficher la date du jour en français

# Vérifier les marges mobile
# Ouvrir DevTools → Toggle device toolbar → iPhone SE (375px)
# Les marges doivent être visibles des deux côtés

# Vérifier le cover
# Il doit apparaître sous la nav, avant le texte de l'article

# Vérifier le contraste
# DevTools → Accessibility → Color contrast
# Ratio minimum : 4.5:1 pour tout texte de corps
```

---

## Ce qui est interdit dans cette commande

```
✗ Modifier le contenu éditorial (texte, titres, données)
✗ Changer les tokens ODL (couleurs, polices) sauf surcharges sombres incorrectes
✗ Ajouter de nouvelles sections ou composants non demandés
✗ Modifier sokohost-homepage.html ou manifeste-oive-v2.html
✗ Changer la structure des tableaux breakdown et corridors
✗ Committer avant que les 3 corrections soient validées
```

---

## Commit message canonique

```
fix(article): date dynamique + design clair LinkedIn + bandeau cover ODL

- Date pub-date et footer-date générées dynamiquement via Date()
- Fond basculé sur --bg #f7f3ec (mode publication clair)
- Marges article-wrap réduites à 24px (mobile 16px)
- Bandeau SVG cover positionné nav → cover → article-wrap
- og:image meta tags ajoutés pour prévisualisation LinkedIn
- id="cover-date-svg" injecté dynamiquement

Réf : design.md ODL v1.0 § règle 10 exception publication
Auteur : Njeng Pierre-Yves / OIVE / sokohost.com
```

---

*Commande v1.0 · OIVE Sprint · 2025*
*Référence : design.md ODL v1.0 · CLAUDE.md projet*
