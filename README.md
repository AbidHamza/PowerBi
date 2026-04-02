# Formation Power BI - Parcours Complet

**4 projets pratiques pour maitriser Power BI de A a Z.**

Chaque "Room" est un projet independant avec un scenario professionnel realiste.
Pas de theorie. Que de la pratique. Vous apprenez en construisant.

---

## Les 4 Rooms

| Room | Projet | Difficulte | Competences cles |
|------|--------|-----------|-----------------|
| [Room 1](Room_1_QuickShop/) | **QuickShop** - E-commerce | ** | Connecteur Web, ETL basique, DAX, Pareto |
| [Room 2](Room_2_TaskFlow/) | **TaskFlow** - Productivite RH | *** | Multi-tables, Modele etoile, Scoring, Clustering |
| [Room 3](Room_3_GlobeTrotter/) | **GlobeTrotter** - Marches internationaux | **** | JSON complexe, Cartes geo, HHI, Normalisation |
| [Room 4](Room_4_CryptoWatch/) | **CryptoWatch** - Finance & Crypto | **** | Donnees temps reel, Heatmap, Risque, Volatilite |

---

## Progression recommandee

```
Room 1 (Debutant+)     -> Vous savez connecter, nettoyer, visualiser.
    |
Room 2 (Intermediaire)  -> Vous savez croiser des tables et scorer.
    |
Room 3 (Avance)         -> Vous savez manipuler du JSON complexe et des cartes.
    |
Room 4 (Avance+)        -> Vous savez analyser des marches financiers.
```

---

## Structure de chaque Room

```
Room_X/
    README.md                    <- Le sujet (consignes completes)
    Solution_Guide/
        GUIDE_ETL.md             <- Comment nettoyer les donnees (pas a pas)
        SOLUTIONS_DAX.md         <- Formules DAX de base (copier-coller)
        SOLUTIONS_DAX_EXPERT.md  <- Formules DAX avancees (defis)
```

> **Conseil prof :** Donnez le README aux eleves. Gardez le Solution_Guide pour vous (ou distribuez-le apres la seance).

---

## APIs utilisees (toutes gratuites, sans cle)

| Room | API | URL de base |
|------|-----|-------------|
| 1 | DummyJSON | `https://dummyjson.com` |
| 2 | JSONPlaceholder | `https://jsonplaceholder.typicode.com` |
| 3 | REST Countries v3.1 | `https://restcountries.com/v3.1/all?fields=...` (max 10 champs par requete) |
| 4 | CoinGecko | `https://api.coingecko.com/api/v3` |

---

## Competences couvertes (par Room)

| Competence | R1 | R2 | R3 | R4 |
|-----------|----|----|----|----|
| Connecteur Web / API | x | x | x | x |
| Power Query / ETL | x | x | xx | x |
| JSON imbrique | x | - | xx | x |
| Modelisation (relations) | x | xx | x | - |
| DAX basique (SUM, COUNT, DIVIDE) | x | x | x | x |
| DAX avance (RANKX, CALCULATE, VAR) | x | x | x | x |
| Time Intelligence | x | - | - | - |
| Mise en forme conditionnelle | - | x | - | xx |
| Cartes geographiques | - | - | xx | - |
| Treemap / Heatmap | - | x | - | x |
| Nuage de points | x | x | x | x |
| Segmentation / Scoring | x | xx | xx | xx |
| Analyse de Pareto | xx | - | - | - |
| Vue mobile | x | - | - | - |
| Images depuis API | x | - | x | x |
| Table manuelle | - | - | x | x |
| Fusion de requetes (Merge) | - | - | x | - |

---

## Consignes generales

### Pour tous les projets :
1. **Nommez votre fichier** : `Nom_Prenom_NomDuProjet.pbix`
2. **Creez une page d'accueil** avec navigation vers les autres pages.
3. **Soignez le design** : Un rapport moche n'est pas lu.
4. **Preparez une demo de 5 minutes** pour presenter vos resultats.

### Evaluation :
| Critere | Points |
|---------|--------|
| Donnees importees et nettoyees correctement | /5 |
| Modelisation (relations, schema etoile) | /3 |
| Mesures DAX fonctionnelles | /4 |
| Visualisations pertinentes et lisibles | /4 |
| Analyse expert (defis avances) | /2 |
| Design et navigation | /2 |
| **Total** | **/20** |

---

## Conseils pour reussir
- **Sauvegardez souvent.** Power BI plante parfois.
- **Testez vos mesures** sur un visuel simple (Carte) avant de les utiliser dans un graphique complexe.
- **Google est votre ami** : Si une formule DAX ne marche pas, copiez l'erreur dans Google.
- **Ne faites pas 15 visuels.** 5 bons visuels > 15 visuels moches.
- **Racontez une histoire.** Chaque page doit repondre a une question precise.

**Bonne formation !**
