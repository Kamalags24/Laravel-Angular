# Laravel-Angular


Pour travailler sur un projet fullstack en utilisant Laravel pour le backend et Angular pour le frontend, voici les étapes que vous pouvez suivre :

### Configuration de l'environnement

1. **Installer Laravel** :
   - Assurez-vous d'avoir Composer installé.
   - Créez un nouveau projet Laravel :
     ```bash
     composer create-project --prefer-dist laravel/laravel project-name
     ```

2. **Installer Angular** :
   - Assurez-vous d'avoir Node.js et npm installés.
   - Installez Angular CLI globalement :
     ```bash
     npm install -g @angular/cli
     ```
   - Créez une nouvelle application Angular :
     ```bash
     ng new frontend
     ```

### Développement de l'API Laravel

1. **Configurer la base de données** :
   - Modifiez le fichier `.env` de Laravel pour configurer votre base de données.

2. **Créer des migrations et des modèles** :
   - Par exemple, pour un modèle `Product` :
     ```bash
     php artisan make:model Product -m
     ```
   - Ajoutez les colonnes nécessaires dans le fichier de migration créé dans `database/migrations`.

3. **Créer des contrôleurs et des routes** :
   - Créez un contrôleur de ressource :
     ```bash
     php artisan make:controller ProductController --resource
     ```
   - Définissez les routes API dans `routes/api.php` :
     ```php
     Route::apiResource('products', ProductController::class);
     ```

4. **Implémenter les méthodes CRUD dans le contrôleur** :
   - Remplissez les méthodes dans `ProductController` pour gérer les produits.

### Développement du frontend Angular

1. **Générer des services et des composants** :
   - Créez un service pour gérer les requêtes HTTP :
     ```bash
     ng generate service product
     ```
   - Créez des composants pour afficher les produits, par exemple :
     ```bash
     ng generate component product-list
     ng generate component product-detail
     ng generate component product-form
     ```

2. **Configurer le service HTTP** :
   - Dans `product.service.ts`, injectez `HttpClient` et créez des méthodes pour interagir avec l'API Laravel.
     ```typescript
     import { HttpClient } from '@angular/common/http';
     import { Injectable } from '@angular/core';

     @Injectable({
       providedIn: 'root'
     })
     export class ProductService {
       private apiUrl = 'http://your-laravel-api-url/api/products';

       constructor(private http: HttpClient) { }

       getProducts() {
         return this.http.get(this.apiUrl);
       }

       getProduct(id: number) {
         return this.http.get(`${this.apiUrl}/${id}`);
       }

       createProduct(product: any) {
         return this.http.post(this.apiUrl, product);
       }

       updateProduct(id: number, product: any) {
         return this.http.put(`${this.apiUrl}/${id}`, product);
       }

       deleteProduct(id: number) {
         return this.http.delete(`${this.apiUrl}/${id}`);
       }
     }
     ```

3. **Créer les composants Angular** :
   - Utilisez les services dans vos composants pour afficher, ajouter, modifier et supprimer des produits.
   - Configurez les routes Angular pour naviguer entre les différents composants.

### Communication entre Laravel et Angular

1. **Configurer les en-têtes CORS dans Laravel** :
   - Installez le middleware CORS si nécessaire :
     ```bash
     composer require fruitcake/laravel-cors
     ```
   - Configurez le fichier `config/cors.php` pour autoriser les requêtes depuis votre application Angular.

2. **Tester les requêtes** :
   - Utilisez des outils comme Postman pour tester votre API Laravel indépendamment.
   - Testez votre application Angular pour vous assurer qu'elle peut communiquer avec l'API.

### Déploiement

1. **Déployer Laravel** :
   - Déployez votre application Laravel sur un serveur web (par exemple, avec Apache ou Nginx).
   - Assurez-vous que votre base de données est configurée et accessible.

2. **Déployer Angular** :
   - Générez la version de production de votre application Angular :
     ```bash
     ng build --prod
     ```
   - Déployez les fichiers générés (`dist/`) sur un serveur web ou un service de déploiement.

En suivant ces étapes, vous pouvez développer et déployer un projet fullstack en utilisant Laravel pour le backend et Angular pour le frontend. Si vous avez des questions spécifiques ou avez besoin de plus de détails sur une étape particulière, n'hésitez pas à demander.
