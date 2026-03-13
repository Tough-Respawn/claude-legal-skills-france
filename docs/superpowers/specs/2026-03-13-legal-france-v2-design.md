# legal-france v2 — Design Spec

**Date:** 2026-03-13
**Author:** Amine Harrak
**Status:** Approved
**Approach:** Chirurgicale (A) — modifier les fichiers existants, aucun nouveau fichier sauf le template

---

## Goals

Resolve three limitations of v1:

1. **Limited local references** — enrich curated articles and case law per domain
2. **No multi-step reasoning** — add automatic detection and structured handling of complex cases
3. **No freshness guarantee** — make web verification mandatory, not optional

**Target audience:** All profiles (lawyer, judge, student, citizen, business) equally.

---

## Change 1 — Complex Case Protocol (SKILL.md)

**Location:** New block inserted between "Research Protocol" and "Response Protocol" in SKILL.md.

### Automatic Detection

The plugin identifies a complex case when ANY of these conditions is met:

- **Multi-domain:** 2+ domains detected via Domain Routing keywords (e.g., travail + numérique)
- **Causal chain:** User describes a sequence where one legal outcome feeds into the next (e.g., contract → nullity → restitution → prescription)
- **Norm conflict:** Tension between French vs. EU law, two contradictory articles, or competing fundamental rights

### Triggered Behavior

When a complex case is detected, the plugin MUST:

1. **Decompose** — Identify and number each distinct legal issue (problème de droit)
2. **Load all domains** — Read ALL reference files for every domain implicated
3. **Treat sequentially** — Apply the full syllogism (Majeure → Mineure → Conclusion) to each issue independently
4. **Cross-synthesis** — Analyze interactions: does resolving issue #1 change the answer to issue #3? Are there contradictions? What is the priority order of norms?
5. **Force template #7** — Use the "Cas complexe" template from methodology.md instead of the role-default template. **Priority rule:** Complex Case Protocol overrides role-default and nature-default template selection (Response Protocol priorities 2 and 3), but does NOT override explicit command-triggered templates (priority 1). If a command is used AND a complex case is detected, use the command's template but incorporate the Synthèse croisée section from template #7 as an addendum.
6. **Context bound** — Load all implicated domain files. If more than 3 domains are implicated, load the primary domain in full and load only the Key Articles and Landmark Decisions sections from secondary domains.

---

## Change 2 — Template #7 "Cas complexe" (methodology.md)

**Location:** Appended at end of methodology.md, after Template 6.

### Trigger Conditions

- Triggered automatically by the Complex Case Protocol in SKILL.md
- Never triggered manually by a user command
- Overrides the role-default template when activated

### Section Structure

#### 1. Cartographie des problèmes de droit
List each identified legal issue, its domain(s), and anticipated interactions. Present as a table: `N° | Problème | Domaine(s) | Lié à`.

#### 2. Analyse par problème (repeated for each issue)
For each issue, full syllogism:
- **Majeure** — applicable rule with full citations
- **Mineure** — application to the specific facts
- **Conclusion intermédiaire** — outcome for this issue alone

Tone adapts to detected role (formal for lawyer, pedagogical for student, accessible for citizen).

#### 3. Résolution des conflits de normes
When rules contradict: apply hierarchy of norms (Constitution > EU Treaties > Loi > Règlement), principle of specialty (lex specialis), and chronology (lex posterior). Explain why one norm prevails.

Only include this section if a norm conflict was detected. Skip if all issues are independent.

#### 4. Synthèse croisée
How intermediate conclusions interact. Does resolving issue #1 change the analysis of issue #3? Cascade effects? Globally motivated conclusion. If all issues are fully independent with no interactions, replace with a brief statement confirming their independence.

**Conditional sections:** Sections 1, 2, 5, and 6 are always mandatory. Section 3 is included only when a norm conflict is detected. Section 4 is included only when issues interact (otherwise replaced by independence statement).

#### 5. Solutions & recommandations
Concrete options accounting for ALL issues simultaneously (not domain by domain). Risks, deadlines, action priorities.

#### 6. Disclaimer
Standard mandatory disclaimer, adapted to user's language.

---

## Change 3 — Mandatory Web Verification (SKILL.md)

**Location:** Modify existing Research Protocol, Steps 2 and new Step 2bis.

### Step 2 — Changed from optional to mandatory

**Before (v1):** "Use web tools **if available**"
**After (v2):** "**Mandatory web verification**"

Even if an article is found in local references, cross-check on Legifrance that the text is still in force and in its current version.

If WebSearch/WebFetch tools are not available, the plugin MUST display this warning:
> "Je n'ai pas pu vérifier en ligne la version en vigueur de cet article. Les références citées proviennent de données embarquées qui peuvent ne pas refléter les modifications récentes. Vérifiez sur legifrance.gouv.fr."

Source priority order (unchanged): Legifrance > EUR-Lex > Conseil constitutionnel > CNIL > service-public.fr.

### New Step 2bis — Divergence handling

When a locally referenced article has been modified according to the web source:
- Use the web version (most current)
- Signal the divergence to the user: "Note : l'article X a été modifié depuis la dernière mise à jour de mes références embarquées. Je cite la version en vigueur consultée sur Legifrance."

### Web verification failure handling

If web tools are available but the verification query fails or returns inconclusive results (Legifrance down, ambiguous results, article split into sub-articles), treat as if tools are unavailable and display the same warning.

Steps 1, 3, 4, 5 remain unchanged.

---

## Change 4 — Enriched Domain References

**Location:** All 8 `references/<domain>.md` files.

### Targets per domain file

| Metric | v1 (varies by domain) | v2 target |
|--------|----------------------|-----------|
| Key articles | ~10-18 | ~50-60 |
| Landmark decisions | 4-8 | 12-15 |
| Recent reforms section | none | Last 3 years (2023-2026) |

### Enrichment principles

- Articles selected by practical usage frequency (curated, not exhaustive)
- Case law: prioritize arrêts de principe (Assemblée plénière, Chambre mixte) and recent evolutions (2020-2026)
- Each added decision: date, pourvoi number, 1-line summary, legal significance (portée)
- Each added article: number, summarized title, keywords matching Domain Routing

### Domain files to enrich

1. `civil.md`
2. `penal.md`
3. `travail.md`
4. `affaires.md`
5. `administratif.md`
6. `numerique.md`
7. `europeen.md`
8. `procedure.md`

---

## Change 5 — Enriched Transversal References

**Location:** 4 existing transversal files.

| File | v1 | v2 target |
|------|-----|-----------|
| `codes-index.md` | Index with article ranges | Add parties/livres/titres for finer navigation |
| `jurisprudence-cle.md` | 5-8 decisions per domain | 12-15 per domain, aligned with domain files |
| `glossaire.md` | ~80-100 terms FR↔EN | ~150-180 terms, add procedural and EU terms |
| `sources.md` | Legal database search guide | Enrich with additional databases and search tips per domain |

---

## Files Modified Summary

| File | Type of change |
|------|---------------|
| `SKILL.md` | Add Complex Case Protocol block (~250 words) + modify Research Protocol (~180 words) + update Response Protocol for template #7 priority (~50 words) |
| `methodology.md` | Add Template #7 "Cas complexe" |
| `references/civil.md` | Enrich articles + jurisprudence + reforms |
| `references/penal.md` | Enrich articles + jurisprudence + reforms |
| `references/travail.md` | Enrich articles + jurisprudence + reforms |
| `references/affaires.md` | Enrich articles + jurisprudence + reforms |
| `references/administratif.md` | Enrich articles + jurisprudence + reforms |
| `references/numerique.md` | Enrich articles + jurisprudence + reforms |
| `references/europeen.md` | Enrich articles + jurisprudence + reforms |
| `references/procedure.md` | Enrich articles + jurisprudence + reforms |
| `references/codes-index.md` | Enrich structure (parties/livres/titres) |
| `references/jurisprudence-cle.md` | Enrich to 12-15 per domain |
| `references/glossaire.md` | Expand to ~150-180 terms |
| `references/sources.md` | Enrich with additional databases and search tips |

**Files created:** 0
**Files modified:** 14
**Estimated SKILL.md word count after v2:** ~1,820 words (1,338 current + ~250 Complex Case Protocol + ~180 Research Protocol changes + ~50 Response Protocol update) — well under 5,000 limit

---

## Out of Scope

- Full code integration (all articles of all codes) — too heavy, not maintainable
- Automatic update mechanism — web verification compensates
- New slash commands — existing 9 commands are sufficient
- New domain files — 7 domains + procedure cover all major branches
