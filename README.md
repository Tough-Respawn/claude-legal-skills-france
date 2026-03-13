# legal-france — French Law Plugin for Claude Code

Get accurate, well-sourced French law assistance directly in Claude Code. The plugin adapts to your profile — whether you're a lawyer, student, or citizen — and covers 7 domains of French law plus procedural references.

---

## Installation

```bash
claude plugin install legal-france
```

---

## Available Commands

| Command | Description |
|---------|-------------|
| `/droit <question>` | Ask any question about French law — routes to the right domain automatically |
| `/jurisprudence <search>` | Search French case law, landmark decisions, and jurisprudential trends |
| `/droit-civil <question>` | Civil law — contracts, liability, property, family, inheritance |
| `/droit-penal <question>` | Criminal law — offenses, penalties, criminal procedure |
| `/droit-travail <question>` | Labor law — employment, dismissal, collective bargaining |
| `/droit-affaires <question>` | Business law — companies, commercial law, IP, competition |
| `/droit-administratif <question>` | Administrative law — public administration, courts |
| `/droit-numerique <question>` | Digital law — GDPR/RGPD, CNIL, data protection |
| `/droit-europeen <question>` | EU law — treaties, directives, regulations, CJEU |

---

## User Roles

The skill automatically detects your profile and adapts:

- **Lawyer / Judge** — Formal legal terminology, consultation juridique format
- **Student** — Academic methodology, cas pratique / commentaire d'arrêt format
- **Citizen** (default) — Plain language, practical steps
- **Business** — Compliance-focused, document analysis format

---

## Response Formats

6 structured templates aligned with French legal methodology:

1. **Consultation juridique** (Legal Consultation)
2. **Cas pratique** (Practical Case Analysis)
3. **Commentaire d'arrêt** (Case Commentary)
4. **Recherche de jurisprudence** (Case Law Research)
5. **Analyse de document** (Document Analysis)
6. **Explication vulgarisée** (Plain Language Explanation)

---

## Supported Domains

7 branches of French law + 1 cross-cutting procedural reference:

- Civil law
- Criminal law
- Labor law
- Business law
- Administrative law
- Digital law (GDPR/RGPD)
- EU law
- Procedural law

---

## Sources

The plugin uses embedded legal references and can search:

- [Legifrance](https://legifrance.gouv.fr)
- [EUR-Lex](https://eur-lex.europa.eu)
- [Conseil constitutionnel](https://www.conseil-constitutionnel.fr)
- [CNIL](https://www.cnil.fr)
- [Service-public.fr](https://www.service-public.fr)

---

## Disclaimer

> **FR:** Ces informations sont fournies à titre indicatif et ne constituent pas un avis juridique. Les lois et la jurisprudence évoluent constamment. Consultez un avocat qualifié pour votre situation particulière.

> **EN:** This information is provided for educational and research purposes only. It does not constitute legal advice. Laws and case law evolve constantly. Always consult a qualified legal professional for specific situations.

---

## Contributing

To enrich the legal references, add articles or decisions to the relevant file under `skills/legal-france/references/<domain>.md`, following the existing format in that file.

Available reference files:

- `references/civil.md` — Civil law
- `references/penal.md` — Criminal law
- `references/travail.md` — Labor law
- `references/affaires.md` — Business law
- `references/administratif.md` — Administrative law
- `references/numerique.md` — Digital law / GDPR
- `references/europeen.md` — EU law
- `references/procedure.md` — Procedural law
- `references/jurisprudence-cle.md` — Landmark decisions
- `references/glossaire.md` — Legal glossary
- `references/codes-index.md` — Index of French legal codes
- `references/sources.md` — Official sources

---

## License

MIT — Copyright (c) 2026 Amine Harrak
