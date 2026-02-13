# Guide des Formules (DAX)

Voici les formules à copier-coller pour réussir vos indicateurs.
*N'oubliez pas : Créez une "Nouvelle Mesure", pas une colonne calculée !*

## 1. Indicateurs de Base

### Chiffre d'Affaires (CA)
C'est la somme de tous les totaux de ligne dans la table Commandes.
```dax
CA Total = SUM(Carts[total])
```

### Nombre de Commandes
On compte combien d'IDs de panier uniques on a.
```dax
Nb Commandes = DISTINCTCOUNT(Carts[id])
```

### Panier Moyen
Combien dépense un client en moyenne par commande ?
```dax
Panier Moyen = DIVIDE([CA Total], [Nb Commandes])
```

## 2. Indicateurs Avancés (Time Intelligence)

### CA Année Précédente (LY - Last Year)
Pour comparer avec l'an dernier.
*Note : Cela suppose que vous avez créé une table Calendrier reliée.*
```dax
CA LY = CALCULATE([CA Total], SAMEPERIODLASTYEAR('Calendrier'[Date]))
```

### Variation (%)
```dax
Variation CA = DIVIDE([CA Total] - [CA LY], [CA LY])
```

## 3. Autres Mesures Utiles

### Marge Estimée
On simule que la marge est le total moins la remise. (Simplification pédagogique).
```dax
Marge Totale = SUMX(Carts, Carts[total] * (1 - (Carts[discountPercentage]/100)))
```

### Nombre de Clients Actifs
```dax
Nb Clients = DISTINCTCOUNT(Carts[userId])
```
