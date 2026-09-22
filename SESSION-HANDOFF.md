# SESSION-HANDOFF.md — skillinjection / sleeperattack

État technique du dépôt à la fin de la dernière session. La trajectoire et les
décisions prises ailleurs vivent dans le Brain (`seo-attack-pages`), pas ici.

---

## Session du 2026-09-22

**Sujet :** première correction d'auteur reçue (SkillsMetric, arXiv 2608.08468)
et appliquée sur `/skill-scanner-evasion/` ; relecture Search Console.

### Ce qui a été établi (prouvé, pas supposé)

- **Les deux URL sont dans l'index Google** (inspection d'URL en direct, via
  l'extension Chrome) : la home est **revenue** dans l'index et
  `/skill-scanner-evasion/` y est **entrée en moins de 48 h** (explorée le
  20/09 à 20:36, juste après la demande). Le rapport Pages, daté du 18/09,
  affiche encore 0 dans l'index et 3 « explorées, non indexées » (home en
  https / http / www) : il est en retard sur l'inspection, pas contradictoire.
- Sitemap lu le 20/09, 2 URL découvertes, « Opération effectuée ». Pas relu
  depuis le changement de `lastmod` du 22/09.
- Deux incohérences côté Google, à relire plutôt qu'à corriger : l'inspection
  de la nouvelle page dit « Sitemaps : erreur de traitement temporaire » et
  « aucune page d'origine détectée », alors que l'écran Sitemaps est vert.
- Non prouvé : la date d'exploration de la home (le panneau de détail ne
  s'ouvrait pas à l'écran ; la valeur lue dans le DOM était identique à celle
  de l'autre URL, donc possiblement résiduelle).
- PR OWASP #87 et PR awesome-list #70 : ouvertes, 0 revue, 0 commentaire.

### Ce qui a été fait (et vérifié)

1. **Correction SkillsMetric** (`e2b8d57`), sur mail de Xinze Chen (premier
   auteur) reçu par Damien : partie expérimentale incomplète, deux tests de
   détection statique sur des jeux de données différents et possiblement
   chevauchants, résultats « pas particulièrement rigoureux », méthodes
   d'attaque présentées comme hypothèses. Sur la page : AUC 0.93 · F1 73.4 %
   marqués « (preliminary) » avec la réserve attribuée nommément dans la
   ligne du tableau ; ventilation par type d'attaque (93 / 93 / 0 / 42 %)
   retirée en bloc ; FAQ (HTML == JSON-LD, vérifié par script) et Sources
   réattribuent la réserve à l'auteur, plus au papier. Son avis sur la
   prudence des modèles (hors sujet) non repris. `dateModified`, pied de page
   et `lastmod` du sitemap au 2026-09-22 ; la home n'a pas bougé.
   Aucune autre page (home, sleeperattack) ne reprenait ces chiffres.
   Déploiement prouvé : workflow `success`, empreintes servi == commit.
2. **Search Console** : nouvelle indexation demandée pour
   `/skill-scanner-evasion/` (confirmation « Indexation demandée »). Rien
   demandé pour la home, inchangée depuis son exploration.
3. **Réponse à Xinze Chen envoyée par Damien** le 2026-09-22 (remerciement,
   lien vers la ligne corrigée, demande de lien depuis sa page projet).
   Consigné dans `OUTREACH-2026-09-20.md` (`1497f1b`).

## État des dépôts

| | skillinjection | sleeperattack |
|---|---|---|
| dernier commit | `1497f1b` (docs) ; page corrigée `e2b8d57` | inchangé depuis le 2026-09-20 |
| `main` == `origin/main` | oui | oui |

Site skillinjection.com à jour, prouvé par empreinte le 2026-09-22.

## Reste à faire

**À relire (vers le 2026-09-29) :**
- [ ] Rapport Pages : doit passer à 2 dans l'index (rattrapage du rapport).
- [ ] Sitemaps : « Dernière lecture » postérieure au 22/09 ?
- [ ] Inspection de `/skill-scanner-evasion/` : exploration postérieure au
      22/09 (version corrigée), et disparition de « erreur de traitement
      temporaire » / « aucune page d'origine ».
- [ ] Le 2026-10-20 : confronter `PREVISION-2026-09-20.md` aux chiffres.

**À surveiller :**
- [ ] Réponses des 3 autres auteurs (Cloak and Detonate, SkillVetBench,
      Bruce W. Lee) et retour de Xinze Chen sur le lien. Pas de relance
      avant le 2026-10-11.
- [ ] PR OWASP #87 et PR awesome-list #70.

**Bloqué sur Damien :**
- [ ] Valider la propriété `https://sleeperattack.com/` dans Search Console.
- [ ] Rendu mobile (< 560 px) de la home section 09 et de
      `/skill-scanner-evasion/` sur téléphone.

**Proposé, sans GO :**
- [ ] Page « vs » #1 « skill injection vs prompt injection », à arbitrer sur
      les impressions (quasi toutes sur « skill injection »).
- [ ] Sortir « Recent research » de la home vers une page dédiée si la
      liste continue de grossir (home à 2 308 mots).
- [ ] Contrôle de fraîcheur hors GitHub.
- [ ] Bootstrap restant : CLAUDE.md projet, template Bureau.

## Décisions structurelles

- **Une correction d'auteur s'applique en bloc, pas à la carte** : quand un
  auteur qualifie un test de non rigoureux, on retire toute la ventilation
  issue de ce test, y compris les chiffres flatteurs, et on garde seulement
  le chiffre global marqué préliminaire avec la réserve attribuée.
- **Attribuer la réserve à qui l'a émise** : un mail d'auteur est une réserve
  de l'auteur, pas une position du papier ; la page dit « its first author »,
  jamais « the paper describes ».
- **Paraphrase fidèle aux nuances** : « not particularly rigorous » ne
  devient pas « not rigorous » ; « merely offered some hypotheses » devient
  « offered as hypotheses ». Le mail complet est relu avant publication.

## Comment reprendre

1. Lire ce fichier, puis `C:\brain\projets\seo-attack-pages\STATE.md` et son
   dernier fichier dans `C:\brain\sessions\`.
2. `git log -3` + `git status` dans les deux dépôts — attendre `main` ==
   `origin/main`.
3. Search Console via l'extension Chrome (compte Google de Damien connecté).
   Si « extension non connectée » alors que Chrome tourne :
   `list_connected_browsers` puis `select_browser` sur le Chrome local, ça
   suffit sans relancer Chrome. Saisie d'URL : `form_input` sur la référence
   du champ « Inspecter n'importe quelle URL », puis Entrée ; l'URL directe
   `/inspect?id=<url>` renvoie un 404. Clics : préférer `ref` aux
   coordonnées, l'échelle de la capture peut dériver.
4. Preuve de fraîcheur = empreinte servi == commit, ou run du workflow. Jamais
   un code HTTP.
5. Builds Pages coincés : `gh api -X POST repos/Arlenjim/<repo>/pages/builds`.
6. Toute nouvelle référence : page `arxiv.org/abs` + API `id_list`, résumé
   complet lu avant de citer un chiffre. Toute correction d'auteur : mail
   complet relu, paraphrase, attribution, jamais de citation du mail.
