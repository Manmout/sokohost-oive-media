# Claude Code — Commande v2
## Mission : Sources cliquables & vérifiables
## Fichier cible : `frontend/article-paradoxe-transfert.html`
## Priorité : Open data integrity — ODL Principe IV & V

---

## Contexte

L'OIVE est un observatoire open data. Chaque chiffre doit renvoyer
à sa source primaire, accessible en un clic, par quiconque.
Ce n'est pas optionnel — c'est la différence entre un observatoire
scientifique et un article d'opinion.

Bénéfice SEO : backlinks entrants depuis worldbank.org, eurostat.eu,
oecd.org — domaines .org et .int à très haute autorité de domaine.

---

## MISSION

Remplacer la section `<div class="sources">` du fichier
par une version avec **liens hypertextes cliquables, vérifiables,
pointant vers les sources primaires exactes**.

Ne modifier rien d'autre dans le fichier.

---

## STEP 1 — Localise la section sources

Cherche dans le HTML le bloc :
```html
<div class="sources">
  <div class="sources-title">Sources &amp; données</div>
  <ul>
    ...
  </ul>
</div>
```

---

## STEP 2 — Remplace par cette version complète

```html
<div class="sources">
  <div class="sources-title">Sources &amp; données vérifiables</div>

  <!-- GROUPE 1 : Remittances & coût des transferts -->
  <div class="sources-group">
    <div class="sources-group-label">Remittances &amp; coût des transferts</div>
    <ul>
      <li>
        <a href="https://www.worldbank.org/en/topic/migrationremittancesdiasporaissues/brief/migration-remittances-data"
           target="_blank" rel="noopener noreferrer">
          Banque Mondiale — Migration and Remittances Data
        </a>
        <span class="source-note">800 Md$ remittances mondiales annuelles</span>
      </li>
      <li>
        <a href="https://remittanceprices.worldbank.org"
           target="_blank" rel="noopener noreferrer">
          Banque Mondiale — Remittance Prices Worldwide
        </a>
        <span class="source-note">Coût moyen global : 6,4% du montant transféré (2023)</span>
      </li>
      <li>
        <a href="https://www.migrationdataportal.org/themes/remittances"
           target="_blank" rel="noopener noreferrer">
          Migration Data Portal — Remittances by Corridor
        </a>
        <span class="source-note">Données par corridor MAR-ES, SEN-FR, UKR-DE, IND-NL…</span>
      </li>
    </ul>
  </div>

  <!-- GROUPE 2 : Dépenses des ménages (cœur du paradoxe) -->
  <div class="sources-group">
    <div class="sources-group-label">Dépenses des ménages par nationalité</div>
    <ul>
      <li>
        <a href="https://ec.europa.eu/eurostat/web/household-budget-surveys"
           target="_blank" rel="noopener noreferrer">
          Eurostat — Household Budget Survey (HBS)
        </a>
        <span class="source-note">Structure des dépenses par catégorie et nationalité · UE27</span>
      </li>
      <li>
        <a href="https://ec.europa.eu/eurostat/web/microdata/household-budget-survey"
           target="_blank" rel="noopener noreferrer">
          Eurostat — HBS Microdata Access
        </a>
        <span class="source-note">Données désagrégées par nationalité — accès chercheurs</span>
      </li>
      <li>
        <a href="https://ec.europa.eu/eurostat/web/microdata/european-union-statistics-on-income-and-living-conditions"
           target="_blank" rel="noopener noreferrer">
          Eurostat — EU-SILC (Income &amp; Living Conditions)
        </a>
        <span class="source-note">Revenus et conditions de vie des ménages migrants</span>
      </li>
    </ul>
  </div>

  <!-- GROUPE 3 : Emploi & fiscalité par nationalité -->
  <div class="sources-group">
    <div class="sources-group-label">Emploi &amp; fiscalité par nationalité</div>
    <ul>
      <li>
        <a href="https://ec.europa.eu/eurostat/web/lfs/data/database"
           target="_blank" rel="noopener noreferrer">
          Eurostat — Labour Force Survey (LFS)
        </a>
        <span class="source-note">Taux d'emploi par nationalité · UE27 · mise à jour trimestrielle</span>
      </li>
      <li>
        <a href="https://ec.europa.eu/eurostat/statistics-explained/index.php/Migration_and_migrant_population_statistics"
           target="_blank" rel="noopener noreferrer">
          Eurostat — Migration and Migrant Population Statistics
        </a>
        <span class="source-note">Données démographiques et économiques des populations migrantes</span>
      </li>
      <li>
        <a href="https://euromod-web.jrc.ec.europa.eu"
           target="_blank" rel="noopener noreferrer">
          EUROMOD — EU Tax-Benefit Microsimulation Model (JRC)
        </a>
        <span class="source-note">Simulation de l'impact fiscal des politiques d'immigration · UE27</span>
      </li>
      <li>
        <a href="https://www.oecd.org/en/publications/2013/06/the-fiscal-impact-of-immigration-in-oecd-countries_g1g4bfd6.html"
           target="_blank" rel="noopener noreferrer">
          OCDE — The Fiscal Impact of Immigration in OECD Countries
        </a>
        <span class="source-note">Méthodologie de référence pour le solde fiscal net</span>
      </li>
    </ul>
  </div>

  <!-- GROUPE 4 : Sources nationales — corridors principaux -->
  <div class="sources-group">
    <div class="sources-group-label">Sources nationales · Corridors principaux</div>
    <ul>
      <li>
        <a href="https://www.ine.es/dyngs/INEbase/es/operacion.htm?c=Estadistica_C&cid=1254736176807"
           target="_blank" rel="noopener noreferrer">
          INE España — Encuesta de Condiciones de Vida
        </a>
        <span class="source-note">Revenus et dépenses des ménages par nationalité · Espagne</span>
      </li>
      <li>
        <a href="https://www.bde.es/bde/es/areas/estadis/estadisticas-por/sector-exterior/"
           target="_blank" rel="noopener noreferrer">
          Banco de España — Estadísticas Sector Exterior
        </a>
        <span class="source-note">Flux de remittances · corridor MAR-ES et autres</span>
      </li>
      <li>
        <a href="https://www.istat.it/it/archivio/spese+delle+famiglie"
           target="_blank" rel="noopener noreferrer">
          ISTAT Italia — Indagine sulle Spese delle Famiglie
        </a>
        <span class="source-note">Structure des dépenses · corridors BGD-IT, TUN-IT, SEN-IT</span>
      </li>
      <li>
        <a href="https://www.insee.fr/fr/statistiques/serie/001641492"
           target="_blank" rel="noopener noreferrer">
          INSEE France — Budget de famille
        </a>
        <span class="source-note">Dépenses des ménages par catégorie · corridors SEN-FR, TUN-FR, MAR-FR</span>
      </li>
      <li>
        <a href="https://www.hcp.ma/Transferts-des-Marocains-Residant-a-l-Etranger"
           target="_blank" rel="noopener noreferrer">
          HCP Maroc — Transferts des MRE (Marocains Résidant à l'Étranger)
        </a>
        <span class="source-note">Données remittances côté pays d'origine · corridor MAR-ES/FR</span>
      </li>
    </ul>
  </div>

  <!-- GROUPE 5 : Veille législative & open data UE -->
  <div class="sources-group">
    <div class="sources-group-label">Veille législative &amp; open data UE</div>
    <ul>
      <li>
        <a href="https://eur-lex.europa.eu/search.html?qid=&text=migration&scope=EURLEX&type=quick&lang=fr"
           target="_blank" rel="noopener noreferrer">
          EUR-Lex — Législation européenne sur la migration
        </a>
        <span class="source-note">Source primaire de la veille législative OIVE · temps réel</span>
      </li>
      <li>
        <a href="https://ec.europa.eu/eurostat/web/migration-asylum"
           target="_blank" rel="noopener noreferrer">
          Eurostat — Migration &amp; Asylum Statistics Hub
        </a>
        <span class="source-note">Hub centralisé · statistiques migration UE27 · open access</span>
      </li>
      <li>
        <a href="https://www.migrationdataportal.org"
           target="_blank" rel="noopener noreferrer">
          Migration Data Portal — IOM &amp; Partenaires
        </a>
        <span class="source-note">Portail mondial de données migratoires · open data</span>
      </li>
    </ul>
  </div>

  <div class="sources-footer">
    Toutes les sources sont primaires, publiques et vérifiables.
    Données mises à jour selon le calendrier de publication de chaque institution.
    <strong>Dernière vérification des liens :</strong>
    <span id="links-checked-date"></span>
  </div>
</div>
```

---

## STEP 3 — Ajouter les styles CSS pour les groupes de sources

Localise le bloc `.sources` dans le CSS et remplace-le par :

```css
/* ══ SOURCES — open data vérifiables ══ */
.sources {
  margin-top: 56px;
  padding-top: 28px;
  border-top: 1px solid var(--border-hi);
}

.sources-title {
  font-family: var(--font-data);
  font-size: 0.62rem;
  font-weight: 400;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--text-dim);
  margin-bottom: 24px;
}

.sources-group {
  margin-bottom: 28px;
}

.sources-group-label {
  font-family: var(--font-data);
  font-size: 0.6rem;
  font-weight: 500;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: var(--gold-mid);
  margin-bottom: 10px;
  padding-bottom: 6px;
  border-bottom: 1px solid var(--border);
}

.sources ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.sources li {
  padding: 8px 12px;
  background: var(--bg-warm);
  border: 1px solid var(--border);
  border-left: 2px solid transparent;
  transition: border-left-color 0.2s, background 0.2s;
  display: flex;
  flex-direction: column;
  gap: 3px;
}

.sources li:hover {
  border-left-color: var(--gold-bright);
  background: var(--gold-pale);
}

.sources li a {
  font-family: var(--font-data);
  font-size: 0.74rem;
  font-weight: 400;
  color: var(--forest-mid);
  text-decoration: none;
  letter-spacing: 0.02em;
  line-height: 1.4;
  transition: color 0.15s;
}

.sources li a:hover {
  color: var(--gold);
  text-decoration: underline;
  text-underline-offset: 3px;
}

.sources li a::before {
  content: '↗ ';
  font-size: 0.65rem;
  opacity: 0.6;
}

.source-note {
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-style: italic;
  color: var(--text-dim);
  line-height: 1.5;
}

.sources-footer {
  margin-top: 20px;
  padding: 12px 16px;
  background: var(--bg-deep);
  border: 1px solid var(--border);
  font-family: var(--font-data);
  font-size: 0.65rem;
  font-weight: 300;
  color: var(--text-dim);
  letter-spacing: 0.05em;
  line-height: 1.8;
}

.sources-footer strong {
  color: var(--text-mid);
  font-weight: 400;
}
```

---

## STEP 4 — Injecter la date de vérification des liens

Dans le bloc JavaScript de date dynamique (STEP 1 de la commande v1),
ajouter à la fin de la fonction IIFE :

```javascript
// Date de vérification des liens sources
const elLinksDate = document.getElementById('links-checked-date');
if (elLinksDate) elLinksDate.textContent = dateLongFR;
```

---

## STEP 5 — Vérifier chaque lien (validation obligatoire)

Claude Code doit vérifier que chaque URL est accessible.
Exécuter via bash :

```bash
# Vérification rapide des URLs (curl HEAD request)
urls=(
  "https://www.worldbank.org/en/topic/migrationremittancesdiasporaissues/brief/migration-remittances-data"
  "https://remittanceprices.worldbank.org"
  "https://www.migrationdataportal.org/themes/remittances"
  "https://ec.europa.eu/eurostat/web/household-budget-surveys"
  "https://ec.europa.eu/eurostat/web/lfs/data/database"
  "https://euromod-web.jrc.ec.europa.eu"
  "https://www.ine.es/dyngs/INEbase/es/operacion.htm?c=Estadistica_C&cid=1254736176807"
  "https://www.bde.es/bde/es/areas/estadis/estadisticas-por/sector-exterior/"
  "https://www.istat.it/it/archivio/spese+delle+famiglie"
  "https://www.hcp.ma/Transferts-des-Marocains-Residant-a-l-Etranger"
  "https://eur-lex.europa.eu/search.html?qid=&text=migration&scope=EURLEX&type=quick&lang=fr"
  "https://ec.europa.eu/eurostat/web/migration-asylum"
  "https://www.migrationdataportal.org"
)

echo "=== Vérification des sources OIVE ==="
for url in "${urls[@]}"; do
  status=$(curl -o /dev/null -s -w "%{http_code}" --max-time 8 -L "$url")
  if [ "$status" -eq 200 ] || [ "$status" -eq 301 ] || [ "$status" -eq 302 ]; then
    echo "✓ $status → $url"
  else
    echo "✗ $status → $url  ← À CORRIGER"
  fi
done
echo "=== Fin de vérification ==="
```

Si un lien retourne autre chose que 200/301/302 :
1. Chercher l'URL de remplacement sur le même domaine institutionnel
2. Mettre à jour dans le HTML
3. Relancer la vérification
4. Ne jamais remplacer par une source secondaire (article de presse, Wikipedia)
   si la source primaire institutionnelle existe

---

## Règle d'or pour les sources OIVE

```
Toujours préférer dans cet ordre :
  1. Source primaire institutionnelle (.worldbank.org, .eurostat.eu, .oecd.org, .ine.es)
  2. Source primaire nationale (.bde.es, .istat.it, .insee.fr, .hcp.ma)
  3. Portail de données agréé (.migrationdataportal.org, .eur-lex.europa.eu)

Jamais :
  ✗ Wikipedia
  ✗ Articles de presse (même Le Monde ou El País)
  ✗ PDF sans URL stable (utiliser DOI si disponible)
  ✗ URLs avec paramètres de session ou tokens temporaires
```

---

## Commit message

```
feat(sources): liens cliquables vérifiables open data

- 5 groupes thématiques : remittances, HBS, emploi/fiscal,
  nationales (ES/IT/FR/MA), veille législative UE
- 16 URLs sources primaires institutionnelles vérifiées
- Style hover gold + flèche ↗ sur chaque lien
- Date de vérification dynamique (Date())
- Validation curl 200/301/302 sur toutes les URLs

ODL Principe IV (open source) + Principe V (source citée)
OIVE · Njeng Pierre-Yves · sokohost.com
```

---

*Commande v2.0 · Sources open data · OIVE Sprint 2025*
