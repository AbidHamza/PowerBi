# Room 4 : CryptoWatch - Dashboard Finance & Crypto

**Bienvenue chez CryptoWatch Capital !**

Vous etes le Data Analyst d'un petit fonds d'investissement crypto.
**Votre mission :** Le gerant veut un dashboard pour suivre le marche en temps reel.
Il n'y connait rien en crypto. Il veut des graphiques simples et des alertes claires.

---

## Ce que vous allez apprendre
1. **Manipuler des donnees financieres** (prix, volumes, variations).
2. **Creer des indicateurs de marche** (dominance, volatilite, ratios).
3. **Mettre en place des alertes visuelles** (mise en forme conditionnelle avancee).

---

## Phase 1 : Recuperer les donnees
L'API CoinGecko est gratuite et ne necessite pas de cle.

### 1. Top 100 Cryptomonnaies
*   **URL** : `https://api.coingecko.com/api/v3/coins/markets?vs_currency=eur&order=market_cap_desc&per_page=100&page=1&sparkline=false&price_change_percentage=1h%2C24h%2C7d`
*   Vous obtenez les 100 plus grosses cryptos avec : prix, market cap, volume 24h, variation 1h/24h/7j.

### 2. Donnees globales du marche
*   **URL** : `https://api.coingecko.com/api/v3/global`
*   Market cap total, dominance Bitcoin, nombre de cryptos actives.
*   Attention : Le JSON est imbrique dans un objet data.

### 3. Top 7 Trending (ce qui buzz)
*   **URL** : `https://api.coingecko.com/api/v3/search/trending`
*   Les 7 cryptos les plus recherchees en ce moment.
*   Structure imbriquee : coins > liste d'objets > item > details.

---

## Phase 2 : Nettoyer les donnees

### Table Markets (Top 100)
C'est la table principale. Apres expansion, vous devez avoir ces colonnes :
- id, symbol, name (identite)
- current_price (prix actuel en EUR)
- market_cap (capitalisation)
- total_volume (volume echange en 24h)
- price_change_percentage_24h (variation en %)
- price_change_percentage_7d_in_currency (variation 7 jours)
- high_24h, low_24h (plus haut / plus bas du jour)
- circulating_supply (nombre de tokens en circulation)
- image (URL du logo)

### Table Global
Developpez l'objet data pour extraire :
- total_market_cap -> developpez pour eur
- market_cap_percentage -> developpez pour btc (dominance Bitcoin)
- active_cryptocurrencies (nombre total)

### Table Trending
Structure complexe. Developpez coins > puis chaque item pour extraire :
- id, name, symbol, market_cap_rank, thumb (mini logo)

---

## Phase 3 : Modelisation
Pas de relations directes entre les 3 tables (elles sont independantes).
La table **Markets** est votre table de faits principale.

> **Astuce** : Creez une table calculee de **Categories** pour regrouper :

| Rang | Categorie |
|------|-----------|
| 1-10 | Blue Chip |
| 11-50 | Mid Cap |
| 51-100 | Small Cap |

---

## Phase 4 : Indicateurs (DAX)
Le gerant veut ces KPI en haut du dashboard :

1. **Market Cap Total** (somme des 100 cryptos).
2. **Volume 24h Total**.
3. **Cryptos en hausse** (% avec variation 24h > 0).
4. **Cryptos en baisse** (% avec variation 24h < 0).
5. **Prix moyen pondere** (par market cap).

---

## Phase 5 : Visualisations

### Question 1 : "Comment va le marche aujourd'hui ?"
*   **Heatmap (Matrice)** : Lignes = cryptos, Couleur = variation 24h.
*   Vert = hausse, Rouge = baisse. Le gerant voit tout en 2 secondes.

### Question 2 : "Ou est l'argent concentre ?"
*   **Treemap** : Taille = Market Cap, Couleur = Variation 7j.
*   Bitcoin et Ethereum domineront visuellement. C'est normal.

### Question 3 : "Quelles cryptos sont sur-echangees ?"
*   **Nuage de points** : Market Cap (X) vs Volume 24h (Y).
*   Les points au-dessus de la diagonale = volume anormalement eleve = a surveiller.

### Question 4 : "C'est quoi le buzz du moment ?"
*   **Tableau avec logos** : Les 7 Trending avec rang, nom et image.
*   Le gerant adore savoir "ce dont tout le monde parle".

### Question 5 : "Est-ce que je dois m'inquieter ?"
*   **Jauge (Gauge)** : % de cryptos en baisse.
*   < 40% = marche sain. > 60% = alerte. > 80% = panique.

---

## Phase 6 : Analyse Expert

### Defi 1 : Indice de Dominance
Calculez la part de marche de chaque crypto :
*   Market Cap crypto / Market Cap total * 100
*   Affichez les 5 plus dominantes. Si Bitcoin > 50%, le marche est "Bitcoin-dependant".

### Defi 2 : Ratio Volume/MarketCap (Liquidite)
*   Un ratio eleve = crypto tres liquide (facile a acheter/vendre).
*   Un ratio faible = crypto "dormante" ou illiquide.
*   Classez les 100 cryptos par ce ratio. Les extremes sont interessants.

### Defi 3 : Volatilite Intra-journaliere
*   Calculez : (high_24h - low_24h) / current_price * 100
*   C'est l'amplitude du prix sur 24h en %.
*   > 10% = tres volatile. < 2% = stable (rare en crypto).

### Defi 4 : Score de Risque
Combinez 3 facteurs :
*   **33%** Volatilite (normalisee, inverse : haute volatilite = haut risque)
*   **33%** Rang Market Cap (normalisee : petit rang = moins risque)
*   **33%** Ratio Volume/MC (normalisee : haute liquidite = moins risque)
*   Classez en : "Faible risque", "Modere", "Eleve", "Tres eleve".

---

## Phase 7 : Presentation
1. **Page d'accueil** : 5 KPI + Jauge de sante du marche + Trending.
2. **Page Marche** : Heatmap + Treemap interactifs.
3. **Page Analyse** : Nuage de points + Top/Flop 10.
4. **Page Risque** : Classement par score de risque.
5. **Logos** : Utilisez la colonne image pour afficher les logos des cryptos !
6. **Couleurs** : Utilisez le vert/rouge comme code couleur universel (hausse/baisse).
7. Enregistrez sous Nom_Prenom_CryptoWatch.pbix
8. Demo de **5 minutes** : Le gerant veut savoir : "J'investis ou pas aujourd'hui ?"

**Les marches n'attendent pas. A vos dashboards !**
