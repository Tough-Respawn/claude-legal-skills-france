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

| Domaine | Domain | Skill auto-déclenchant | Fichier de référence |
|---------|--------|------------------------|----------------------|
| Droit civil | Civil law | `legal-france-civil` | `skills/legal-france-civil/references/civil.md` |
| Droit pénal | Criminal law | `legal-france-penal` | `skills/legal-france-penal/references/penal.md` |
| Droit du travail | Labor law | `legal-france-travail` | `skills/legal-france-travail/references/travail.md` |
| Droit des affaires | Business law | `legal-france-affaires` | `skills/legal-france-affaires/references/affaires.md` |
| Droit administratif | Administrative law | `legal-france-administratif` | `skills/legal-france-administratif/references/administratif.md` |
| Droit numérique | Digital law (GDPR) | `legal-france-numerique` | `skills/legal-france-numerique/references/numerique.md` |
| Droit européen | EU law | `legal-france-europeen` | `skills/legal-france-europeen/references/europeen.md` |
| Procédure | Procedural law | `legal-france` (meta) | `skills/legal-france/references/procedure.md` |

Références transversales / Cross-cutting references (méta skill `legal-france`) :
- `skills/legal-france/references/jurisprudence-cle.md` — 96 décisions clés / 96 landmark decisions
- `skills/legal-france/references/glossaire.md` — ~170 termes / ~170 terms
- `skills/legal-france/references/codes-index.md` — Index des codes français / Index of French legal codes
- `skills/legal-france/references/sources.md` — Sources officielles / Official sources

Tous les chemins sont relatifs à `plugins/legal-france/`.

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

### Étapes détaillées / Detailed steps

#### Étape 1 — Créer un compte PISTE

Allez sur [piste.gouv.fr](https://piste.gouv.fr) → bouton **"Créer un compte"** (en haut à droite). Remplissez le formulaire (email, mot de passe, acceptez les CGU, captcha). Validez par email.

#### Étape 2 — Créer une application **de PRODUCTION** (point critique)

> **Important** : à l'inscription, PISTE crée automatiquement une application **Sandbox** nommée `APP_SANDBOX_<votre-email>`. **Ne l'utilisez pas pour le plugin** — les credentials Sandbox utilisent une URL différente (`sandbox-oauth.piste.gouv.fr`) alors que le plugin appelle l'URL Production (`oauth.piste.gouv.fr`).
>
> Vous **devez créer une application de Production manuellement**.

1. Connecté à PISTE → menu **APPLICATIONS** → bouton **"Créer une application"**.
2. Renseignez :
   - **Nom de l'application** : unique, sans caractères spéciaux autres que `-` ou `_` (ex : `claude-legal-france`).
   - **Description**, **Email**, **Information sur la structure**, **Responsable d'application** (obligatoires).
   - Laissez **Activer l'application** coché.
3. Cliquez **"Sauvegarder l'application"**.

#### Étape 3 — Raccorder l'API Judilibre à votre application

1. Sur la fiche de votre nouvelle application, cliquez **"Modifier l'application"**.
2. Validez les CGU de l'API Judilibre via le lien **"Cliquez ici pour accéder à la page de consentement"** (rubrique "Consentement CGU API").
3. De retour sur la modification de l'application, cochez **Judilibre — Cour de cassation** dans le tableau "Sélectionner les API".
4. Cliquez **"Appliquer les modifications"**.

L'approbation est généralement automatique pour Judilibre (vérifiez que la case "Souscrite" devient grisée et cochée).

#### Étape 4 — Générer les identifiants Oauth (vos VRAIES clés)

> **Deux types d'identifiants existent dans l'onglet Authentification — utilisez le bon :**
> - **API Keys** — ce n'est PAS ce qu'utilise le plugin (méthode d'auth différente).
> - **Identifiants Oauth** — c'est ce qu'il faut.

1. Sur la fiche de votre application → onglet **"Authentification"**.
2. Section **"Identifiants Oauth"** → bouton **"Générer"**.
3. Dans la popup :
   - **Type d'application** : `Confidentiel` (sélectionné par défaut)
   - **URL de rappel** : laisser **vide** (pas nécessaire pour le flux Client Credentials utilisé par le plugin)
   - **Certificat X.509** : laisser **vide**
4. Cliquez **"Générer un identifiant"**.

Vous voyez maintenant dans la section "Identifiants Oauth" :
- **Client ID** (long identifiant alphanumérique) → c'est votre `PISTE_CLIENT_ID`.
- **Secret key** masqué → cliquez **"Consulter le client secret"** → bouton **"Copy"** pour copier le secret → c'est votre `PISTE_CLIENT_SECRET`.

> **Conservez le secret immédiatement** dans un gestionnaire de mots de passe. Vous pouvez le re-consulter à tout moment, mais PISTE recommande de le **régénérer tous les 3 mois** (action "Modifier" → "Régénérer" sur l'identifiant).

#### Étape 5 — Définir deux variables d'environnement

**Choisissez l'option qui correspond à votre setup** — une seule des deux suffit :

##### Option A — Settings Claude Code (recommandée, persiste, marche partout)

Ouvrez `~/.claude/settings.json` (Linux/macOS) ou `%USERPROFILE%\.claude\settings.json` (Windows) et ajoutez le bloc `env` :

```json
{
  "env": {
    "PISTE_CLIENT_ID": "votre_client_id",
    "PISTE_CLIENT_SECRET": "votre_client_secret"
  }
}
```

Si le fichier contient déjà d'autres clés, fusionnez le bloc `env` avec l'existant. Pas besoin de relancer le terminal — relancez juste la session Claude Code.

##### Option B — Variables d'environnement système (persistent globalement, utile si vous utilisez les creds avec d'autres outils)

**Linux / macOS** — ajoutez à la fin de `~/.bashrc`, `~/.zshrc` ou `~/.profile` :
```bash
export PISTE_CLIENT_ID="votre_client_id"
export PISTE_CLIENT_SECRET="votre_client_secret"
```
Puis `source ~/.bashrc` (ou rouvrez votre terminal).

**Windows** — méthode graphique :
1. Touche Windows → tapez "variables d'environnement" → ouvrir.
2. Cliquez "Variables d'environnement" → section "Variables utilisateur" → "Nouveau".
3. Créez `PISTE_CLIENT_ID` et `PISTE_CLIENT_SECRET` avec vos valeurs.
4. Rouvrez Claude Code (les variables sont lues au démarrage).

#### Étape 6 — Vérifier que tout marche

Invoquez `/jurisprudence harcèlement moral`. Trois cas possibles :

- **[OK] Citation au format `Cass. soc., date, n° pourvoi (Judilibre: id)`** → tout fonctionne, Judilibre répond.
- **[FALLBACK] Citation sans l'identifiant `(Judilibre: ...)` et footer mentionnant *"configurez l'API Judilibre"*** → les variables d'environnement ne sont pas détectées par Claude Code. Vérifiez votre fichier de config et relancez la session.
- **[ERREUR AUTH] Footer mentionnant une erreur d'authentification PISTE** → soit les identifiants sont incorrects, soit vous avez utilisé l'app **Sandbox** au lieu de Production. Régénérez une paire `Identifiants Oauth` dans votre **application de Production**.

### Quotas et bonnes pratiques

- **Quota par défaut en Production** : 20 requêtes / seconde. Largement suffisant pour un usage perso ou petite équipe. Au-delà, HTTP 429 et le plugin retombe sur le WebSearch Legifrance pour la requête en cours.
- **Sécurité** : ne commitez jamais vos credentials PISTE dans un repo Git. Le `.gitignore` du projet exclut déjà `.claude/` pour cette raison. Si vous suspectez une fuite, "Modifier" → "Régénérer" sur l'identifiant Oauth dans PISTE.
- **Rotation** : PISTE recommande de régénérer le `client_secret` tous les 3 mois.

---

## Versions

| Version | Date | Description |
|---------|------|-------------|
| **v3.0.0** | Mai 2026 | 8 skills modulaires (1 méta + 7 domaines), 10 modèles de documents, intégration API Judilibre, suite de tests / 8 modular skills, 10 document templates, Judilibre API integration, test suite |
| **v2.0.0** | Mars 2026 | Références enrichies, protocole cas complexes, vérification web obligatoire / Enriched references, complex case protocol, mandatory web verification |
| **v0.1.0** | Février 2026 | Version initiale / Initial release |

---

## Contribuer / Contributing

Pour enrichir les références :
- **Référence d'un domaine spécifique** : ajoutez dans `plugins/legal-france/skills/legal-france-<domaine>/references/<domaine>.md` (par exemple `legal-france-travail/references/travail.md`).
- **Référence transversale** (procédure, jurisprudence clé, glossaire, codes-index, sources) : ajoutez dans `plugins/legal-france/skills/legal-france/references/<fichier>.md`.

_To enrich references:_
- _Domain-specific: add to `plugins/legal-france/skills/legal-france-<domain>/references/<domain>.md`._
- _Cross-cutting (procedure, key case law, glossary, codes-index, sources): add to `plugins/legal-france/skills/legal-france/references/<file>.md`._

---

## Avertissement / Disclaimer

> **FR :** Ces informations sont fournies à titre indicatif et ne constituent pas un avis juridique. Les lois et la jurisprudence évoluent constamment. Consultez un avocat qualifié pour votre situation particulière.

> **EN:** This information is provided for educational and research purposes only. It does not constitute legal advice. Laws and case law evolve constantly. Always consult a qualified legal professional for specific situations.

---

## Licence / License

MIT — Copyright (c) 2026 Amine Harrak
