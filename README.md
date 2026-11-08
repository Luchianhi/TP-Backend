# LAB 1 : Conception et test d'une API REST avec HTTP et Postman

> Cours : **Développement Backend avec Java, Node.js et PHP**
> API utilisée : [DummyJSON](https://dummyjson.com) (API publique de démonstration simulant une gestion de produits)

# Avant de commencer
  - Installez Postman et vérifiez que curl --version fonctionne dans votre terminal.
  - Toutes les requêtes ciblent l’API de démonstration https://dummyjson.com.

# Objectifs
  - Comprendre le protocole **HTTP** et l'architecture **REST**.
  - Maîtriser l'interface et les fonctionnalités de **Postman**.
  - Savoir manipuler les **méthodes**, les **headers**, les **query params** et les **bodies JSON**.

# Étape 1 : Tester l’API avec cURL
Dans le terminal :
curl -X GET "https://dummyjson.com/products?limit=5" -H "Accept: application/json"
Repérez dans la réponse le tableau products et les champs total, skip et limit. Ouvrez aussi https://dummyjson.com/products/1 dans le navigateur.

<img width="885" height="1118" alt="Capture d&#39;écran 2026-11-08 193433" src="https://github.com/user-attachments/assets/7dfade52-9c9f-40e0-965e-84c8dea09bd5" />

<img width="1072" height="1198" alt="Capture d&#39;écran 2026-11-08 193638" src="https://github.com/user-attachments/assets/f85268c7-c539-42a3-a22b-974d5feb8642" />

# Étape 2 : Créer la collection Postman
New → Collection, nommez-la LAB1 - Gestion Produits REST.
Ajoutez 4 dossiers : Lecture (GET), Création (POST), Modification (PUT/PATCH), Suppression (DELETE).

# Étape 3 : Configurer l’environnement
Cliquez sur l’icône d’œil, puis créez l’environnement Demo API Env.
Ajoutez baseUrl = https://dummyjson.com et productId = 1.
Sélectionnez cet environnement en haut à droite.
Utilisez ensuite {{baseUrl}} dans toutes vos requêtes.
Étape 4 : Requêtes GET (dossier Lecture)
