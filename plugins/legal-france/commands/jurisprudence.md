---
description: Search French case law, landmark decisions, and jurisprudential trends
argument-hint: <search terms, article number, or legal topic>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---

Invoke the `legal-france` skill with the case law research template to answer the user's question.

## Workflow
1. Search `references/jurisprudence-cle.md` first
2. WebSearch Legifrance, EUR-Lex for additional results
3. Parse local documents if the user provides them
4. Use the "Recherche de jurisprudence" response template from methodology.md
5. Cite all sources with decision numbers and dates
