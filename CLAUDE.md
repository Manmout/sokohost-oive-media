# SOKOHOST — Project CLAUDE.md

## Identity

OIVE — **Observatoire de l'Impact des Vagues d'Immigration en Europe**.
Flagship initiative under sokohost.com (Brussels, founded 2025).
Lead: Njeng Pierre-Yves.
Central concept: **The Spending Paradox** / **Paradoxe du Transfert**.

Mission line:
- FR : « L'intelligence économique au service des migrants. »
- EN : "Economic intelligence for migrants."

## Files in this folder

- `paradoxe-du-transfert.html` — FR long-form article (1750+ lines)
- `spending-paradox.html` — EN long-form article (1750+ lines, authored autonomous, NOT a translation)
- `COMMIT.txt` — bilingual deployment commit message (no hardcoded year — git captures it)
- Logos PNG/SVG for Sokohost + Money Overseas Center

**To sync from Claude.ai outputs at deployment time** (BEFORE `git init`):
- `design.md` — ODL v1.0 canonique
- `manifeste-oive-v2.html` — signed Njeng Pierre-Yves
- `sokohost-homepage.html` — bilingual FR/EN
- `claude-code-correction-article.md`
- `claude-code-sources-opendata.md`

After sync, re-run the `202[0-9]` audit on the new HTMLs and apply the §dates discipline below.

## Canonical nomenclature (locked, never translate or reword)

- Concept: **Paradoxe du Transfert** (FR) / **The Spending Paradox** (EN)
- API key: `spending_paradox_ratio` (both languages)
- Section I title (EN): **The pile of receipts** (h2 + TOC, never "The pile" alone)
- Citation canonique courte (cite-ribbon):
  - FR: `Paradoxe du Transfert (OIVE, Njeng Pierre-Yves, 2025)`
  - EN: `The Spending Paradox (OIVE, Njeng Pierre-Yves, 2025)`
- Citation canonique longue (cite-block §IX) — **Brussels, 2025** in cite-org line:
  - EN: `Njeng Pierre-Yves (2025). The Spending Paradox. OIVE — Observatory of Immigration Waves Economic Impact in Europe. Brussels, 2025. https://sokohost.com/en/spending-paradox`
- Byline: `Njeng Pierre-Yves · Founder, OIVE · sokohost.com · Economic intelligence for migrants.`

## §dates — Date discipline

**Rule**: No hardcoded year in HTML/MD/JSON. Only source of truth: `new Date().getFullYear()` injected at page load. Excluded: COMMIT.txt (git captures the moment).

**Categories**:

| Cat | Where | Action |
|-----|-------|--------|
| **A** | Footer ©, byline, meta-line "City · YYYY" | Replace with `<span class="current-year"></span>` + IIFE injection |
| **B** | Publication date, Schema.org datePublished, academic citation year | Keep hardcoded + `<!-- date historique fondatrice -->` adjacent |
| **meta-year** | `<meta name="description">` / `<meta property="og:description">` | Keep hardcoded (crawlers don't run JS) + `<!-- meta-year: maj manuelle au 1er janvier -->` |
| **JSON-LD** | datePublished, dateModified, citation inside `<script type="application/ld+json">` | Comment-block BEFORE the script tag (HTML comments inside JSON would break it) |
| **snapshot** | "for 2025 / pour 2025" article millésime | Keep + `<!-- millésime article, fixe -->` |
| **dataset** | "INE 2024 data" | Keep + `<!-- millésime dataset INE, fixe -->` |
| **forecast** | "planned for second half of YYYY" obsolete | Rewrite without year, anchor on internal milestone + `<!-- jalon interne Sprint 1, sans date -->` |

**IIFE pattern** (end of `<script>` block, fr-FR or en-GB):

```js
(function() {
  const now = new Date();
  const dateLong = now.toLocaleDateString('fr-FR', { day: 'numeric', month: 'long', year: 'numeric' });
  const elDate = document.getElementById('links-checked-date');
  if (elDate) elDate.textContent = dateLong;
  const yr = now.getFullYear();
  document.querySelectorAll('#current-year, .current-year').forEach(el => { el.textContent = yr; });
})();
```

**Audit grep**: `grep -rn "202[0-9]" --include="*.html"` — every match must have an adjacent comment marker.

## §sources — Open data integrity

Each figure must link to its primary institutional source. Verification protocol:

```bash
curl -o /dev/null -s -w "%{http_code}" --max-time 12 -L \
  -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36..." \
  "$url"
```

- **200/301/302** → accept
- **404/500** → find replacement on same institutional domain (WebSearch with `allowed_domains`)
- **403/202** → anti-bot or async render — **keep URL**, add `<!-- 403 anti-bot curl — URL valide humain, vérifiée manuellement -->` before the `<li>`

**Never downgrade** to Wikipedia / press / blogs when a primary institutional source exists.

**Known anti-bot domains** (don't hunt alternatives):
- `oecd.org` / `oecd-ilibrary.org` (Cloudflare 403)
- `migrationdataportal.org` / `iom.int` (Cloudflare 403)
- `eur-lex.europa.eu` (async render 202)

**Sources block structure** (Section X, both articles): 5 thematic groups · `.sources-group` + `.sources-group-label` + `<ul>` of `<li>` with `<a>` + `.source-note` · footer `.sources-footer` with verification stats.

EN article includes Migration Policy Institute (peer-reviewed US/EU comparative data) in Group 3 — absent from FR.

## §design — Tokens

Brand triptych (in `:root`):
```css
--oive-gold:      #c49a2a
--oive-green-live:#4dcc66
--oive-night:     #1a2d4a
--oive-void:      #09100a   (background)
```

Fonts: Playfair Display (`--font-ed`) · Libre Baskerville (`--font-body`) · Spectral (`--font-essay`) · JetBrains Mono (`--font-data`).

Domain structure: single domain `sokohost.com/fr/` + `sokohost.com/en/` with hreflang — never sub-domains.

Six corridors at launch: MAR-ES, SEN-FR, UKR-DE, IND-NL, BGD-IT, TUN-FR. Core ratio: ×6 to ×8 local-vs-remittance.

## Editorial discipline

- **Fusion ciblée over mechanical retranslation** — when an EN file is already authored, propose surgical patches with section-by-section audit, never silent rewrite.
- **Always show diff/categorization table BEFORE writing** — when a patch could touch TOC, anchors, pronoun antecedents, or visible text. Stop on doubt.
- **Three-options offering on cascading edits** — when a "replace just this sentence" creates a downstream coherence issue, offer strict/extended/insert-instead and let user choose.

## Language

Respond in French unless the user writes in English.
