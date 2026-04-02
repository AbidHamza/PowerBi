# Guide ETL - Room 4 : CryptoWatch

## Etape 1 : Importer la table Markets (Top 100)
1. Obtenir les donnees > Web > Collez l'URL complete.
2. Power BI affiche une liste de 100 Records.
3. Vers la table > OK.
4. Developpez la colonne (deux fleches).
5. Selectionnez les colonnes utiles (voir liste dans le README).
6. Decochez "Utiliser le nom de la colonne d'origine comme prefixe".

### Colonnes a garder :
id, symbol, name, image, current_price, market_cap, market_cap_rank, total_volume, high_24h, low_24h, price_change_percentage_24h, price_change_percentage_1h_in_currency, price_change_percentage_7d_in_currency, circulating_supply, ath, atl

### Colonnes a supprimer :
roi, last_updated, fully_diluted_valuation, max_supply, total_supply, ath_date, atl_date, ath_change_percentage, atl_change_percentage

## Etape 2 : Importer la table Global
1. Obtenir les donnees > Web > URL Global.
2. Vous voyez un seul Record data.
3. Cliquez sur data pour entrer dedans.
4. Vous voyez plusieurs Records et valeurs.
5. Pour total_market_cap : cliquez > developpez > selectionnez eur.
6. Pour market_cap_percentage : cliquez > developpez > selectionnez btc.
7. Gardez aussi active_cryptocurrencies et markets.

*Resultat : 1 seule ligne avec les stats globales du marche.*

## Etape 3 : Importer la table Trending
1. Obtenir les donnees > Web > URL Trending.
2. Vous voyez un Record avec coins.
3. Cliquez sur coins > c'est une List de 7 elements.
4. Vers la table > OK.
5. Developpez > vous voyez des Records item.
6. Developpez item > selectionnez : id, name, symbol, market_cap_rank, thumb.

*Resultat : 7 lignes = les 7 cryptos trending.*

## Etape 4 : Creer la table Categories (manuelle)
1. Accueil > Entrer des donnees.
2. Creez :

| RangMin | RangMax | Categorie |
|---------|---------|-----------|
| 1 | 10 | Blue Chip |
| 11 | 50 | Mid Cap |
| 51 | 100 | Small Cap |

3. Pas de relation directe. Vous utiliserez une colonne calculee DAX pour assigner la categorie.

## Etape 5 : Typage
| Colonne | Type |
|---------|------|
| current_price, high_24h, low_24h | Nombre decimal (Devise EUR) |
| market_cap, total_volume | Nombre entier |
| price_change_* | Nombre decimal (%) |
| market_cap_rank | Nombre entier |
| circulating_supply | Nombre entier |
| image, thumb | URL (Texte) |

## Etape 6 : Verification
- **Markets** : 100 lignes exactement
- **Global** : 1 ligne
- **Trending** : 7 lignes

Note : Les donnees CoinGecko changent en temps reel. Vos chiffres seront differents de ceux de votre voisin. C'est normal !

---
**Donnees financieres pretes. Place aux indicateurs !**
