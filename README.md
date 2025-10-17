# Championnat de Ping Pong

Cette page HTML autonome vous permet de configurer et d'animer un championnat de ping pong (simples ou doubles) pour votre entreprise. Toutes les données sont synchronisées en temps réel via Firebase Realtime Database afin que chaque participant accède à la même interface, quel que soit son navigateur ou son appareil.

## Prérequis

- Un projet [Firebase](https://firebase.google.com/) avec la Realtime Database activée.
- Les identifiants Web du projet (clé API, domaine d'authentification, etc.).
- Un identifiant de tournoi (`TOURNAMENT_ID`) que tous les participants partageront.

## Configuration du stockage partagé (Firebase)

1. Créez un projet Firebase ou utilisez un projet existant.
2. Activez **Realtime Database** en mode verrouillé, puis ajoutez des règles d'accès adaptées à votre organisation. Par exemple, pour un usage interne simple sans authentification :
   ```json
   {
     "rules": {
       "tournaments": {
         "$id": {
           ".read": true,
           ".write": true
         }
       }
     }
   }
   ```
   > 💡 Pour plus de sécurité, vous pouvez activer l'authentification Firebase (email/mot de passe ou SSO d'entreprise) et mettre à jour les règles en conséquence.
3. Dans la console Firebase, ouvrez **Paramètres du projet → Vos applications → Web** et copiez la configuration JavaScript fournie.
4. Ouvrez le fichier [`index.html`](./index.html) et remplacez les valeurs d'exemple du bloc `firebaseConfig` (clé API, `projectId`, `databaseURL`, etc.) par celles de votre projet.
5. Ajustez la constante `TOURNAMENT_ID` pour isoler un tournoi (exemple : `championnat-entreprise-2024`). Tous les utilisateurs doivent utiliser la même valeur pour partager les données.
6. Déployez la page sur votre hébergement (voir section suivante). Lors du premier chargement, la structure par défaut est automatiquement créée dans la base si elle n'existe pas.

## Déploiement sur WordPress

1. Dans l'admin WordPress, créez une nouvelle page et basculez l'éditeur en mode **HTML/Code**.
2. Collez l'intégralité du contenu du fichier `index.html` (après avoir mis à jour la configuration Firebase) puis publiez la page.
3. Assurez-vous que la page est protégée (noindex déjà inclus) et, si nécessaire, restreignez l'accès via un mot de passe WordPress ou un plugin dédié.
4. Partagez l'URL de la page avec les participants ; toutes les mises à jour seront immédiatement reflétées pour tout le monde.

> 📄 Alternative : vous pouvez aussi téléverser `index.html` dans la médiathèque WordPress (ou via FTP) et créer un lien direct vers ce fichier si votre hébergement autorise l'exécution de fichiers HTML autonomes.

## Utilisation

- Paramétrez le tournoi (nom, format, règles, planning, rappels email, durée des matchs, lieu...).
- Ajoutez les participants (ou composez des équipes) et générez automatiquement les matchs ou créez-les manuellement.
- Chaque match possède un code de validation unique ; les joueurs saisissent leur score, qui est ensuite verrouillé pour éviter la triche. Les admins peuvent forcer un résultat via un code administrateur.
- Les organisateurs peuvent exporter/importer la configuration en JSON et générer un CSV des résultats.

## Sauvegarde et synchronisation

- Toutes les actions déclenchent une sauvegarde vers Firebase. Une pastille en haut de la page indique l'état de la synchronisation (connexion, sauvegarde en cours, dernière mise à jour ou erreur).
- Si la page est ouverte avant que la connexion Firebase soit opérationnelle, les modifications sont mises en file d'attente et seront envoyées dès que la synchronisation sera prête.
- Aucun `localStorage` n'est utilisé : les données sont partagées entre tous les navigateurs via la base de données distante.

## Tests et prévisualisation locale

1. Après avoir configuré `firebaseConfig`, ouvrez un terminal dans le dossier et lancez `python -m http.server`.
2. Accédez à `http://localhost:8000/index.html` et saisissez quelques données.
3. Ouvrez la page dans un second navigateur ou une fenêtre privée : vous verrez les mises à jour en temps réel.

## Personnalisation

- Le code est volontairement regroupé dans un seul fichier pour un déploiement facile. Vous pouvez le scinder (CSS/JS séparés) ou ajouter vos propres styles/sections si besoin.
- Adaptez les règles Firebase pour refléter la gouvernance de votre entreprise (authentification, audit, archivage...).
- Modifiez `TOURNAMENT_ID` ou dupliquez la page pour organiser plusieurs compétitions en parallèle.

Bon tournoi !
