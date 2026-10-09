# 🌦️ Vue Weather App

Une application météo développée avec Vue 3, permettant de consulter les conditions météorologiques actuelles de différentes villes.

Ce projet a été réalisé dans le cadre de l'apprentissage de Vue.js, des composants, de la navigation et des requêtes HTTP.

## ✨ Fonctionnalités

* Ajouter des villes à une liste.
* Afficher ou masquer la liste des villes.
* Sélectionner une ville pour consulter sa météo actuelle.
* Afficher la température, la température ressentie, l'humidité, la vitesse du vent et la couverture nuageuse.
* Afficher une icône correspondant aux conditions météorologiques.
* Gérer les états de chargement et les erreurs lors des requêtes API.
* Naviguer entre la page d'accueil et la page À propos.
* Adapter l'interface aux différentes tailles d'écran.

## 🛠️ Technologies utilisées

* **Vue 3** : création de l'interface utilisateur.
* **JavaScript - Options API** : gestion des données réactives et des méthodes.
* **Vite** : environnement de développement et de build.
* **Vue Router** : navigation entre les pages.
* **Axios** : envoi des requêtes HTTP.
* **CSS** : mise en forme et design responsive.
* **OpenWeatherMap API** : récupération des données météorologiques.

## 📋 Prérequis

Avant de lancer le projet, assurez-vous d'avoir installé :

* Node.js
* npm
* Une clé API OpenWeatherMap

## 🚀 Installation et lancement

### 1. Récupérer le projet

Clonez le dépôt GitHub, puis placez-vous dans le dossier du projet.

```bash
git clone https://github.com/gheisariyeh/vue-weather-app.git
cd vue-weather-app
```

### 2. Installer les dépendances

```bash
npm install
```

### 3. Configurer la clé API

Créez un fichier `.env.local` à la racine du projet et ajoutez votre clé API :

```env
VITE_OPENWEATHER_API_KEY=votre_cle_api
```

Remplacez `votre_cle_api` par votre clé personnelle OpenWeatherMap.

Après toute modification du fichier `.env.local`, redémarrez le serveur de développement si nécessaire.

### 4. Lancer le serveur de développement

```bash
npm run dev
```

Ouvrez ensuite l'adresse indiquée dans le terminal, généralement `http://localhost:5173/`.

## 📦 Commandes disponibles

### Développement

```bash
npm run dev
```

Lance le serveur de développement avec rechargement à chaud.

### Build de production

```bash
npm run build
```

Génère la version optimisée de l'application dans le dossier `dist`.

### Prévisualisation du build

```bash
npm run preview
```

Permet de prévisualiser localement la version de production.

## 📁 Structure du projet

```text
src/
├── assets/
│   └── main.css
├── components/
│   └── CityList.vue
├── views/
│   ├── HomeView.vue
│   └── AboutView.vue
├── router/
│   └── index.js
├── App.vue
└── main.js
```

* `App.vue` : composant racine et navigation principale.
* `HomeView.vue` : gestion des villes et affichage des données météo.
* `AboutView.vue` : présentation de l'application.
* `CityList.vue` : affichage de la liste des villes et transmission de la ville sélectionnée au composant parent.
* `router/index.js` : définition des routes.
* `main.js` : point d'entrée de l'application.

## 🔐 Configuration et sécurité

Le fichier `.env.local` contient la clé API personnelle et ne doit pas être ajouté au dépôt Git.

Les variables commençant par `VITE_` sont intégrées au code côté navigateur et peuvent être visibles par les utilisateurs. Cette configuration convient à un projet d'apprentissage, mais une application en production nécessitant une clé secrète devrait utiliser un backend pour protéger cette clé.

## 📚 Ressources

* [Documentation officielle de Vue.js](https://vuejs.org/)
* [Documentation de Vue Router](https://router.vuejs.org/)
* [Documentation d'Axios](https://axios-http.com/)
* [Documentation d'OpenWeatherMap](https://openweathermap.org/api)
* [Documentation de Vite](https://vite.dev/)
