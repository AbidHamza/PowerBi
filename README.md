# Projet Power BI : QuickShop Live

**Bienvenue dans l'équipe Data de QuickShop !** 🚀

Vous êtes le nouveau Data Analyst d'une start-up e-commerce.
**Votre mission :** Créer l'outil qui permettra au PDG de suivre les ventes en direct.
Fini les fichiers Excel ! Vous allez connecter Power BI directement au "Cœur" du système (l'API).

---

## Ce que vous allez apprendre
Pas de théorie ici, que de la pratique. Vous allez :
1.  **Récupérer des données réelles** (sans fichiers CSV !).
2.  **Nettoyer des données complexes** (le vrai travail du Data Analyst).
3.  **Créer des visuels utiles** pour répondre à des questions business.

---

## Phase 1 : Récupérer les données
Au lieu de télécharger des fichiers, vous allez utiliser le connecteur **Web** de Power BI.
Voici les 4 adresses à copier-coller :

### 1. Les Produits (Le Catalogue)
*   **URL** : `https://dummyjson.com/products?limit=100` ('limit=100' sert à récupérer 100 produits).
*   *Astuce* : Une fois chargé, cliquez sur "Convertir en Table".

### 2. Les Clients
*   **URL** : `https://dummyjson.com/users?limit=100`

### 3. Les Avis Clients
*   **URL** : `https://dummyjson.com/comments?limit=100`

### 4. Les Commandes (Le Boss Final)
*   **URL** : `https://dummyjson.com/carts?limit=50`
*   ⚠️ **Attention** : Cette table est "imbriquée". Une commande contient PLUSIEURS produits.
*   **Votre défi** : Trouver le bouton "Développer" (deux petites flèches) pour voir le détail de chaque produit vendu.

---

## Phase 2 : Organiser les données (Modélisation)
Une fois les données chargées, n'essayez pas de tout mélanger.
Créez des relations simples (Lier les tables entre elles avec la souris) :
*   Le `productId` des Commandes va avec l'`id` des Produits.
*   Le `userId` des Commandes va avec l'`id` des Clients.

> **Règle d'or** : Une bonne relation forme un schéma en étoile (Les ventes au milieu, le reste autour).

---

## Phase 3 : Créer les Indicateurs (DAX)
Le PDG veut voir 4 chiffres clés en gros en haut de la page :
1.  **Chiffre d'Affaires** (Total des ventes).
2.  **Nombre de Commandes**.
3.  **Panier Moyen** (Chiffre d'Affaires / Nombre de Commandes).
4.  **Note Moyenne** (Moyenne des avis clients).

---

## Phase 4 : La Visualisation (Répondre aux problèmes)
Ne faites pas des graphiques au hasard. Chaque visuel doit répondre à une question du PDG :

### Question 1 : "Est-ce qu'on perd de l'argent avec les promos ?"
*   *Le PDG pense qu'on remise trop.*
*   👉 **Faites un Nuage de Points** : Mettez la "Remise %" en bas (Axe X) et la "Marge" sur le côté (Axe Y). On verra tout de suite si les points sont bas !

### Question 2 : "Où sont nos meilleurs clients ?"
*   *Le Marketing veut lancer une pub locale.*
*   👉 **Faites une Carte** : Affichez les villes des clients. Plus la bulle est grosse, plus ils achètent.

### Question 3 : "Pourquoi les gens se plaignent ?"
*   👉 **Analysez les Commentaires** : Affichez les produits qui ont le plus de commentaires.

---

## Phase 5 : Rendre le rapport "Sexy"
Un rapport moche n'est pas lu.
1.  **Navigation** : Créez une page d'accueil avec des boutons pour aller vers les détails.
2.  **Mobile** : Créez la vue "Téléphone" pour que le PDG puisse regarder les chiffres dans l'ascenseur.
3.  **Images** : L'API vous donne les liens des images produits... affichez-les !

---

## Comment rendre votre travail ?
1.  Enregistrez votre fichier sous `Nom_Prenom_QuickShop.pbix`
2.  Déposez-le ici sur GitHub (ou envoyez-le selon les consignes du prof).
3.  Préparez une démo de **5 minutes** pour présenter vos trouvailles au PDG.

**Bonne chance, l'équipe compte sur vous !**
