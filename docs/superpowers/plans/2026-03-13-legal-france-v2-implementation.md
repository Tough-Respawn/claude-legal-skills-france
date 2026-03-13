# legal-france v2 Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Upgrade legal-france plugin with complex case handling, mandatory web verification, and enriched references.

**Architecture:** Surgical approach — modify 14 existing files, create 0 new files. SKILL.md gets two new protocol blocks. methodology.md gets a 7th template. All 12 reference files get enriched content.

**Tech Stack:** Claude Code plugin (Markdown-only, no code). All files are `.md` in `plugins/legal-france/`.

**Spec:** `docs/superpowers/specs/2026-03-13-legal-france-v2-design.md`

---

## File Map

All paths relative to repo root (`c:\Users\Amine\Documents\legal-skills-france\`).

| File | Action | Responsibility |
|------|--------|----------------|
| `plugins/legal-france/skills/legal-france/SKILL.md` | Modify | Add Complex Case Protocol + modify Research Protocol + update Response Protocol |
| `plugins/legal-france/skills/legal-france/methodology.md` | Modify | Add Template #7 "Cas complexe" |
| `plugins/legal-france/skills/legal-france/references/civil.md` | Modify | Enrich to ~50-60 articles, 12-15 decisions, add reforms |
| `plugins/legal-france/skills/legal-france/references/penal.md` | Modify | Enrich to ~50-60 articles, 12-15 decisions, add reforms |
| `plugins/legal-france/skills/legal-france/references/travail.md` | Modify | Enrich to ~50-60 articles, 12-15 decisions, add reforms |
| `plugins/legal-france/skills/legal-france/references/affaires.md` | Modify | Enrich to ~50-60 articles, 12-15 decisions, add reforms |
| `plugins/legal-france/skills/legal-france/references/administratif.md` | Modify | Enrich to ~50-60 articles, 12-15 decisions, add reforms |
| `plugins/legal-france/skills/legal-france/references/numerique.md` | Modify | Enrich to ~50-60 articles, 12-15 decisions, add reforms |
| `plugins/legal-france/skills/legal-france/references/europeen.md` | Modify | Enrich to ~50-60 articles, 12-15 decisions, add reforms |
| `plugins/legal-france/skills/legal-france/references/procedure.md` | Modify | Enrich to ~50-60 articles, 12-15 decisions, add reforms |
| `plugins/legal-france/skills/legal-france/references/codes-index.md` | Modify | Add parties/livres/titres structure |
| `plugins/legal-france/skills/legal-france/references/jurisprudence-cle.md` | Modify | Expand to 12-15 decisions per domain |
| `plugins/legal-france/skills/legal-france/references/glossaire.md` | Modify | Expand to ~150-180 terms |
| `plugins/legal-france/skills/legal-france/references/sources.md` | Modify | Add domain-specific search tips |

---

## Chunk 1: Core Logic (SKILL.md + methodology.md)

### Task 1: Add Complex Case Protocol to SKILL.md

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/SKILL.md` (insert between lines 86-87, after Research Protocol, before Response Protocol)

- [ ] **Step 1: Insert Complex Case Protocol block**

Insert the following new section between the `## Research Protocol` section (ends at line 86) and the `## Response Protocol` section (starts at line 88):

```markdown
---

## Complex Case Protocol

When ANY of the following conditions is detected, activate complex case handling:

- **Multi-domain:** 2+ domains identified in Domain Routing (e.g., keywords matching both `travail` and `numerique`)
- **Causal chain:** User describes a sequence where one legal outcome feeds into the next (e.g., contract → nullity → restitution → prescription)
- **Norm conflict:** Tension between French and EU law, two contradictory articles, or competing fundamental rights (e.g., liberté d'expression vs. droit à l'image)

**When triggered, follow these steps in order:**

1. **Decompose** — Identify and number each distinct legal issue (problème de droit). Present as a numbered list before proceeding.
2. **Load all implicated domains** — Read ALL reference files for every domain concerned. **Context bound:** if more than 3 domains are implicated, load the primary domain in full and load only the Key Articles and Landmark Decisions sections from secondary domains.
3. **Treat sequentially** — Apply the full syllogism (Majeure → Mineure → Conclusion) to each issue independently, in the order listed.
4. **Cross-synthesis** — Analyze interactions between issues: does resolving issue #1 change the answer to issue #3? Are there contradictions? What is the priority order of norms?
5. **Force template #7** — Use the "Cas complexe" template from `methodology.md` instead of the role-default template. **Priority rule:** this overrides role-default and nature-default template selection (Response Protocol priorities 2 and 3), but does NOT override explicit command-triggered templates (priority 1). If a command is used AND a complex case is detected, use the command's template but incorporate the Synthèse croisée section from template #7 as an addendum.

```

- [ ] **Step 2: Modify Research Protocol Step 2 — make web verification mandatory**

Replace lines 69-75 of SKILL.md (the current Step 2):

**Old text (lines 69-75):**
```
**Step 2 — Use web tools if available**
If WebSearch or WebFetch tools are available, search the following priority sources:
- `legifrance.gouv.fr` — consolidated legislation, case law (Cour de cassation, Conseil d'État, Cour d'appel)
- `eur-lex.europa.eu` — EU regulations and directives
- `conseil-constitutionnel.fr` — constitutional decisions (QPC, DC)
- `cnil.fr` — data protection guidance and decisions
- `service-public.fr` — administrative procedures (useful for citizen-role responses)
```

**New text:**
```
**Step 2 — Mandatory web verification**
Even if an article or decision is found in embedded references, cross-check it using WebSearch or WebFetch against these priority sources (in order):
- `legifrance.gouv.fr` — consolidated legislation, case law (Cour de cassation, Conseil d'État, Cour d'appel)
- `eur-lex.europa.eu` — EU regulations and directives
- `conseil-constitutionnel.fr` — constitutional decisions (QPC, DC)
- `cnil.fr` — data protection guidance and decisions
- `service-public.fr` — administrative procedures (useful for citizen-role responses)

If WebSearch/WebFetch tools are not available, or if the verification query fails or returns inconclusive results, display this warning before the response:
> ⚠️ Je n'ai pas pu vérifier en ligne la version en vigueur des articles cités. Les références proviennent de données embarquées qui peuvent ne pas refléter les modifications récentes. Vérifiez sur legifrance.gouv.fr.

**Step 2bis — Divergence handling**
When a locally referenced article has been modified according to the web source: use the web version (most current) and signal the divergence:
> Note : l'article X a été modifié depuis la dernière mise à jour de mes références embarquées. Je cite la version en vigueur consultée sur Legifrance.
```

- [ ] **Step 3: Update Response Protocol for template #7 priority**

Add the following paragraph after line 96 of SKILL.md (after `Read skills/legal-france/methodology.md for the full template specifications before composing your response.`), before the `---` separator:

```
**Complex Case override:** When the Complex Case Protocol (above) is triggered, template #7 (Cas complexe) overrides the role-based and nature-based default (priorities 2 and 3). Command-triggered templates (priority 1) are NOT overridden — instead, append the Synthèse croisée section from template #7 as an addendum.
```

- [ ] **Step 4: Verify SKILL.md word count**

Run: `wc -w plugins/legal-france/skills/legal-france/SKILL.md`
Expected: ~1,750-1,900 words (must be under 5,000)

- [ ] **Step 5: Commit SKILL.md changes**

```bash
git add plugins/legal-france/skills/legal-france/SKILL.md
git commit -m "feat(v2): add complex case protocol + mandatory web verification to SKILL.md"
```

---

### Task 2: Add Template #7 to methodology.md

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/methodology.md` (append after line 344, after Template 6)

- [ ] **Step 1: Update the file header**

Replace line 3 of methodology.md:
**Old:** `This file defines the six structured response templates used by the legal-france skill.`
**New:** `This file defines the seven structured response templates used by the legal-france skill.`

- [ ] **Step 2: Append Template #7 after the closing of Template 6**

Append the following after line 344 (the closing backtick+newline of Template 6):

```markdown

---

## Template 7 — Cas complexe (Complex Case Analysis)

**Trigger conditions:**
- Triggered automatically by the Complex Case Protocol in SKILL.md
- Never triggered manually by a user command
- Overrides role-default and nature-default templates (priorities 2 and 3 of Response Protocol)
- Does NOT override command-triggered templates (priority 1) — in that case, the command's template is used but section 4 (Synthèse croisée) is appended as an addendum

**Tone:** Adapts to detected user role:
- `lawyer` / `judge`: formal, complete, Latin maxims acceptable
- `student`: pedagogical, all reasoning steps visible, methodology explained
- `citizen`: accessible, plain language, practical focus
- `business`: risk-oriented, compliance-focused, concrete recommendations

**Section structure:**

### 1. Cartographie des problèmes de droit (Issue Mapping)
Identify and number each distinct legal issue. Present as a table:

| N° | Problème de droit | Domaine(s) | Lié à |
|----|-------------------|------------|-------|
| 1  | [Issue description] | [Domain(s)] | — |
| 2  | [Issue description] | [Domain(s)] | N°1 |

This section sets the structure for the entire analysis. Every issue identified here must be treated in section 2.

### 2. Analyse par problème (Per-Issue Analysis — repeated for each issue)
For each issue identified in section 1, apply the full syllogism:
- **Majeure** — State the applicable rule with full citations (article numbers, code name, version in force, leading case law)
- **Mineure** — Apply the rule to the specific facts. Test each element of the rule against the facts explicitly.
- **Conclusion intermédiaire** — State the legal outcome for this issue alone. This is a partial conclusion — the global conclusion comes in section 4.

Number each analysis to match the issue mapping: "**Problème n°1 :**", "**Problème n°2 :**", etc.

### 3. Résolution des conflits de normes (Norm Conflict Resolution)
**Conditional section — include ONLY if a norm conflict was detected. Skip entirely if all issues are independent.**

When rules contradict, resolve using (in order):
1. **Hierarchy of norms:** Constitution > EU Treaties and Regulations > Loi > Décret > Arrêté
2. **Principle of specialty:** lex specialis derogat legi generali — the more specific text prevails
3. **Chronology:** lex posterior derogat legi priori — the more recent text prevails (same-level norms only)

For each conflict: identify the competing norms, state which principle resolves the conflict, explain why one prevails, and cite the authority for this resolution (Constitutional Council decision, CJEU ruling, etc.).

### 4. Synthèse croisée (Cross-Synthesis)
**Conditional section — include ONLY if issues interact. If all issues are fully independent with no interactions, replace with a brief statement confirming their independence.**

Analyze how the intermediate conclusions from section 2 interact:
- Does resolving issue #1 change the analysis of issue #3?
- Are there cascade effects (one outcome triggering another)?
- What is the globally motivated conclusion when all issues are considered together?

This section must produce a unified conclusion that accounts for all issues simultaneously.

### 5. Solutions & recommandations (Solutions and Recommendations)
Concrete options accounting for ALL issues at once (not domain by domain). For each option:
- Action to take
- Legal basis
- Risks and likelihood of success
- Relevant deadlines (prescription, délai de forclusion, délai de recours)
- Priority level (urgent / normal / optional)

If recommending one option over others, explain why.

### 6. Mise en garde (Disclaimer)
Standard mandatory disclaimer in the user's language. Same as all other templates.

**Example skeleton:**

```
## Analyse de cas complexe

**Cartographie des problèmes de droit**

| N° | Problème | Domaine(s) | Lié à |
|----|----------|------------|-------|
| 1  | Le licenciement est-il justifié ? | Travail | — |
| 2  | La surveillance des e-mails était-elle licite ? | Numérique, Travail | N°1 |
| 3  | Le salarié peut-il invoquer la protection des lanceurs d'alerte ? | Pénal, Travail | N°1, N°2 |

**Problème n°1 : Le licenciement est-il justifié ?**
Majeure : Aux termes de l'art. L. 1232-1 C. trav., tout licenciement doit être justifié par une cause réelle et sérieuse...
Mineure : En l'espèce, l'employeur invoque la faute grave consistant en...
Conclusion intermédiaire : Le licenciement pour faute grave apparaît / n'apparaît pas justifié au regard de...

**Problème n°2 : La surveillance des e-mails était-elle licite ?**
Majeure : ...
Mineure : ...
Conclusion intermédiaire : ...

**Problème n°3 : Protection lanceur d'alerte ?**
Majeure : L'art. L. 1132-3-3 C. trav. (loi Sapin II) protège...
Mineure : ...
Conclusion intermédiaire : ...

**Résolution des conflits de normes**
Le droit à la vie privée du salarié (art. 8 CEDH, art. 9 C. civ.) entre en tension avec le pouvoir de contrôle de l'employeur (art. L. 1121-1 C. trav.)...
Résolution : La CEDH a posé le test de proportionnalité (CEDH, Barbulescu c. Roumanie, 2017)...

**Synthèse croisée**
Si la surveillance est déclarée illicite (problème n°2), les preuves obtenues sont irrecevables, ce qui affaiblit le fondement du licenciement (problème n°1). Par ailleurs, si la qualité de lanceur d'alerte est retenue (problème n°3), le licenciement constituerait une mesure de représailles prohibée...
Conclusion globale : ...

**Solutions & recommandations**
1. Contester le licenciement devant le CPH en soulevant les trois moyens conjointement...
2. Saisir la CNIL pour la surveillance illicite des e-mails...
Recommandation : Priorité à l'action 1 (délai de prescription : 12 mois, art. L. 1471-1 C. trav.)...

---
*Ces informations sont fournies à titre indicatif et ne constituent pas un avis juridique...*
```
```

- [ ] **Step 3: Commit methodology.md changes**

```bash
git add plugins/legal-france/skills/legal-france/methodology.md
git commit -m "feat(v2): add Template #7 Cas complexe to methodology.md"
```

---

## Chunk 2: Domain Reference Enrichment (8 files)

Each of the 8 domain reference files must be enriched following the same pattern:
- Expand from ~10-18 articles to ~50-60 articles
- Expand from 4-8 landmark decisions to 12-15 decisions
- Add a new `## Réformes récentes (2023-2026)` section at the end

**Enrichment principles (applies to ALL tasks in this chunk):**
- Articles selected by practical usage frequency (curated, not exhaustive)
- Case law: prioritize arrêts de principe (Assemblée plénière, Chambre mixte) and recent evolutions (2020-2026)
- Each added decision: date, pourvoi/requête number, 1-line summary, legal significance (portée)
- Each added article: number, summarized title, keywords for Domain Routing
- **Do NOT fabricate case law.** Use only well-known, widely-cited decisions. If unsure about a pourvoi number, omit it and note "à vérifier".
- Maintain the existing file structure and formatting conventions — just add more entries.

**Important:** Read each file FIRST to understand its current structure before editing. Preserve the existing content and add to it.

### Task 3: Enrich `civil.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/civil.md`
- Current size: 1,754 words → Target: ~4,000-5,000 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Expand Key Articles section** — Add articles covering: droit des obligations (1100-1231-7), responsabilité délictuelle (1240-1244), régimes matrimoniaux (1387+), successions (720+), droit des biens (544+), prescription (2224+), preuve (1353+). Target: ~50-60 total articles.
- [ ] **Step 3: Expand Landmark Decisions** — Add 8-10 more decisions. Must include: Jand'heur (1930), Desmares (1982), arrêt Blieck (1991), Perruche (2000), Chronopost (1996), Baldus (2000), Faurecia (2010), Costedoat (2000), Boot Shop (2001), Lemaire (2003). Target: 12-15 total.
- [ ] **Step 4: Add Réformes récentes section** — Cover: Ordonnance 2016-131 reform of obligations (entry into force), Loi 2024 on successions, any recent Cour de cassation shifts on responsabilité.
- [ ] **Step 5: Verify word count** — Run: `wc -w plugins/legal-france/skills/legal-france/references/civil.md` — Expected: ~4,000-5,000 words
- [ ] **Step 6: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/civil.md
git commit -m "feat(v2): enrich civil.md references — ~50 articles, 12+ decisions, reforms"
```

### Task 4: Enrich `penal.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/penal.md`
- Current size: 1,827 words → Target: ~4,000-5,000 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Expand Key Articles** — Add articles from: Code pénal (111-1 to 132-75 principes généraux, 221-1+ atteintes à la vie, 311-1+ vols, 313-1+ escroqueries, 321-1 recel, 226-1+ vie privée, 421-1+ terrorisme, 431-1+ attroupements) and Code de procédure pénale (63+ garde à vue, 137+ détention provisoire, 393+ comparution immédiate, 567+ pourvoi). Target: ~50-60 total.
- [ ] **Step 3: Expand Landmark Decisions** — Must include key arrêts on: élément moral (Laboube 1956), complicité, légitime défense, non bis in idem, nullités de procédure, QPC on garde à vue (2010). Target: 12-15 total.
- [ ] **Step 4: Add Réformes récentes section** — Cover: Loi confiance dans l'institution judiciaire (2021), réformes du CPP, comparution à délai différé, etc.
- [ ] **Step 5: Verify word count**
- [ ] **Step 6: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/penal.md
git commit -m "feat(v2): enrich penal.md references — ~50 articles, 12+ decisions, reforms"
```

### Task 5: Enrich `travail.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/travail.md`
- Current size: 2,036 words → Target: ~4,000-5,000 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Expand Key Articles** — Cover: formation du contrat (L.1221-1+), CDD (L.1242-1+), période d'essai (L.1221-19+), licenciement (L.1232-1+, L.1233-1+ éco), rupture conventionnelle (L.1237-11+), harcèlement (L.1152-1+), discrimination (L.1132-1+), temps de travail (L.3121-1+), congés (L.3141-1+), représentants du personnel (L.2311-1+), négociation collective (L.2231-1+). Target: ~50-60 total.
- [ ] **Step 3: Expand Landmark Decisions** — Must include: Nikon (2001), Brinon (1954), arrêt Société Générale (liberté vestimentaire), Baby Loup (2014), arrêt Aberkane (2013), Barbier (2004), arrêt Mr X télétravail. Target: 12-15 total.
- [ ] **Step 4: Add Réformes récentes section** — Cover: Ordonnances Macron (2017, barème Macron), loi avenir professionnel (2018), réforme assurance chômage (2023-2024), partage de la valeur (2023).
- [ ] **Step 5: Verify word count**
- [ ] **Step 6: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/travail.md
git commit -m "feat(v2): enrich travail.md references — ~50 articles, 12+ decisions, reforms"
```

### Task 6: Enrich `affaires.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/affaires.md`
- Current size: 2,289 words → Target: ~4,000-5,000 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Expand Key Articles** — Cover: Code de commerce (L.110-1+ actes de commerce, L.210-1+ sociétés, L.223-1+ SARL, L.225-1+ SA, L.227-1+ SAS, L.611-1+ procédures collectives, L.420-1+ concurrence), Code de la consommation (L.111-1+ information, L.121-1+ pratiques commerciales, L.217-1+ garantie), CPI (L.111-1+ droit d'auteur, L.611-1+ brevets, L.711-1+ marques). Target: ~50-60 total.
- [ ] **Step 3: Expand Landmark Decisions** — Must include: arrêts sur responsabilité des dirigeants, abus de majorité/minorité, extension de procédure collective, concurrence déloyale, parasitisme. Target: 12-15 total.
- [ ] **Step 4: Add Réformes récentes section** — Cover: loi PACTE (2019), réforme des sûretés (2021), loi Industrie verte (2023), DORA (2024).
- [ ] **Step 5: Verify word count**
- [ ] **Step 6: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/affaires.md
git commit -m "feat(v2): enrich affaires.md references — ~50 articles, 12+ decisions, reforms"
```

### Task 7: Enrich `administratif.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/administratif.md`
- Current size: 1,819 words → Target: ~4,000-5,000 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Expand Key Articles** — Cover: CJA (L.1+ compétence, L.211-1+ TA, L.311-1+ CAA, L.521-1+ référés, L.911-1+ injonctions), CRPA (L.100-1+ relations avec l'admin, L.211-1+ décisions, L.311-1+ accès aux documents), CGCT (L.2121-1+ commune, L.2212-1+ police municipale), Code de l'urbanisme, Code de l'environnement (L.110-1+). Target: ~50-60 total.
- [ ] **Step 3: Expand Landmark Decisions** — Must include: Blanco (1873), Cadot (1889), Nicolo (1989), Dehaene (1950), Barel (1954), Danthony (2011), Czabaj (2016), Tarn-et-Garonne (2014), GISTI (2012). Target: 12-15 total.
- [ ] **Step 4: Add Réformes récentes section** — Cover: Code des relations entre le public et l'administration, réforme des juridictions administratives, Czabaj et ses suites.
- [ ] **Step 5: Verify word count**
- [ ] **Step 6: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/administratif.md
git commit -m "feat(v2): enrich administratif.md references — ~50 articles, 12+ decisions, reforms"
```

### Task 8: Enrich `numerique.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/numerique.md`
- Current size: 2,491 words → Target: ~4,000-5,000 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Expand Key Articles** — Cover: RGPD (art. 1-99, focus on 5-9 principes, 12-22 droits, 24-43 responsable, 44-49 transferts, 77-84 recours), Loi Informatique et Libertés (LIL, art. 1-13), LCEN (art. 1-7 hébergeurs, 14+ e-commerce), Code pénal numérique (226-16+ données, 323-1+ STAD), DSA (art. 1-14), DMA, AI Act (principes). Target: ~50-60 total.
- [ ] **Step 3: Expand Landmark Decisions** — Must include: Google Spain (CJUE 2014 droit à l'oubli), Schrems I (2015) et II (2020), Planet49 (2019 cookies), Google LLC CNIL (2019), Fashion ID (2019), arrêts CNIL sanctions récentes. Target: 12-15 total.
- [ ] **Step 4: Add Réformes récentes section** — Cover: DSA/DMA entrée en application (2024), AI Act (2024), Data Act (2024), CNIL lignes directrices cookies (2024), jurisprudence CJUE transferts.
- [ ] **Step 5: Verify word count**
- [ ] **Step 6: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/numerique.md
git commit -m "feat(v2): enrich numerique.md references — ~50 articles, 12+ decisions, reforms"
```

### Task 9: Enrich `europeen.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/europeen.md`
- Current size: 2,436 words → Target: ~4,000-5,000 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Expand Key Articles** — Cover: TUE (art. 1-19), TFUE (art. 18-25 citoyenneté, 26-66 marché intérieur, 101-109 concurrence, 110-118 fiscalité, 119-144 UEM, 258-260 manquement, 267 renvoi préjudiciel, 340 responsabilité), Charte des droits fondamentaux (art. 1-54), CEDH (art. 1-18 droits, 34-35 requête, 41 satisfaction équitable). Target: ~50-60 total.
- [ ] **Step 3: Expand Landmark Decisions** — Must include: Van Gend en Loos (1963), Costa c. ENEL (1964), Simmenthal (1978), Francovich (1991), Factortame (1990), Kadi (2008), Melloni (2013), Åkerberg Fransson (2013), avis 2/13 (CEDH), Achmea (2018). Target: 12-15 total.
- [ ] **Step 4: Add Réformes récentes section** — Cover: traité de Lisbonne suites, mécanisme État de droit (art. 7 TUE), Conférence sur l'avenir de l'Europe, jurisprudence CJUE 2023-2025.
- [ ] **Step 5: Verify word count**
- [ ] **Step 6: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/europeen.md
git commit -m "feat(v2): enrich europeen.md references — ~50 articles, 12+ decisions, reforms"
```

### Task 10: Enrich `procedure.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/procedure.md`
- Current size: 1,740 words → Target: ~4,000-5,000 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Expand Key Articles** — Cover: CPC (1-24 principes directeurs, 31-32 intérêt à agir, 55-70 compétence, 117-121 nullités, 480+ jugements, 527+ appel, 604+ cassation, 808+ référés, 1442+ arbitrage), CPP (1-10 action publique, 40-44 procureur, 63-65 garde à vue, 137-150 détention, 393 comparution immédiate, 567+ pourvoi), CJA (L.1+ compétence, L.521-1+ référés admin, L.911-1+ injonctions). Target: ~50-60 total.
- [ ] **Step 3: Expand Landmark Decisions** — Must include: arrêts sur compétence, nullités, appel (décrets Magendie), pourvoi, exécution provisoire, arbitrage (Putrabali), médiation. Target: 12-15 total.
- [ ] **Step 4: Add Réformes récentes section** — Cover: réforme de la procédure civile (décret 2019-1333, exécution provisoire de droit), réforme de l'appel, procédure pénale numérique, audiences par visioconférence.
- [ ] **Step 5: Verify word count**
- [ ] **Step 6: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/procedure.md
git commit -m "feat(v2): enrich procedure.md references — ~50 articles, 12+ decisions, reforms"
```

---

## Chunk 3: Transversal Reference Enrichment (4 files)

### Task 11: Enrich `codes-index.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/codes-index.md`
- Current size: 3,845 words → Target: ~5,500-6,500 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Add parties/livres/titres structure** — For each code already listed, expand the article ranges into a hierarchical structure: `Partie → Livre → Titre → Chapitre` with article ranges. Focus on the 5 most-used codes: Code civil, Code pénal, Code du travail, Code de commerce, CJA.
- [ ] **Step 3: Verify word count**
- [ ] **Step 4: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/codes-index.md
git commit -m "feat(v2): enrich codes-index.md with hierarchical structure"
```

### Task 12: Enrich `jurisprudence-cle.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/jurisprudence-cle.md`
- Current size: 4,586 words → Target: ~7,000-8,000 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Expand to 12-15 decisions per domain** — Align with the decisions added in each domain file (Tasks 3-10). Every decision cited in a domain file should appear here too. Maintain the existing format: date, pourvoi, 1-line summary, portée.
- [ ] **Step 3: Add `procedure` section** — This domain was not in v1's jurisprudence-cle. Add a new section with the 12-15 procedure decisions from Task 10.
- [ ] **Step 4: Verify word count**
- [ ] **Step 5: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/jurisprudence-cle.md
git commit -m "feat(v2): enrich jurisprudence-cle.md — 12-15 decisions per domain"
```

### Task 13: Enrich `glossaire.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/glossaire.md`
- Current size: 4,197 words → Target: ~6,500-7,500 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Add procedural terms** — Add ~30 terms covering: action en justice, appel, cassation, référé, sursis à statuer, exception d'incompétence, fin de non-recevoir, autorité de la chose jugée, exécution provisoire, voies de recours, ministère public, partie civile, etc.
- [ ] **Step 3: Add EU law terms** — Add ~20 terms covering: renvoi préjudiciel, effet direct, primauté, subsidiarité, proportionnalité, directive, règlement, transposition, recours en manquement, question préjudicielle, marge d'appréciation, etc.
- [ ] **Step 4: Add digital/data terms** — Add ~15 terms covering: responsable de traitement, sous-traitant, DPO, AIPD, BCR, clauses contractuelles types, droit à l'oubli, profilage, consentement, hébergeur, éditeur, etc.
- [ ] **Step 5: Verify total** — Count total terms. Target: ~150-180.
- [ ] **Step 6: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/glossaire.md
git commit -m "feat(v2): expand glossaire.md to ~170 terms — procedural, EU, digital"
```

### Task 14: Enrich `sources.md`

**Files:**
- Modify: `plugins/legal-france/skills/legal-france/references/sources.md`
- Current size: 1,503 words → Target: ~2,500-3,000 words

- [ ] **Step 1: Read the current file**
- [ ] **Step 2: Add domain-specific search tips** — For each of the 8 domains, add a short section (3-5 lines) with: the best Legifrance search filters for that domain, specialized databases (e.g., DILA for admin, INPI for IP, CNIL deliberations for numerique), and search query examples.
- [ ] **Step 3: Add a section on EU sources** — Cover: EUR-Lex advanced search, CURIA (CJUE case law), HUDOC (ECHR), EU Official Journal.
- [ ] **Step 4: Verify word count**
- [ ] **Step 5: Commit**
```bash
git add plugins/legal-france/skills/legal-france/references/sources.md
git commit -m "feat(v2): enrich sources.md with domain-specific search tips"
```

---

## Execution Notes

**Parallelism:**
- Chunk 1 (Tasks 1-2) and Chunk 2 (Tasks 3-10) are independent — they can execute in parallel. Chunk 1 modifies SKILL.md and methodology.md; Chunk 2 modifies reference files. No overlap.
- Within Chunk 2 (Tasks 3-10), all 8 domain files are independent — execute in parallel.
- Within Chunk 3: Tasks 11, 13, 14 are independent of each other and of Chunks 1-2 — can start immediately. Task 12 (jurisprudence-cle) must execute AFTER Chunk 2 completes (to align decisions across domain files).

**Recommended execution order:**
1. Wave 1 (parallel): Chunk 1 (Tasks 1-2 sequential) + Chunk 2 (Tasks 3-10 parallel) + Tasks 11, 13, 14 from Chunk 3
2. Wave 2 (after Chunk 2 done): Task 12 (jurisprudence-cle alignment)

**Domain enrichment guidance (Tasks 3-10):**
- Append new entries at the end of each existing section, maintaining the same formatting pattern as existing entries.
- Do not reorder or restructure existing content — only add.

**Quality checks after all tasks:**
- `wc -w plugins/legal-france/skills/legal-france/SKILL.md` — must be under 5,000 words
- All 14 files must exist and be non-empty
- `git log --oneline` should show 14 commits (one per task)
- Final verification: read SKILL.md and confirm Complex Case Protocol references "template #7" and "methodology.md" correctly. Confirm all 8 domain files listed in Domain Routing exist in `references/`.
