# Ondea Staff Manager

**Plateforme locale de gestion du personnel, missions et communication interne — 100 % autonome, sans serveur.**

Application web mono-fichier (HTML + CSS + JavaScript vanilla) conçue pour équiper une petite ou moyenne structure d'un outil RH complet, sans hébergement ni base de données : tout fonctionne hors-ligne, directement dans le navigateur. Identité visuelle « **Obsidienne & Or** », commune à l'ensemble des applications Ondea.

![Aperçu de l'application](images/_apercu.png)

---

## Sommaire

- [Fonctionnalités](#fonctionnalités)
- [Rôles & permissions](#rôles--permissions)
- [Comptes de démonstration](#comptes-de-démonstration)
- [Installation](#installation)
- [Stockage des données](#stockage-des-données)
- [Modules bonus](#modules-bonus)
- [Structure du projet](#structure-du-projet)
- [Personnalisation](#personnalisation)
- [Feuille de route — V2](#feuille-de-route--v2)
- [Licence](#licence)

---

## Fonctionnalités

L'application s'adapte automatiquement selon le rôle de la personne connectée : la Direction et les managers accèdent à un espace de **pilotage**, les salariés à un **espace personnel** allégé.

### Espace Direction / Manager

| Module | Description |
|---|---|
| Tableau de bord | Vue d'ensemble en temps réel : effectifs présents, missions actives, demandes en attente, retards |
| Personnel | Annuaire complet avec fiches individuelles (compétences, contrat, présence, activation/désactivation du compte) |
| Missions | Suivi en tableau **Kanban**, checklists, priorités, échéances, alerte automatique sur les missions en retard |
| Planning | Vue calendrier mensuelle des évènements et disponibilités |
| Messages | Messagerie interne par conversation |
| Demandes | Validation des demandes de congé / télétravail, badge de notifications synchronisé |
| Documents | Espace de dépôt de fichiers (photos, justificatifs) |
| Évaluations | Grilles d'évaluation par critères, moyennes et historique |
| Statistiques | Indicateurs graphiques : taux de complétion, retards, répartition par service |
| Journal d'activité | Historique horodaté de toutes les actions |
| Paramètres | Export / import des données, activation ou désactivation de modules entiers |

### Espace Salarié

| Module | Description |
|---|---|
| Mon tableau de bord | Résumé personnel : missions en cours, présence du jour |
| Mes missions | Missions qui lui sont assignées, en Kanban |
| Mon planning | Son propre planning |
| Messages | Messagerie interne |
| Mes demandes | Dépôt de demandes de congé / télétravail et suivi de leur statut |
| Documents | Ses documents personnels |
| Mon profil | Informations personnelles et compétences |

---

## Rôles & permissions

Quatre niveaux d'accès (`accessRole`) contrôlent l'affichage et les actions disponibles :

- **`admin`** — Accès système complet ; compte non désactivable.
- **`direction`** — Pilotage global : personnel, missions, statistiques, paramètres.
- **`manager`** — Pilotage d'équipe, sans les réglages globaux.
- **`salarie`** — Espace personnel uniquement (missions assignées, planning, demandes).

---

## Comptes de démonstration

L'application est livrée avec neuf comptes préchargés pour la démonstration (données réinitialisables à tout moment) :

| Nom | Poste | Rôle | Identifiant | Mot de passe |
|---|---|---|---|---|
| Marie Martin | Directrice | `direction` | `marie.martin` | `admin123` |
| Thomas Bernard | Responsable IT | `manager` | `thomas.bernard` | `manager123` |
| Léa Moreau | Chargée RH | `manager` | `lea.moreau` | `manager123` |
| Jean Dupont | Technicien | `salarie` | `jean.dupont` | `staff123` |
| Sophie Petit | Développeuse | `salarie` | `sophie.petit` | `staff123` |
| Paul Durand | Commercial | `salarie` | `paul.durand` | `staff123` |
| Hugo Lefèvre | Technicien | `salarie` | `hugo.lefevre` | `staff123` |
| Camille Roux | Designer | `salarie` | `camille.roux` | `staff123` |
| Admin Système | Administrateur | `admin` | `admin` | `admin` |

Les identifiants des comptes de démonstration sont aussi proposés en un clic depuis l'écran de connexion.

> Pensez à remplacer ces comptes par vos propres collaborateurs avant toute mise en production, et à modifier les mots de passe.

---

## Installation

Aucune installation n'est nécessaire.

1. Téléchargez le dossier du projet.
2. Ouvrez `index.html` dans un navigateur récent (Chrome, Firefox, Edge, Safari).

C'est tout : il n'y a ni serveur, ni base de données, ni dépendance externe à installer. Seules deux polices Google Fonts et les émojis météo nécessitent une connexion Internet ponctuelle ; tout le reste fonctionne strictement hors-ligne.

---

## Stockage des données

Les données restent en local, dans le navigateur qui a ouvert la page :

- **`localStorage`** (clé `ondea_staff_v1`) — personnel, missions, messages, demandes, planning, évaluations, journal, paramètres.
- **`IndexedDB`** (base `OndeaStaffMediaDB`) — photos de profil et documents déposés, trop volumineux pour `localStorage`.

Ce stockage étant propre à chaque navigateur/appareil, un module **Export / Import** (menu *Paramètres*) permet de sauvegarder l'état complet dans un fichier `.json` et de le recharger — pratique pour migrer les données, faire une démonstration ou passer d'un poste à un autre. Un export d'exemple est fourni dans `export-etat-actuel/`.

---

## Modules bonus

Au-delà du cœur fonctionnel, plusieurs modules de confort s'ajoutent sans jamais modifier le code existant (chacun s'enveloppe autour des fonctions d'origine, et peut être retiré sans rien casser) :

- **Tableau de bord vivant** — les indicateurs se rafraîchissent automatiquement.
- **Alerte missions en retard** — colonne dédiée dans le Kanban.
- **Retour en haut** — bouton flottant lors du défilement.
- **Horloge & météo** — widgets dans la barre latérale (météo géolocalisée via l'API OpenWeatherMap — clé à renseigner).
- **Contraste élevé** — bouton d'accessibilité agissant sur toute l'application.
- **Raccourcis** — la cloche de notifications et le bouton de retour facilitent la navigation vers les demandes.
- **Activation / désactivation des comptes** — la Direction et l'administrateur peuvent désactiver le compte d'un salarié (départ, suspension) directement depuis sa fiche ; un compte désactivé ne peut plus se connecter et reste repéré dans l'annuaire.
- **Carte « Salariés inactifs »** — indicateur dédié sur le tableau de bord.
- **Badges synchronisés** — la cloche et l'onglet Demandes affichent toujours le même nombre, en temps réel.

---

## Structure du projet

```
Ondea-Staff-Manager/
├── index.html                     # Application complète (HTML + CSS + JS, fichier unique)
├── images/
│   ├── _apercu.png                 # Capture d'écran de présentation
│   ├── admin.png
│   ├── marie.martin.png
│   ├── thomas.bernard.png
│   ├── lea.moreau.png
│   ├── jean.dupont.png
│   ├── sophie.petit.png
│   ├── paul.durand.png
│   ├── hugo.lefevre.png
│   └── camille.roux.png            # Avatars des comptes de démonstration
└── export-etat-actuel/
    └── ondea-staff-*.json          # Exemple d'export des données
```

---

## Personnalisation

- **Clé météo** — dans `index.html`, remplacez `VotreCléAPIOpenWeatherMapIci` (variable `OWM_KEY`) par une clé [OpenWeatherMap](https://openweathermap.org/api) valide pour activer le widget météo.
- **Thème clair / sombre** — basculable depuis l'interface ; les couleurs du design system se règlent via les variables CSS `:root` en tête de fichier.
- **Modules** — chaque module métier (missions, planning, messagerie, demandes, évaluations) peut être désactivé indépendamment depuis *Paramètres*.

---

## Feuille de route — V2

Le code est volontairement cloisonné pour permettre, dans une version future, de remplacer le stockage local par un back-end **PHP / PDO** en architecture **MVC**, sans avoir à retoucher l'interface.

---

## Licence

© Ondea Web Studio. Application distribuée dans le cadre d'une licence d'utilisation (Gumroad / Payhip / Ko-fi) : usage autorisé selon les conditions associées à votre achat. Redistribution ou revente du code source non autorisée sans accord préalable.
