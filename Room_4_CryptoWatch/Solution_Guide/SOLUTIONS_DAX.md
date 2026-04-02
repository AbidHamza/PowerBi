# Formules DAX - Room 4 : CryptoWatch

## 1. Indicateurs de Base

### Market Cap Total (Top 100)
```dax
Market Cap Total = SUM(Markets[market_cap])
```

### Volume 24h Total
```dax
Volume 24h = SUM(Markets[total_volume])
```

### Nombre de Cryptos en Hausse
```dax
Nb Hausse = CALCULATE(COUNTROWS(Markets), Markets[price_change_percentage_24h] > 0)
```

### Nombre de Cryptos en Baisse
```dax
Nb Baisse = CALCULATE(COUNTROWS(Markets), Markets[price_change_percentage_24h] < 0)
```

### Pourcentage en Hausse
```dax
Pct Hausse = DIVIDE([Nb Hausse], COUNTROWS(Markets))
```

### Pourcentage en Baisse
```dax
Pct Baisse = DIVIDE([Nb Baisse], COUNTROWS(Markets))
```

## 2. Categorie par crypto (Colonne Calculee)

*Creez une "Nouvelle Colonne" (pas une mesure) dans la table Markets :*
```dax
Categorie = 
SWITCH(TRUE(),
    Markets[market_cap_rank] <= 10, "Blue Chip",
    Markets[market_cap_rank] <= 50, "Mid Cap",
    "Small Cap"
)
```

## 3. Indicateurs de Marche

### Variation Moyenne 24h
```dax
Variation Moy 24h = AVERAGE(Markets[price_change_percentage_24h])
```

### Prix Moyen Pondere (par Market Cap)
```dax
Prix Moyen Pondere = 
DIVIDE(
    SUMX(Markets, Markets[current_price] * Markets[market_cap]),
    [Market Cap Total]
)
```

## 4. Indicateurs pour la Jauge

### Sante du Marche (0 a 100)
```dax
Indice Sante = 
VAR PctHausse = [Pct Hausse]
VAR VarMoy = [Variation Moy 24h]
RETURN
ROUND(PctHausse * 70 + MIN(MAX(VarMoy + 5, 0), 10) * 3, 0)
```
*Simplifie : Plus il y a de cryptos en hausse et plus la variation moyenne est positive, plus l'indice est eleve.*
