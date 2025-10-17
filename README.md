# Championnat de Ping Pong

Cette application est une page HTML statique qui permet d'organiser un tournoi de ping pong en interne. Elle ne nécessite pas de serveur spécifique ni de base de données distante : toutes les données sont sauvegardées dans le navigateur via le `localStorage`.

## Comment lancer la page ?

1. Téléchargez le fichier [`index.html`](./index.html) sur votre ordinateur ou sur votre hébergement web.
2. **Option rapide (localement)** : ouvrez simplement le fichier avec votre navigateur (double-clic depuis le Finder/Explorer).
3. **Option serveur** : placez le fichier sur votre hébergement ou lancez un petit serveur local `python -m http.server` depuis ce dossier, puis ouvrez `http://localhost:8000/index.html`.

Aucun build ni dépendance n'est nécessaire.

## Sauvegarde des données

- Les paramètres, participants, matchs et résultats sont stockés automatiquement dans le `localStorage` du navigateur utilisé.
- Vous pouvez exporter/importer un fichier JSON depuis l'interface pour transférer la configuration vers un autre navigateur ou sauvegarder un état.
- Il n'y a **pas** de base de données externe. Pour un stockage centralisé entre plusieurs machines, hébergez la page sur un site et utilisez le même navigateur (ou l'import/export) ou adaptez le code pour pointer vers une API de votre choix.

## Fonctionnalités principales

- Configuration du tournoi (simple/double, règles personnalisées, planning).
- Gestion des participants/équipes et génération des matchs.
- Saisie des scores avec codes de validation, verrouillage par l'administrateur et historique anti-triche.
- Export CSV, modèle d'email et rappels configurables.

## Authentification basique

Par défaut, la page propose un code administrateur et des codes de validation par match. Vous pouvez activer l'option d'authentification légère (formulaire dédié dans la section "Participants") pour limiter la saisie des scores aux personnes inscrites.

## Déploiement "no index"

La balise `<meta name="robots" content="noindex, nofollow">` est déjà présente pour éviter l'indexation par les moteurs de recherche lorsque la page est publiée.

