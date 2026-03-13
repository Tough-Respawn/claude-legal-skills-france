# Legal France Plugin — Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the `legal-france` Claude Code plugin with 1 main skill, 9 commands, and domain-specific legal references for French law.

**Architecture:** Single skill (`legal-france`) with progressive disclosure — SKILL.md for core logic, `methodology.md` for response templates, `references/` for domain-specific legal knowledge. Commands are thin wrappers that invoke the skill with pre-filtered context.

**Tech Stack:** Markdown files only (Claude Code plugin standard). No code dependencies. Uses built-in tools (Read, Grep, Glob, WebSearch, WebFetch).

**Spec:** `docs/superpowers/specs/2026-03-13-legal-france-plugin-design.md`

---

## Chunk 1: Plugin Scaffold & Core Skill

### Task 1: Plugin metadata

**Files:**
- Create: `.claude-plugin/plugin.json`
- Create: `LICENSE`

- [ ] **Step 1: Create plugin.json**

```json
{
  "name": "legal-france",
  "description": "French law assistant with domain-specific expertise across civil, criminal, labor, business, administrative, digital, and European law. Supports legal consultation, case law research, contract analysis, and document parsing.",
  "version": "0.1.0",
  "author": {
    "name": "Amine Harrak"
  },
  "repository": "https://github.com/amineharrak/legal-france",
  "license": "MIT",
  "keywords": [
    "french-law",
    "droit",
    "legal",
    "jurisprudence",
    "legifrance",
    "consultation",
    "contract-analysis",
    "gdpr",
    "rgpd"
  ]
}
```

- [ ] **Step 2: Create MIT LICENSE file**

Standard MIT license with `Copyright (c) 2026 Amine Harrak`.

- [ ] **Step 3: Commit**

```bash
git add .claude-plugin/plugin.json LICENSE
git commit -m "feat: initialize legal-france plugin scaffold"
```

---

### Task 2: SKILL.md — Main skill file

**Files:**
- Create: `skills/legal-france/SKILL.md`

This is the core of the plugin. Must stay under 5000 words. Contains: role, user role detection, domain routing, research protocol, response protocol, disclaimer.

- [ ] **Step 1: Create SKILL.md with frontmatter**

Frontmatter:
```yaml
---
name: legal-france
description: "French law assistant covering civil, criminal, labor, business, administrative, digital, and European law. Adapts to user role (lawyer, judge, student, citizen). Use when user asks about French legislation, legal analysis, contract review, case law research, or mentions 'droit', 'loi', 'article', 'jurisprudence', 'contrat', 'licenciement', 'RGPD', 'Code civil', 'Code penal'."
---
```

- [ ] **Step 2: Write Role & Identity section**

Content per spec Section 3.1:
- French law research assistant
- Respond in the user's language
- Never fabricate sources
- Cite precisely (article, date, pourvoi number)

- [ ] **Step 3: Write User Role Detection section**

Content per spec Section 3.2:
- Detection rules for lawyer/judge, student, citizen, business
- Default fallback: citizen
- Table of roles → language level → default response format

- [ ] **Step 4: Write Domain Routing section**

Content per spec Section 3.3:
- Keyword → domain file mapping table
- Instruction: use Read tool to load `references/<domain>.md`
- Instruction: always also load `references/codes-index.md` for quick lookup

- [ ] **Step 5: Write Research Protocol section**

Content per spec Section 3.4:
- 5-step protocol (check refs → web search → parse docs → cross-ref → state uncertainty)
- Priority sites list

- [ ] **Step 6: Write Response Protocol section**

Content per spec Section 3.5:
- Strict priority: command > role > request nature
- Reference to `methodology.md` for templates

- [ ] **Step 7: Write Mandatory Disclaimer section**

Content per spec Section 3.6:
- FR and EN disclaimer text
- Instruction: append to every response

- [ ] **Step 8: Verify word count is under 5000**

```bash
wc -w skills/legal-france/SKILL.md
```

Expected: under 5000 words.

- [ ] **Step 9: Commit**

```bash
git add skills/legal-france/SKILL.md
git commit -m "feat: add main SKILL.md with core logic"
```

---

### Task 3: methodology.md — Response templates

**Files:**
- Create: `skills/legal-france/methodology.md`

Contains the 6 structured response formats with full instructions for each.

- [ ] **Step 1: Write Consultation juridique template**

Per spec Section 4.1:
1. Rappel des faits
2. Problème de droit
3. Règle applicable
4. Application (syllogisme): Majeure → Mineure → Conclusion
5. Solutions & recommandations
6. Mise en garde

Include: trigger conditions, example structure, tone guidance.

- [ ] **Step 2: Write Cas pratique template**

Per spec Section 4.2:
1. Faits
2. Problème de droit
3. Majeure ("Selon l'article X...")
4. Mineure ("En l'espèce...")
5. Conclusion

- [ ] **Step 3: Write Commentaire d'arrêt template**

Per spec Section 4.3:
1. Fiche d'arrêt (faits, procédure, prétentions, problème, solution)
2. Sens
3. Valeur
4. Portée

- [ ] **Step 4: Write Recherche de jurisprudence template**

Per spec Section 4.4:
1. Termes de recherche
2. Décisions trouvées
3. Analyse
4. Sources

- [ ] **Step 5: Write Analyse de document template**

Per spec Section 4.5:
1. Résumé du document
2. Clauses sensibles
3. Conformité
4. Recommandations

- [ ] **Step 6: Write Explication vulgarisée template**

Per spec Section 4.6:
1. Réponse courte
2. Explication
3. Ce que dit la loi
4. Que faire concrètement
5. Pour aller plus loin

- [ ] **Step 7: Commit**

```bash
git add skills/legal-france/methodology.md
git commit -m "feat: add methodology.md with 6 response templates"
```

---

## Chunk 2: Commands

### Task 4: Main commands — /droit and /jurisprudence

**Files:**
- Create: `commands/droit.md`
- Create: `commands/jurisprudence.md`

- [ ] **Step 1: Create droit.md**

```yaml
---
description: Ask any question about French law — routes to the right domain automatically
argument-hint: <your legal question>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---
```

Body: Invoke `legal-france` skill. Workflow steps:
1. Detect domain from keywords
2. Read relevant `references/<domain>.md`
3. Read `references/codes-index.md`
4. Apply response template matching user role
5. WebSearch Legifrance if refs insufficient
6. Cite all sources precisely
7. End with disclaimer

- [ ] **Step 2: Create jurisprudence.md**

```yaml
---
description: Search French case law, landmark decisions, and jurisprudential trends
argument-hint: <search terms, article number, or legal topic>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---
```

Body: Invoke `legal-france` skill with case law research template. Workflow:
1. Search `references/jurisprudence-cle.md` first
2. WebSearch Legifrance, EUR-Lex for additional results
3. Parse local documents if user provides them
4. Use the "Recherche de jurisprudence" response template
5. Cite all sources with decision numbers and dates

- [ ] **Step 3: Commit**

```bash
git add commands/droit.md commands/jurisprudence.md
git commit -m "feat: add /droit and /jurisprudence commands"
```

---

### Task 5: Domain-specific commands (7 commands)

**Files:**
- Create: `commands/droit-civil.md`
- Create: `commands/droit-penal.md`
- Create: `commands/droit-travail.md`
- Create: `commands/droit-affaires.md`
- Create: `commands/droit-administratif.md`
- Create: `commands/droit-numerique.md`
- Create: `commands/droit-europeen.md`

All follow the same pattern. Each:
- Has frontmatter with domain-specific description + `allowed-tools`
- Body: invokes `legal-france` skill, skips routing, loads specific `references/<domain>.md` directly

- [ ] **Step 1: Create droit-civil.md**

```yaml
---
description: French civil law — contracts, liability, property, family, inheritance. Use for questions about Code civil, obligations, marriage, divorce, succession.
argument-hint: <your civil law question>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---
```

Body: Invoke `legal-france` skill. Skip domain routing. Read `references/civil.md` directly. Apply response template based on user role.

- [ ] **Step 2: Create droit-penal.md**

```yaml
---
description: French criminal law — offenses, penalties, criminal procedure. Use for questions about Code penal, infractions, garde a vue, prosecution.
argument-hint: <your criminal law question>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---
```

- [ ] **Step 3: Create droit-travail.md**

```yaml
---
description: French labor law — employment contracts, dismissal, collective bargaining, labor courts. Use for questions about Code du travail, CDI, CDD, licenciement, prud'hommes.
argument-hint: <your labor law question>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---
```

- [ ] **Step 4: Create droit-affaires.md**

```yaml
---
description: French business law — companies, commercial law, competition, IP, consumer law. Use for questions about SAS, SARL, Code de commerce, fonds de commerce, brevets, marques.
argument-hint: <your business law question>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---
```

- [ ] **Step 5: Create droit-administratif.md**

```yaml
---
description: French administrative law — public administration, administrative contracts, liability, courts. Use for questions about Conseil d'Etat, contentieux administratif, prefet, maire.
argument-hint: <your administrative law question>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---
```

- [ ] **Step 6: Create droit-numerique.md**

```yaml
---
description: French digital law and data protection — GDPR/RGPD, CNIL, privacy, e-commerce, cybersecurity. Use for questions about donnees personnelles, cookies, consentement, droit a l'oubli.
argument-hint: <your digital law question>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---
```

- [ ] **Step 7: Create droit-europeen.md**

```yaml
---
description: EU law as applied in France — treaties, directives, regulations, CJEU case law. Use for questions about primaute, effet direct, marche interieur, citoyennete europeenne, CJUE.
argument-hint: <your EU law question>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---
```

- [ ] **Step 8: Commit**

```bash
git add commands/droit-civil.md commands/droit-penal.md commands/droit-travail.md commands/droit-affaires.md commands/droit-administratif.md commands/droit-numerique.md commands/droit-europeen.md
git commit -m "feat: add 7 domain-specific commands"
```

---

## Chunk 3: Transversal References

### Task 6: sources.md — How to search legal databases

**Files:**
- Create: `skills/legal-france/references/sources.md`

- [ ] **Step 1: Write sources.md**

Content:
- **Legifrance** (legifrance.gouv.fr): how to search codes, laws, jurisprudence. URL patterns. Decision number formats (e.g., Cass. civ. 1re, 12 janv. 2023, n° 21-12.345).
- **EUR-Lex** (eur-lex.europa.eu): how to search directives, regulations, CJEU decisions. CELEX number format.
- **Conseil constitutionnel** (conseil-constitutionnel.fr): QPC decisions, DC decisions.
- **CNIL** (cnil.fr): deliberations, guides, sanctions.
- **Service-public.fr**: practical information for citizens.
- **Conseil d'État** (conseil-etat.fr): administrative decisions.
- **Cour de cassation** (courdecassation.fr): civil/criminal supreme court decisions.

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/sources.md
git commit -m "feat: add sources.md — legal database search guide"
```

---

### Task 7: codes-index.md — Index of French legal codes

**Files:**
- Create: `skills/legal-france/references/codes-index.md`

- [ ] **Step 1: Write codes-index.md**

Quick routing table listing all major French codes with their most commonly cited articles:
- Code civil (art. 1100-1386 obligations, 1240-1244 responsabilité, 212-309 famille, 720-892 successions)
- Code pénal (art. 111-1 to 133-17 général, 211-1 to 450-5 spécial)
- Code du travail (L1231-1 to L1238-5 licenciement, L1221-1 to L1227-1 contrat)
- Code de commerce (L210-1 to L252-13 sociétés, L110-1 to L110-4 commercial)
- Code de procédure civile
- Code de procédure pénale
- Code de la consommation
- Code de la propriété intellectuelle
- RGPD (articles 1-99)
- Loi Informatique et Libertés

For each code: name, key article ranges, typical use cases.

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/codes-index.md
git commit -m "feat: add codes-index.md — French legal codes quick reference"
```

---

### Task 8: jurisprudence-cle.md — Landmark decisions

**Files:**
- Create: `skills/legal-france/references/jurisprudence-cle.md`

- [ ] **Step 1: Write jurisprudence-cle.md**

Organized by domain. For each decision: name, court, date, number, facts (1 sentence), rule established, significance. v1 scope: 5-8 landmark decisions per domain.

Key decisions to include:
- **Civil:** Jand'heur (1930, responsabilité), Perruche (2000, préjudice de naissance), Chronopost (1996, clauses limitatives)
- **Pénal:** Lacour (1997, responsabilité pénale des personnes morales), Consorts Martinez (légitime défense)
- **Travail:** Nikon (2001, vie privée au travail), Brinon (1958, licenciement économique)
- **Administratif:** Blanco (1873, responsabilité admin), Nicolo (1989, primauté droit européen), Dehaene (1950, droit de grève)
- **Numérique/RGPD:** CNIL Google LLC (2019, 50M€), Schrems II (CJUE 2020)
- **Européen:** Costa c/ ENEL (1964, primauté), Van Gend en Loos (1963, effet direct)
- **Constitutionnel:** Liberté d'association (1971), QPC (2010 premiers arrêts)

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/jurisprudence-cle.md
git commit -m "feat: add jurisprudence-cle.md — landmark decisions"
```

---

### Task 9: glossaire.md — Legal glossary FR<>EN

**Files:**
- Create: `skills/legal-france/references/glossaire.md`

- [ ] **Step 1: Write glossaire.md**

Alphabetical. For each term: French term, English translation, brief definition. v1 scope: 80-100 essential terms.

Categories: general legal terms, civil law, criminal law, procedural terms, business law, labor law, digital law.

Example entries:
- **Arrêt** / Judgment — Decision rendered by a court of appeal or the Cour de cassation
- **Mise en demeure** / Formal notice — Written demand to perform an obligation
- **Pourvoi en cassation** / Appeal to the Supreme Court — Remedy before the Cour de cassation

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/glossaire.md
git commit -m "feat: add glossaire.md — legal glossary FR-EN"
```

---

## Chunk 4: Domain References (Part 1)

### Task 10: civil.md — Civil law references

**Files:**
- Create: `skills/legal-france/references/civil.md`

- [ ] **Step 1: Write civil.md**

Follow the domain file template from the spec (Section 6.1). Content:

**Applicable Codes:** Code civil (obligations art. 1100+, responsabilité art. 1240+, famille art. 212+, biens art. 544+, successions art. 720+)

**Key Articles (10-15):** Art. 1101 (contrat), 1103 (force obligatoire), 1104 (bonne foi), 1128 (conditions de validité), 1217 (inexécution), 1240 (responsabilité délictuelle), 1241 (faute), 1242 (responsabilité du fait d'autrui), 9 (vie privée), 16 (dignité), 544 (propriété), 212 (devoirs des époux), 371-1 (autorité parentale)

**Landmark Decisions (3-5):** Jand'heur, Perruche, Chronopost, Baldus

**Common Questions:** "Est-ce que mon contrat est valide?", "Puis-je obtenir des dommages-intérêts?"

**Cross-references:** procedure.md for enforcement, affaires.md for commercial contracts

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/civil.md
git commit -m "feat: add civil.md — civil law domain references"
```

---

### Task 11: penal.md — Criminal law references

**Files:**
- Create: `skills/legal-france/references/penal.md`

- [ ] **Step 1: Write penal.md**

**Applicable Codes:** Code pénal, Code de procédure pénale

**Key Articles (10-15):** Art. 111-1 (légalité des délits et des peines), 111-3 (interprétation stricte), 121-1 (responsabilité personnelle), 121-3 (intention), 122-1 (irresponsabilité trouble mental), 122-5 (légitime défense), 131-3 (peines criminelles), 311-1 (vol), 313-1 (escroquerie), 221-1 (meurtre), 222-1 (tortures), CPP art. 63 (garde à vue), CPP art. 393 (comparution immédiate)

**Landmark Decisions (3-5):** Specific to criminal law

**Common Questions:** "Quelle est la différence entre crime, délit et contravention?", "Quels sont les droits en garde à vue?"

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/penal.md
git commit -m "feat: add penal.md — criminal law domain references"
```

---

### Task 12: travail.md — Labor law references

**Files:**
- Create: `skills/legal-france/references/travail.md`

- [ ] **Step 1: Write travail.md**

**Applicable Codes:** Code du travail

**Key Articles (10-15):** L1221-1 (contrat de travail), L1232-1 (licenciement cause réelle et sérieuse), L1234-1 (préavis), L1234-9 (indemnité légale), L1235-3 (barème Macron), L1242-1 (CDD), L1243-1 (rupture CDD), L1237-11 (rupture conventionnelle), L2511-1 (droit de grève), L4121-1 (obligation de sécurité), L3121-27 (durée légale 35h)

**Landmark Decisions (3-5):** Nikon, Brinon, and key Cour de cassation sociale rulings

**Common Questions:** "Quels sont mes droits en cas de licenciement?", "Comment fonctionne la rupture conventionnelle?"

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/travail.md
git commit -m "feat: add travail.md — labor law domain references"
```

---

### Task 13: affaires.md — Business law references

**Files:**
- Create: `skills/legal-france/references/affaires.md`

- [ ] **Step 1: Write affaires.md**

**Applicable Codes:** Code de commerce, Code de la consommation, Code de la propriété intellectuelle

**Key Articles (10-15):** Code de commerce L210-1 (sociétés commerciales), L223-1 (SARL), L227-1 (SAS), L631-1 (redressement judiciaire), L640-1 (liquidation), L110-1 (actes de commerce). Code de la consommation L111-1 (information précontractuelle), L121-1 (pratiques commerciales déloyales), L217-4 (garantie de conformité). CPI L111-1 (droit d'auteur), L611-1 (brevets), L711-1 (marques)

**Landmark Decisions (3-5):** Key commercial and IP cases

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/affaires.md
git commit -m "feat: add affaires.md — business law domain references"
```

---

## Chunk 5: Domain References (Part 2)

### Task 14: administratif.md — Administrative law references

**Files:**
- Create: `skills/legal-france/references/administratif.md`

- [ ] **Step 1: Write administratif.md**

**Applicable Codes:** Code de justice administrative, Code des relations entre le public et l'administration (CRPA)

**Key Articles (10-15):** CJA L1 (juridictions), R421-1 (délai recours 2 mois), R421-5 (notification). CRPA L211-1 (décisions admin), L231-1 (silence vaut acceptation), L311-1 (accès aux documents)

**Landmark Decisions (5+):** Blanco (1873), Nicolo (1989), Dehaene (1950), Barel (1954), Canal (1962)

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/administratif.md
git commit -m "feat: add administratif.md — administrative law domain references"
```

---

### Task 15: numerique.md — Digital law & GDPR references

**Files:**
- Create: `skills/legal-france/references/numerique.md`

- [ ] **Step 1: Write numerique.md**

**Applicable Texts:** RGPD (Règlement UE 2016/679), Loi Informatique et Libertés (loi n° 78-17), Loi pour la confiance dans l'économie numérique (LCEN, loi n° 2004-575), Directive e-Privacy

**Key Articles (10-15):** RGPD art. 5 (principes), 6 (licéité), 7 (consentement), 12-22 (droits des personnes), 25 (privacy by design), 33 (notification violations), 37-39 (DPO), 83 (sanctions). Loi IL art. 1, 8. LCEN art. 6 (hébergeurs)

**Landmark Decisions:** CNIL Google LLC 50M€ (2019), Schrems II (CJUE 2020), Planet49 (CJUE 2019, cookies)

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/numerique.md
git commit -m "feat: add numerique.md — digital law and GDPR references"
```

---

### Task 16: europeen.md — EU law references

**Files:**
- Create: `skills/legal-france/references/europeen.md`

- [ ] **Step 1: Write europeen.md**

**Applicable Texts:** Traité sur l'Union européenne (TUE), Traité sur le fonctionnement de l'UE (TFUE), Charte des droits fondamentaux

**Key Articles (10-15):** TUE art. 4 (compétences), 6 (droits fondamentaux). TFUE art. 18 (non-discrimination), 21 (libre circulation citoyens), 34 (libre circulation marchandises), 49 (liberté d'établissement), 56 (libre prestation services), 101-102 (concurrence), 258 (recours en manquement), 263 (recours en annulation), 267 (renvoi préjudiciel)

**Landmark Decisions:** Van Gend en Loos (1963), Costa c/ ENEL (1964), Cassis de Dijon (1979), Francovich (1991), Factortame (1990)

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/europeen.md
git commit -m "feat: add europeen.md — EU law domain references"
```

---

### Task 17: procedure.md — Procedural law references (cross-cutting)

**Files:**
- Create: `skills/legal-france/references/procedure.md`

- [ ] **Step 1: Write procedure.md**

Covers civil, criminal, and administrative procedure. Cross-cutting reference loaded when procedural questions arise in any domain.

**Applicable Codes:** Code de procédure civile (CPC), Code de procédure pénale (CPP), Code de justice administrative (CJA)

**Key Articles (10-15):**
- CPC: art. 1 (initiative des parties), 9 (charge de la preuve), 32 (intérêt à agir), 56 (assignation), 808 (référé), 900 (appel)
- CPP: art. 1 (action publique), 63 (garde à vue), 80 (instruction), 388 (tribunal correctionnel), 567 (pourvoi)
- CJA: R421-1 (délai 2 mois), R421-5 (notification)

**Key Concepts:** Prescription, voies de recours, compétence, charge de la preuve, modes alternatifs (médiation, arbitrage)

- [ ] **Step 2: Commit**

```bash
git add skills/legal-france/references/procedure.md
git commit -m "feat: add procedure.md — cross-cutting procedural law references"
```

---

## Chunk 6: README & Final Assembly

### Task 18: README.md

**Files:**
- Create: `README.md`

- [ ] **Step 1: Write README.md**

Per spec Section 8. Sections:
1. **What it does** — outcome-focused: "Get accurate, well-sourced French law assistance directly in Claude Code. The plugin adapts to your profile — whether you're a lawyer, student, or citizen — and covers 7 domains of French law."
2. **Installation** — `claude plugin install legal-france` (or marketplace link)
3. **Available commands** — table of 9 commands with example usage
4. **User roles** — how the skill adapts (4 roles)
5. **Response formats** — the 6 templates briefly described
6. **Supported domains** — list of 7 domains + procedure
7. **Sources** — Legifrance, EUR-Lex, CNIL, etc.
8. **Disclaimer** — both FR and EN
9. **Contributing** — how to add articles/decisions to reference files
10. **License** — MIT

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "feat: add README.md with installation and usage docs"
```

---

### Task 19: Verify complete structure

- [ ] **Step 1: Verify all files exist**

```bash
find . -type f -not -path './.git/*' -not -path './docs/*' | sort
```

Expected output:
```
./.claude-plugin/plugin.json
./commands/droit-administratif.md
./commands/droit-affaires.md
./commands/droit-civil.md
./commands/droit-europeen.md
./commands/droit-numerique.md
./commands/droit-penal.md
./commands/droit-travail.md
./commands/droit.md
./commands/jurisprudence.md
./LICENSE
./README.md
./skills/legal-france/methodology.md
./skills/legal-france/references/administratif.md
./skills/legal-france/references/affaires.md
./skills/legal-france/references/civil.md
./skills/legal-france/references/codes-index.md
./skills/legal-france/references/europeen.md
./skills/legal-france/references/glossaire.md
./skills/legal-france/references/jurisprudence-cle.md
./skills/legal-france/references/numerique.md
./skills/legal-france/references/penal.md
./skills/legal-france/references/procedure.md
./skills/legal-france/references/sources.md
./skills/legal-france/references/travail.md
./skills/legal-france/SKILL.md
```

25 files total (excluding docs/ and .git/).

- [ ] **Step 2: Verify SKILL.md is under 5000 words**

```bash
wc -w skills/legal-france/SKILL.md
```

- [ ] **Step 3: Verify plugin.json is valid JSON**

```bash
python -c "import json; json.load(open('.claude-plugin/plugin.json')); print('Valid JSON')"
```

- [ ] **Step 4: Verify all command files have valid frontmatter**

```bash
for f in commands/*.md; do echo "=== $f ==="; head -5 "$f"; done
```

Each should start with `---` and contain `description:` and `allowed-tools:`.

- [ ] **Step 5: Final commit if any fixes needed**

```bash
git add -A
git commit -m "fix: address any structural issues found during verification"
```

---

## Task Dependencies

```
Task 1 (plugin.json + LICENSE)
  └→ Task 2 (SKILL.md)
       └→ Task 3 (methodology.md)
            └→ Task 4 (main commands)
                 └→ Task 5 (domain commands)

Task 6 (sources.md)      ──┐
Task 7 (codes-index.md)  ──┤
Task 8 (jurisprudence)   ──┤── Can run in parallel
Task 9 (glossaire.md)    ──┘

Task 10 (civil.md)         ──┐
Task 11 (penal.md)         ──┤
Task 12 (travail.md)       ──┤
Task 13 (affaires.md)      ──┤── Can run in parallel
Task 14 (administratif.md) ──┤
Task 15 (numerique.md)     ──┤
Task 16 (europeen.md)      ──┤
Task 17 (procedure.md)     ──┘

Task 18 (README) ── depends on all above
Task 19 (verify) ── depends on all above
```

**Parallelization opportunities:**
- Tasks 6-9 (transversal refs) can run in parallel with Tasks 4-5 (commands)
- Tasks 10-17 (domain refs) can all run in parallel
- Tasks 1-3 must be sequential (each builds on the previous)
