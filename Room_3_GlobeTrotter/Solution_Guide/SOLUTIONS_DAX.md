# Formules DAX - Room 3 : GlobeTrotter Analytics

## 1. Indicateurs de Base

### Population Totale
```dax
Population Totale = SUM(Countries[population])
```

### Superficie Totale
```dax
Superficie Totale = SUM(Countries[area])
```

### Nombre de Pays
```dax
Nb Pays = COUNTROWS(Countries)
```

### Densite Moyenne
```dax
Densite Moyenne = DIVIDE([Population Totale], [Superficie Totale])
```
*Resultat en habitants par km2.*

### Taille Moyenne d'un Pays
```dax
Taille Moyenne = DIVIDE([Superficie Totale], [Nb Pays])
```

## 2. Indicateurs par Region

### Population d'une Region (%)
```dax
Part Population Region = 
DIVIDE(
    [Population Totale],
    CALCULATE([Population Totale], ALL(Countries[region]))
)
```

### Budget par Habitant
*Necessite la table Budget reliee par region.*
```dax
Budget Par Habitant = 
DIVIDE(
    SUM(Budget[Budget_Marketing_EUR]),
    [Population Totale]
)
```

## 3. Indicateurs Geographiques

### Densite par pays (colonne calculee)
```dax
Densite = DIVIDE(Countries[population], Countries[area])
```
*Attention : utilisez "Nouvelle colonne" et pas "Nouvelle mesure" pour celle-ci.*

### Nombre de pays frontaliers
*Si vous avez garde borders comme texte separe par des virgules :*
```dax
Nb Frontieres = 
IF(
    Countries[borders] = BLANK(), 
    0, 
    LEN(Countries[borders]) - LEN(SUBSTITUTE(Countries[borders], ",", "")) + 1
)
```
*Astuce : On compte les virgules + 1 pour avoir le nombre d'elements.*
