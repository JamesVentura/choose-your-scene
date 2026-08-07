# Acte II — Spécifications fonctionnelles

> Statut : **validé le 7 août 2026**. Ce document détaille ce qui a été posé dans l'idée d'origine (page Notion *Find Your Scene*), rendu concret et testable, et tranché sur les six points qui restaient ouverts (§7).

> **Portée actuelle (précisée le 7 août 2026) :** ce n'est pas un lancement public. La cible, c'est l'entourage proche de la porteuse du projet — **moins de dix personnes** — pour un vrai test d'usage. Aucun déploiement en ligne ni publication sur les stores n'est prévu pour l'instant. La réflexion business plan n'est pas d'actualité : elle viendra une fois qu'au moins une semaine de test réel aura eu lieu. Ça allège une partie du périmètre (§5) et ça redéfinit ce que sont les Actes VI et VII de la timeline.

## 1. Principes directeurs

- **Un journal avant un catalogue.** L'usage central, c'est noter ce qu'on a vu — comme sur Letterboxd ou Babelio. Le catalogue (fiches spectacle, compagnie) est le support qui rend ce journal possible, pas l'inverse.
- **Le spectacle vivant, au sens large.** Théâtre, danse, cirque, magie, comédie musicale, battles — pas seulement le théâtre comme le font les apps anglophones existantes (Mezzanine, Theatregoer).
- **France d'abord, structure prête à s'étendre.** Les lieux et compagnies sont des données, pas du contenu codé en dur — ce qui permet d'ajouter une ville ou un pays sans changer l'application.
- **Accessible par défaut.** Pas d'italique en texte courant, contraste élevé, alignement à gauche, pensé dès les specs et pas rajouté après-coup.
- **Sécurité de la communauté non négociable.** La modération anti-harcèlement fait partie du MVP, pas d'une version future.

## 2. Catégories

Catégories reprises telles quelles depuis l'idée d'origine :

| Catégorie | Notes |
|---|---|
| Magie | |
| Danse contemporaine | |
| Ballet classique | |
| Battle all style | |
| Battle électro | |
| Cirque contemporain | |
| Cirque traditionnel | |
| Comédie musicale | |
| Spectacle jeune public | Filtrage par âge à prévoir |
| Théâtre contemporain | |
| Théâtre classique | |
| Musique | Ajoutée le 7 août 2026 |
| Drag | Ajoutée le 7 août 2026 |
| Cabaret | Ajoutée le 7 août 2026 |

Chaque spectacle peut appartenir à **une catégorie principale + des tags secondaires** (ex. un spectacle "cirque + jeune public"), pour éviter de multiplier les catégories au fil du temps.

Musique, drag et cabaret étaient cités dans l'idée de départ sans figurer dans la liste détaillée : décision prise de les traiter comme des **catégories à part entière**, au même niveau que les onze premières, plutôt que comme des tags secondaires.

## 3. Modèle de données

Onze entités suffisent à couvrir le MVP. Les relations principales sont indiquées entre parenthèses.

### Utilisateur (`User`)
Pseudo, avatar, bio, ville, catégories favorites, rôle (`spectateur` / `compagnie` / `modérateur`), date d'inscription, visibilité du profil (**public par défaut**, réglable en amis uniquement ou privé).

### Spectacle (`Show`)
Titre, catégorie principale + tags, description, durée, teaser vidéo, photos, âge conseillé, compagnie(s) associée(s) *(→ Company)*, dates de représentation *(→ TourDate)*.

### Compagnie (`Company`)
Nom, description, logo, réseaux sociaux, artistes *(→ Artist)*, spectacles *(→ Show)*, statut de vérification (*revendiquée* / *non revendiquée*). Pour le MVP, le catalogue est alimenté par l'équipe Find Your Scene — le champ existe dès le départ mais la revendication en self-service par les compagnies elles-mêmes arrive après validation du MVP.

### Artiste (`Artist`)
Nom, bio, photo, compagnies associées *(→ Company)*, rôle (metteur en scène, interprète, chorégraphe...).

### Lieu (`Venue`)
Nom, adresse, ville, accessibilité (PMR, etc.), spectacles programmés *(→ TourDate)*.

### Date de représentation (`TourDate`)
Spectacle *(→ Show)*, lieu *(→ Venue)*, date et heure, lien de réservation, statut (à venir / complet / annulé).

### Entrée de journal / avis (`Entry`)
Utilisateur *(→ User)*, spectacle *(→ Show)*, date vue, lieu, personnes accompagnantes *(→ User, optionnel)*, **note en étoiles (1 à 5, façon Letterboxd)**, avis texte, photos personnelles, visibilité (**publique par défaut**, réglable en amis uniquement ou privé, entrée par entrée).

### Liste (`List`)
Titre, créateur *(→ User)*, spectacles *(→ Show)*, partageable via lien public ou non.

### Objectif (`Goal`)
Utilisateur *(→ User)*, catégorie ciblée (ou global), nombre cible, période (mois / année), progression calculée depuis les entrées de journal, visibilité (**publique par défaut**, réglable comme les entrées de journal).

### Billet (`Ticket`)
Utilisateur *(→ User)*, date de représentation *(→ TourDate)*, fichier ou QR code, origine. Pour le MVP, **ajout manuel uniquement** (photo, PDF ou QR) — l'import automatique depuis les e-mails et l'intégration Apple/Google Wallet sont repoussés après le MVP (§5).

### Signalement (`Report`)
Signalant *(→ User)*, cible (utilisateur, avis ou fiche), motif, statut (en attente / traité), décision, date.

## 4. Parcours par onglet

### Accueil
Fil d'actualité : sorties récentes des personnes suivies, recommandations selon catégories favorites et localisation, mises en avant éditoriales (nouveautés, spectacles qui se terminent bientôt).

### Chercher
Recherche par titre, compagnie, lieu ou catégorie. Filtres combinables : catégorie, ville, période, disponibilité de billets. Résultats : fiches spectacle et fiches compagnie.

### Fiche spectacle
Teaser vidéo et/ou photos, résumé, catégorie et tags, compagnie, note moyenne de la communauté, dates de représentation avec accès direct à la réservation, avis des personnes suivies en priorité, bouton "Ajouter à mes envies" / "Marquer comme vu".

### Fiche compagnie
Présentation, tournée en cours (liste de dates), spectacles au catalogue, page artiste pour chaque membre (cliquable depuis la fiche compagnie). Alimentée par l'équipe Find Your Scene au lancement ; l'auto-revendication par les compagnies est prévue après le MVP.

### Mes spectacles (journal)
Liste chronologique des spectacles vus, avec note et avis. Sous-sections : "à voir" (envies), "vus", "listes" personnalisées et partageables. Bilan mensuel et annuel : répartition par catégorie, spectacles marquants, comparaison à l'objectif fixé.

### Objectifs
Définir un nombre de spectacles à voir par catégorie ou en global, sur une période donnée. Progression alimentée automatiquement par le journal, pas de saisie manuelle en double.

### Profil
Spectacles vus, notes moyennes par catégorie, objectifs en cours, abonnés / suivis, listes publiques.

### Communauté
Suivre d'autres profils, voir leurs avis en priorité dans le fil et sur les fiches spectacle, recommandations affinées par le réseau suivi.

### Agenda
Vue calendrier des dates de représentation liées aux spectacles suivis ou mis en envie, croisée avec les billets déjà achetés (wallet).

### Wallet billets
Billets ajoutés manuellement (photo, PDF ou QR) pour le MVP, rattachés aux dates de représentation correspondantes, consultables hors-ligne, rappel avant la date. L'import automatique depuis les e-mails et l'intégration Apple/Google Wallet suivront en V2.

### Réductions & jeux-concours
Offres réservées aux utilisateurs de l'application, rattachées à des spectacles, compagnies ou catégories précises.

### Modération
Signalement disponible sur tout profil ou avis. Pour le MVP, chaque signalement est validé par **une personne dédiée** côté Find Your Scene avant toute décision — pas de suspension automatique par seuil, pour éviter les faux positifs et les abus du signalement. Une personne bannie reçoit une explication : "cette personne n'est pas sur l'application car elle ne respecte pas l'éthique portée par le site."

## 5. Périmètre de la version testable (Acte V)

Toujours appelée "MVP" ci-dessous par commodité, mais à comprendre comme **la version installée sur le téléphone de moins de dix personnes**, pas une version publique.

**Dans cette version :**
Fiche spectacle, fiche compagnie/artiste, journal personnel (vu / envies), avis et notes, recherche et filtres par catégorie, profil, objectifs simples, modération de base.

**Repoussé après cette version (donc après le retour de l'entourage, pas avant) :**
Import automatique des billets depuis les e-mails et intégration Apple/Google Wallet, comptes compagnie en self-service (revendication de fiche), réductions et jeux-concours, recommandations avancées par algorithme (une version simple par catégories favorites suffit), signalement communautaire à seuil automatique (la validation humaine reste la règle), extension hors de France, **et plus largement tout ce qui suppose un public au-delà de l'entourage** : publication sur l'App Store / Google Play, infrastructure pensée pour monter en charge, business plan.

**Conséquence pratique pour l'Acte IV et l'Acte V :** pas besoin de viser une distribution grand public tout de suite — une installation directe (lien de test, profil de développement) sur les téléphones du cercle proche suffit. Ça simplifie la maquette comme le développement, et ça peut être revu si le test se passe bien et qu'on veut aller plus loin.

## 6. Ce qu'on réutilise de la recherche (Acte I)

`todam-app/todam` reste la référence la plus proche : son découpage de données (lieux et compagnies en base plutôt que codés en dur, fiches vérifiables par les compagnies) correspond exactement à ce qui est décrit en §3 et §4 ci-dessus pour les fiches compagnie. À revisiter une fois ce document validé, pour évaluer précisément ce qui est repris comme référence d'architecture.

## 7. Décisions validées le 7 août 2026

| Sujet | Décision |
|---|---|
| Musique, drag, cabaret | Catégories à part entière (§2) |
| Notation | Étoiles, 1 à 5, façon Letterboxd (§3, `Entry`) |
| Visibilité par défaut (journal, objectifs) | Publique par défaut, réglable entrée par entrée (§3, §4) |
| Modération | Une personne dédiée valide chaque signalement pour le MVP, pas de seuil automatique (§4) |
| Wallet billets | Ajout manuel pour le MVP, intégration Apple/Google Wallet en V2 (§3, §4, §5) |
| Fiches compagnie | Alimentées par l'équipe Find Your Scene au lancement, revendication en self-service après le MVP (§3, §4, §5) |

L'Acte II est clos. Prochaine étape : Acte III, design UX/UI & identité visuelle.
