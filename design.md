# design.md — SOKOHOST-OIVE' · ODL v1.0
> Operational Design Language — Document canonique  
> Artclic Studios · Belgique · 2025  
> Référence : `SKH-OIV-DS-001`

---

## 0. À propos de ce document

Ce fichier est la **source de vérité unique** du système visuel SOKOHOST-OIVE'.  
Toute décision de design, tout composant, tout format social doit s'y conformer.  
Toute déviation nécessite une mise à jour de ce fichier d'abord.

```
Projet    : SOKOHOST-OIVE'
Type      : Média éditorial africain
Studio    : Artclic Studios (Belgique)
DS version: v1.0
Fichier   : design.md
Dernière MAJ: 2025-04-29
```

---

## 1. Concept directeur

SOKOHOST-OIVE' est un média éditorial africain à destination de la diaspora mondiale.  
Son identité visuelle est une **fusion de 4 directions** :

| Direction | Référence | Registre |
|---|---|---|
| Editorial Minimal | Magazine de référence (fond blanc, rouge accent) | Rigueur, autorité |
| Cyberpunk Y2K | Underground africain, jaune électrique, chrome | Énergie, rupture |
| Brutalist Tech | Swiss condensed, bleu Klein, hardware | Structure, force |
| Maximalist Pink | Starburst, hot pink, type oversized | Chaos, célébration |

La fusion n'est pas un compromis — c'est une **tension intentionnelle**.  
Chaque format choisit sa dominante selon le registre du contenu.

---

## 2. Palette — Tokens CSS

```css
:root {
  /* ── Noyau ── */
  --ink:        #080806;   /* Noir encre — fond principal */
  --bone:       #f4efe6;   /* Ivoire chaud — fond éditorial */
  --bone-warm:  #ede5d4;   /* Ivoire foncé — variante */

  /* ── Couleurs signature ── */
  --gold:       #f0b429;   /* Or électrique — couleur PIVOT */
  --gold-dark:  #c8901a;   /* Or sombre — hover, accent */
  --red:        #cc2a18;   /* Rouge feu — rubriques, accents */
  --blue:       #1b3f78;   /* Bleu Klein — rubrique Diaspora */
  --pink:       #e42d5a;   /* Rose vif — événements, maximalist */
  --chrome:     #adbec9;   /* Chrome — données, stats */

  /* ── Utilitaires alpha ── */
  --gold-10:    rgba(240,180,41,0.1);
  --gold-20:    rgba(240,180,41,0.2);
  --bone-dim:   rgba(244,239,230,0.45);
  --red-10:     rgba(204,42,24,0.1);

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

### Règle d'or (non négociable)
> **`--gold` est présent dans chaque format**, même en quantité minimale.  
> C'est le fil rouge visuel qui unifie tous les templates.

---

## 3. Typographie

### Familles

| Rôle | Famille | Variable | Usage |
|---|---|---|---|
| Display | Bebas Neue | `--display` | Titres géants, sections, rubriques, CTA |
| Editorial | Playfair Display | `--editorial` | Titres articles, citations, pull quotes |
| Mono UI | Space Mono | `--mono` | Labels, méta, handles, navigation, prix |
| Corps | DM Sans | `--body` | Corps de texte, descriptions, excerpts |

### Import Google Fonts (HEAD)
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500;9..40,600&display=swap" rel="stylesheet">
```

### Hiérarchie type — Landing page

```
H1 display    : Bebas Neue · clamp(5rem, 13vw, 11rem) · line-height 0.85
H2 display    : Bebas Neue · clamp(2.5rem, 6vw, 5rem) · line-height 0.9
H3 editorial  : Playfair Display 900 · clamp(1.5rem, 4vw, 3rem) · line-height 1.1
Body          : DM Sans 400 · 1rem · line-height 1.6
Label         : Space Mono 700 · 0.55–0.65rem · letter-spacing 0.2–0.3em · uppercase
```

### Règles typographiques strictes
- **Jamais** Inter, Roboto, Arial, ou system-font pour les visuels
- **Jamais** border-radius sur les conteneurs typographiques display
- **Toujours** `letter-spacing: 0.15em+` sur Bebas Neue en petite taille
- Italic = exclusivement Playfair Display
- Mono = exclusivement pour méta, labels, handles, code

---

## 4. Règles visuelles — Non négociables

```
1.  Zero border-radius                → jamais de coins arrondis, sauf :
                                          · badges : 2px max
                                          · dots ronds (live-dot, ticker-sep) : border-radius:50%
                                          Ces deux exceptions sont les seules autorisées.
2.  Zero Inter/Roboto/Arial           → uniquement les 4 familles définies en §3
3.  Gold toujours présent             → même trace minimale dans chaque format
4.  Stripe noire gauche sur T2 Quote  → signature visuelle non négociable
5.  Starburst = fond pink uniquement  → jamais sur autre couleur de fond
6.  Ticker = fond gold, dots rouges   → texte Bebas Neue, animation 20s linear
7.  Posts sociaux = zero border-radius sur blocs info
8.  Carousel slide 9 = fond gold      → CTA final, jamais autre couleur
9.  Grain overlay = fonds sombres     → opacity 0.035 max, z-index 9999
10. Rubriques = couleurs fixes        → voir §5
```

---

## 5. Rubriques éditoriales

| # | Rubrique | Couleur dominante | Token |
|---|---|---|---|
| 01 | Héritage & Mémoire | Bleu Klein | `--blue` |
| 02 | Identité Plurielle | Or électrique | `--gold` |
| 03 | Diaspora Mondiale | Bleu Klein | `--blue` |
| 04 | Création Contemporaine | Rose vif | `--pink` |
| 05 | Même le Futur | Chrome | `--chrome` |

Couleur d'accent rubrique = toujours utilisée sur `.article-card-rubrique` et les tags.

---

## 6. Composants — Référence

### 6.1 Boutons

| Variante | BG | Text | Border | Usage |
|---|---|---|---|---|
| `btn-primary-gold` | `--gold` | `--ink` | — | CTA principal |
| `btn-outline-gold` | transparent | `--gold` | 2px gold | CTA secondaire |
| `btn-ghost` | transparent | `--bone-dim` | 1px bone/15% | Action tertiaire |
| `btn-display` | `--red` | `--bone` | — | CTA événement |

Police : Space Mono · 0.62rem · letter-spacing 0.2em · uppercase · font-weight 700

### 6.2 Badges

```
badge-gold    : bg --gold    · text --ink
badge-red     : bg --red     · text --bone
badge-blue    : bg --blue    · text --bone
badge-pink    : bg --pink    · text --bone
badge-outline : transparent  · text --gold · border gold-20
badge-ghost   : bg gold-10   · text --gold · border gold-20
```

Police : Space Mono · 0.52rem · letter-spacing 0.15em · uppercase · font-weight 700  
Border-radius : 2px (exception unique)

### 6.3 Cards article

```css
.article-card {
  background: rgba(244,239,230,0.03);
  border: 1px solid rgba(244,239,232,0.07);
  padding: 1.5rem;
  transition: border-color 0.3s, transform 0.3s cubic-bezier(0.16,1,0.3,1);
}
.article-card:hover {
  border-color: rgba(240,180,41,0.2);
  transform: translateY(-2px);
}
```

### 6.4 Inputs

```css
.input-field {
  background: rgba(244,239,230,0.04);
  border: 1px solid rgba(244,239,230,0.1);
  color: var(--bone);
  font-family: var(--mono);
  font-size: 0.72rem;
  letter-spacing: 0.08em;
  padding: 0.85rem 1rem;
  border-radius: 0; /* JAMAIS de radius */
}
.input-field:focus { border-color: var(--gold); }
```

### 6.5 Ticker

```
Fond        : --gold
Texte       : Bebas Neue · 1rem+ · letter-spacing 0.15em · --ink
Séparateurs : points ronds --red · 6px
Animation   : translateX(-50%) · 20s linear infinite
Hover       : animation-play-state: paused
Border      : 3px solid --ink top + bottom
```

### 6.6 Grain overlay

```css
body::after {
  content: '';
  position: fixed; inset: 0;
  background-image: url('/assets/grain.png'); /* PNG 200×200 tileable */
  opacity: 0.035;
  pointer-events: none;
  z-index: 9999;
}
/* Uniquement sur fonds sombres (--ink, --blue, --red) */
```

---

## 7. Formats sociaux — Spécifications

### 7.1 Posts Instagram 1:1

| ID | Nom | Fond dominant | Direction | Fréquence |
|---|---|---|---|---|
| T1 | Cover / Une | `--bone` (ivoire) | Editorial Minimal | 1×/semaine |
| T2 | Citation / Quote | `--gold` (or) | Cyberpunk Y2K | 3×/semaine |
| T3 | Rubrique | `--blue` (Klein) | Brutalist Tech | 1×/mois |
| T4 | Événement | `--pink` (rose) | Maximalist | Ad hoc |
| T5 | Statistique | `--ink` (noir) | Chrome Stat | 2×/semaine |

Dimensions export : **1080 × 1080 px · @2x (2160×2160)**

```html
<!-- Dans chaque fichier social/post-*.html -->
<meta name="viewport" content="width=1080">
<!-- body : width:1080px; height:1080px; overflow:hidden; margin:0 -->
```

### 7.2 Stories 9:16

| ID | Nom | Fond | Direction |
|---|---|---|---|
| ST1 | Hero Annonce | `--ink` + diagonale `--gold` | Cyberpunk diagonal |
| ST2 | Quote Blue | `--blue` + coin `--gold` | Brutalist Editorial |
| ST3 | Événement Maximalist | `--pink` + starburst | Maximalist |

Dimensions export : **1080 × 1920 px · @2x**

### 7.3 Carousel 9 slides — Structure narrative

```
Slide 1  : Cover intro         → fond --ink, brand gold, titre éditorial
Slide 2  : Stat impact         → fond --red, chiffre massif
Slide 3  : Citation            → fond --bone, Playfair italic
Slide 4  : Photo/terrain       → fond sombre, caption minimal
Slide 5  : Stat bleu           → fond --blue, chiffre + contexte
Slide 6  : Citation or         → fond --gold, stripe noire, quote
Slide 7  : Photo communauté    → fond dark warm, caption gold
Slide 8  : Data pink           → fond --pink, chiffre + starburst
Slide 9  : CTA final           → fond --gold OBLIGATOIRE, CTA noir
```

---

## 8. Palettes d'humeur — Combinaisons validées

| Nom | Combinaison | Usage |
|---|---|---|
| Editorial Minimal | Bone + Red + Ink | T1, articles longs, couvertures |
| Cyberpunk Or | Gold + Ink + Red | T2, quotes, manifesto |
| Brutalist Klein | Blue + Bone + Gold | T3, rubriques, séries |
| Maximalist Pink | Pink + Ink + Gold | T4, événements, CTA |
| Chrome Stat | Ink + Bone + Red | T5, data, impact |

---

## 9. Contraste — Accessibilité (WCAG AA)

| Combinaison | Ratio | Niveau |
|---|---|---|
| `--bone` sur `--blue` | ~5.8:1 | AA ✓ |
| `--ink` sur `--gold` | ~8.2:1 | AAA ✓ |
| `--bone` sur `--pink` | ~4.1:1 | AA large ✓ |
| `--bone` sur `--ink` | ~16:1 | AAA ✓ |
| `--ink` sur `--bone` | ~16:1 | AAA ✓ |

---

## 10. Architecture fichiers cible

```
sokohost-oive-media/
├── design.md                          ← CE FICHIER (source de vérité)
├── CLAUDE.md
├── COMMIT.txt
├── .gitignore
├── manifeste-oive-v2.html
├── sokohost-homepage.html
├── paradoxe-du-transfert.html         ← root (commit 1)
├── spending-paradox.html              ← root (commit 1)
├── claude-code-correction-article.md
├── claude-code-sources-opendata.md
├── claude-code-migration-skh.md
├── SokoHost Logo.png
├── SokoHost Logo.svg
├── SokoHost Logo00.png
├── SokoHost Logo01.png
└── assets/                            ← reorg différée
    └── logos/                           commit 3
```

> **Note §10 — Structure cible.** Reorg différée au commit 3.
> Liens internes à mettre à jour simultanément (homepage, articles, manifeste).

---

## 11. Pipeline export social (Puppeteer)

```bash
# Installation
npm install puppeteer

# Export tous les formats
node export.js

# Sortie : _output/*.png @2x
# post-t1-cover.png    (2160×2160)
# post-t2-quote.png    (2160×2160)
# post-t3-rubrique.png (2160×2160)
# post-t4-event.png    (2160×2160)
# post-t5-stat.png     (2160×2160)
# st1-hero.png         (2160×3840)
# st2-quote.png        (2160×3840)
# st3-event.png        (2160×3840)
```

Voir `export.js` pour le script complet.

---

## 12. Variables de contenu éditorial

```json
{
  "brand":      "SOKOHOST-OIVE'",
  "handle":     "@sokohostoive",
  "site":       "sokohost.com",
  "volume":     "Vol.001",
  "issue_date": "Avr. 2025",
  "ds_version": "v1.0",
  "rubriques": {
    "heritage": { "label": "Héritage & Mémoire",      "color": "#1b3f78", "num": "01" },
    "identite": { "label": "Identité Plurielle",       "color": "#f0b429", "num": "02" },
    "diaspora": { "label": "Diaspora Mondiale",        "color": "#1b3f78", "num": "03" },
    "creation": { "label": "Création Contemporaine",   "color": "#e42d5a", "num": "04" },
    "futur":    { "label": "Même le Futur",            "color": "#adbec9", "num": "05" }
  }
}
```

---

## 13. Historique des versions

| Version | Date | Changements |
|---|---|---|
| v1.0 | 2025-04-29 | Version initiale — Design System complet livré |

---

*SKH-OIV-DS-001 · Artclic Studios · Belgique · 2025*
