---
description: French civil law — contracts, liability, property, family, inheritance
argument-hint: <your civil law question>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---

Invoke the `legal-france` skill to answer the user's question.

## Workflow
1. Skip domain routing — read `references/civil.md` directly
2. Also read `references/codes-index.md` for quick article lookup
3. Apply the response template based on detected user role (see SKILL.md Response Protocol)
4. If embedded references are insufficient, use WebSearch to query Legifrance
5. Cite all sources precisely (article numbers, decision references)
6. End with the mandatory legal disclaimer
