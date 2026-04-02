# DAX Expert - Room 4 : CryptoWatch

## 1. Dominance (Part de Marche)

### Part de marche par crypto
```dax
Dominance = DIVIDE(Markets[market_cap], [Market Cap Total]) * 100
```
*Colonne calculee. Bitcoin sera autour de 40-60%.*

### Dominance cumulee (Top N)
```dax
Dominance Cumulee = 
VAR RangActuel = Markets[market_cap_rank]
RETURN
CALCULATE(
    DIVIDE(SUM(Markets[market_cap]), CALCULATE(SUM(Markets[market_cap]), ALL(Markets))),
    FILTER(ALL(Markets), Markets[market_cap_rank] <= RangActuel)
) * 100
```

## 2. Ratio Liquidite (Volume / Market Cap)

### Ratio V/MC
```dax
Ratio Liquidite = DIVIDE(Markets[total_volume], Markets[market_cap])
```
*Colonne calculee.*
*   > 0.3 = Tres liquide (beaucoup d'echanges)
*   0.05 - 0.3 = Normal
*   < 0.05 = Faible liquidite (attention)

### Classification Liquidite
```dax
Classe Liquidite = 
SWITCH(TRUE(),
    [Ratio Liquidite] > 0.3, "Hyper liquide",
    [Ratio Liquidite] > 0.05, "Normal",
    "Illiquide"
)
```

## 3. Volatilite Intra-journaliere

### Amplitude 24h (%)
```dax
Volatilite 24h = 
DIVIDE(
    Markets[high_24h] - Markets[low_24h],
    Markets[current_price]
) * 100
```
*Colonne calculee.*

### Classification Volatilite
```dax
Classe Volatilite = 
SWITCH(TRUE(),
    [Volatilite 24h] > 15, "Extreme",
    [Volatilite 24h] > 10, "Tres volatile",
    [Volatilite 24h] > 5, "Volatile",
    [Volatilite 24h] > 2, "Modere",
    "Stable"
)
```

## 4. Score de Risque Composite

### Etape A : Normaliser chaque facteur (0 a 1)
```dax
Risque Volatilite = 
DIVIDE(
    [Volatilite 24h],
    CALCULATE(MAX([Volatilite 24h]), ALL(Markets))
)
```

```dax
Risque Rang = 
DIVIDE(
    Markets[market_cap_rank],
    100
)
```

```dax
Risque Liquidite = 
1 - DIVIDE(
    [Ratio Liquidite],
    CALCULATE(MAX([Ratio Liquidite]), ALL(Markets))
)
```
*Inverse : faible liquidite = haut risque.*

### Etape B : Score final
```dax
Score Risque = 
ROUND(([Risque Volatilite] * 0.33 + [Risque Rang] * 0.33 + [Risque Liquidite] * 0.33) * 100, 1)
```

### Etape C : Classification
```dax
Niveau Risque = 
SWITCH(TRUE(),
    [Score Risque] > 75, "Tres eleve",
    [Score Risque] > 50, "Eleve",
    [Score Risque] > 25, "Modere",
    "Faible"
)
```

## 5. Distance au ATH (All-Time High)

```dax
Distance ATH = 
DIVIDE(
    Markets[ath] - Markets[current_price],
    Markets[ath]
) * 100
```
*Resultat en %. Si Bitcoin est a 50% de son ATH, ca veut dire qu'il a perdu la moitie de sa valeur max.*

### Opportunite d'achat ?
```dax
Signal Achat = 
SWITCH(TRUE(),
    [Distance ATH] > 80, "Opportunite forte",
    [Distance ATH] > 50, "A surveiller",
    [Distance ATH] > 20, "Prix correct",
    "Proche du sommet"
)
```
*Attention : Ce n'est PAS un conseil financier ! C'est un exercice pedagogique.*
