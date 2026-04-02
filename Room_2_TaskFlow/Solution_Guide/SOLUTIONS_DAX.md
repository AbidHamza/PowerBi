# Formules DAX - Room 2 : TaskFlow Agency

## 1. Indicateurs de Base

### Nombre total de taches
```dax
Nb Taches = COUNTROWS(Todos)
```

### Taches terminees
```dax
Taches Terminees = CALCULATE(COUNTROWS(Todos), Todos[completed] = TRUE)
```

### Taux de completion
```dax
Taux Completion = DIVIDE([Taches Terminees], [Nb Taches])
```
*Formatez en % dans les proprietes de la mesure.*

### Nombre de Posts
```dax
Nb Posts = COUNTROWS(Posts)
```

### Nombre de Commentaires
```dax
Nb Commentaires = COUNTROWS(Comments)
```

### Nombre d'Albums
```dax
Nb Albums = COUNTROWS(Albums)
```

## 2. Indicateurs par Employe

### Posts par Employe (moyenne)
```dax
Moy Posts Employe = DIVIDE([Nb Posts], DISTINCTCOUNT(Users[id]))
```

### Commentaires recus par Employe
*Nombre de commentaires sur les posts d'un employe donne.*
```dax
Commentaires Recus = 
CALCULATE(
    COUNTROWS(Comments),
    RELATEDTABLE(Posts)
)
```

## 3. Score Productivite

### Score combine (sur 100)
```dax
Score Productivite = 
VAR MaxPosts = CALCULATE(MAX(COUNTROWS(Posts)), ALL(Users))
VAR MaxTaches = CALCULATE(MAX([Taches Terminees]), ALL(Users))
VAR MaxAlbums = CALCULATE(MAX(COUNTROWS(Albums)), ALL(Users))
VAR PctPosts = DIVIDE([Nb Posts], MaxPosts)
VAR PctTaches = DIVIDE([Taches Terminees], MaxTaches)
VAR PctAlbums = DIVIDE([Nb Albums], MaxAlbums)
RETURN
ROUND((PctTaches * 40 + PctPosts * 40 + PctAlbums * 20), 1)
```
*Note : Ce score est une simplification pedagogique. En vrai, on normaliserait autrement.*

## 4. Mesures pour les visuels

### Top 10 Posts (par commentaires)
Utilisez un visuel Tableau :
- Colonnes : Posts[title], Users[name] (via relation)
- Valeur : [Nb Commentaires]
- Filtre Top N = 10
