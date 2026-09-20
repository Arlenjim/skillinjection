# SESSION-HANDOFF.md — skillinjection / sleeperattack

État technique du dépôt à la fin de la dernière session. La trajectoire et les
décisions prises ailleurs vivent dans le Brain (`seo-attack-pages`), pas ici.

---

## Session du 2026-09-20

**Sujet :** « faire vivre la page » skillinjection.com — déblocage du
déploiement, enrichissement, Search Console, puis construction de la première
page dédiée du domaine pour rendre le site liable (route 1 du plan backlinks).
Précédée d'une PR de contribution pure vers
`LLMSecurity/awesome-agent-skills-security` (#70, en attente de revue).

### Ce qui a été établi (prouvé, pas supposé)

- **Search Console (lu via l'extension Chrome, compte connecté)** : la home a
  été **indexée du ~16/08 au ~03/09 puis éjectée** (« Explorée, actuellement
  non indexée »). Dernière exploration 19/09, tout autorisé : jugement de
  valeur, pas blocage. 3 mois : 236 impressions, 6 clics, position 7,2.
  Cause la plus probable : **aucun lien entrant connu de Google**.
- **Le sitemap n'avait jamais été lu** (soumis 17/08, « Impossible de
  récupérer », 0 page) bien que servi en 200.
- **Builds Pages bloqués 25 jours** après la panne du 26/08 ; débloqués par
  `gh api -X POST repos/<owner>/<repo>/pages/builds`.
- **sleeperattack.com n'est pas une propriété validée** dans Search Console.
- Détail et leçons dans `SEO-PROCESS.md`, « Constats de terrain (2026-09-20) ».

### Ce qui a été fait (et vérifié)

1. Pages débloqué ; commits en attente poussés ; `sleeperattack` reconstitué
   (workflow + `SEO-PROCESS.md` identiques, md5 vérifié). Premier run réel de
   `verifier-mise-en-ligne.yml` : `success` sur les deux dépôts.
2. Home enrichie : 7 papiers 2026 (section 09), paragraphe section 04, phrase
   Trail of Bits corrigée et liée, dates au 2026-09-20. Déploiement prouvé.
3. Search Console : sitemap re-soumis, indexation de la home demandée
   (confirmation affichée).
4. **Nouvelle page `/skill-scanner-evasion/`** (`5e374e2`) : deux tableaux —
   attaques (taux d'évasion) et détecteurs (taux de détection) — pour 14
   papiers + Trail of Bits, chaque chiffre pris dans le résumé arXiv et
   vérifié page `abs` + API, avec la définition de succès à côté. FAQ (4) ==
   JSON-LD caractère par caractère. Deux liens depuis le corps de la home,
   ancre « skill scanner evasion ». Sitemap à 2 URL. Règles CSS `.cmp` en fin
   de `style.css`. Rendu vérifié en Chrome headless (l'extension s'était
   déconnectée), défaut de tableau attrapé et corrigé. Déploiement prouvé :
   workflow `success`, 4/4 empreintes servi == commit, page en 200.
5. `PREVISION-2026-09-20.md` : prévision datée (28 jours, trois scénarios,
   probabilités), à confronter le 2026-10-20.
6. `OUTREACH-2026-09-20.md` : 5 cibles pour un lien suivi, `rel` vérifié sur
   le HTML servi (0 nofollow), angle par cible, brouillon, règles. **Rien
   d'envoyé** — chaque message part sur GO explicite de Damien.
7. `SEO-PROCESS.md` mis à jour dans les deux dépôts (identiques).

## État des dépôts

`main` == `origin/main` des deux côtés après les commits de docs ci-dessous.

| | skillinjection | sleeperattack |
|---|---|---|
| nouvelle page + home + sitemap + CSS | `5e374e2` | — |
| home enrichie | `67762a7` | — |
| workflow de contrôle | `8377bd4` | `cdf7610` |
| `SEO-PROCESS.md` | dernier commit docs | dernier commit docs |

Sites en ligne à jour, prouvé par empreinte.

## Reste à faire

**Non fait ce jour, à faire dès que l'extension Chrome est reconnectée :**
- [ ] Search Console : **demander l'indexation de
      `https://skillinjection.com/skill-scanner-evasion/`** et **re-soumettre
      `sitemap.xml`** (il a maintenant 2 URL). L'extension s'est déconnectée
      pendant la construction de la page ; sans elle, Damien le fait à la
      main (inspection d'URL → « Demander une indexation » ; Sitemaps →
      `sitemap.xml` → Envoyer).

**À relire (2–3 semaines) :**
- [ ] Rapport Pages : home revenue dans l'index ? nouvelle page indexée ?
- [ ] Sitemaps : « Dernière lecture » remplie ? Sinon creuser.
- [ ] Le 2026-10-20 : confronter `PREVISION-2026-09-20.md` aux chiffres.

**Bloqué sur Damien :**
- [ ] Route 2 : choisir les cibles de `OUTREACH-2026-09-20.md` et donner le
      GO message par message (recommandé pour commencer : OWASP AST10 + les 3
      auteurs cités).
- [ ] Valider la propriété `https://sleeperattack.com/` dans Search Console.
- [ ] Rendu mobile (< 560 px) de la home section 09 et de la nouvelle page :
      les tableaux défilent horizontalement (`overflow-x:auto`), à voir sur
      téléphone.

**Proposé, sans GO :**
- [ ] Page « vs » #1 « skill injection vs prompt injection », à arbitrer sur
      les 236 impressions (quasi toutes sur « skill injection »).
- [ ] Sortir la liste « Recent research » de la home vers une page dédiée si
      elle continue de grossir (home à 2 308 mots).
- [ ] Contrôle de fraîcheur hors GitHub.
- [ ] Bootstrap restant : CLAUDE.md projet, template Bureau.

## Comment reprendre

1. Lire ce fichier, puis `C:\brain\projets\seo-attack-pages\STATE.md` et son
   dernier fichier `sessions/`.
2. `git log -3` + `git status` dans les deux dépôts — attendre `main` ==
   `origin/main`.
3. Search Console via l'extension Chrome (compte Google de Damien connecté).
   Saisie : `form_input` sur la référence du champ, jamais la frappe simulée.
   Si l'extension est déconnectée : Chrome headless pour le rendu, et les
   clics Search Console reviennent à Damien.
4. Preuve de fraîcheur = empreinte servi == commit, ou run du workflow. Jamais
   un code HTTP.
5. Builds Pages coincés : `gh api -X POST repos/Arlenjim/<repo>/pages/builds`.
6. Toute nouvelle référence : page `arxiv.org/abs` + API `id_list`, résumé
   complet lu avant de citer un chiffre.
