# Legal France — Claude Code Plugin Design Spec

**Date:** 2026-03-13
**Author:** Amine Harrak
**Status:** Draft
**Plugin Name:** `legal-france`

---

## 1. Overview

A Claude Code plugin providing comprehensive French law assistance. The plugin adapts to any user profile (lawyer, judge, student, citizen, business) and responds in the user's language. It combines embedded legal knowledge with real-time web research capabilities.

### Goals
- Provide accurate, well-sourced legal information on French law
- Support 8 domains of French law with domain-specific expertise
- Offer 6 structured response formats aligned with French legal methodology
- Enable case law research via web and local document parsing
- Publish as an open-source plugin on the Claude Code marketplace

### Non-Goals
- Replace professional legal advice
- Provide legal representation or draft binding legal documents
- Cover non-French jurisdictions (except EU law as it applies in France)

---

## 2. Plugin Structure

```
legal-france/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   ├── droit.md                    # /droit <question> — main entry point
│   ├── jurisprudence.md            # /jurisprudence <search> — case law search
│   ├── droit-civil.md              # /droit-civil <question>
│   ├── droit-penal.md              # /droit-penal <question>
│   ├── droit-travail.md            # /droit-travail <question>
│   ├── droit-affaires.md           # /droit-affaires <question>
│   ├── droit-administratif.md      # /droit-administratif <question>
│   ├── droit-numerique.md          # /droit-numerique <question>
│   └── droit-europeen.md           # /droit-europeen <question>
├── skills/
│   └── legal-france/
│       ├── SKILL.md                # Main skill: role, methodology, routing
│       ├── methodology.md          # Response templates (6 formats)
│       └── references/
│           ├── civil.md            # Civil law: key articles, landmark cases
│           ├── penal.md            # Criminal law
│           ├── travail.md          # Labor law
│           ├── affaires.md         # Business law
│           ├── administratif.md    # Administrative law
│           ├── numerique.md        # Digital law, GDPR/RGPD
│           ├── europeen.md         # EU law
│           ├── procedure.md        # Civil, criminal, administrative procedure
│           ├── codes-index.md      # Index of all French codes + key articles
│           ├── jurisprudence-cle.md # 50-100 landmark decisions
│           ├── glossaire.md        # Legal glossary FR<>EN
│           └── sources.md          # How to search Legifrance, EUR-Lex, CNIL
├── LICENSE                         # MIT
└── README.md                       # Installation, usage, examples
```

### Anthropic Standards Compliance
- `SKILL.md` exactly (case-sensitive) as main skill file
- Folder naming: kebab-case only, no spaces/underscores/capitals
- Frontmatter: `name` + `description` fields, under 1024 characters, no XML tags
- No "claude" or "anthropic" in skill name
- SKILL.md body under 5000 words; detailed content in `references/`
- Progressive disclosure: 3 levels (frontmatter → SKILL.md body → linked files)
- No README.md inside the skill folder
- Pattern used: "Domain-specific intelligence" (Pattern 5 from Anthropic guide)

---

## 3. SKILL.md — Core Logic

### Frontmatter

```yaml
---
name: legal-france
description: "French law assistant covering civil, criminal, labor, business, administrative, digital, and European law. Adapts to user role (lawyer, judge, student, citizen). Use when user asks about French legislation, legal analysis, contract review, case law research, or mentions 'droit', 'loi', 'article', 'jurisprudence', 'contrat', 'licenciement', 'RGPD', 'Code civil', 'Code penal'."
---
```

### Body Sections

#### 3.1 Role & Identity
- French law research assistant
- Responds in the user's language (French, English, or other)
- Never fabricates legal sources — if unsure, says so
- Always cites precisely: article number, decision date, pourvoi number

#### 3.2 User Role Detection
Detect from context or ask explicitly:

| Role | Language Level | Default Format |
|------|---------------|----------------|
| `lawyer` / `judge` | Formal legal terminology | Consultation juridique |
| `student` | Academic, pedagogical | Cas pratique / Commentaire d'arrêt |
| `citizen` | Plain language, accessible | Explication vulgarisée |
| `business` | Professional, compliance-oriented | Contract/document analysis |

#### 3.3 Domain Routing
Based on keywords in the user's question, load the relevant `references/<domain>.md` via Read tool:

| Keywords | Domain File |
|----------|-------------|
| contrat, responsabilité, propriété, succession, mariage, divorce | `civil.md` |
| infraction, peine, vol, meurtre, garde à vue, procureur | `penal.md` |
| licenciement, CDI, CDD, prud'hommes, convention collective | `travail.md` |
| société, SAS, SARL, concurrence, fonds de commerce, brevet | `affaires.md` |
| administration, préfet, maire, contentieux administratif | `administratif.md` |
| RGPD, données personnelles, CNIL, cookies, e-commerce | `numerique.md` |
| directive, règlement européen, CJUE, marché intérieur | `europeen.md` |
| procédure, appel, cassation, référé, prescription | `procedure.md` |

#### 3.4 Research Protocol

```
Step 1: Check embedded references (codes-index.md, jurisprudence-cle.md)
Step 2: If WebSearch/WebFetch available → search Legifrance, EUR-Lex
        Priority sites: legifrance.gouv.fr, eur-lex.europa.eu,
        conseil-constitutionnel.fr, cnil.fr, service-public.fr
Step 3: If user provides documents → Read and analyze them
Step 4: Cross-reference all findings, cite precisely
Step 5: If information cannot be verified → state uncertainty clearly
```

#### 3.5 Response Protocol
Select response template from `methodology.md` based on:
1. The command used (e.g., `/jurisprudence` → case law research format)
2. The detected user role
3. The nature of the request (document provided → document analysis)

#### 3.6 Mandatory Disclaimer
Every response ends with a disclaimer adapted to the user's language:
- FR: "Ces informations sont fournies à titre indicatif et ne constituent pas un avis juridique. Consultez un avocat pour votre situation particulière."
- EN: "This information is provided for educational purposes only and does not constitute legal advice. Consult a qualified attorney for your specific situation."

---

## 4. Response Templates (methodology.md)

### 4.1 Consultation juridique (Legal Consultation)
*Trigger: lawyer/judge role, or explicit legal advice request*

1. **Rappel des faits** — Pertinent facts, legally qualified
2. **Problème de droit** — Question reformulated in legal terms
3. **Règle applicable** — Statutory texts + case law
4. **Application (syllogisme)** — Majeure (rule) → Mineure (facts) → Conclusion
5. **Solutions & recommandations** — Options compared, concrete advice
6. **Mise en garde** — Disclaimer

### 4.2 Cas pratique (Practical Case Analysis)
*Trigger: student role, academic exercise*

1. **Faits** — Selection and legal qualification
2. **Problème de droit** — Interrogative formulation
3. **Majeure** — "Selon l'article X..." (abstract legal rule)
4. **Mineure** — "En l'espèce..." (application to facts)
5. **Conclusion** — Motivated legal solution

### 4.3 Commentaire d'arrêt (Case Commentary)
*Trigger: user provides a court decision to analyze*

1. **Fiche d'arrêt** — Facts, procedure, claims, issue, solution
2. **Sens** — Explanation of the court's reasoning
3. **Valeur** — Critical assessment (doctrine, coherence, equity)
4. **Portée** — Impact on legal evolution, precedent value

### 4.4 Recherche de jurisprudence (Case Law Research)
*Trigger: /jurisprudence command*

1. **Termes de recherche** — Keywords, articles, domain
2. **Décisions trouvées** — Court, date, number, summary
3. **Analyse** — Jurisprudential trend, evolution
4. **Sources** — Legifrance links, exact citations

### 4.5 Analyse de document (Document Analysis)
*Trigger: user provides contract, terms of service, legal document*

1. **Résumé du document** — Nature, parties, purpose
2. **Clauses sensibles** — Identification + legal qualification
3. **Conformité** — Compliance check against applicable law
4. **Recommandations** — Suggested modifications, identified risks

### 4.6 Explication vulgarisée (Plain Language Explanation)
*Trigger: citizen role, simple question, non-technical language*

1. **Réponse courte** — Direct answer in one sentence
2. **Explication** — Context in simple language
3. **Ce que dit la loi** — Simplified article + source
4. **Que faire concrètement** — Steps, deadlines, authorities
5. **Pour aller plus loin** — Links to service-public.fr, lawyer consultation

### Core Principle
The **syllogisme juridique** (Majeure → Mineure → Conclusion) is the backbone of all professional response formats. It ensures logical, verifiable legal reasoning.

---

## 5. Commands

9 commands total. Each is a markdown file in `commands/` that invokes the `legal-france` skill.

### 5.1 Main Commands

**`/droit <question>`**
```yaml
---
description: Ask any question about French law — routes to the right domain automatically
argument-hint: <your legal question>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---
```
Instructions: Invoke the legal-france skill. Detect the domain from the question, load relevant references, apply the appropriate response template.

**`/jurisprudence <search>`**
```yaml
---
description: Search French case law, landmark decisions, and jurisprudential trends
argument-hint: <search terms, article number, or legal topic>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---
```
Instructions: Search `jurisprudence-cle.md` first, then Legifrance/EUR-Lex via web. Parse local documents if provided. Use the case law research response template.

### 5.2 Domain-Specific Commands

All follow the same pattern:

| Command | Domain | References File |
|---------|--------|-----------------|
| `/droit-civil` | Civil law | `civil.md` |
| `/droit-penal` | Criminal law | `penal.md` |
| `/droit-travail` | Labor law | `travail.md` |
| `/droit-affaires` | Business law | `affaires.md` |
| `/droit-administratif` | Administrative law | `administratif.md` |
| `/droit-numerique` | Digital/GDPR law | `numerique.md` |
| `/droit-europeen` | EU law | `europeen.md` |

Each domain command skips the routing step and loads the domain-specific references directly.

---

## 6. References Content Structure

### 6.1 Domain Files (civil.md, penal.md, etc.)

Each follows the same template:

```markdown
# [Domain] — French [Domain] Law

## Applicable Codes
- [Code name] (key article ranges)
- [Specific laws with numbers and dates]

## Key Articles
### Article [number]
> [exact text]
Source: [Legifrance URL]

## Core Principles
- [Principle]: explanation + founding article

## Landmark Decisions
### [Case name] — [Court], [Date], n° [number]
- Facts: [brief]
- Rule: [legal rule established]
- Significance: [why it matters]

## Common Questions & Patterns
- "[typical question]" → [applicable articles, reasoning approach]

## Cross-references
- [links to related domains]
```

### 6.2 Transversal Files

| File | Purpose |
|------|---------|
| `codes-index.md` | Quick routing table: all French legal codes with their most important articles |
| `jurisprudence-cle.md` | 50-100 landmark decisions across all domains (Blanco, Jand'heur, Perruche, Nikon, etc.) |
| `glossaire.md` | Legal terms FR with definitions + EN translations for international users |
| `sources.md` | How to search Legifrance, EUR-Lex, CNIL, Conseil constitutionnel — URLs, search tips, decision number formats |
| `methodology.md` | The 6 response templates detailed in Section 4 |

### 6.3 v1 Scope per Domain
- 10-15 most important articles
- 3-5 landmark decisions
- Core principles
- Most frequent questions
- Enrichment domain by domain in subsequent versions

---

## 7. plugin.json

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

---

## 8. README.md Structure

1. **What it does** — Outcome-focused description
2. **Installation** — `/plugin install legal-france`
3. **Available commands** — Table of 9 commands with examples
4. **User roles** — How the skill adapts responses
5. **Response formats** — The 6 structured templates
6. **Supported domains** — 8 branches of French law
7. **Sources** — Legifrance, EUR-Lex, CNIL, etc.
8. **Disclaimer** — Educational purposes only, not legal advice
9. **Contributing** — How to enrich references
10. **License** — MIT

---

## 9. Legal Disclaimer

Embedded in README and in every skill response:

> **FR:** Ces informations sont fournies à titre indicatif et ne constituent pas un avis juridique. Les lois et la jurisprudence évoluent constamment. Consultez un avocat qualifié pour votre situation particulière.

> **EN:** This information is provided for educational and research purposes only. It does not constitute legal advice. Laws and case law evolve constantly. Always consult a qualified legal professional for specific situations.

---

## 10. Success Criteria

### Quantitative
- Skill triggers on 90% of French law queries
- Does NOT trigger on non-French or non-legal queries
- Response includes verifiable legal citations in 100% of cases
- Web search used when references are insufficient

### Qualitative
- Users don't need to re-explain context
- Response format matches user profile automatically
- Syllogisme juridique applied consistently
- Sources are accurate and current

---

## 11. Future Enhancements (post-v1)

- Enrich each domain with 50+ articles and 20+ decisions
- Add Alsace-Moselle local law specifics
- Add overseas territories (DOM-TOM) specifics
- Integrate Legifrance API (when API key available)
- Add `/droit-fiscal` (tax law) domain
- Add `/droit-immobilier` (real estate law) domain
- Support for parsing PDF court decisions
- Fiche d'arrêt auto-generation from pasted decisions
