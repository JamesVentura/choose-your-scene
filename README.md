# Find Your Scene — tableau de bord du projet

Ce dépôt héberge le **tableau de bord de suivi** du projet *Find Your Scene* : une future application façon Letterboxd/Babelio, mais pour le spectacle vivant (théâtre, danse, cirque, magie, musique, battles, drag, cabaret...).

Le concept complet vient de la page Notion **[Find Your Scene](https://spiffy-catsup-fd5.notion.site/Find-Your-Scene-3b4e034dfd4c80a99895e927b90ba8c8)**. Ce dépôt ne construit pas encore l'application elle-même : il centralise, pour la porteuse du projet, l'avancée de sa concrétisation — timeline, pourcentage de complétion, inspirations, dépôts open-source utiles, et bientôt l'accès à la maquette testable.

## Consulter le tableau de bord

Ouvrir `index.html` (aucune dépendance, aucun build — un seul fichier autonome). Une fois ce dépôt fusionné sur `main` avec GitHub Pages activé (Settings → Pages → branche `main`, dossier `/`), le tableau de bord sera accessible en ligne à une URL du type `https://<utilisateur>.github.io/choose-your-scene/`.

## Mettre à jour l'avancement

Toutes les données affichées (les 7 actes du projet, leur statut, leur poids, le journal de bord) sont regroupées dans le bloc `<script>` en bas de `index.html`, dans les tableaux `phases` et `journalEntries`. Modifier une entrée — par exemple passer un acte de `"todo"` à `"progress"` ou `"done"`, ajuster son `percent` — met automatiquement à jour l'anneau de progression globale, la barre de répartition et la timeline, sans toucher au reste de la page.

## Recherche déjà effectuée

- **Applications proches** : Dixit (OnParticipe), le projet similaire trouvé en parallèle sur onparticipe.fr, Mezzanine (Theater Diary), Theatregoer.
- **Dépôts GitHub explorés** : [todam-app/todam](https://github.com/todam-app/todam) (le plus proche en ambition — journal open-source du spectacle vivant, monorepo Expo + Fastify + PostgreSQL), [jameslittle230/thtr](https://github.com/jameslittle230/thtr), des clones Letterboxd pour les patterns UI de notation, et [StageOps-EIP/StageOps](https://github.com/StageOps-EIP/StageOps) côté régie technique.

Le détail complet est dans le tableau de bord lui-même (sections « Ce qui existe déjà » et « Dépôts GitHub explorés »).

## Documents

- [`docs/02-specifications-fonctionnelles.md`](docs/02-specifications-fonctionnelles.md) — spécifications fonctionnelles (Acte II) : parcours par onglet, modèle de données, catégories, périmètre du MVP, questions ouvertes en attente de validation.
