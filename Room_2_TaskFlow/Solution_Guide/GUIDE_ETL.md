# Guide ETL - Room 2 : TaskFlow Agency

## Etape 1 : Importer les 5 tables
Pour chaque URL :
1. Obtenir les donnees > Web > Collez l'URL.
2. Power BI affiche une liste de Records.
3. Cliquez sur **Vers la table** (To Table) > OK.
4. Cliquez sur les **deux fleches** en haut de la colonne pour developper.
5. Decochez "Utiliser le nom de la colonne d'origine comme prefixe" > OK.

## Etape 2 : Nettoyage par table

### Users (Employes)
- La colonne address contient un Record imbrique.
- Developpez-la pour extraire city et zipcode (ignorez geo/lat/lng).
- La colonne company contient aussi un Record -> extrayez name et renommez en companyName.
- Supprimez les colonnes inutiles : phone, website, suite, zipcode (optionnel).

### Posts
- Table simple. Gardez : userId, id, title, body.
- Renommez id en postId pour eviter les conflits.

### Comments
- Gardez : postId, id, name, email, body.
- Renommez id en commentId.

### Todos
- La colonne completed est un booleen (true/false).
- Verifiez que Power BI la detecte bien comme **Vrai/Faux** (pas du texte).
- Renommez id en todoId.

### Albums
- Table simple : userId, id, title.
- Renommez id en albumId.

## Etape 3 : Typage
| Colonne | Type attendu |
|---------|-------------|
| Tous les IDs | Nombre entier |
| completed (Todos) | Vrai/Faux |
| email | Texte |
| title, body, name | Texte |

## Etape 4 : Verifications
Avant de fermer l'editeur Power Query :
- **Users** : 10 lignes
- **Posts** : 100 lignes
- **Comments** : 500 lignes
- **Todos** : 200 lignes
- **Albums** : 100 lignes

Si vos chiffres ne correspondent pas, vous avez rate une etape d'expansion.

---
**Vos 5 tables sont pretes. Direction la modelisation !**
