# legal-france — Plugin Claude Code pour le droit français / French Law Plugin for Claude Code

> **FR :** Assistant juridique français pour Claude Code — 8 skills modulaires auto-déclenchants, 10 modèles de documents juridiques, intégration jurisprudence Cour de cassation (Judilibre).
> **EN:** French law assistant for Claude Code — 8 modular auto-triggering skills, 10 legal document templates, Cour de cassation case-law integration (Judilibre).

---

## Installation

```bash
claude plugin install legal-france
```

---

## Commandes / Commands

| Commande | Description (FR) | Description (EN) |
|----------|-------------------|-------------------|
| `/droit <question>` | Routage automatique vers le bon domaine | Auto-routes to the right domain |
| `/jurisprudence <recherche>` | Recherche de jurisprudence et décisions clés | Case law search and landmark decisions |
| `/droit-civil <question>` | Contrats, responsabilité, famille, succession | Contracts, liability, family, inheritance |
| `/droit-penal <question>` | Infractions, peines, procédure pénale | Offenses, penalties, criminal procedure |
| `/droit-travail <question>` | Emploi, licenciement, négociation collective | Employment, dismissal, collective bargaining |
| `/droit-affaires <question>` | Sociétés, commercial, PI, concurrence | Companies, commercial law, IP, competition |
| `/droit-administratif <question>` | Administration, juridictions administratives | Public administration, administrative courts |
| `/droit-numerique <question>` | RGPD, CNIL, protection des données | GDPR, CNIL, data protection |
| `/droit-europeen <question>` | Traités, directives, règlements, CJUE | Treaties, directives, regulations, CJEU |
| `/rediger <type>` | Générer un modèle de document juridique (10 modèles disponibles) | Generate a legal document template (10 templates available) |

---

## Profils utilisateur / User Profiles

Le plugin détecte automatiquement votre profil et adapte sa réponse :
_The plugin auto-detects your profile and adapts its response:_

- **Avocat / Magistrat** — Format consultation juridique structurée / Structured legal consultation
- **Étudiant en droit** — Cas pratique, commentaire d'arrêt / Case analysis, case commentary
- **Citoyen** _(défaut / default)_ — Langage clair, démarches pratiques / Plain language, practical steps
- **Entreprise** — Conformité, analyse de documents / Compliance, document analysis

---

## Documents disponibles / Available documents

Le rédacteur génère 10 modèles de documents prêts à personnaliser :

| # | Document | Domaine |
|---|---|---|
| 1 | Mise en demeure générique | Transversal |
| 2 | Attestation sur l'honneur | Transversal |
| 3 | Lettre de licenciement | Travail |
| 4 | Convention de rupture conventionnelle | Travail |
| 5 | Lettre de démission | Travail |
| 6 | Mise en demeure restitution caution | Civil / Bail |
| 7 | Plainte simple au procureur | Pénal |
| 8 | Contestation d'amende (OMP) | Pénal |
| 9 | Recours gracieux administratif | Administratif |
| 10 | Mentions légales + politique de confidentialité | Numérique |

Invocation : `/rediger <type>` (ex : `/rediger lettre-licenciement`). Le rédacteur pose 5 à 15 questions ciblées, vérifie les articles cités sur Legifrance, puis génère le document avec une checklist de vérifications à effectuer avant envoi.

---

## Formats de réponse / Response Formats

7 modèles structurés alignés sur la méthodologie juridique française :
_7 structured templates aligned with French legal methodology:_

1. **Consultation juridique** / Legal Consultation
2. **Cas pratique** / Practical Case Analysis
3. **Commentaire d'arrêt** / Case Commentary
4. **Recherche de jurisprudence** / Case Law Research
5. **Analyse de document** / Document Analysis
6. **Explication vulgarisée** / Plain Language Explanation
7. **Cas complexe** / Complex Case Analysis _(v2.0)_

---

## Domaines couverts / Domains Covered

| Domaine | Domain | Fichier de référence |
|---------|--------|---------------------|
| Droit civil | Civil law | `references/civil.md` |
| Droit pénal | Criminal law | `references/penal.md` |
| Droit du travail | Labor law | `references/travail.md` |
| Droit des affaires | Business law | `references/affaires.md` |
| Droit administratif | Administrative law | `references/administratif.md` |
| Droit numérique | Digital law (GDPR) | `references/numerique.md` |
| Droit européen | EU law | `references/europeen.md` |
| Procédure | Procedural law | `references/procedure.md` |

Références transversales / Cross-cutting references:
- `references/jurisprudence-cle.md` — 96 décisions clés / 96 landmark decisions
- `references/glossaire.md` — ~170 termes / ~170 terms
- `references/codes-index.md` — Index des codes français / Index of French legal codes
- `references/sources.md` — Sources officielles / Official sources

---

## Indicateurs de progression / Progress Indicators

Le plugin affiche les étapes en temps réel pendant le traitement :
_The plugin displays real-time step indicators while processing:_

> **[1/5]** Identification du domaine juridique...
> **[2/5]** Chargement des références...
> **[3/5]** Vérification sur Legifrance...
> **[4/5]** Analyse et recoupement des sources...
> **[5/5]** Rédaction de la réponse...

---

## Sources

- [Legifrance](https://legifrance.gouv.fr)
- [EUR-Lex](https://eur-lex.europa.eu)
- [Conseil constitutionnel](https://www.conseil-constitutionnel.fr)
- [CNIL](https://www.cnil.fr)
- [Service-public.fr](https://www.service-public.fr)

---

## Configuration Judilibre (optionnelle) / Judilibre setup (optional)

> **FR :** Pour des recherches jurisprudentielles structurées via l'API officielle de la Cour de cassation. Gratuit. Sans cette config, le plugin retombe automatiquement sur les recherches web Legifrance.
> **EN:** For structured case-law search via the official Cour de cassation API. Free of charge. Without this setup, the plugin transparently falls back to Legifrance web search.

### Étapes / Steps

1. Créer un compte sur [piste.gouv.fr](https://piste.gouv.fr) (la plateforme API de l'État).
2. Dans le catalogue, souscrire à l'API **Judilibre — Cour de cassation**.
3. Créer une application (générer une paire `client_id` / `client_secret`).
4. Définir deux variables d'environnement :

   **Linux / macOS :**
   ```bash
   export PISTE_CLIENT_ID="votre_client_id"
   export PISTE_CLIENT_SECRET="votre_client_secret"
   ```

   **Windows PowerShell :**
   ```powershell
   $env:PISTE_CLIENT_ID = "votre_client_id"
   $env:PISTE_CLIENT_SECRET = "votre_client_secret"
   ```

5. Relancer votre session Claude Code. Le plugin détecte automatiquement la présence des variables et utilise Judilibre en priorité.

### Vérification / Verification

Invoquez `/jurisprudence harcèlement moral` : la réponse doit citer les pourvois avec format `Cass. soc., date, n° pourvoi (Judilibre: id)`. Si la citation n'a pas l'identifiant Judilibre, c'est que le fallback Legifrance a été utilisé.

---

## Versions

| Version | Date | Description |
|---------|------|-------------|
| **v3.0.0** | Mai 2026 | 8 skills modulaires (1 méta + 7 domaines), 10 modèles de documents, intégration API Judilibre, suite de tests / 8 modular skills, 10 document templates, Judilibre API integration, test suite |
| **v2.0.0** | Mars 2026 | Références enrichies, protocole cas complexes, vérification web obligatoire / Enriched references, complex case protocol, mandatory web verification |
| **v0.1.0** | Février 2026 | Version initiale / Initial release |

---

## Contribuer / Contributing

Pour enrichir les références, ajoutez articles ou décisions dans le fichier correspondant sous `plugins/legal-france/skills/legal-france/references/<domaine>.md` en suivant le format existant.

_To enrich references, add statutes or decisions to the relevant file under `plugins/legal-france/skills/legal-france/references/<domain>.md`, following the existing format._

---

## Avertissement / Disclaimer

> **FR :** Ces informations sont fournies à titre indicatif et ne constituent pas un avis juridique. Les lois et la jurisprudence évoluent constamment. Consultez un avocat qualifié pour votre situation particulière.

> **EN:** This information is provided for educational and research purposes only. It does not constitute legal advice. Laws and case law evolve constantly. Always consult a qualified legal professional for specific situations.

---

## Licence / License

MIT — Copyright (c) 2026 Amine Harrak
