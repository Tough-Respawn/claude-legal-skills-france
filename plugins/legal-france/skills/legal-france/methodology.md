# Response Templates — legal-france

This file defines the six structured response templates used by the legal-france skill. Each template includes trigger conditions, section structure, tone guidance, and an example skeleton. The template to use is selected by `SKILL.md`'s Response Protocol (command > role > request nature).

---

## Core Principle

The **syllogisme juridique** (legal syllogism) is the backbone of all professional response formats:

- **Majeure** — The abstract legal rule ("According to Art. X, the law provides that...")
- **Mineure** — The application to the specific facts ("In the present case, the facts show that...")
- **Conclusion** — The motivated legal outcome ("Therefore, it follows that...")

Every consultation, cas pratique, and explication must be anchored in this three-part logical structure, even when condensed for plain-language responses.

---

## Template 1 — Consultation juridique (Legal Consultation)

**Trigger conditions:**
- User role is `lawyer` or `judge`
- User invokes `/droit` (or any domain command) and role is detected as `lawyer` or `judge`
- User phrases their request as a professional seeking advice on a client situation
- Question requires a formal legal opinion with applicable texts and reasoning

**Tone:** Formal, precise, professional. Use full legal terminology. Latin maxims are acceptable when they add precision. Structure must be tight and complete — this is a professional document.

**Section structure:**

### 1. Rappel des faits (Statement of Facts)
Restate the pertinent facts as provided by the user, legally qualified. Distinguish between established facts and alleged facts. Identify legally relevant elements (dates, parties, legal relationship, acts performed). Keep this section factual — no legal analysis yet.

### 2. Problème de droit (Legal Issue)
Reformulate the user's question as a precise legal issue. Use interrogative form: "La question est de savoir si..." / "The question is whether..." Identify the applicable branch of law and narrow the issue to its essential legal tension.

### 3. Règle applicable (Applicable Rule)
State the relevant statutory texts with full citations (article numbers, code name, version in force). Add the dominant case law position: leading decisions, jurisprudential evolution, doctrinal consensus if relevant. If there is a contested area, present the competing interpretations.

### 4. Application — Syllogisme (Application)
Apply the rule to the facts using the three-part syllogism:
- **Majeure:** State the rule abstractly ("Art. 1240 C. civ. provides that any act causing damage to another obliges the person by whose fault it occurred to repair it.")
- **Mineure:** Apply rule to facts ("In the present case, the defendant's action on [date] directly caused damage to the claimant by...")
- **Conclusion:** State the legal outcome ("It therefore follows that the defendant is liable and owes compensation for...")

### 5. Solutions & recommandations (Options and Advice)
Compare available legal options (litigation, negotiation, administrative remedy, etc.) with their respective advantages, risks, costs, and timelines. Give a concrete recommendation. Where urgency applies, note procedural deadlines (prescription, délai de forclusion).

### 6. Mise en garde (Disclaimer)
End with the mandatory disclaimer in the user's language.

**Example skeleton:**

```
## Consultation juridique

**Rappel des faits**
M. X, salarié en CDI depuis le [date], a été licencié pour faute grave par lettre du [date]...

**Problème de droit**
La question est de savoir si le licenciement pour faute grave est justifié au regard des exigences posées par l'article L. 1234-1 du Code du travail.

**Règle applicable**
Aux termes de l'art. L. 1234-1 C. trav., la faute grave prive le salarié de l'indemnité de préavis...
La chambre sociale a précisé que... (Cass. soc., [date], n° [pourvoi])

**Application**
Majeure : La faute grave s'entend de tout fait ou ensemble de faits imputables au salarié...
Mineure : En l'espèce, les faits reprochés consistent en...
Conclusion : Il s'ensuit que...

**Solutions & recommandations**
Option 1 — Contestation devant le CPH : ...
Option 2 — Négociation transactionnelle : ...
Recommandation : ...

---
*Ces informations sont fournies à titre indicatif et ne constituent pas un avis juridique...*
```

---

## Template 2 — Cas pratique (Practical Case Analysis)

**Trigger conditions:**
- User role is `student`
- User invokes `/droit` (or any domain command) and role is detected as `student`
- User describes a hypothetical fact scenario and asks for legal analysis
- User mentions "devoir", "TD", "exercice", "cas pratique"

**Tone:** Academic, pedagogical, methodologically rigorous. This is a teaching format — show all reasoning steps explicitly. Avoid shortcuts. The syllogisme must be fully visible.

**Section structure:**

### 1. Faits (Facts)
Select only the legally relevant facts from the scenario. Briefly qualify them in legal terms ("les parties sont liées par un contrat de vente..."). Discard legally irrelevant details. Do not yet state any legal rule.

### 2. Problème de droit (Legal Issue)
Formulate the legal question in interrogative form, precisely and abstractly: "La question est de savoir si..." The issue must be general enough to prompt a rule statement but specific enough to be answerable. Avoid restating the facts here.

### 3. Majeure (Abstract Rule)
Begin: "Selon l'article X de [Code], ..." or "La jurisprudence de la Cour de cassation a posé que..." State the applicable rule in full, abstractly, without any reference to the facts. If multiple rules apply, state each one separately.

### 4. Mineure (Application to Facts)
Begin: "En l'espèce, ..." Apply the abstract rule to the specific facts of the case. Each element of the rule must be tested against the facts. Be explicit about which facts satisfy (or fail to satisfy) which elements of the rule.

### 5. Conclusion (Legal Solution)
State the motivated legal outcome clearly. If the case is uncertain, present both possible outcomes and explain what would determine the result. End with any procedural consequence (remedy available, competent court, deadline).

**Tone note:** The conclusion must be motivated — "Therefore X because Y" — not just "X wins." The reasoning chain must be visible at every step.

**Example skeleton:**

```
## Cas pratique

**Faits**
En l'espèce, Mme A et M. B ont conclu le [date] un contrat de vente portant sur...

**Problème de droit**
La question est de savoir si le vice caché affectant la chose vendue ouvre droit à l'action rédhibitoire.

**Majeure**
Selon l'article 1641 du Code civil, le vendeur est tenu de la garantie à raison des défauts cachés de la chose vendue...

**Mineure**
En l'espèce, le défaut était antérieur à la vente, inconnu de l'acheteur au moment de la conclusion du contrat, et suffisamment grave pour rendre la chose impropre...

**Conclusion**
Il s'ensuit que Mme A dispose de l'action rédhibitoire prévue à l'article 1644 C. civ., lui permettant de rendre la chose et de se faire restituer le prix...
```

---

## Template 3 — Commentaire d'arrêt (Case Commentary)

**Trigger conditions:**
- User provides a court decision (full text or citation) and asks for analysis
- User provides a court decision via any command and role is `student`
- User mentions "commenter", "analyser cet arrêt", "fiche d'arrêt"
- User role is `student` and provides a decision

**Tone:** Academic and critical. The commentaire d'arrêt is not a summary — it is an analytical exercise. The student must explain what the court decided, why, how it fits into (or departs from) existing law, and what its broader significance is.

**Section structure:**

### 1. Fiche d'arrêt (Case Summary)
Structured summary with: facts (only legally relevant), procedural history (which courts, in which order, what they decided), parties' claims and arguments, precise legal issue, and the court's holding (solution). This section is purely descriptive — no evaluation yet.

### 2. Sens — Explanation of the Decision
Explain the court's legal reasoning. Why did it reach this result? Which rule did it apply, and how did it interpret it? Identify the legal basis relied upon. Explain the logical structure of the reasoning. Highlight any significant interpretive choice made by the court.

### 3. Valeur — Critical Assessment
Evaluate the decision critically. Is it consistent with prior case law (confirmation, reversal, evolution)? Does it align with statutory text or depart from it? What do legal scholars (doctrine) say? Is the decision equitable? Could it have been decided differently?

### 4. Portée — Significance and Impact
Assess the decision's legal impact. Is it an isolated case or does it signal a jurisprudential trend? What is its authority (Assemblée plénière = highest authority; chambre simple = more limited)? Has it been followed by subsequent decisions or overruled? What does it change for practitioners?

**Example skeleton:**

```
## Commentaire d'arrêt — Cass. civ. 3e, [date], n° [pourvoi]

**Fiche d'arrêt**
Faits : ...
Procédure : La cour d'appel de [ville] a jugé que... / Un pourvoi en cassation a été formé.
Problème de droit : La question est de savoir si...
Solution : La Cour de cassation casse / rejette, en jugeant que...

**Sens**
La Cour a raisonné en deux temps. D'abord, elle a retenu que... Ce faisant, elle a interprété l'article X comme...

**Valeur**
Cette solution s'inscrit dans / rompt avec la lignée jurisprudentielle...
La doctrine avait anticipé / critiqué cette orientation...

**Portée**
Cet arrêt constitue un arrêt de principe / d'espèce. Il a pour conséquence de...
```

---

## Template 4 — Recherche de jurisprudence (Case Law Research)

**Trigger conditions:**
- User invokes `/jurisprudence <topic>`
- User explicitly asks to "find", "search for", or "compile" case law on a topic
- User asks about the current state of jurisprudence on a legal question

**Tone:** Research-oriented, systematic, neutral. Present findings objectively with full citations. Analyze trends without advocacy. Distinguish between binding decisions (Assemblée plénière, Cour de cassation) and persuasive authority (Cours d'appel, doctrine).

**Section structure:**

### 1. Termes de recherche (Search Parameters)
State the keywords used, the legal domain, the relevant articles, the time range considered, and the courts targeted. This makes the research reproducible and transparent.

### 2. Décisions trouvées (Decisions Found)
For each relevant decision, provide:
- Court and chamber
- Date
- Pourvoi / requête number
- One-sentence summary of the holding
- Legifrance or EUR-Lex URL if retrieved via WebFetch

Present decisions chronologically or grouped by sub-question.

### 3. Analyse — Jurisprudential Trend
Synthesize the decisions found. What is the dominant position? Has there been an evolution (before/after a landmark decision)? Are there contradictions between chambers or between courts? What does the current state of the law appear to be?

### 4. Sources (Citations and Links)
Full citations in correct French legal format. Direct links to Legifrance records where available. Note any decisions that could not be verified.

**Example skeleton:**

```
## Recherche de jurisprudence — [Topic]

**Termes de recherche**
Domaine : droit du travail | Mots-clés : licenciement, faute grave, télétravail
Articles concernés : L. 1234-1, L. 1237-19 C. trav.
Période : 2018-2025 | Juridictions : Cass. soc., Cours d'appel

**Décisions trouvées**
1. Cass. soc., [date], n° [pourvoi] — La Cour a jugé que...
2. CA Paris, [date], n° [RG] — La cour a retenu que...

**Analyse**
La jurisprudence est constante sur le point X, mais divisée sur Y...
Depuis l'arrêt [date], on observe une tendance vers...

**Sources**
- Cass. soc., [date], n° [pourvoi] : https://www.legifrance.gouv.fr/...
- Art. L. 1234-1 C. trav. : https://www.legifrance.gouv.fr/...
```

---

## Template 5 — Analyse de document (Document Analysis)

**Trigger conditions:**
- User provides a contract, terms of service, employment agreement, privacy policy, or other legal document
- User provides a document via any command and role is `business` or request nature involves a document
- User asks to "review", "check", "analyze" a document they have provided
- User role is `business` and submits a document

**Tone:** Professional, compliance-focused, risk-oriented. Be systematic and complete. Flag every potentially problematic clause — the user is relying on this analysis to make decisions. Be direct about risks without being alarmist.

**Section structure:**

### 1. Résumé du document (Document Summary)
Nature of the document (contract type, governing law), parties and their roles, main purpose and scope, key dates (effective date, duration, renewal terms), applicable law and jurisdiction clause.

### 2. Clauses sensibles (Sensitive Clauses)
Identify each clause that is potentially problematic, unfair, non-compliant, or unusual. For each clause:
- Quote the relevant passage
- Identify the legal issue it raises
- Cite the applicable rule (article or regulation)
- Rate the risk level: low / medium / high

### 3. Conformité (Compliance Check)
Assess the document's overall compliance with applicable French and EU law. Areas to check (as relevant): consumer law (Code de la consommation), RGPD/data protection, labor law, commercial law, unfair terms (clauses abusives), mandatory provisions that cannot be contracted out of.

### 4. Recommandations (Recommended Modifications)
List specific changes to make the document compliant and protect the user's interests. For each recommendation: identify the clause, state the problem, propose corrective language or approach, note urgency.

**Example skeleton:**

```
## Analyse de document — [Document title / type]

**Résumé**
Type : Contrat de prestation de services | Parties : Société A (prestataire) / M. B (client)
Durée : 12 mois à compter du [date] | Droit applicable : droit français | For : Tribunal de commerce de Paris

**Clauses sensibles**
Clause 7.3 (limitation de responsabilité) : "Le prestataire ne pourra être tenu responsable..."
Problème : Cette clause exclut toute responsabilité y compris en cas de faute lourde, ce qui est nul selon l'art. 1231-3 C. civ.
Risque : ÉLEVÉ

**Conformité**
RGPD : La clause de traitement des données (art. 12) ne précise pas la durée de conservation — non conforme à l'art. 13 RGPD.
Clauses abusives : ...

**Recommandations**
1. Clause 7.3 : Supprimer l'exclusion totale de responsabilité. Remplacer par un plafonnement limité aux dommages directs.
2. Art. 12 : Ajouter une durée de conservation déterminée et les droits des personnes concernées.
```

---

## Template 6 — Explication vulgarisée (Plain Language Explanation)

**Trigger conditions:**
- User role is `citizen` (detected or default)
- User invokes `/droit` (or any domain command) and role is `citizen` (or default)
- User asks a simple, non-technical legal question in plain language
- No contract or case provided — just a general legal question

**Tone:** Accessible, warm, and clear. No Latin, no legal jargon unless immediately explained. Use short sentences. Focus on what the person needs to do, not on legal theory. Practical steps are more important than doctrinal precision.

**Section structure:**

### 1. Réponse courte (Short Answer)
One to two sentences. Answer the question directly. No conditions, no hedging — just the clearest possible answer to what was asked. The user should understand the answer before reading any further.

### 2. Explication (Context)
Explain the answer in plain language. Give enough background for the user to understand why the law says what it says. Use analogies if helpful. Avoid "however" walls of caveats — save nuance for the next section.

### 3. Ce que dit la loi (What the Law Says)
Cite the relevant article in simplified form: "Article 2224 of the Civil Code says you have 5 years to file a claim after you discover the damage." Provide the Legifrance or service-public.fr link if retrieved. Do not quote full article text — paraphrase clearly.

### 4. Que faire concrètement (Practical Steps)
Numbered list of concrete actions. Include: who to contact, what to say or write, relevant deadlines, which authority or court is involved, whether a lawyer is required or optional.

### 5. Pour aller plus loin (Further Resources)
Links to service-public.fr for the relevant procedure. Suggest consulting a lawyer (and mention free consultations available at Maisons de Justice et du Droit). Note any free legal aid (aide juridictionnelle) if relevant.

**Example skeleton:**

```
## Explication

**Réponse courte**
Oui, votre employeur doit vous remettre un bulletin de salaire à chaque paie — c'est une obligation légale.

**Explication**
Le bulletin de salaire est le document qui détaille votre rémunération, les cotisations sociales prélevées, et les heures travaillées...

**Ce que dit la loi**
L'article L. 3243-2 du Code du travail impose à tout employeur de remettre un bulletin de paie au salarié à chaque versement de salaire.
Source : https://www.legifrance.gouv.fr/...

**Que faire concrètement**
1. Demandez le bulletin par écrit (e-mail ou lettre) à votre employeur ou service RH.
2. Si l'employeur refuse, signalez-le à l'Inspection du travail.
3. Délai de prescription pour agir : 3 ans (art. L. 3245-1 C. trav.).

**Pour aller plus loin**
- service-public.fr : https://www.service-public.fr/particuliers/vosdroits/F559
- Consultez gratuitement un juriste à la Maison de Justice et du Droit de votre ville.

---
*Ces informations sont fournies à titre indicatif et ne constituent pas un avis juridique. Consultez un avocat pour votre situation particulière.*
```
