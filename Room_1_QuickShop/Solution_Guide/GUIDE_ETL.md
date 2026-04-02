# Guide Pédagogique : Nettoyer les Données (ETL)

Ceci est la solution pas à pas pour transformer l'API brute en tables utilisables.

## Étape 1 : Importer les données
1.  Dans Power BI, faites `Obtenir les données` > `Web`.
2.  Collez l'URL (ex: `https://dummyjson.com/products?limit=100`).
3.  Power BI vous montre une liste avec un seul élément "products".
4.  Cliquez sur **Transformer les données**.

## Étape 2 : Le piège du JSON
Vous voyez une ligne avec "Record" ou "List".
1.  Cliquez sur le lien **List** (en jaune ou vert) pour entrer dans le niveau inférieur.
2.  Maintenant vous avez une liste de "Record".
3.  Allez dans l'onglet **Transformer** > Cliquez sur le bouton **Vers la table** (To Table).
4.  Une colonne apparaît. Cliquez sur les deux petites flèches en haut à droite de l'en-tête (Extension).
5.  Décochez "Utiliser le nom de la colonne d'origine comme préfixe" et faites OK.
   -> Vous avez votre table !

## Étape 3 : La table Commandes / Carts
C'est la plus difficile. Voici comment faire :
1.  Répétez l'étape 2 pour obtenir la table des paniers.
2.  Vous voyez une colonne `products` qui contient `[List]`.
3.  **Ne paniquez pas.** Cliquez sur les deux flèches d'extension de cette colonne.
4.  Choisissez "Développer sur de nouvelles lignes" (Expand to new rows).
    *   Votre nombre de lignes augmente ! (Une ligne par produit vendu).
5.  Re-cliquez sur les flèches de la même colonne (maintenant ce sont des Records).
6.  Sélectionnez : `id` (c'est l'ID du produit), `quantity`, `total`, `discountPercentage`.
7.  Renommez `id` en `productId` pour ne pas confondre avec l'ID du panier.

## Étape 4 : Le Typage (Indispensable)
Power BI se trompe souvent sur les types. Vérifiez :
*   Prix (Price) : Doit être **Nombre décimal fixe** (Devise).
*   Date : Doit être **Date** (pas Texte).
*   Latitude/Longitude : Doit être **Nombre décimal**.

---
**Bravo, vos données sont prêtes à être reliées !**
