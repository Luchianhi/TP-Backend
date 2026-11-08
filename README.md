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

<img width="885" height="1118" alt="Image 01" src="https://github.com/user-attachments/assets/439c496a-46e4-4dea-a965-72008ff1da82" />

<img width="1072" height="1198" alt="Image 02" src="https://github.com/user-attachments/assets/c358eb6e-11b2-4bf4-bd2c-ae44bcadb816" />

# Étape 2 : Créer la collection Postman
  1. New → Collection, nommez-la LAB1 - Gestion Produits REST.
  2. Ajoutez 4 dossiers : Lecture (GET), Création (POST), Modification (PUT/PATCH), Suppression (DELETE).

<img width="1907" height="377" alt="Image 03" src="https://github.com/user-attachments/assets/7fbf57bb-3ecf-4d0f-9227-6b0579ad076e" />

# Étape 3 : Configurer l’environnement
  1. Cliquez sur l’icône d’œil, puis créez l’environnement Demo API Env.
  2. Ajoutez baseUrl = https://dummyjson.com et productId = 1.
  3. Sélectionnez cet environnement en haut à droite.
  4. Utilisez ensuite {{baseUrl}} dans toutes vos requêtes.

<img width="1900" height="415" alt="Image 04" src="https://github.com/user-attachments/assets/11a4b621-1c19-45ad-b8ca-8e190b7ace1e" />

# Étape 4 : Requêtes GET (dossier Lecture)
Requête	        | URL	                                                | Résultat attendu
Produit unique	| {{baseUrl}}/products/{{productId}}                  | 200 OK
Recherche	      | {{baseUrl}}/products/search avec le param q = phone |	200 OK, total = 1

<img width="823" height="1517" alt="Image 05" src="https://github.com/user-attachments/assets/7e8a6294-b129-45cd-99c2-01695461cb12" />

<img width="825" height="1853" alt="Image 06" src="https://github.com/user-attachments/assets/06b8f47f-cc8f-4ee7-b80b-c122fd021f23" />

# Étape 5 : Requête POST (dossier Création)
  - URL : {{baseUrl}}/products/add
  - Headers : Content-Type: application/json
  - Body : raw → JSON
json
{
  "title": "Casque Audio Sans Fil",
  "price": 129.99,
  "category": "audio",
  "stock": 25
}

<img width="1457" height="973" alt="Image 07" src="https://github.com/user-attachments/assets/8013fe83-e72f-4d56-b8a2-ca53225de126" />

# Étape 6 : PUT et PATCH (dossier Modification)
Les deux requêtes ciblent {{baseUrl}}/products/{{productId}}.
  - PUT remplace tout : envoyez title, price, category et stock.
  - PATCH modifie une partie : envoyez seulement { "price": 139.99 }.

<img width="1457" height="841" alt="Image 08" src="https://github.com/user-attachments/assets/1ec7e120-c0aa-4087-a1a0-acf35ccfc8a9" />

<img width="1466" height="838" alt="Image 09" src="https://github.com/user-attachments/assets/55b9be13-f49f-4f11-81ea-055bae5bb4d1" />

# Étape 7 : DELETE (dossier Suppression)
  - URL : {{baseUrl}}/products/{{productId}}
  - Résultat attendu : 200 avec "isDeleted": true.

<img width="1467" height="970" alt="Image 10" src="https://github.com/user-attachments/assets/ad2b282e-3bf9-4c13-9bca-f3cddf003564" />

# Étape 8 : Ajouter des tests Postman

Dans l’onglet Scripts → Post-response (ou Tests) de la requête POST :

pm.test("Statut de création valide", function () {
    pm.expect(pm.response.code).to.be.oneOf([200, 201]);
});
var jsonData = pm.response.json();
pm.environment.set("createdProductId", jsonData.id);
console.log("ID du produit créé : " + jsonData.id);

Exécutez la requête, puis vérifiez que createdProductId apparaît dans l’environnement.

<img width="1458" height="971" alt="Image 11" src="https://github.com/user-attachments/assets/b0be2938-0e4f-42e1-b2fb-2d75b0bb3b7c" />

# Étape 9 : Tester les erreurs
  - 404 : GET {{baseUrl}}/products/99999, qui renvoie {"message": "Product with id '99999' not found"}.
  - 400 : un POST avec un JSON malformé ou un price en texte.

Test à ajouter sur le 404 :
javascript
pm.test("Produit inexistant → 404", function () {
    pm.response.to.have.status(404);
});

<img width="1468" height="728" alt="Image 12" src="https://github.com/user-attachments/assets/4b12c303-f32d-461c-ab07-aafb97bd66be" />

# Étape 10 : Exercices
  1. Catégorie : GET {{baseUrl}}/products/category/smartphones
  2. Utilisateur : POST {{baseUrl}}/users/add avec {"firstName": "Awa", "lastName": "Diallo", "age": 25}
  3. Temps de réponse :

javascript
pm.test("Temps de réponse < 500 ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});

# Étape 11 : Préparer les livrables
  1. Exporter la collection : clic droit sur la collection → Export → Collection v2.1 (JSON).
  2. Rapport PDF : vos observations, les captures Postman de chaque étape et l’explication des codes HTTP rencontrés (200, 201, 400, 404).
