# DAX Expert - Room 2 : TaskFlow Agency

## 1. Classification Automatique des Employes

```dax
Classe Employe = 
VAR ScoreActuel = [Score Productivite]
RETURN
SWITCH(TRUE(),
    ScoreActuel > 80, "Star",
    ScoreActuel > 50, "Stable",
    "A risque"
)
```

## 2. Ratio Effort / Resultat

### Taches assignees par employe
```dax
Taches Assignees = COUNTROWS(Todos)
```

### Ratio completion individuel
```dax
Ratio Completion = DIVIDE([Taches Terminees], [Taches Assignees])
```

### Ecart a la moyenne
```dax
Ecart Moyenne = 
VAR MoyGlobale = CALCULATE([Taux Completion], ALL(Users))
RETURN
[Ratio Completion] - MoyGlobale
```
*Positif = au-dessus de la moyenne. Negatif = en-dessous.*

## 3. Detection d'employes fantomes

```dax
Est Fantome = 
VAR PostsUser = [Nb Posts]
VAR TachesFinies = [Taches Terminees]
RETURN
IF(PostsUser = 0 && TachesFinies = 0, "FANTOME", "Actif")
```

## 4. Ranking des employes

```dax
Rang Employe = RANKX(ALL(Users), [Score Productivite], , DESC)
```

### Top 3 employes (filtre dynamique)
```dax
Est Top 3 = IF([Rang Employe] <= 3, 1, 0)
```
*Utilisez cette mesure comme filtre visuel : Est Top 3 = 1*

## 5. Engagement moyen par post

```dax
Engagement Moyen = DIVIDE([Commentaires Recus], [Nb Posts])
```
*Un post genere en moyenne combien de commentaires ? Utile pour le nuage de points.*
