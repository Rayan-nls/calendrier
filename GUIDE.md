# Mettre le calendrier en ligne, pas à pas

Le site se compose de deux choses :
- **`index.html`** : la page (calendrier, watchlist, liste à manger).
- **Firebase** : une base de données gratuite qui garde les données et les partage entre vous deux.

Tu n'as besoin d'aucune connaissance technique. Suis les étapes dans l'ordre.

---

## Étape 1 : créer le projet Firebase (5 min)

1. Va sur https://console.firebase.google.com et connecte-toi avec ton compte Google.
2. Clique sur **Ajouter un projet**, donne-lui un nom (ex. `calendrier-rayan`).
3. Désactive Google Analytics si on te le propose, puis clique sur **Créer le projet**.

## Étape 2 : récupérer la configuration

1. Dans la page du projet, clique sur l'icône **`</>`** (Web).
2. Donne un nom à l'application (ex. `calendrier`), ne coche pas Firebase Hosting, puis **Enregistrer l'application**.
3. Firebase affiche un bloc `const firebaseConfig = { ... }`. Copie les valeurs.
4. Ouvre `index.html`, cherche `const FIREBASE_CONFIG = {` et remplace les valeurs `REMPLACE...` par les tiennes. Garde les guillemets.

## Étape 3 : activer la base de données

1. Dans le menu de gauche, va dans **Build → Firestore Database**.
2. Clique sur **Créer une base de données**, choisis une région proche (ex. `eur3` ou `europe-west`), puis **Mode production**.
3. Ouvre l'onglet **Règles**, remplace tout le texte par ceci, puis clique sur **Publier** :

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

Ces règles laissent **n'importe qui avec le lien** lire et modifier les données. C'est le choix « lien ouvert ». Si le site se retrouve entre de mauvaises mains, tu peux à tout moment supprimer la base dans la console.

## Étape 4 : mettre le site sur GitHub

1. Va sur https://github.com, connecte-toi, puis clique sur **New repository**.
2. Nom : `calendrier`. Visibilité : **Public** (obligatoire avec un compte gratuit pour GitHub Pages). Clique sur **Create repository**.
3. Clique sur **uploading an existing file**, glisse `index.html` (et ce `GUIDE.md` si tu veux), puis **Commit changes**.
4. Va dans **Settings → Pages**. Dans **Source**, choisis **Deploy from a branch**, branche **main**, dossier **/ (root)**, puis **Save**.
5. Après une minute, le site est en ligne à l'adresse :
   `https://TON-PSEUDO-GITHUB.github.io/calendrier/`

## Étape 5 : partager

Envoie l'adresse à ton amie. Elle l'ouvre dans son navigateur, sur ordinateur ou téléphone, et peut ajouter, modifier ou supprimer. Tout ce qui est ajouté est visible en direct pour vous deux.

---

## Si ça ne marche pas

- **« La base de données n'est pas encore branchée »** : la configuration de l'étape 2 n'a pas été remplacée dans `index.html`.
- **« Tu n'as pas le droit de modifier »** : les règles de l'étape 3 n'ont pas été publiées.
- **La page ne se met pas à jour** : rafraîchis-la (F5 ou Cmd+R), puis attends une minute après un changement sur GitHub.
