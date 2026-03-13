---
description: Ask any question about French law — routes to the right domain automatically
argument-hint: <your legal question>
allowed-tools: [Read, Grep, Glob, WebSearch, WebFetch]
---

Invoke the `legal-france` skill to answer the user's question.

## Workflow
1. Detect the legal domain from the question keywords
2. Read the relevant `references/<domain>.md` file from the skill directory
3. Also read `references/codes-index.md` for quick article lookup
4. Apply the response template matching the user's role (see methodology.md)
5. If embedded references are insufficient, use WebSearch to query Legifrance
6. Cite all sources precisely (article numbers, decision references)
7. End with the mandatory legal disclaimer
