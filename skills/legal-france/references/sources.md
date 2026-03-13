# Legal Database Search Guide — France & EU

This reference covers the primary legal databases for French and European law: what each contains, how to search it, and how to cite decisions found there.

---

## 1. Légifrance

**URL:** https://www.legifrance.gouv.fr
**Operator:** Direction de l'information légale et administrative (DILA)

### What it contains
- All French legislation in force: codes, lois, ordonnances, décrets, arrêtés
- Consolidated versions of codes (with amendment history)
- Official Journal (Journal officiel de la République française — JORF)
- Case law from: Cour de cassation, Conseil d'État, cours d'appel, tribunaux administratifs, Conseil constitutionnel
- Collective labor agreements (conventions collectives)
- European texts transposed into French law

### How to search
- **Free text search:** Use the search bar at the top. Filter by category (Codes, Jurisprudence, Textes, etc.)
- **Browse a code:** Go to "Codes en vigueur" → select the code → navigate by book/title/chapter
- **Search by article number:** Enter the article number directly (e.g., "article 1240 code civil")
- **Search case law:** Go to "Jurisprudence" → filter by court, date range, or keywords
- **Search by decision number:** For Cour de cassation, use the pourvoi number; for Conseil d'État, use the requête number

### URL patterns
- Code article: `https://www.legifrance.gouv.fr/codes/article_lc/[LEGIARTI_ID]`
- Code section: `https://www.legifrance.gouv.fr/codes/section_lc/[LEGISCTA_ID]`
- Full code: `https://www.legifrance.gouv.fr/codes/id/[LEGITEXT_ID]`
- JORF text: `https://www.legifrance.gouv.fr/jorf/id/[JORFTEXT_ID]`
- Cour de cassation decision: `https://www.legifrance.gouv.fr/juri/id/[JURITEXT_ID]`

### Decision citation formats

**Cour de cassation:**
```
Cass. [chambre], [date], n° [pourvoi]
```
- Chambre abbreviations: `civ. 1re`, `civ. 2e`, `civ. 3e`, `com.`, `soc.`, `crim.`, `ass. plén.`, `ch. mixte`, `ch. réunies`
- Date format: `DD [month abbrev.] YYYY` (e.g., `12 janv. 2023`)
- Pourvoi number format: `YY-NN.NNN` (e.g., `21-12.345`)
- Full example: `Cass. civ. 1re, 12 janv. 2023, n° 21-12.345`
- Published in Bulletin: add `Bull. civ. I, n° [N]` for pre-2017 decisions

**Conseil d'État:**
```
CE, [formation], [date], n° [requête], [nom de l'affaire]
```
- Formation abbreviations: `Ass.` (Assemblée), `Sect.` (Section), `ord.` (ordonnance de référé)
- Example: `CE Ass., 20 oct. 1989, n° 108243, Nicolo`
- Published decisions add: `Rec. CE p. [page]` or `Lebon p. [page]`

**Conseil constitutionnel:**
```
Cons. const., [date], n° [year]-[number] [type]
```
- Decision types: `DC` (contrôle a priori), `QPC` (question prioritaire de constitutionnalité), `LP` (loi du pays), `L` (déclassement)
- Example (DC): `Cons. const., 16 juil. 1971, n° 71-44 DC`
- Example (QPC): `Cons. const., 28 mai 2010, n° 2010-1 QPC`

---

## 2. EUR-Lex

**URL:** https://eur-lex.europa.eu
**Operator:** Publications Office of the European Union

### What it contains
- All EU legislation: règlements (regulations), directives, décisions (decisions)
- Official Journal of the EU (OJ/JOUE): L series (legislation), C series (information/notices)
- CJEU (Court of Justice of the EU) and General Court case law
- Consolidated versions of EU acts
- Preparatory documents (COM documents, legislative proposals)
- International agreements to which the EU is a party

### How to search
- **Free text search:** Use the search bar; filter by resource type, year, author institution
- **Search by CELEX number:** Directly enter the CELEX number in the search bar
- **Browse by subject matter:** Use the EuroVoc thesaurus classification
- **Search case law:** Go to "Case law" → filter by court, year, subject
- **Search by case number:** Enter the case number (e.g., `C-311/18`)

### CELEX number format
```
[Sector][Year][Document type][Number]
```
- Sector: `1` = Treaties, `2` = International agreements, `3` = Secondary legislation, `6` = CJEU case law, `7` = General Court, `8` = Civil Service Tribunal
- Document types for sector 3: `L` = regulation, `L` = directive (distinguished by number range), `D` = decision, `R` = regulation
- Example (regulation): `32016R0679` = GDPR (Regulation 2016/679)
- Example (directive): `31995L0046` = Data Protection Directive 95/46/EC
- Example (CJEU judgment): `62018CJ0673` = Planet49, Case C-673/17 (sector 6, year 2018 filing, CJ = Court of Justice judgment)

### Citation format — CJEU decisions
```
CJUE [or CJCE pre-Lisbon], [date], [name], aff. [C-/T-number]
```
- CJCE = Cour de justice des Communautés européennes (pre-1 Dec 2009)
- CJUE = Cour de justice de l'Union européenne (post-1 Dec 2009)
- Example: `CJCE, 5 févr. 1963, Van Gend en Loos, aff. 26/62`
- Example: `CJUE, 16 juil. 2020, Schrems II, aff. C-311/18`

---

## 3. Conseil constitutionnel

**URL:** https://www.conseil-constitutionnel.fr

### What it contains
- All decisions (DC, QPC, L, LP, FNR, I, ELEC, REF, AN, SEN)
- Press releases and dossiers documentaires for major decisions
- QPC transmissions and filtering decisions from Cour de cassation and Conseil d'État
- Commentaries in the Cahiers du Conseil constitutionnel (official doctrinal notes)
- Constitution of 4 October 1958 and the bloc de constitutionnalité texts

### How to search
- **By decision number:** Use the search field with the format `[year]-[number] DC` or `[year]-[number] QPC`
- **By theme:** Use the classification by subject or keyword
- **QPC tracker:** Dedicated section showing pending and decided QPCs
- **Chronological browsing:** Filter by year and decision type

### Key URL pattern
`https://www.conseil-constitutionnel.fr/decision/[year]/[number][type].htm`
Example: `https://www.conseil-constitutionnel.fr/decision/1971/7144DC.htm`

---

## 4. CNIL

**URL:** https://www.cnil.fr
**Operator:** Commission nationale de l'informatique et des libertés

### What it contains
- Délibérations (deliberations): formal decisions, authorizations, recommendations, sanctions
- Referential documents (guides, fiches pratiques) on GDPR compliance
- Sanctions and formal notices (mises en demeure)
- Annual reports
- Guidelines on specific topics (cookies, health data, AI, etc.)
- Standard simplified norms (now mostly replaced by GDPR guidelines)

### How to search
- **Sanctions:** Go to "Espace professionnel" → "Les sanctions de la CNIL" for the full list of sanctioned entities
- **Deliberations:** Use the search bar with keywords + filter by document type "Délibération"
- **By registration number:** Délibérations are numbered as `n° [year]-[NNN]` (e.g., `n° 2019-001`)
- **Guides:** Browse by theme (e.g., "cookies et traceurs", "sous-traitance", "droits des personnes")

### Citation format
```
CNIL, [date], délibération n° [year]-[NNN], [name/subject]
```
Example: `CNIL, 21 janv. 2019, délibération n° 2019-001, Google LLC`

---

## 5. Service-public.fr

**URL:** https://www.service-public.fr
**Operator:** DILA (Direction de l'information légale et administrative)

### What it contains
- Plain-language explanations of administrative procedures for individuals and businesses
- Step-by-step guides for legal procedures (divorce, succession, contract disputes, etc.)
- Official forms (cerfa) and downloadable documents
- Information on rights and obligations in everyday situations
- Links to competent administrative authorities

### How to search
- Use the search bar with everyday language (e.g., "licenciement", "contester une amende")
- Browse by theme: "Particuliers", "Professionnels", "Associations"
- Direct links to competent tribunals and administrative bodies
- Note: Not a primary legal source — use for orientation and procedure steps, not for legal argument

---

## 6. Conseil d'État

**URL:** https://www.conseil-etat.fr

### What it contains
- Full text of Conseil d'État decisions (Assemblée, Section, sous-sections réunies, ordonnances de référé)
- Avis contentieux and avis consultatifs
- Annual reports and études (policy studies)
- Legal guides on administrative law
- Database of administrative case law (searchable by keyword, date, requête number)

### How to search
- **By requête number:** Use the search tool with the 6-digit requête number (e.g., `108243`)
- **By keywords:** Full-text search across all decisions
- **Lebon tables:** The annual Recueil Lebon tables are available online for published decisions
- **Arianeweb:** The integrated jurisprudence search tool at `https://www.conseil-etat.fr/fr/recherche-avancee-en-jurisprudence`

### Citation format
See Légifrance section above. The requête number is the key identifier.

---

## 7. Cour de cassation

**URL:** https://www.courdecassation.fr

### What it contains
- Full text of all Cour de cassation decisions (published and unpublished)
- Bulletin civil and Bulletin criminel (published/selected decisions with headnotes)
- Avis de la Cour de cassation
- Rapports annuels
- Communiqués de presse for major decisions
- Judicial committee reports (rapports de conseiller, avis d'avocat général)

### How to search
- **By pourvoi number:** Use the dedicated search; enter the pourvoi number in format `YY-NN.NNN`
- **By ECLI:** European Case Law Identifier format `ECLI:FR:CCASS:[YEAR]:[CHAMBER][NUMBER]`
- **Advanced search:** Filter by chambre, date range, publication status (P = publié au Bulletin, R = mentionné, D = diffusé)
- **Publication indicators:**
  - `P` (or `B`) = published in the Bulletin (leading decision)
  - `R` = mentioned in the Bulletin tables
  - `D` = diffusé (available online but not in Bulletin)
  - `I` = inédit (unpublished, internal use)

### Citation format
See Légifrance section above. For published decisions, the Bulletin reference adds authority:
```
Cass. civ. 1re, 12 janv. 2023, n° 21-12.345, Bull. civ. I, n° 5
```

---

## Cross-database search tips

| Goal | Primary source | Secondary source |
|------|---------------|-----------------|
| Find current text of a French code article | Légifrance (consolidated codes) | Service-public.fr (plain language) |
| Find a Cour de cassation decision by pourvoi | courdecassation.fr | Légifrance |
| Find a Conseil d'État decision | conseil-etat.fr (Arianeweb) | Légifrance |
| Find a QPC decision | conseil-constitutionnel.fr | Légifrance |
| Find an EU regulation or directive | EUR-Lex | Légifrance (transposition) |
| Find a CJEU judgment | EUR-Lex | EUR-Lex case law section |
| Find a CNIL sanction | cnil.fr | Légifrance (if published in JORF) |
| Check administrative procedure steps | service-public.fr | Code de justice administrative on Légifrance |
