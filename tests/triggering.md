# Triggering Test Scenarios — legal-france v3

These scenarios verify that the right skill auto-triggers (without forcing
via "demande à legal" or a slash command). To run: in a fresh Claude Code
session with the plugin loaded, paste each user phrasing and verify which
skill activates. Pass = the matching skill activates first. Fail = the user
must force-trigger.

---

## Positive cases (21) — must trigger the listed skill

### Civil (3)
| # | User phrasing | Expected skill | Rationale |
|---|---|---|---|
| C1 | mon proprio refuse de me rendre la caution | legal-france-civil | "proprio" + "caution" in description |
| C2 | ma femme veut divorcer, on a un enfant | legal-france-civil | "divorcer" + "enfant" everyday phrasing |
| C3 | j'ai acheté un produit défectueux sur internet, je peux le retourner ? | legal-france-civil | consumer/civil + everyday |

### Travail (3)
| # | User phrasing | Expected skill | Rationale |
|---|---|---|---|
| T1 | j'ai été viré, j'ai quoi comme indemnités ? | legal-france-travail | "viré" + "indemnités" |
| T2 | mon patron veut me faire signer une rupture conventionnelle | legal-france-travail | "patron" + "rupture conventionnelle" |
| T3 | combien d'heures sup max par semaine ? | legal-france-travail | "heures sup" allusion |

### Pénal (3)
| # | User phrasing | Expected skill | Rationale |
|---|---|---|---|
| P1 | comment porter plainte contre un voisin ? | legal-france-penal | "porter plainte" |
| P2 | j'ai reçu une amende, je peux la contester ? | legal-france-penal | "amende" + "contester" |
| P3 | mon fils a été placé en garde à vue, on fait quoi ? | legal-france-penal | "garde à vue" |

### Affaires (3)
| # | User phrasing | Expected skill | Rationale |
|---|---|---|---|
| A1 | je veux créer une SAS, c'est compliqué ? | legal-france-affaires | "SAS" |
| A2 | mon client refuse de me payer ma facture, je fais quoi ? | legal-france-affaires | unpaid invoice (commercial) |
| A3 | comment déposer une marque ? | legal-france-affaires | "déposer une marque" |

### Administratif (3)
| # | User phrasing | Expected skill | Rationale |
|---|---|---|---|
| AD1 | la préfecture refuse ma demande de naturalisation | legal-france-administratif | "préfecture" + "naturalisation" |
| AD2 | la CAF me réclame un trop-perçu, je peux contester ? | legal-france-administratif | "CAF" + "contester" |
| AD3 | comment faire un recours gracieux ? | legal-france-administratif | "recours gracieux" |

### Numérique (3)
| # | User phrasing | Expected skill | Rationale |
|---|---|---|---|
| N1 | il faut un bandeau cookies sur mon site ? | legal-france-numerique | "bandeau cookies" |
| N2 | quelqu'un publie ma photo sur Facebook sans mon accord | legal-france-numerique | data privacy / image |
| N3 | je veux exercer mon droit à l'oubli sur Google | legal-france-numerique | "droit à l'oubli" + "Google" |

### Européen (3)
| # | User phrasing | Expected skill | Rationale |
|---|---|---|---|
| E1 | que dit la CJUE sur le RGPD ? | legal-france-europeen | "CJUE" |
| E2 | cette directive a-t-elle été transposée en France ? | legal-france-europeen | "directive" + "transposée" |
| E3 | quels sont mes droits en tant que citoyen européen vivant en France ? | legal-france-europeen | "citoyen européen" |

---

## Negative cases (6) — must NOT trigger any legal-france skill

| # | User phrasing | Why no trigger |
|---|---|---|
| NEG1 | comment faire une boucle for en Python ? | programming |
| NEG2 | donne-moi une recette de tarte aux pommes | cooking |
| NEG3 | calcule 17 × 39 | arithmetic |
| NEG4 | quelle est la capitale de l'Australie ? | general knowledge |
| NEG5 | écris un poème sur l'automne | creative writing |
| NEG6 | comment configurer un serveur nginx ? | sysadmin |

---

## Borderline cases (3) — accepted either way, document outcome

| # | User phrasing | Reasonable skills | Notes |
|---|---|---|---|
| B1 | j'ai un problème avec mon abonnement Spotify | legal-france-civil (conso) OR no trigger | If triggers: civil OK |
| B2 | mon site marketing parle d'un concurrent | legal-france-affaires (parasitism) OR legal-france-numerique (LCEN) OR no | Either is fine if it triggers |
| B3 | mon employeur a demandé mon dossier médical | legal-france-travail (preferred) OR legal-france-numerique (data protection) | Should trigger one of the two |

---

## Multi-domain cases (3) — should engage the meta skill `legal-france`

| # | User phrasing | Why meta |
|---|---|---|
| M1 | mon entreprise me licencie après que j'ai signalé une fuite de données RGPD à la CNIL | travail + numérique + lanceur d'alerte = genuine cross-domain |
| M2 | je veux contester une amende et porter plainte pour usurpation d'identité | pénal + procédure transversale |
| M3 | quel est le délai de prescription en général ? | transversal procedural |

---

## Pass/Fail record

| Date | Case ID | Triggered skill | Pass/Fail | Notes |
|---|---|---|---|---|
| _ | _ | _ | _ | _ |
