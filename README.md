# Find Your Scene — tableau de bord du projet

Ce dépôt héberge le **tableau de bord de suivi** du projet *Find Your Scene* : une future application façon Letterboxd/Babelio, mais pour le spectacle vivant (théâtre, danse, cirque, magie, musique, battles, drag, cabaret...).

Le concept complet vient de la page Notion **[Find Your Scene](https://spiffy-catsup-fd5.notion.site/Find-Your-Scene-3b4e034dfd4c80a99895e927b90ba8c8)**. Portée actuelle du projet : un test avec l'entourage proche de la porteuse du projet (moins de dix personnes), pas un lancement public — voir `docs/02-specifications-fonctionnelles.md` pour le détail.

Ce dépôt centralise, pour la porteuse du projet, l'avancée de sa concrétisation — timeline, pourcentage de complétion, inspirations, dépôts open-source utiles, et l'accès à la maquette testable.

## Consulter le tableau de bord

Le dépôt est public avec GitHub Pages activé sur cette branche : **[jamesventura.github.io/choose-your-scene](https://jamesventura.github.io/choose-your-scene/)**. En local, ouvrir `index.html` suffit aussi (aucune dépendance, aucun build — un seul fichier autonome).

La maquette interactive vit dans `maquette/index.html`, servie par Pages à `/choose-your-scene/maquette/` — le dashboard y renvoie depuis l'en-tête et depuis la section « À tester ».

## Mettre à jour l'avancement

Toutes les données affichées (les 7 actes du projet, leur statut, leur poids, le journal de bord, les retours du test) sont regroupées dans le bloc `<script>` en bas de `index.html`, dans les tableaux `phases`, `journalEntries` et `feedback`. Modifier une entrée — par exemple passer un acte de `"todo"` à `"progress"` ou `"done"`, ajuster son `percent`, ou ajouter un objet dans `feedback` — met automatiquement à jour l'anneau de progression globale, la barre de répartition, la timeline et la section « Retours du test », sans toucher au reste de la page.

## Recherche déjà effectuée

- **Applications proches** : Dixit (OnParticipe), le projet similaire trouvé en parallèle sur onparticipe.fr, Mezzanine (Theater Diary), Theatregoer.
- **Dépôts GitHub explorés** : [todam-app/todam](https://github.com/todam-app/todam) (le plus proche en ambition — journal open-source du spectacle vivant, monorepo Expo + Fastify + PostgreSQL), [jameslittle230/thtr](https://github.com/jameslittle230/thtr), des clones Letterboxd pour les patterns UI de notation, et [StageOps-EIP/StageOps](https://github.com/StageOps-EIP/StageOps) côté régie technique.

Le détail complet est dans le tableau de bord lui-même (sections « Ce qui existe déjà » et « Dépôts GitHub explorés »).

## Documents

- [`docs/02-specifications-fonctionnelles.md`](docs/02-specifications-fonctionnelles.md) — spécifications fonctionnelles (Acte II), validées : parcours par onglet, modèle de données, catégories, périmètre de la version testable.
- [`maquette/index.html`](maquette/index.html) — prototype cliquable (Actes III & IV) : 5 écrans, fiche spectacle, contenu d'exemple dans les 14 catégories. État de démonstration, rien n'est persisté après rechargement. Illustrations en SVG dessinées à la main — à remplacer par de vraies photos libres de droit depuis une session avec un accès réseau plus large.
- [`docs/03-questions-testeurs.md`](docs/03-questions-testeurs.md) — questions à poser à l'entourage après le test (Acte VI), pensées pour des réponses concrètes plutôt que des impressions vagues.
