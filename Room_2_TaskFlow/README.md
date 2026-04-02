# Room 2 : TaskFlow Agency - Dashboard Productivite

**Bienvenue chez TaskFlow, l'agence digitale qui deborde !**

Vous etes le Data Analyst d'une agence de 10 employes.
**Votre mission :** Le directeur veut savoir qui bosse, qui poste, et qui traine.
Il en a marre des reunions hebdo inutiles. Il veut un dashboard en temps reel.

---

## Ce que vous allez apprendre
1. **Croiser plusieurs sources** pour construire un vrai modele relationnel.
2. **Analyser la productivite** avec des mesures DAX avancees.
3. **Detecter des anomalies** (employes inactifs, surcharge, etc.).

---

## Phase 1 : Recuperer les donnees
Vous allez connecter **5 tables** depuis l'API JSONPlaceholder.
Dans Power BI : Obtenir les donnees > Web > collez chaque URL.

### 1. Les Employes
*   **URL** : `https://jsonplaceholder.typicode.com/users`
*   10 employes avec nom, email, entreprise, ville.

### 2. Les Articles publies (Posts)
*   **URL** : `https://jsonplaceholder.typicode.com/posts`
*   100 articles. Chaque article a un userId (qui l'a ecrit).

### 3. Les Commentaires
*   **URL** : `https://jsonplaceholder.typicode.com/comments`
*   500 commentaires lies aux posts via postId.

### 4. Les Taches (Todos)
*   **URL** : `https://jsonplaceholder.typicode.com/todos`
*   200 taches avec un statut completed (true/false).
*   C'est la table la plus precieuse pour mesurer la productivite !

### 5. Les Albums Photo (Projets creatifs)
*   **URL** : `https://jsonplaceholder.typicode.com/albums`
*   100 albums, chacun attribue a un userId.

---

## Phase 2 : Organiser les donnees (Modelisation)
Toutes les tables tournent autour des **Employes**. Creez les relations :
*   Posts[userId] -> Users[id]
*   Todos[userId] -> Users[id]
*   Albums[userId] -> Users[id]
*   Comments[postId] -> Posts[id]

> **Schema attendu :** Etoile avec Users au centre. 5 tables, 4 relations.

---

## Phase 3 : Indicateurs cles (DAX)
Le directeur veut voir ces chiffres en haut du dashboard :

1. **Taux de completion** : % de taches terminees sur le total.
2. **Nb Posts par employe** : Qui produit le plus de contenu ?
3. **Nb Commentaires recus** : Engagement sur les posts de chaque employe.
4. **Score Productivite** : Combinaison ponderee (40% taches + 40% posts + 20% albums).

---

## Phase 4 : Visualisations (Repondre aux questions)

### Question 1 : "Qui sont mes Top Performers ?"
*   **Graphique a barres empilees** : Employes en axe, avec Posts (bleu), Taches terminees (vert), Albums (orange).
*   Le directeur verra d'un coup d'oeil qui fait quoi.

### Question 2 : "Est-ce que les taches sont bien distribuees ?"
*   **Treemap (Carte proportionnelle)** : Taille = Nb taches assignees, Couleur = Taux de completion.
*   Un gros carre rouge = employe surcharge qui ne finit pas.

### Question 3 : "Quels posts generent le plus d'engagement ?"
*   **Top 10 - Tableau** : Les 10 posts avec le plus de commentaires.
*   Ajoutez le nom de l'auteur (via la relation Users).

### Question 4 : "Y a-t-il des employes fantomes ?"
*   **Matrice conditionnelle** : Employes en lignes, metriques en colonnes.
*   Mettez une mise en forme conditionnelle (rouge si 0 posts ET 0 taches terminees).

---

## Phase 5 : Analyse Expert - Clustering de performance

### Defi 1 : Classification Automatique
Creez une mesure qui classe les employes en 3 categories :
*   **Star** : Score productivite > 80%
*   **Stable** : Score entre 50% et 80%
*   **A risque** : Score < 50%

### Defi 2 : Correlation Posts / Commentaires
*   Faites un nuage de points : Nb Posts (X) vs Nb Commentaires recus (Y).
*   Y a-t-il une correlation ? Plus on publie, plus on recoit de commentaires ?

### Defi 3 : Ratio Effort / Resultat
*   Calculez : Taches terminees / Taches assignees par employe.
*   Qui a le meilleur ratio ? Qui a le pire ?

---

## Phase 6 : Presentation
1. **Page d'accueil** avec 4 cartes KPI et navigation.
2. **Page Detail Employe** : Cliquez sur un nom -> tout se filtre.
3. **Page Alertes** : Les employes "A risque" en rouge.
4. Enregistrez sous Nom_Prenom_TaskFlow.pbix
5. Demo de **5 minutes** : Presentez au directeur pourquoi il devrait (ou pas) s'inquieter.

**Allez, montrez-nous qui merite une augmentation !**
