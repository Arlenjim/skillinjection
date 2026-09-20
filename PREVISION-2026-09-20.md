# Prévision Search Console — skillinjection.com — écrite le 2026-09-20

Prévision **datée et falsifiable**, à confronter aux chiffres réels vers le
**2026-10-20**. Elle est volontairement large : quatre semaines de données sur un
terme qui n'a pas encore de volume de recherche. Écrite par Claude ; les
hypothèses sont les siennes, pas des consignes de Damien.

## Point de départ (mesuré le 2026-09-20, fenêtre 3 mois 19/07 → 18/09)

| Mesure | Valeur |
|---|---|
| Impressions | 236 (dont 100 sur requêtes visibles, 136 anonymisées) |
| Clics | 6 |
| Position moyenne | 7,2 |
| Requête principale | « skill injection » : 49 impressions, 2 clics |
| Jours dans l'index | ~18 (du ~16/08 au ~03/09), puis éjectée |
| Impressions par jour indexé | ≈ 8 (236 / ~28 jours d'impressions, 17/08 → 14/09) |
| Liens entrants connus de Google | 0 |

## Ce qui a été fait le 2026-09-20

Contenu enrichi (7 papiers 2026, section 04 étendue, date de mise à jour),
sitemap re-soumis, indexation redemandée. Détail : `SESSION-HANDOFF.md`.

## Hypothèses

- H1 — Google ré-explore et ré-évalue la page dans les 14 jours suivant la
  demande (en août, l'indexation a suivi la demande de quelques jours).
- H2 — Le volume de recherche sur « skill injection » ne change pas (1 à 2
  affichages par jour).
- H3 — Aucun lien entrant suivi n'est obtenu d'ici le 2026-10-20.
- H4 — Aucune autre modification de la page d'ici là.
- H5 — Pas de mise à jour majeure de l'algorithme Google sur la période.

Si H1 tombe (pas ré-indexée au 2026-10-05), tout le reste tombe avec.

## Prévision — fenêtre 28 jours, 2026-09-21 → 2026-10-18

| Scénario | Condition | Impressions | Clics | Position « skill injection » |
|---|---|---|---|---|
| Pessimiste | pas ré-indexée, ou ré-éjectée sous une semaine | 0 – 30 | 0 – 1 | absente |
| **Central** | ré-indexée sous 14 jours et maintenue | **80 – 200** | **2 – 6** | 5 – 10 |
| Optimiste | ré-indexée vite + longue traîne sur les noms des nouveaux papiers | 200 – 400 | 5 – 12 | 3 – 8 |

Raisonnement du central : ≈ 8 impressions par jour indexé en août-septembre ;
si la page revient dans l'index pour la moitié de la fenêtre, on obtient ≈ 110.
La fourchette couvre une ré-indexation plus lente ou plus rapide.

Probabilités que je mets sur chaque scénario : pessimiste 35 %, central 45 %,
optimiste 20 %. Le pessimiste est haut parce que la page a déjà été éjectée
une fois sans blocage technique : le contenu seul peut ne pas suffire.

## Indicateurs à relever le 2026-10-20 (Search Console, via Chrome ou Damien)

1. Rapport **Pages** : « Dans l'index » = 1 ou 0, et depuis quand.
2. **Sitemaps** : « Dernière lecture » remplie ou toujours « Impossible de
   récupérer ». Si toujours vide au 2026-10-05, creuser (test « URL active »,
   en-têtes vus par Googlebot) sans attendre le 20.
3. **Performances**, fenêtre 28 jours : impressions, clics, position sur
   « skill injection », et part des requêtes anonymisées.
4. **Liens** : toujours 0 page d'origine ?

## Ce que chaque issue voudrait dire

- **Pessimiste réalisé** : le levier « contenu + fraîcheur » ne suffit pas à
  rester dans l'index. Prochain levier = signal externe (un lien suivi, une
  citation hors GitHub) ou une page dédiée qui cible une requête réellement
  cherchée. Ne pas ré-enrichir la home une troisième fois sans ça.
- **Central réalisé** : la page tient ; on peut alors décider la page « vs »
  sur données, et chercher un premier lien suivi.
- **Optimiste réalisé** : la longue traîne sur les noms de papiers fonctionne ;
  c'est un argument pour une page dédiée à la recherche (section 09 sortie de
  la home), qui capterait ces requêtes sans alourdir la définition.
