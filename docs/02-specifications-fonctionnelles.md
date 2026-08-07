# Acte II — Spécifications fonctionnelles

> Statut : **premier jet, à valider**. Ce document détaille ce qui a été posé dans l'idée d'origine (page Notion *Find Your Scene*) pour que ce soit concret et testable. Les points qui demandent un choix de ta part sont regroupés en fin de document, dans **§7 Questions ouvertes** — c'est le seul endroit où j'ai besoin d'un retour pour passer cet acte à « Terminé ».

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

Chaque spectacle peut appartenir à **une catégorie principale + des tags secondaires** (ex. un spectacle "cirque + jeune public"), pour éviter de multiplier les catégories au fil du temps.

> ⚠️ Voir §7 — musique, drag et cabaret sont cités dans l'idée de départ mais n'apparaissent pas dans la liste de catégories détaillée. À trancher.

## 3. Modèle de données

Onze entités suffisent à couvrir le MVP. Les relations principales sont indiquées entre parenthèses.

### Utilisateur (`User`)
Pseudo, avatar, bio, ville, catégories favorites, rôle (`spectateur` / `compagnie` / `modérateur`), date d'inscription, visibilité du profil (public / amis / privé).

### Spectacle (`Show`)
Titre, catégorie principale + tags, description, durée, teaser vidéo, photos, âge conseillé, compagnie(s) associée(s) *(→ Company)*, dates de représentation *(→ TourDate)*.

### Compagnie (`Company`)
Nom, description, logo, réseaux sociaux, artistes *(→ Artist)*, spectacles *(→ Show)*, statut de vérification (*revendiquée* / *non revendiquée*).

### Artiste (`Artist`)
Nom, bio, photo, compagnies associées *(→ Company)*, rôle (metteur en scène, interprète, chorégraphe...).

### Lieu (`Venue`)
Nom, adresse, ville, accessibilité (PMR, etc.), spectacles programmés *(→ TourDate)*.

### Date de représentation (`TourDate`)
Spectacle *(→ Show)*, lieu *(→ Venue)*, date et heure, lien de réservation, statut (à venir / complet / annulé).

### Entrée de journal / avis (`Entry`)
Utilisateur *(→ User)*, spectacle *(→ Show)*, date vue, lieu, personnes accompagnantes *(→ User, optionnel)*, note, avis texte, photos personnelles, visibilité (public / amis / privé).

### Liste (`List`)
Titre, créateur *(→ User)*, spectacles *(→ Show)*, partageable via lien public ou non.

### Objectif (`Goal`)
Utilisateur *(→ User)*, catégorie ciblée (ou global), nombre cible, période (mois / année), progression calculée depuis les entrées de journal.

### Billet (`Ticket`)
Utilisateur *(→ User)*, date de représentation *(→ TourDate)*, fichier ou QR code, origine (import e-mail / ajout manuel).

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
Présentation, tournée en cours (liste de dates), spectacles au catalogue, page artiste pour chaque membre (cliquable depuis la fiche compagnie).

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
Billets rattachés automatiquement aux dates de représentation correspondantes, consultables hors-ligne, rappel avant la date.

### Réductions & jeux-concours
Offres réservées aux utilisateurs de l'application, rattachées à des spectacles, compagnies ou catégories précises.

### Modération
Signalement disponible sur tout profil ou avis. Traitement par un rôle dédié pendant la phase pilote. Une personne bannie reçoit une explication : "cette personne n'est pas sur l'application car elle ne respecte pas l'éthique portée par le site."

## 5. Périmètre MVP

**Dans le MVP (Acte V) :**
Fiche spectacle, fiche compagnie/artiste, journal personnel (vu / envies), avis et notes, recherche et filtres par catégorie, profil, objectifs simples, modération de base.

**Repoussé après le MVP :**
Wallet billets avec import automatique depuis les e-mails, réductions et jeux-concours, recommandations avancées par algorithme (une version simple par catégories favorites suffit au lancement), extension hors de France.

## 6. Ce qu'on réutilise de la recherche (Acte I)

`todam-app/todam` reste la référence la plus proche : son découpage de données (lieux et compagnies en base plutôt que codés en dur, fiches vérifiables par les compagnies) correspond exactement à ce qui est décrit en §3 et §4 ci-dessus pour les fiches compagnie. À revisiter une fois ce document validé, pour évaluer précisément ce qui est repris comme référence d'architecture.

## 7. Questions ouvertes

Pour passer l'Acte II à « Terminé », j'ai besoin d'un choix sur ces points :

1. **Musique, drag, cabaret** : catégories à part entière au même titre que les onze déjà listées, ou tags secondaires rattachés à une catégorie existante ?
2. **Notation** : étoiles (comme Letterboxd), note chiffrée, ou catégories qualitatives ("coup de cœur", "à revoir", "pas pour moi") ?
3. **Visibilité par défaut** des entrées de journal et des objectifs : public, amis uniquement, ou privé — avec réglage possible au cas par cas ?
4. **Modération** : une personne dédiée dans un premier temps, ou un système de signalement communautaire avec seuil avant action ?
5. **Wallet billets** : simple stockage de fichier/QR importé manuellement pour le MVP, ou intégration Apple Wallet / Google Wallet dès le départ ?
6. **Compagnies** : peuvent-elles créer un compte pour revendiquer et tenir leur fiche à jour dès le MVP, ou est-ce l'équipe Find Your Scene qui alimente le catalogue au lancement ?

Dès que tu as tranché ces six points (ici, sur le dashboard, ou autrement), je mets à jour ce document et on passe à l'Acte III (design UX/UI).
