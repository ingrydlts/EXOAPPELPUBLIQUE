# EXOAPPELPUBLIQUE · Observatoire européen des marchés publics

Projet fil rouge du cours **BI, Dashboards & Data Storytelling** (Master 2, Programme Grande École, Paris School of Business). Enseignant : Olivier Mamavi, professeur associé. Auteures : Ingryd Lo Tierzo Silva et Sara Lhasseni.

Ce dépôt documente les décisions clés du projet, la consigne de la séance en cours et l'historique des rendus. Il ne contient ni les données brutes ni les enregistrements de cours.

## 1. Le projet en bref

| Élément | Contenu |
| --- | --- |
| Rôle | Consultante data pour la Commission européenne |
| Client | L'Observatoire des marchés publics, qui vérifie que les achats publics fonctionnent bien dans toute l'Europe |
| Données | 149 813 marchés attribués de 2009 à 2017 dans 33 pays, après nettoyage. Une ligne est une **attribution**, pas un marché (identifiant ID_AW). Un fichier à part contient 6 022 procédures rares, jamais empilées avec le principal |
| Livrable final | Une application web interactive, ouverte par un lien public, en quatre vues : globale, analyse, segmentation, exploration |
| Mission | Préparer l'exercice de surveillance 2018 : non pas décrire le marché, mais décider où agir |

Trois questions, chacune avec une variable imposée à expliquer :

| Axe | Question | Variable cible | Décision à éclairer |
| --- | --- | --- | --- |
| A · Concurrence | Où y a-t-il trop peu d'entreprises qui répondent ? | NUMBER_OFFERS | Quels 20 segments instruire |
| B · PME | Comment aider les petites entreprises à gagner ? | B_CONTRACTOR_SME | Découper en 6 à 10 lots ? |
| C · Budget | Où l'argent public est-il dépensé de façon anormale ? | AWARD_VALUE_EURO | Quels marchés auditer (5 %) |

Idée centrale du cours : la BI sert à aider à décider. Un tableau de bord est une hypothèse causale rendue visible et vérifiable, pas une pile de graphiques.

## 2. Consigne de la séance 4 : architecture décisionnelle

**Objectif.** Les six indicateurs sont testés, mais il n'existe pas encore de tableau de bord. Il manque une décision de conception : à quoi sert chaque écran, pour qui, et quelle décision permet-il de prendre ? La séance produit un plan, pas un prototype, et se fait sans outil de visualisation.

**Déroulé.** Reprise des livrables (15h00), briefing (15h20), étape 1 note de modélisation (16h05), étape 2 maquettes des quatre vues avec ordinateurs fermés (16h45), étape 3 huit user stories (17h45), débriefing (18h20).

### Étape 1 · Poser le modèle de données

- Déclarer le **grain** : une phrase pour dire ce que représente une ligne de la table de faits.
- **Classer chaque KPI** : mesure brute stockée ligne à ligne, agrégat calculé selon les filtres, ou indicateur (rapport de deux agrégats dont le dénominateur bouge avec les filtres).
- Lister les **six dimensions** (géographique, temporelle, sectorielle, procédure, acheteur, contrat) : nombre de modalités, traitement des modalités résiduelles, hiérarchie de drill-down.
- Fixer **trois règles transversales** : seuil d'effectif minimal et comportement en dessous ; périmètre par défaut de chaque vue (notamment l'axe PME, dont la fenêtre temporelle est restreinte) ; répartition des deux fichiers entre les écrans.

### Étape 2 · Maquetter les quatre vues

| Vue | Question | Contenu imposé | Interactions |
| --- | --- | --- | --- |
| 1. Globale | Où en sommes-nous ? | Six indicateurs au maximum, chacun avec son effectif | Filtres de contexte |
| 2. Analyse | Pourquoi ? | Les relations testées en séance 3, rendues visibles | Choix de la relation, stratification activable |
| 3. Segmentation | Où agir ? | Croisements pays, secteur, procédure ; priorisation par valeur, pas par taux | Filtres croisés, tris multiples |
| 4. Exploration | Quel cas précis ? | Descente jusqu'à la ligne | Drill-down depuis les trois autres vues |

Une feuille par vue, avec pour chaque bloc : l'indicateur affiché, son dénominateur, son effectif minimal, le type de visualisation et la justification de l'encodage en une ligne. Une cinquième feuille dessine les chemins de navigation (un chemin qui ne mène nulle part signale un écran mort). La vue 2 doit afficher au moins une relation testée, sa stratification par un confondant et les effectifs des deux groupes : si elle ressemble à la vue 1 avec plus de graphiques, elle est à refaire.

### Étape 3 · Écrire les user stories

Huit stories au format imposé : *En tant que [utilisateur identifié], je veux [objectif précis], afin de [décision].* Quatre champs complémentaires : indicateurs mobilisés, vue concernée, interaction nécessaire, décision déclenchée. Couverture obligatoire : deux stories par axe au minimum, trois profils différents (responsable de la surveillance, analyste de l'Observatoire, décideur politique) et une story qui traverse plusieurs vues. Une story qui se termine par « afin de mieux comprendre » est descriptive : elle est à réécrire ou à supprimer.

### Livrables (à déposer avant la fin de la séance)

| Livrable | Format | Contenu |
| --- | --- | --- |
| Note de modélisation | 2 pages | Grain, classement des six KPI, tableau des dimensions, trois règles transversales |
| Maquettes annotées | 5 feuilles photographiées | Quatre vues et schéma de navigation |
| User stories | Un tableau | Huit stories au format imposé |

### Évaluation

Notée sur 20, elle alimente le critère « dashboard, architecture et interactivité » de la grille du jury.

| Critère | Points | Attendu | Piège |
| --- | --- | --- | --- |
| Modèle et règles transversales | 5 | Grain cohérent avec la séance 2, distinction mesure / agrégat / indicateur, trois règles chiffrées | Modèle calqué sur les colonnes du fichier ; seuil d'effectif non fixé |
| Architecture des quatre vues | 6 | Chaque vue répond à une question distincte, vue 2 réellement explicative | Vue globale surchargée ; vue 2 indistincte de la vue 1 ; pas de drill-down |
| Justification des encodages | 4 | Choix argumenté par la précision perceptive | Camembert, carte en couleurs pour une comparaison fine, axe tronqué |
| User stories | 5 | Décision concrète, profils différenciés, trois axes couverts | Story se terminant par « afin de mieux comprendre » |

**Connaissances à mobiliser.** Modélisation dimensionnelle (Kimball) ; architecture de l'information (Shneiderman, 1996) ; modèle imbriqué (Munzner, 2009) ; perception graphique (Cleveland et McGill, 1984) ; sémiologie graphique (Bertin, 1967) ; tableau de bord et contrôle de gestion (Kaplan et Norton) ; usage diagnostique et interactif (Simons, 1995) ; règle d'affichage reconduite : tout pourcentage est accompagné de son effectif.

### Évaluation du projet entier

Le projet compte pour 50 % de la note (60 % jury, 20 % épreuve de requêtes de 5 questions en 8 minutes, 20 % pairs) ; l'examen individuel de 2 heures sans documents compte pour les 50 % restants et porte sur le jeu de données du cours. Critères du jury : rigueur du traitement des données (5), recommandations prescriptives (5), construction des KPI (4), qualité analytique (4), dashboard et architecture (4), rapport, soutenance et journal (3 + 3 + 2). L'usage de l'IA est permis, à condition de comprendre assez pour la corriger et de pouvoir défendre chaque choix à l'oral.

## 3. Historique des rendus

| Date | Rendu | Contenu | Statut |
| --- | --- | --- | --- |
| Séance 2 | Note d'audit des données | Diagnostic des anomalies : doublons, valeurs manquantes, codes à normaliser ; 13 règles de nettoyage qui ramènent la base de 156 171 à 155 835 lignes | Rendu, puis corrigé sur quatre points dans la note de la séance 3 |
| 3 octobre 2026 | Hypothèses H1 à H6 | Écrites avant tout test, jugées après | Déposées |
| 10 octobre 2026 | Livrables repris en début de séance 4 | Étapes 1 à 4 : base, variables, relations explorées, relations contrôlées | Rendus |
| 13 octobre 2026 | Note de tests et de conception, version finale | Étape 5 : six fiches KPI, carte causale à quatre niveaux, recommandation du 6-10 lots (rapport de cotes ajusté 1,24 [1,06 ; 1,45]) | Rendue |
| 17 octobre 2026 | Séance 4 | Présentation de la note par Ingryd et Sara, puis lancement du travail d'architecture décisionnelle | Faite |
| Novembre 2026 | Livrable de la séance 4 | Note de modélisation, maquettes annotées des quatre vues et de la navigation, huit user stories, annexe sur le choix des six KPI | Rédigé, voir `livrables/` |
| 19 novembre 2026 | Prototype HTML du tableau de bord | Fichier « Observatoire européen des marchés publics · Tableau de bord.html » déposé sur `main`, avec les vues 1 à 4 | Déposé, à confronter aux maquettes de la séance 4 |
| À venir | Séance 5 | Déploiement du tableau de bord (Power BI ou autre outil) ; les trois règles transversales y seraient arbitrées sous contrainte technique | À faire |

Les dates de la séance 2 et du dépôt exact de la séance 4 sont à compléter si besoin.

## 4. Contenu du dépôt

| Chemin | Contenu |
| --- | --- |
| `livrables/S4_BI_Livrable_Observatoire_marches_publics.docx` | Livrable unifié de la séance 4 : note de modélisation, maquettes annotées, user stories, annexe « Pourquoi ces six KPI » |
| `Observatoire européen des marchés publics · Tableau de bord.html` | Prototype HTML du tableau de bord (vues 1 à 4), déposé sur `main` |
| `docs/superpowers/specs/2026-11-04-s4-architecture-dashboard-design.md` | Plan de travail de la séance 4 : intention, contraintes, méthode, arbitrages |
| `README.md` | Ce fichier |

## 5. Décisions clés

**Les six KPI**, deux par axe : l'état, puis le levier ou le ciblage.

| Axe | KPI | Type | Lien qui le fonde | Action déclenchée |
| --- | --- | --- | --- | --- |
| A | 1 · Taux d'offre unique, procédure ouverte | indicateur | associatif | entre dans les 20 dossiers |
| A | 2 · Médiane des offres | agrégat non additif | associatif faible | liste de surveillance |
| B | 3 · Part de PME, 2016-2017 | indicateur | associatif | revue d'allotissement |
| B | 4 · Gain simulé du 6-10 lots | indicateur simulé | causal plausible (R3) | recommandation 6-10 lots |
| C | 5 · Montant total pondéré | agrégat additif | descriptif | vérifier la queue avant l'audit |
| C | 6 · Indice d'anomalie (z en log10) | mesure stockée | associatif | liste d'audit |

**Grain.** Une ligne est une attribution (ID_AW), dans le fichier principal dédoublonné.

**Trois règles transversales.**

1. Seuil d'effectif par KPI : 100 marchés pour les KPI 1 à 3, 100 non-allotis pour le KPI 4, 30 attributions pour le KPI 5, 30 marchés par strate pour le KPI 6. Sous le seuil, la case affiche « effectif insuffisant ».
2. Périmètre par défaut : fichier principal ; procédure ouverte pour les KPI 1 et 2 ; fenêtre 2016-2017 verrouillée pour les KPI 3 et 4, qui ignorent le filtre d'année global.
3. Deux fichiers : le principal alimente les vues 1 à 3 ; les procédures rares n'apparaissent qu'en vue 4, lues procédure par procédure, sans jamais être additionnées.

**Un seul lien survit au contrôle des confondants** : le passage à 6-10 lots et la part de PME (R3). Les autres relations servent à cibler et à surveiller, pas à recommander.

## 6. Points à vérifier dans les données

Tous les chiffres viennent de la note de la séance 3 et n'ont pas été recalculés.

- Bornes exactes des classes de valeur et de lots (règle 11 du nettoyage) et nombre de divisions CPV.
- Les deux modalités sans information du type d'acheteur, regroupées en « Non précisé ».
- Dénominateurs de la part des pays dans la liste d'audit : 149 813 pour le Royaume-Uni, 149 218 pour la Pologne.
- Le suivi de la recommandation est annuel : le fichier n'a pas de donnée infra-annuelle.
- La fiche du KPI 2 qualifie la médiane d'« indicateur avancé » qui « précède » l'offre unique : aucun test dans le temps ne le soutient, écrire « associée à ».
