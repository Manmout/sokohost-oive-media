# Claude Code — Migration SKH-OIV-DS-001
## Mission : Migrer tous les fichiers HTML vers le nouveau Design System
## Référence : design.md (SKH-OIV-DS-001 · Artclic Studios · v1.0)
## Domaine canonique : sokohost.com

---

## ÉTAPE 0 — Avant toute écriture

```
1. Lis design.md en entier
2. Corrige design.md §12 :
   "site": "sokohostoive.com" → "site": "sokohost.com"
3. Liste tous les fichiers .html présents
4. Montre-moi la liste avant de commencer
```

---

## TOKENS DE MIGRATION — Correspondances exactes

Utilise ce tableau pour chaque remplacement CSS.
Ne pas interpoler. Ne pas inventer de valeurs intermédiaires.

```
ANCIEN TOKEN          NOUVEAU TOKEN          VALEUR EXACTE
─────────────────     ───────────────────    ──────────────
--oive-void           --ink                  #080806
--oive-deep           --ink                  #080806
--oive-surface        rgba(244,239,230,0.03) (card bg)
--oive-border         rgba(244,239,232,0.07) (card border)
--oive-border-hi      rgba(240,180,41,0.2)   (gold border)
--oive-gold           --gold                 #f0b429
--oive-gold-dim       --gold-dark            #c8901a
--oive-gold-pale      --gold-10              rgba(240,180,41,0.1)
--oive-green-live     --gold                 #f0b429 (pas de vert)
--oive-green-mid      --red                  #cc2a18 (accent rubrique)
--oive-text-hi        --bone                 #f4efe6
--oive-text           --bone-dim             rgba(244,239,230,0.45) (peut varier)
--oive-text-mid       rgba(244,239,230,0.6)  (interpolé)
--oive-text-dim       rgba(244,239,230,0.3)  (interpolé)
--oive-data           --chrome               #adbec9
--oive-positive       --gold                 #f0b429
--oive-negative       --red                  #cc2a18
--oive-neutral        --gold-dark            #c8901a
--oive-night          --blue                 #1b3f78

ANCIEN FONT           NOUVEAU FONT
─────────────────     ───────────────────
'Playfair Display'    'Playfair Display'  (conservé — rôle éditorial)
'Libre Baskerville'   'DM Sans'           (corps de texte)
'JetBrains Mono'      'Space Mono'        (labels, méta, données)
'Spectral'            'Playfair Display'  (fusionné)
'Overpass Mono'       'Space Mono'        (fusionné)

TITRES DISPLAY (nouveaux) :
  H1 homepage hero  → Bebas Neue
  H2 sections       → Bebas Neue
  H3 sous-titres    → Playfair Display (italic conservé)
  Titres articles   → Playfair Display (longform — lisibilité)
  Labels, méta, KPI → Space Mono
```

---

## IMPORT FONTS — À remplacer dans chaque fichier

Retire tous les anciens imports Google Fonts.
Remplace par exactement :

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500;9..40,600&display=swap" rel="stylesheet">
```

---

## VARIABLES CSS — Bloc :root à insérer dans chaque fichier

Remplace le bloc :root existant par :

```css
:root {
  /* ── Noyau SKH-OIV-DS-001 ── */
  --ink:        #080806;
  --bone:       #f4efe6;
  --bone-warm:  #ede5d4;

  /* ── Couleurs signature ── */
  --gold:       #f0b429;
  --gold-dark:  #c8901a;
  --red:        #cc2a18;
  --blue:       #1b3f78;
  --pink:       #e42d5a;
  --chrome:     #adbec9;

  /* ── Utilitaires alpha ── */
  --gold-10:    rgba(240,180,41,0.1);
  --gold-20:    rgba(240,180,41,0.2);
  --bone-dim:   rgba(244,239,230,0.45);
  --red-10:     rgba(204,42,24,0.1);

  /* ── Typographie ── */
  --display:    'Bebas Neue', sans-serif;
  --editorial:  'Playfair Display', Georgia, serif;
  --mono:       'Space Mono', monospace;
  --body:       'DM Sans', sans-serif;

  /* ── Espacement ── */
  --sp-xs:  0.25rem;
  --sp-sm:  0.5rem;
  --sp-md:  1rem;
  --sp-lg:  2rem;
  --sp-xl:  4rem;
  --sp-2xl: 6rem;

  /* ── Motion ── */
  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
  --dur-fast: 0.15s;
  --dur-med:  0.3s;
  --dur-slow: 0.8s;

  /* ── Z-index ── */
  --z-base:  1;
  --z-float: 10;
  --z-nav:   100;
  --z-modal: 200;
}
```

---

## RÈGLES ABSOLUES SKH-OIV-DS-001 (design.md §4)

```
1.  Zero border-radius           → jamais, sauf badges : 2px max
2.  Zero Inter/Roboto/Arial      → uniquement les 4 familles
3.  Gold toujours présent        → même trace minimale dans chaque fichier
4.  Grain overlay fonds sombres  → opacity 0.035 max, z-index 9999
```

Après chaque fichier migré, vérifie ces 4 règles.
Si une règle est violée → corriger avant de passer au fichier suivant.

---

## FICHIER 1 — sokohost-homepage.html

### Fond et structure
- `background: var(--oive-void)` → `background: var(--ink)`
- Appliquer grain overlay (§4 règle 9) si pas déjà présent

### Hero title
- `font-family: var(--font-ed)` → `font-family: var(--display)`
- `font-size` → `clamp(5rem, 13vw, 11rem)`
- `line-height` → `0.85`
- Conserver `<em>` en Playfair Display italic

### Navigation
- Labels nav : `font-family` → `var(--mono)` (Space Mono)
- Logo OIVE : `font-family` → `var(--editorial)` (Playfair)

### KPI Cards
- Labels : `var(--mono)` · 0.55rem · letter-spacing 0.2em · uppercase
- Valeurs : `var(--editorial)` (Playfair Display) · conserver

### Paradox Display
- Chiffres `1€` et `6–8€` : `var(--editorial)` · conserver tailles
- Multiplier `×6–8` : `var(--editorial)` · `color: var(--gold)`

### Corridor Cards
- `border-radius` → 0 (règle absolue §4)
- Hover border : `rgba(240,180,41,0.2)` (--gold-20)

### Boutons
- `.btn-primary` → bg `var(--gold)` · color `var(--ink)`
- `.btn-secondary` → border `var(--gold-20)` · color `var(--bone-dim)`
- `font-family` → `var(--mono)` · 0.62rem · uppercase · weight 700
- `border-radius` → 0

### Language toggle
- `.lang-btn.active` → bg `var(--gold)` · color `var(--ink)`
- `border-radius` → 0

### Mise à jour meta
- `<meta property="og:site_name"` → `content="SOKOHOST-OIVE' · sokohost.com"`

---

## FICHIER 2 — paradoxe-du-transfert.html

### Fond
- `background: var(--bg, #f7f3ec)` → `background: var(--bone)`
- Nav : `background: rgba(244,239,230,0.92)` → conserver (mode article clair)

### Cover SVG
- Fond SVG : conserver `var(--forest)` → remplacer par `var(--ink)`
- Gold dans SVG : `#c49a2a` → `#f0b429`
- Vert SVG `#4dcc66` → `#f0b429` (pas de vert dans SKH-OIV-DS-001)

### Titres de sections (h2)
- Articles longform : conserver Playfair Display (lisibilité)
- `font-weight: 700` (Playfair 700 disponible)

### Labels, kickers, byline-role
- Tout ce qui était JetBrains Mono → Space Mono
- `font-family: var(--mono)`

### Paradox Display (bloc sombre central)
- Fond : `var(--forest)` → `var(--ink)`
- Chiffre visible `1€` : `color: var(--red)` (--cc2a18)
- Chiffre invisible `6–8€` : `color: var(--gold)` (#f0b429)
- Multiplicateur `×6–8` : `color: var(--gold-dark)`

### Tableau breakdown
- Barres `.bar.green` → `background: var(--gold)`
- Barres `.bar.red` → `background: var(--red)`
- `.val-green` → `color: var(--gold-dark)`

### Sources
- Liens `a` : `color: var(--blue)` (#1b3f78) → lisibilité sur fond bone
- Hover `a` : `color: var(--gold-dark)`
- Border-left groupes : `var(--gold-dark)`

### Border-radius
- Audit complet — mettre à 0 partout sauf badges (2px)

---

## FICHIER 3 — spending-paradox.html

Migration symétrique au fichier 2.
Même tableau de correspondances.
Même règles cover SVG.
Vérifier que "The Spending Paradox" reste intact partout
(aucune modification éditoriale — design uniquement).

---

## FICHIER 4 — manifeste-oive-v2.html

### Fond
- `background: var(--void, #080a07)` → `background: var(--ink)`

### Typographie
- Spectral → Playfair Display (même rôle éditorial)
- Overpass Mono → Space Mono
- Cormorant Garamond → Playfair Display

### Import fonts
- Remplacer par le bloc SKH-OIV-DS-001 standard

### Couleurs
- `--sienna: #a04828` → `var(--red)` (#cc2a18)
- `--forest: #2d4a2d` → `var(--blue)` (#1b3f78) pour les accents de section
- Or : tous les or existants → `var(--gold)` (#f0b429)

### Witness box / Déclic box
- Border-left : `var(--gold)`
- Background : `var(--gold-10)`

### Pull quotes
- Fond : `var(--gold-10)` · border `var(--gold-20)`

### Signature Njeng Pierre-Yves
- `.sig-name` : `font-family: var(--editorial)` · italic · conservé
- `.sig-domain` : `font-family: var(--mono)` · border 0 radius

---

## SÉQUENCE D'EXÉCUTION

```
1.  Corriger design.md §12 (sokohost.com)
2.  Lister les fichiers HTML présents
3.  Migrer sokohost-homepage.html
    → Vérifier 4 règles absolues
    → Ouvrir dans navigateur · screenshot mental
4.  Migrer paradoxe-du-transfert.html
    → Vérifier lisibilité article sur fond --bone
    → Vérifier Paradox Display fond --ink
5.  Migrer spending-paradox.html (symétrique)
6.  Migrer manifeste-oive-v2.html
7.  Vérification finale cross-fichiers :
    grep -rn "border-radius" --include="*.html" .
    → Seuls les badges (2px) sont autorisés
    grep -rn "JetBrains\|Baskerville\|Spectral\|Overpass" --include="*.html" .
    → Zéro résultat attendu
    grep -rn "var(--oive-" --include="*.html" .
    → Zéro résultat attendu (tous migrés)
8.  Mettre à jour COMMIT.txt :
    feat(design): migration complète SKH-OIV-DS-001
    - Tokens --oive-* → tokens SKH natifs
    - Fonts : Bebas Neue + Playfair + Space Mono + DM Sans
    - Gold #f0b429 unifié sur 4 fichiers
    - Zero border-radius validé (badges 2px exception)
    - design.md §12 corrigé : sokohost.com canonique
    SKH-OIV-DS-001 · Artclic Studios · sokohost.com
```

---

## CE QUI NE CHANGE PAS

```
✗ Contenu éditorial (texte, données, citations)
✗ Structure HTML (sections, ancres, TOC)
✗ Logique JS (date dynamique, lang toggle, IIFE)
✗ Schema.org JSON-LD
✗ Balises meta et hreflang
✗ Sources et leurs URLs
✗ Les commentaires <!-- date historique --> etc.
✗ COMMIT.txt (sauf ajout section migration)
```

---

## ARRÊT OBLIGATOIRE SI

```
→ Un patch casse une ancre TOC (#section)
→ Un patch modifie du texte visible
→ La lisibilité du corps de texte article
  devient inférieure à WCAG AA (4.5:1)
→ Le Paradox Display perd sa hiérarchie
  visuelle 1€ vs 6–8€
→ "The Spending Paradox" ou "Paradoxe du
  Transfert" apparaissent modifiés
```

Montrer le problème. Attendre validation.

---

*SKH-OIV-DS-001 · Migration v1.0 → v1.0 new tokens*
*sokohost.com · Njeng Pierre-Yves · Artclic Studios*
