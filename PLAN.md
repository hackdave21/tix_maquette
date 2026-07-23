# TixTogo — Plan d'implémentation des maquettes UI

## Charte graphique existante — mapping Tailwind

### Palette de couleurs (à configurer dans `tailwind.config`)

| Token CSS | Couleur | Usage Tailwind |
|---|---|---|
| `--ink` | `#1B160F` | `text-ink`, `bg-ink` |
| `--ink-soft` | `#5C5344` | `text-ink-soft` |
| `--paper` | `#F2E8D4` | `bg-paper` |
| `--paper-soft` | `#F9F3E6` | `bg-paper-soft` |
| `--paper-white` | `#FFFCF6` | `bg-paper-white` |
| `--amber` | `#E8A33D` | `bg-amber`, `text-amber` (CTA principal) |
| `--amber-deep` | `#C97F1E` | `bg-amber-deep` (hover CTA) |
| `--amber-pale` | `#FBE6BE` | `bg-amber-pale` (fond badge ambre) |
| `--teal` | `#1C7A6B` | `bg-teal`, `text-teal` (statut valide) |
| `--teal-pale` | `#DCEFE9` | `bg-teal-pale` |
| `--red` | `#C2402F` | `bg-red-custom`, `text-red-custom` (statut invalide) |
| `--red-pale` | `#F7DEDA` | `bg-red-pale` |
| `--line` | `rgba(27,22,15,0.16)` | `border-line` |
| `--line-strong` | `rgba(27,22,15,0.30)` | `border-line-strong` |

### Typographie

| Font | Usage | Tailwind class |
|---|---|---|
| Archivo Black | Titres / tampons | `font-display` |
| Archivo 400-700 | Corps de texte | `font-body` |
| IBM Plex Mono 400-500 | Codes billet / data | `font-mono` |

### Composants réutilisables (à créer en partials)

| Composant | Classes CSS correspondantes |
|---|---|
| `.btn` (primary, dark, outline) | `btn btn-primary`, `btn btn-dark`, `btn btn-outline` |
| `.badge` (valid, used, amber) | `badge badge-valid`, `badge badge-used`, `badge badge-amber` |
| `.field` (label + input) | `field label` + `field input/select` |
| `.ticket-card` | `ticket-card` |
| `.stub-divider` | `stub-divider` (perforation visuelle) |
| `.ticket-code` | `ticket-code` (IBM Plex Mono) |
| `.eyebrow` | `eyebrow` (monospace, uppercase, amber-deep) |

### Structure des 5 dossiers

```
maquette/
├── public/          ← Dossier 1 : Espace acheteur
│   ├── index.html                (page d'accueil / vitrine)
│   ├── recherche.html            (recherche et filtres)
│   ├── evenement.html            (page événement détaillée)
│   ├── achat.html                (tunnel d'achat rapide)
│   ├── paiement.html             (confirmation mobile money)
│   ├── confirmation.html         (billet électronique + QR)
│   └── mes-billets.html          (espace personnel acheteur)
│
├── organisateur/   ← Dossier 2 : Espace organisateur
│   ├── index.html                (dashboard organisateur)
│   ├── evenement-creation.html   (création / édition événement)
│   ├── billets.html              (gestion catégories de billets)
│   ├── ventes.html               (suivi ventes temps réel)
│   ├── equipe.html               (gestion équipe événementielle)
│   ├── ambassadeurs.html         (ambassadeurs et affiliation)
│   ├── points-de-vente.html      (points de vente physiques)
│   ├── invitations.html          (invitations et listes)
│   └── reversements.html         (reversement des fonds)
│
├── scan/           ← Dossier 3 : Application de contrôle d'accès (PWA)
│   ├── index.html                (connexion / sélection événement)
│   ├── scanner.html              (scan QR — plein écran caméra)
│   └── manifest.json             (PWA manifest)
│
├── pos/            ← Dossier 4 : Interface de vente terrain
│   ├── index.html                (sélection catégorie + quantité)
│   ├── ventes.html               (historique ventes du point de vente)
│   └── confirmation.html         (émission billet + envoi SMS)
│
├── backoffice/     ← Dossier 5 : Back-office administrateur
│   ├── index.html                (dashboard global + stats)
│   ├── kyc.html                  (validation organisateurs)
│   ├── commissions.html          (gestion des commissions)
│   ├── moderation.html           (modération des événements)
│   ├── paiements.html            (supervision paiements + réconciliation)
│   ├── remboursements.html       (gestion des remboursements)
│   ├── utilisateurs.html         (gestion utilisateurs + rôles)
│   └── audit.html                (journal d'audit)
│
├── css/
│   └── tixtogo.css               (styles communs + charte graphique)
│
├── assets/
│   ├── icons/                    (icônes SVG)
│   └── images/                   (images placeholder)
│
└── components/
    ├── header.html               (navigation commune)
    ├── sidebar-org.html          (sidebar organisateur)
    ├── sidebar-admin.html        (sidebar administrateur)
    ├── footer.html               (footer)
    ├── ticket-card.html          (composant carte billet)
    └── scan-result.html          (écran résultat scan)
```

---

## Détail par dossier

### 1. `public/` — Espace public / acheteur

**Principes :** mobile-first, rapide, sans friction, pas de compte classique.

| Fichier | Écran CDP | Contenu |
|---|---|---|
| `index.html` | ACH-01 | Vitrine événements, grille avec image/titre/date/prix, barre de recherche, navigation bottom mobile |
| `recherche.html` | ACH-02 | Filtres (ville, date, catégorie), tri, résultats en grille |
| `evenement.html` | ACH-03 | Affiche, description, carte lieu, catégories avec disponibilité, bouton WhatsApp, bouton achat, champ promo |
| `achat.html` | ACH-04 | Sélection catégorie/quantité, récapitulatif, formulaire (téléphone obligatoire, nom, email facultatif) |
| `paiement.html` | ACH-05 | Choix opérateur (Flooz/T-Money), écran d'attente USSD, indicateur de chargement |
| `confirmation.html` | ACH-06 | QR code billet, récapitulatif, bouton « Mes billets », envoi SMS/email confirmé |
| `mes-billets.html` | ACH-07 | Liste billets (passés/à venir), accès par OTP ou lien magique, statut de chaque billet |

**Composants clés :**
- Header minimal avec logo TixTogo + icône recherche + icône « Mes billets »
- Bottom navigation mobile (Accueil / Recherche / Billets)
- Card d'événement avec image cover, badge catégorie, prix
- Tunnel d'achat en étapes (sélection → coordonnées → paiement → confirmation)
- QR code du billet avec perforation (stub-divider)
- Badge statut : Valide (teal), Déjà utilisé (red), En attente (amber)

---

### 2. `organisateur/` — Espace organisateur

**Principes :** responsive, sidebar collapse mobile, widgets KPI, données temps réel.

| Fichier | Écran CDP | Contenu |
|---|---|---|
| `index.html` | ORG-02 | Dashboard : liste événements, widgets (billets vendus, CA, prochain événement), ventilation par canal |
| `evenement-creation.html` | ORG-03 | Formulaire création/édition : titre, description, lieu, dates, image, catégorie, type accès, accès privé |
| `billets.html` | ORG-04 | Liste catégories (prix, quantité restante), fenêtre de vente, ajout/modification/désactivation |
| `ventes.html` | ORG-06 | Graphique évolution ventes, billets vendus par catégorie/canal, CA brut/net, dernières transactions |
| `equipe.html` | ORG-08 | Invitation membre (nom, téléphone, rôle), liste membres avec statut, révocation |
| `ambassadeurs.html` | ORG-09 | Création ambassadeur, code unique, paramétrage commission, suivi clics/ventes/CA |
| `points-de-vente.html` | ORG-10 | Création point de vente, rattachement agents, suivi ventes terrain |
| `invitations.html` | ORG-11 | Types d'invitations, émission individuelle/CSV, QR unique, stats |
| `reversements.html` | ORG-12 | Solde disponible, historique reversements, statut (en attente/traité/échoué) |

**Composants clés :**
- Sidebar avec navigation complète (Dashboard, Événements, Billets, Ventes, Équipe, Ambassadeurs, POS, Invitations, Reversements)
- Header avec avatar organisateur + nom + badge vérifié
- KPI cards avec stub-divider (talon perforé) entre titre et valeur
- Tableaux de données avec badges statut
- Formulaire multi-étapes pour création d'événement
- Graphiques (placeholder ou simple chart CSS)

---

### 3. `scan/` — Application de contrôle d'accès (PWA)

**Principes :** plein écran, mode hors ligne, minimal, rapide, tactile.

| Fichier | Écran CDP | Contenu |
|---|---|---|
| `index.html` | CTRL-01 | Connexion par code/lien, sélection événement, indicateur connectivité |
| `scanner.html` | CTRL-02/03/04 | Caméra plein écran, compteur entrées, indicateur EN LIGNE/HORS LIGNE, écran vert (valide) / rouge (invalide/déjà utilisé) |
| `manifest.json` | — | Manifest PWA (nom, icône, start_url, display: standalone, background color) |

**Composants clés :**
- Interface minimaliste, pas de sidebar
- Bandeau de statut connectivité (fixe, en haut)
- Compteur d'entrées (grand chiffre central)
- Écran de résultat scan : plein écran vert avec checkmark ou plein écran rouge avec X
- Indicateur de synchronisation (nombre de scans en attente)
- Design optimisé pour touch (grandes zones cliquables)

---

### 4. `pos/` — Interface de vente terrain

**Principes :** simplifié, rapide, un écran = une action, tactile.

| Fichier | Écran CDP | Contenu |
|---|---|---|
| `index.html` | POS-01 | Sélection catégorie + quantité, mode d'encaissement (espèces/MM), bouton « Émettre » |
| `ventes.html` | POS-02 | Historique ventes agent, total encaissé par mode |
| `confirmation.html` | POS-01 (suite) | Billet émis, QR affiché, bouton « Imprimer » / « Envoyer SMS » |

**Composants clés :**
- Navigation simplifiée (3 onglets : Vendre / Historique / Profil)
- Sélecteur de catégorie en grands boutons/cards
- Compteur quantité (+/-) tactile
- Mode d'encaissement : toggle espèces / Mobile Money
- Billet émis avec QR code et perforation
- Historique en liste compacte avec horodatage

---

### 5. `backoffice/` — Back-office administrateur

**Principes :** dense en informations, tableaux, supervision, audit trail.

| Fichier | Écran CDP | Contenu |
|---|---|---|
| `index.html` | ADM-04 | Dashboard global : volume transactions, événements actifs, revenus plateforme, filtres période/canal |
| `kyc.html` | ADM-01 | File d'attente KYC, consultation pièces, valider/rejeter avec motif |
| `commissions.html` | ADM-02 | Taux par défaut, taux dérogatoires, historique reversements |
| `moderation.html` | ADM-03 | Événements signalés, suspendre/supprimer avec notification |
| `paiements.html` | ADM-05 | Journal webhooks, réconciliation commande/paiement/billet/versement |
| `remboursements.html` | ADM-06 | Demandes de remboursement, statut, gestion échecs, billets concernés |
| `utilisateurs.html` | ADM-07 | Identité consolidée + rôles, attribution/retrait permissions |
| `audit.html` | ADM-08 | Journal d'actions (KYC, suspension, remboursement, reversement, permissions), anomalies scan |

**Composants clés :**
- Sidebar avec navigation complète (Dashboard, KYC, Commissions, Modération, Paiements, Remboursements, Utilisateurs, Audit)
- Header avec badge « Admin »
- Tableaux avec colonnes triables, pagination
- Fiches détaillées (profil organisateur, détail commande)
- Timeline / historique d'actions
- Badges statut colorés

---

## Fichier commun `css/tixtogo.css`

Contient :
1. Variables CSS (palette, polices, rayons, ombres) — reprises de la charte
2. Classes Tailwind custom (`@layer utilities` ou `@apply`) pour les composants réutilisables
3. Composants non-Tailwind (stub-divider, perforation, animations de scan)
4. Base responsive (polices, body, scrollbar)

## Fichiers `components/`

Partials HTML réutilisables inclus via `<iframe>` ou copiés dans chaque page :
- `header.html` : navigation principale publique
- `sidebar-org.html` : sidebar organisateur (liste liens + état actif)
- `sidebar-admin.html` : sidebar administrateur
- `footer.html` : footer avec mentions
- `ticket-card.html` : carte billet avec stub-divider
- `scan-result.html` : écran résultat scan (vert/rouge)

---

## Priorité d'implémentation

### Sprint 1 — Fondations
1. Créer `tailwind.config.js` avec la palette complète
2. Créer `css/tixtogo.css` avec variables + composants charte
3. Créer les composants (`components/`)
4. Créer `public/index.html` (vitrine)

### Sprint 2 — Parcours acheteur complet
5. `public/recherche.html`
6. `public/evenement.html`
7. `public/achat.html`
8. `public/paiement.html`
9. `public/confirmation.html`
10. `public/mes-billets.html`

### Sprint 3 — Espace organisateur
11. `organisateur/index.html` (dashboard)
12. `organisateur/evenement-creation.html`
13. `organisateur/billets.html`
14. `organisateur/ventes.html`
15. `organisateur/equipe.html`
16. `organisateur/ambassadeurs.html`
17. `organisateur/points-de-vente.html`
18. `organisateur/invitations.html`
19. `organisateur/reversements.html`

### Sprint 4 — Scan PWA + POS
20. `scan/index.html` + `manifest.json`
21. `scan/scanner.html`
22. `pos/index.html`
23. `pos/ventes.html`
24. `pos/confirmation.html`

### Sprint 5 — Back-office admin
25. `backoffice/index.html` (dashboard)
26. `backoffice/kyc.html`
27. `backoffice/commissions.html`
28. `backoffice/moderation.html`
29. `backoffice/paiements.html`
30. `backoffice/remboursements.html`
31. `backoffice/utilisateurs.html`
32. `backoffice/audit.html`

---

## Règles de design transversales

- **Toutes les pages** utilisent la charte graphique TixTogo (palette, polices, composants)
- **Mobile-first** pour `public/` et `scan/`
- **Sidebar collapse** en hamburger sur mobile pour `organisateur/` et `backoffice/`
- **Stub-divider** (perforation) utilisé sur les cartes billet et les KPI cards
- **Badges** systématiques pour les statuts (valide/teal, utilisé/red, en attente/amber)
- **Boutons** : primary (amber) pour CTA principal, dark pour actions secondaires, outline pour annuler
- **Eyebrow** (monospace uppercase amber-deep) pour les sections
- **Responsive breakpoints** : sm (640px), md (768px), lg (1024px), xl (1280px)
- **Pas de JS lourd** : interactivité CSS uniquement (hover, focus, transitions) sauf pour le scan (caméra)
- **Images placeholder** : rectangles colorés avec texte descriptif, pas d'images réelles nécessaires
