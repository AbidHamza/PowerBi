# Room 3 : GlobeTrotter Analytics - Dashboard Marches Internationaux

**Bienvenue chez GlobeTrotter, l'entreprise qui exporte partout !**

Vous etes le Data Analyst d'une PME qui vend a l'international.
**Votre mission :** La directrice commerciale veut savoir ou investir son budget.
Elle hesite entre l'Afrique, l'Asie et l'Amerique du Sud. A vous de trancher avec les donnees.

---

## Ce que vous allez apprendre
1. **Travailler avec des donnees geographiques** (cartes Power BI).
2. **Nettoyer du JSON profondement imbrique** (objets dans des objets).
3. **Construire des indicateurs de marche** (densite, PIB, langues).

---

## Phase 1 : Recuperer les donnees
Cette fois, une seule URL mais BEAUCOUP de donnees imbriquees.

### Source principale : Tous les pays du monde
*   **URL** : `https://restcountries.com/v3.1/all`
*   250+ pays avec : nom, population, superficie, region, sous-region, langues, monnaies, drapeaux, etc.
*   Attention : Le JSON est tres imbrique. Chaque pays a des objets dans des objets.

### Source complementaire : Indicateurs par region
*   Pas d'API supplementaire. Vous allez **creer une table manuelle** dans Power BI :
    Entrer des donnees > Creez cette table :

| Region | Budget_Marketing_EUR | Priorite |
|--------|---------------------|----------|
| Africa | 50000 | Haute |
| Americas | 80000 | Moyenne |
| Asia | 120000 | Haute |
| Europe | 60000 | Basse |
| Oceania | 20000 | Basse |

---

## Phase 2 : Nettoyer les donnees (Le vrai defi)
C'est la room la plus technique en ETL. Voici ce qu'il faut extraire :

### Colonnes a garder et developper :
1. name -> developpez pour extraire common (nom courant) et official (nom officiel).
2. population -> nombre entier, directement utilisable.
3. area -> superficie en km2.
4. region -> continent (Africa, Americas, Asia, Europe, Oceania).
5. subregion -> sous-region (Western Europe, South America...).
6. languages -> Record imbrique. Developpez et gardez la **premiere langue** seulement.
7. currencies -> Record imbrique. Developpez pour extraire le **nom** et le **symbole**.
8. flags -> developpez pour extraire png (URL de l'image du drapeau).
9. latlng -> Liste de 2 valeurs. Extrayez latitude (index 0) et longitude (index 1).
10. borders -> Liste de codes pays frontaliers (utile pour Phase 5).

---

## Phase 3 : Creer les indicateurs (DAX)
La directrice veut ces KPIs :

1. **Population totale** par region.
2. **Densite moyenne** (Population / Superficie).
3. **Nombre de pays** par region.
4. **Superficie totale** par region.
5. **Taille moyenne d'un pays** (Superficie / Nb pays).

---

## Phase 4 : Visualisations

### Question 1 : "Ou sont les plus gros marches ?"
*   **Carte geographique (Map)** : Taille des bulles = Population, Couleur = Region.
*   La directrice verra tout de suite ou sont les concentrations.

### Question 2 : "Quelle region a le plus de potentiel ?"
*   **Graphique a barres groupees** : Regions en axe Y, Population + Superficie en valeurs.
*   Ajoutez le Budget_Marketing de la table manuelle en tooltip.

### Question 3 : "Est-ce qu'un petit pays peut etre interessant ?"
*   **Nuage de points** : Superficie (X) vs Population (Y), colore par Region.
*   Les points en haut a gauche = petits pays tres peuples = marches denses !

### Question 4 : "Combien de langues doit-on supporter ?"
*   **Graphique en anneau (Donut)** : Repartition des langues principales.
*   Si 60% des pays cibles parlent anglais, pas besoin de 10 traductions.

---

## Phase 5 : Analyse Expert

### Defi 1 : Score d'Attractivite de Marche
Creez un score composite pour chaque pays :
*   **40%** Population (normalisee)
*   **30%** Densite (normalisee)
*   **30%** Nombre de pays frontaliers (accessibilite logistique)
*   Classez les 20 pays les plus attractifs.

### Defi 2 : Concentration geographique (Herfindahl)
*   Calculez l'indice HHI de concentration de la population par region.
*   Formule : Somme des (part de chaque pays dans sa region)^2
*   HHI > 0.25 = region dominee par 1-2 pays (risque de dependance).

### Defi 3 : Budget par habitant cible
*   Croisez la table Budget_Marketing avec la population par region.
*   Calculez le cout par habitant potentiel. Quelle region est la moins chere a atteindre ?

---

## Phase 6 : Presentation
1. **Page d'accueil** : Carte du monde interactive + 5 KPI en haut.
2. **Page Region** : Filtre par region -> detail des pays.
3. **Page Recommandation** : Top 5 pays recommandes avec justification chiffree.
4. **Drapeaux** : Utilisez les URLs des drapeaux comme images dans les tableaux !
5. Enregistrez sous Nom_Prenom_GlobeTrotter.pbix
6. Demo de **5 minutes** : Recommandez 3 marches a la directrice avec preuves.

**A vous de convaincre. Les donnees ne mentent pas !**
