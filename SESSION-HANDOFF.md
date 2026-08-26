# SESSION-HANDOFF.md — skillinjection / sleeperattack

État technique du dépôt à la fin de la dernière session. La trajectoire et les
décisions prises ailleurs vivent dans le Brain (`seo-attack-pages`), pas ici.

---

## Session du 2026-08-26 (2e session du jour)

**Sujet :** pourquoi les workflows « pages build and deployment » échouent sur
les deux dépôts alors que les sites sont en ligne et à jour.

### Ce qui a été établi (prouvé, pas supposé)

**Aucun workflow custom n'existait.** `.github/` était absent des deux dépôts
(404 sur l'API). Un seul workflow enregistré : `pages-build-deployment`, chemin
`dynamic/pages/…` — généré par GitHub, sans fichier correspondant. Il n'est ni
éditable ni supprimable sans désactiver Pages : il **est** le déploiement.

**Les échecs avaient deux causes distinctes, aucune liée au contenu.**

1. **2026-08-17 (#6/#7/#8) — échec *après* un déploiement réussi.** Le workflow
   enchaîne `build` → `deploy` → `report-build-status`. Cette dernière étape ne
   fait qu'envoyer une statistique à `repos/…/pages/telemetry`. Log littéral :
   `CONCLUSION: success`, puis `HTTP 503`, puis `exit 1`. Le run passe en échec
   alors que le site est déjà publié. Simultané sur les deux dépôts à 17:59:15,
   depuis deux régions Azure différentes → panne côté GitHub.
2. **2026-08-26 (#12/#13) — panne majeure d'Actions.** Incident `critical`
   ouvert à 15:11:58 UTC (`Actions=major_outage`). Le push de 15:26 est tombé
   14 min après. Les jobs n'ont jamais démarré et ont été tués à **15 min
   pile** (timeout) → `startup_failure`. Ici le déploiement n'a **pas** eu lieu.

**Les deux sites étaient bien à jour**, vérifié par empreinte MD5 (contenu servi
vs contenu du commit) : 3/3 fichiers sur skillinjection, 3/3 sur sleeperattack.

### Décision structurelle

**Un HTTP 200 ne prouve pas qu'un site est à jour.** Pages continue de servir la
dernière version construite avec succès : un build raté donne un site en ligne,
au contenu périmé, qui répond 200 partout. Toute vérification de déploiement
compare désormais le **contenu servi** au **contenu du commit** — jamais un code
de statut. Consigné dans `SEO-PROCESS.md`, section « Constats de terrain
(2026-08-26) », répliqué dans les deux dépôts.

### Ce qui a été construit

`.github/workflows/verifier-mise-en-ligne.yml` — identique octet pour octet dans
les deux dépôts (md5 `de512f58`), le domaine étant lu dans `CNAME`.

À chaque push touchant le site, il compare l'empreinte de chaque `.html`/`.css`/
`.xml` du commit à celle du fichier réellement servi, et ne devient rouge que si
l'écart persiste après 10 minutes. Deux contraintes posées par Damien, tenues :
`paths-ignore: ['**.md']` (un push de doc ne déclenche rien) et lisibilité par
un non-développeur (commentaires en français, pas d'astuce shell).

**Défaut rattrapé par le test :** la première version comparait le fichier **sur
le disque**. Avec `core.autocrlf=true`, git réécrit les fins de ligne à la copie
→ 4 faux positifs sur 4 fichiers dans sleeperattack, sans qu'aucun contenu
n'ait changé. Corrigé : la référence est lue dans le commit
(`git show HEAD:<fichier>`). Sur runner Ubuntu le défaut ne se serait pas
manifesté ce jour-là, mais un `.gitattributes` aurait suffi à le réveiller.

Tests exécutés : YAML parse · `bash -n` · les deux sites réels (sortie 0) ·
fichier du commit absent du site → 404 annoncé dès la tentative 1 (sortie 1).

## État du dépôt

Branche `main`, **2 commits locaux non poussés** dans chacun des deux dépôts :

| | skillinjection | sleeperattack |
|---|---|---|
| leçon `SEO-PROCESS.md` | `0511517` | `5f3cf26` |
| workflow de contrôle | `8377bd4` | `eeea0a7` |

**Rien n'est poussé** : Damien a demandé que les commits partent seulement une
fois l'incident GitHub clos. À la clôture, `Actions=major_outage` toujours, et
les builds Pages des deux dépôts encore bloqués en `building` depuis 15:26 UTC
(Pages lui-même était repassé `operational`).

⚠️ **Le clone de `sleeperattack` était dans le scratchpad de session — ses deux
commits sont donc perdus.** Rien d'irrécupérable : les deux artefacts sont
identiques dans `skillinjection`, qui est en sécurité. Pour reconstituer :
cloner `sleeperattack`, y copier `.github/workflows/verifier-mise-en-ligne.yml`
tel quel depuis `skillinjection`, et reporter le bloc « Un HTTP 200 ne prouve
pas… » de `SEO-PROCESS.md` (les deux fichiers doivent rester identiques octet
pour octet — le vérifier par `md5sum` avant de commiter).

## Reste à faire

**Bloqué sur l'état de GitHub :**
- [ ] Vérifier que l'incident Actions est clos et que les builds Pages ne sont
      plus `building` sur les deux dépôts. S'ils sont toujours bloqués bien
      après la fin de l'incident, re-déclencher par un commit vide.
- [ ] Reconstituer le clone `sleeperattack` (procédure ci-dessus).
- [ ] Pousser les deux commits sur les deux dépôts, **ensemble**. Le push
      contient le `.yml`, donc le nouveau workflow se déclenchera sur lui-même :
      première validation réelle, sur des fichiers déjà en ligne → doit passer
      au vert. Prévenir Damien avec le résultat de ce run.

**Bloqué sur Damien :**
- [ ] Rendu mobile de skillinjection.com section 09 sous 560 px — toujours non
      vérifié (reporté de la session précédente).
- [ ] Demander l'indexation de skillinjection.com dans Search Console.

**Proposé, sans GO à ce jour :**
- [ ] Contrôle de fraîcheur **hors GitHub** (cron local ou service tiers). Le
      workflow ci-dessus tourne sur Actions : pendant une panne Actions il ne
      donne ni vert ni rouge. Il couvre « le déploiement a échoué en silence »,
      pas « GitHub est cassé ».
- [ ] Bootstrap restant du projet : CLAUDE.md projet, template Bureau
      `SEO-ATTACK-PAGES-REPRISE.txt` (aucun n'existe aujourd'hui).

## Comment reprendre

1. Lire ce fichier, puis `C:\brain\projets\seo-attack-pages\STATE.md` et son
   dernier fichier `sessions/`.
2. `git log -3` + `git status` dans `Projects/skillinjection` — attendre
   `ahead 2` sur `main`, rien de poussé.
3. Vérifier l'état de GitHub avant toute action :
   `curl -s https://www.githubstatus.com/api/v2/summary.json` et
   `gh api repos/Arlenjim/<repo>/pages --jq .status`.
4. Ne jamais conclure qu'un site est à jour depuis un code HTTP : comparer
   l'empreinte du contenu servi à celle du commit.
