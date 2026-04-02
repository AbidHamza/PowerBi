# Guide DAX : Niveau Expert 🌶️

Voici les formules pour les défis avancés (Pareto & Segmentation).
Accaccrochez-vous, c'est du vrai DAX.

## 1. Segmentation Client Dynamique (ABC)

Cette mesure classe dynamiquement un client selon son CA.
Vous devez d'abord créer la mesure `[CA Total]`.

```dax
Class Client = 
VAR SalesUser = [CA Total]
RETURN
SWITCH(TRUE(),
    SalesUser > 5000, "Or 🥇",
    SalesUser > 2000, "Argent 🥈",
    "Bronze 🥉"
)
```
*Astuce : Vous pouvez utiliser cette mesure en "Légende" d'un graphique pour voir combien de "Or" vous avez.*

## 2. Analyse de Pareto (Les 20/80)

C'est le Saint Graal. On veut le % cumulé du CA par produit.

### Étape A : Le Rang du produit
D'abord, on classe les produits du meilleur au moins bon.
```dax
Rang Produit = RANKX(ALL(Products), [CA Total], , DESC)
```

### Étape B : Le CA Cumulé
On additionne le CA de tous les produits qui sont avant le produit actuel.
```dax
CA Cumulé = 
VAR CurrentRank = [Rang Produit]
RETURN
CALCULATE(
    [CA Total],
    FILTER(ALL(Products), [Rang Produit] <= CurrentRank)
)
```

### Étape C : La Courbe (%)
On divise par le CA total global.
```dax
% Pareto = DIVIDE([CA Cumulé], CALCULATE([CA Total], ALL(Products)))
```

Si vous affichez le `Nom Produit` (Axe Partagé) et `[CA Total]` (Barre) + `[% Pareto]` (Ligne), vous verrez la courbe monter !
Les produits où la courbe dépasse 80% sont les produits mineurs.
