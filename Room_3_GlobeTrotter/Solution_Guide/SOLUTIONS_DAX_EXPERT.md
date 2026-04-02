# DAX Expert - Room 3 : GlobeTrotter Analytics

## 1. Score d'Attractivite de Marche

### Etape A : Normaliser la population (0 a 1)
```dax
Pop Normalisee = 
DIVIDE(
    Countries[population] - MIN(Countries[population]),
    MAX(Countries[population]) - MIN(Countries[population])
)
```

### Etape B : Normaliser la densite
```dax
Densite Normalisee = 
DIVIDE(
    [Densite] - CALCULATE(MIN([Densite]), ALL(Countries)),
    CALCULATE(MAX([Densite]), ALL(Countries)) - CALCULATE(MIN([Densite]), ALL(Countries))
)
```

### Etape C : Score composite
```dax
Score Attractivite = 
VAR PopNorm = [Pop Normalisee]
VAR DensNorm = [Densite Normalisee]
VAR FrontNorm = DIVIDE([Nb Frontieres], CALCULATE(MAX([Nb Frontieres]), ALL(Countries)))
RETURN
ROUND(PopNorm * 0.4 + DensNorm * 0.3 + FrontNorm * 0.3, 3)
```

### Etape D : Classement
```dax
Rang Attractivite = RANKX(ALL(Countries), [Score Attractivite], , DESC)
```
*Filtrez sur Rang <= 20 pour voir le Top 20.*

## 2. Indice de Concentration (HHI simplifie)

### Part de chaque pays dans sa region
```dax
Part Region = 
DIVIDE(
    Countries[population],
    CALCULATE(SUM(Countries[population]), ALL(Countries), VALUES(Countries[region]))
)
```

### HHI par region
```dax
HHI Region = 
SUMX(
    VALUES(Countries[name_common]),
    [Part Region] ^ 2
)
```
*HHI > 0.25 = region tres concentree (un pays domine).*
*HHI < 0.10 = region equilibree.*

## 3. Budget optimal par region

### Cout par habitant potentiel
```dax
Cout Par Habitant = 
DIVIDE(
    SUM(Budget[Budget_Marketing_EUR]),
    [Population Totale]
)
```

### ROI estime (simplifie)
```dax
ROI Estime = 
VAR CoutHab = [Cout Par Habitant]
VAR Attractivite = AVERAGE([Score Attractivite])
RETURN
DIVIDE(Attractivite, CoutHab)
```
*Plus le ROI est eleve, meilleur est le rapport qualite/prix de la region.*

## 4. Pays isoles vs connectes

```dax
Type Connectivite = 
SWITCH(TRUE(),
    [Nb Frontieres] >= 6, "Hub logistique",
    [Nb Frontieres] >= 3, "Bien connecte",
    [Nb Frontieres] >= 1, "Peu connecte",
    "Ile / Isole"
)
```
