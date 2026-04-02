# Guide ETL - Room 3 : GlobeTrotter Analytics

## Etape 1 : Importer les pays
1. Obtenir les donnees > Web > `https://restcountries.com/v3.1/all?fields=name,population,area,region,subregion,languages,currencies,flags,latlng,capital`
2. Power BI affiche une liste de 250 Records.
3. Cliquez sur **Vers la table** (To Table) > OK.
4. Developpez la colonne principale (deux fleches).
5. Vous verrez 10 colonnes principales (grace au filtre fields dans l'URL).

## Etape 2 : Extraire le nom du pays
1. La colonne name affiche "Record".
2. Cliquez sur les deux fleches > selectionnez common et official.
3. Vous avez maintenant name.common (ex: "France") et name.official (ex: "Republique francaise").

## Etape 3 : Extraire les coordonnees GPS
1. La colonne latlng affiche "List".
2. Faites clic droit > **Extraire les valeurs** > Separateur virgule.
3. Ensuite : **Fractionner la colonne** > Par delimiteur (virgule).
4. Renommez en Latitude et Longitude.
5. Changez le type en **Nombre decimal**.

## Etape 4 : Extraire la langue principale
1. La colonne languages affiche "Record".
2. Chaque pays a un format different (fra, eng, spa...).
3. **Astuce** : Clic droit sur la colonne > **Convertir en texte JSON** (ou Stringify).
4. Ensuite utilisez **Extraire** > Texte entre delimiteurs :" et ".
5. Renommez en Langue_Principale.

*Alternative plus simple :* Developpez la colonne, prenez la premiere valeur qui apparait.

## Etape 5 : Extraire la monnaie
1. La colonne currencies affiche "Record".
2. Meme technique que les langues : convertir en texte puis extraire.
3. Ou bien developpez et gardez name et symbol.

## Etape 6 : Extraire le drapeau
1. La colonne flags affiche "Record".
2. Developpez > selectionnez png.
3. Renommez en Drapeau_URL.

## Etape 7 : Colonnes a supprimer
Supprimez tout ce qui n'est pas utile :
translations, demonyms, maps, gini, car, coatOfArms, postalCode, idd, tld, cca2, cca3, ccn3, cioc, fifa, altSpellings, capitalInfo

## Etape 8 : Colonnes finales attendues
| Colonne | Type | Exemple |
|---------|------|---------|
| name_common | Texte | France |
| name_official | Texte | Republique francaise |
| population | Nombre entier | 67390000 |
| area | Nombre decimal | 551695 |
| region | Texte | Europe |
| subregion | Texte | Western Europe |
| Langue_Principale | Texte | French |
| Monnaie_Nom | Texte | Euro |
| Monnaie_Symbole | Texte | EUR |
| Drapeau_URL | Texte | https://... |
| Latitude | Nombre decimal | 46.0 |
| Longitude | Nombre decimal | 2.0 |
| capital | Texte | Paris |
| borders | Texte/Liste | ESP,BEL,DEU... |

## Etape 8b : Importer les frontieres (Source 2)
1. Obtenir les donnees > Web > `https://restcountries.com/v3.1/all?fields=name,borders`
2. Developpez name pour extraire common.
3. Developpez borders (List) en texte separe par des virgules.
4. **Fusionner** avec la table principale : Accueil > Fusionner des requetes.
5. Cle de fusion : name_common (table principale) = name.common (table frontieres).
6. Gardez la colonne borders de la fusion.

## Etape 9 : Creer la table Budget manuellement
1. Accueil > Entrer des donnees.
2. Creez 5 lignes (Africa, Americas, Asia, Europe, Oceania).
3. Ajoutez les colonnes Budget_Marketing_EUR et Priorite.
4. Reliez cette table a Countries via la colonne region.

---
**250 pays nettoyes. Pret pour la carte du monde !**
