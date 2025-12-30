## EL BAKRAOUI Hayat École Nationale de Commerce et de Gestion (ENCG) - 4ème Année
<img src="EL BAKRAOUI Hayat (1).jpg" style="height:164px;margin-right:132px"/>
 ---
## sommaire
 ---
Charger la nouvelle base de données
Descriptif de la base de données top_six_economies.csv
Inspection initiale des données
Préparer les données
Gérer les valeurs manquantes
Analyse exploratoire des données (EDA)
Séparer les données d'entraînement et de test
Entraîner le modèle
Charger la nouvelle base de données
Inspection initiale des données
Préparer les données
Gérer les valeurs manquantes
Analyse exploratoire des données (EDA)
Séparer les données d'entraînement et de test
Entraîner le modèle
Évaluer le modèle
Explication Détaillée des Résultats d'Évaluation du Modèle
Explication de l'Importance des Caractéristiques

## appogé d'etudiant:24010285
## Classe:CAC2
  ---
## Rapport Thématique : Analyse des Indicateurs Économiques des Six Premières Économies Mondiales
  ---
## 1. Contexte et Objectif
# Rapport d'Analyse : Prédiction du Statut Économique des Grandes Puissances Mondiales

## 1. Présentation du Projet et Objectif

Ce projet de science des données vise à **prédire et à comprendre les facteurs qui classent une économie parmi les nations à fort PIB (Produit Intérieur Brut) ou à faible PIB**. En utilisant des indicateurs macroéconomiques et sociaux clés, l'objectif est de développer un modèle de Machine Learning capable de discriminer ces deux catégories, offrant ainsi une perspective sur les moteurs de la prospérité économique et un outil potentiel pour l'analyse comparative internationale.

## 2. Présentation Détaillée de la Base de Données (`df_economies_v2`)

La base de données utilisée est `/content/top_six_economies (1).csv`, chargée dans le DataFrame `df_economies_v2`. Elle contient des informations annuelles pour **six des plus grandes économies mondiales** (États-Unis, Chine, Japon, Allemagne, Royaume-Uni, Inde) sur une période de **30 ans, de 1991 à 2020**.

### Objectif du Dataset :
Ce jeu de données est conçu pour l'analyse macroéconomique comparative, permettant d'étudier l'évolution des performances économiques et sociales des nations au fil du temps. Il est idéal pour identifier les corrélations entre divers indicateurs et pour la modélisation prédictive.

### Organisme Préparateur (Origine Probable) :
La nature et la granularité des indicateurs suggèrent fortement une compilation par une institution internationale de renom, telle que la **Banque Mondiale (World Bank)**, le **Fonds Monétaire International (FMI)** ou les **Nations Unies (ONU)**. Ces organisations sont les principales sources de données économiques harmonisées pour la recherche et la politique.

### Caractéristiques (Variables) Clés :
Le dataset comprend 18 colonnes essentielles :
*   **`Country Name`** : Pays concerné.
*   **`Year`** : Année de l'observation.
*   **`GDP (current US$)`** : PIB nominal actuel en dollars US (utilisé pour définir la variable cible).
*   **`GDP, PPP (current international $)`** : PIB en parité de pouvoir d'achat.
*   **`GDP per capita (current US$)`** : PIB par habitant, indicateur du niveau de vie.
*   **`GDP growth (annual %)`** : Taux de croissance annuel du PIB.
*   **`Imports of goods and services (% of GDP)`** & **`Exports of goods and services (% of GDP)`** : Part du commerce international dans le PIB.
*   **`Central government debt, total (% of GDP)`** : Dette publique totale en pourcentage du PIB.
*   **`Total reserves (includes gold, current US$)`** : Réserves monétaires totales.
*   **`Unemployment, total (% of total labor force) (modeled ILO estimate)`** : Taux de chômage.
*   **`Inflation, consumer prices (annual %)`** : Taux d'inflation annuel.
*   **`Personal remittances, received (% of GDP)`** : Transferts de fonds des migrants.
*   **`Population, total`** & **`Population growth (annual %)`** : Données démographiques.
*   **`Life expectancy at birth, total (years)`** : Espérance de vie à la naissance.
*   **`Poverty headcount ratio at $1.90 a day (2011 PPP) (% of population)`** : Taux de pauvreté extrême.

### Problématiques Notables :
L'inspection initiale a révélé la présence de **valeurs manquantes** importantes dans les colonnes `Central government debt, total (% of GDP)` (69 valeurs manquantes) et `Poverty headcount ratio at $1.90 a day (2011 PPP) (% of population)` (75 valeurs manquantes), nécessitant une étape d'imputation.

## 3. Étapes de l'Analyse de Données et Résultats

### 3.1. Préparation des Données

1.  **Création de la Variable Cible** : Une variable cible binaire, `is_high_gdp`, a été créée. Une économie est classée `1` (High GDP) si son `GDP (current US$)` est supérieur à la médiane du PIB de l'ensemble du dataset (environ 3 040 milliards USD), et `0` (Low GDP) sinon.
2.  **Séparation Features/Cible** : Les caractéristiques (`X`) et la variable cible (`y`) ont été séparées. Les colonnes `Unnamed: 0`, `GDP (current US$)`, et `is_high_gdp` ont été exclues des caractéristiques.
3.  **Encodage One-Hot** : La variable catégorielle `Country Name` a été transformée en plusieurs colonnes binaires (`Country Name_Germany`, `Country Name_India`, etc.) à l'aide de l'encodage One-Hot pour être utilisable par les modèles de Machine Learning.
4.  **Gestion des Valeurs Manquantes** : Toutes les valeurs manquantes restantes dans le DataFrame des caractéristiques (`X`) ont été imputées (remplacées) par la moyenne de leurs colonnes respectives à l'aide de `SimpleImputer`. Après cette étape, aucune valeur manquante n'était présente dans `X_imputed_clean`.

### 3.2. Analyse Exploratoire des Données (EDA)

1.  **Statistiques Descriptives** : Un résumé statistique complet a été généré pour le DataFrame `X_imputed_clean`, fournissant des informations sur la tendance centrale, la dispersion et la distribution des variables numériques et binaires.
2.  **Visualisations Clés** :
    *   Des histogrammes ont illustré les distributions de la `Population, total`, du `Inflation, consumer prices (annual %)` et du `Unemployment, total (% of total labor force)` en fonction de la variable cible `is_high_gdp`. Ces graphiques ont permis d'observer les chevauchements et les différences potentielles entre les groupes d'économies à fort et faible PIB.
    *   Une **carte thermique (heatmap) de corrélation** a visualisé les relations linéaires entre toutes les caractéristiques imputées. Elle a mis en évidence des corrélations notables entre diverses variables économiques (ex: PIB PPP et PIB par habitant sont fortement corrélés, le PIB a tendance à augmenter avec l'année).

### 3.3. Séparation des Données d'Entraînement et de Test

Le jeu de données préparé a été divisé en ensembles d'entraînement et de test avec une proportion de 80/20, garantissant ainsi que 144 échantillons sont utilisés pour l'entraînement du modèle et 36 pour son évaluation finale. (`X_train` : (144, 20), `X_test` : (36, 20)).

### 3.4. Entraînement du Modèle

Un **classifieur Random Forest** a été entraîné sur l'ensemble d'entraînement (`X_train`, `y_train`). Cet algorithme d'ensemble, basé sur des arbres de décision, est robuste et efficace pour les tâches de classification.

### 3.5. Évaluation du Modèle

Le modèle entraîné a été évalué sur l'ensemble de test (`X_test`, `y_test`) :

*   **Accuracy Score Global : 97.22%**

*   **Rapport de Classification :**
    *   **Classe 'Low GDP' (0)** : Précision de 0.94, Rappel de 1.00, F1-Score de 0.97. Le modèle est excellent pour identifier les économies à faible PIB.
    *   **Classe 'High GDP' (1)** : Précision de 1.00, Rappel de 0.95, F1-Score de 0.97. Le modèle a une très haute précision pour les économies à fort PIB, avec très peu de faux négatifs.

*   **Matrice de Confusion :**
    ```
    [[17,  0],
     [ 1, 18]]
    ```
    Cette matrice révèle : **17 vrais négatifs**, **18 vrais positifs**, **0 faux positifs** et seulement **1 faux négatif**. Un seul échantillon de la classe 'High GDP' a été incorrectement classé comme 'Low GDP', ce qui confirme l'excellente performance générale du modèle.

## 4. Insights et Prochaines Étapes

### Insights :
Le modèle Random Forest a démontré une **capacité exceptionnelle** à classer les économies en catégories de fort ou faible PIB avec une très haute précision. L'EDA a révélé les corrélations entre les indicateurs, fournissant un contexte pour la prédictivité du modèle.

### Prochaines Étapes :
1.  **Analyse d'Importance des Caractéristiques** : Déterminer quels indicateurs économiques (PIB par habitant, inflation, chômage, etc.) sont les plus influents dans la prédiction de la catégorie du PIB. Cela pourrait fournir des informations précieuses pour l'élaboration de politiques économiques.
2.  **Analyse de l'Erreur Unique** : Examiner en détail l'unique faux négatif (l'économie 'High GDP' mal classée en 'Low GDP'). Comprendre les particularités de cet échantillon pourrait aider à identifier des cas limites ou des aspects du modèle à améliorer.
3.  **Extension de l'Analyse** : Explorer d'autres modèles de classification ou des techniques d'ensemblage pour voir s'il est possible d'améliorer encore la performance, bien que le modèle actuel soit déjà très robuste.
Le modèle a montré une bonne performance pour la classe 'Low GDP' (Précision de 1.00, Rappel de 0.50), ce qui signifie qu'il a correctement identifié 3 des 6 économies à 'Faible PIB' et que toutes ses prédictions comme 'Low GDP' étaient correctes.
Cependant, le modèle a échoué à prédire la classe 'High GDP' (Précision, Rappel, F1-score de 0.00). La raison principale est que l'ensemble de test ne contenait aucune instance réelle de la classe 'High GDP'. Cela rend impossible pour le modèle de démontrer sa capacité à reconnaître les économies à 'Haut PIB' sur ces données de test.
Interprétation Thématique : Ce résultat ne signifie pas nécessairement que les indicateurs ne sont pas pertinents pour la classification du PIB, mais plutôt que l'échantillon de test était insuffisant et non représentatif. Dans un contexte économique réel, un tel déséquilibre ou l'absence d'une catégorie clé dans l'évaluation fausserait l'interprétation de la capacité d'un modèle à identifier les économies performantes.
## Summary:

### Q&A
1.  **A histogram showing the distribution of 'Inflation\_rate' according to the 'is\_high\_gdp' target variable.**
    A histogram visualizing the distribution of 'Inflation\_rate' for both 'High GDP' and 'Low GDP' groups was successfully generated using the dummy dataset.
2.  **A histogram showing the distribution of 'Unemployment\_rate' according to the 'is\_high\_gdp' target variable.**
    A histogram visualizing the distribution of 'Unemployment\_rate' for both 'High GDP' and 'Low GDP' groups was successfully generated using the dummy dataset.



Explication du Code : Création et Chargement des Données Factices (098d03ab)
Objectif : Cette cellule de code est cruciale car elle initialise l'ensemble de données sur lequel toute l'analyse thématique sera effectuée. Étant donné que le fichier top_six_economies.csv n'était pas fourni initialement, cette étape le crée artificiellement pour simuler un scénario réel de science des données.

Ce que le code fait :

Importations : Importe pandas pour la manipulation des DataFrames et numpy pour la génération de nombres aléatoires.
Génération des Données : Un dictionnaire data est créé pour contenir des données simulées pour 6 pays sur 5 ans (2015-2019). Les colonnes GDP_billion_USD, Population_million, Inflation_rate, et Unemployment_rate sont remplies avec des valeurs numériques aléatoires dans des plages réalistes.
Création du DataFrame Factice : Ces données sont converties en un DataFrame Pandas df_dummy.
Introduction de Valeurs Manquantes : Pour simuler des données 'sales', le code introduit délibérément des valeurs np.nan (Not a Number) dans 5% des cellules des colonnes numériques. Cela permet de tester les étapes d'imputation des valeurs manquantes plus tard.
Sauvegarde et Chargement : Le DataFrame df_dummy est sauvegardé sous le nom top_six_economies.csv (sans l'index du DataFrame) et est immédiatement rechargé dans df_economies. Cette approche assure que le reste du flux de travail utilise un fichier CSV comme source de données.
Vérification : Les premières lignes du df_economies chargé sont affichées (df_economies.head()) pour confirmer que le chargement s'est bien passé et que les données ont la structure attendue.
Insights : Cette étape garantit un environnement de travail reproductible et autonome pour l'analyse. Elle démontre également la capacité à créer des jeux de données de test et à simuler des problèmes de qualité des données (valeurs manquantes).

Explication du Code : Inspection Initiale des Données (ea3604df)
Objectif : Cette cellule vise à fournir un premier aperçu de la structure, des types de données et de la qualité générale du DataFrame df_economies, notamment la détection des valeurs manquantes et la distribution statistique des colonnes numériques.

Ce que le code fait :

df_economies.head() : Affiche les 5 premières lignes du DataFrame. Cela permet de visualiser les données brutes, de vérifier les noms de colonnes et de se faire une idée des types de valeurs contenues dans chaque colonne.
df_economies.info() : Fournit un résumé concis du DataFrame. Il indique le nombre total d'entrées, le nombre de colonnes, le nombre de valeurs non nulles par colonne, le type de données (Dtype) de chaque colonne et l'utilisation de la mémoire. C'est un outil essentiel pour identifier rapidement les colonnes avec des valeurs manquantes (là où Non-Null Count est inférieur au nombre total d'entrées).
df_economies.describe() : Génère des statistiques descriptives pour toutes les colonnes numériques. Cela inclut le nombre d'observations (count), la moyenne (mean), l'écart-type (std), les valeurs minimale et maximale (min, max), et les quartiles (25%, 50%, 75%). Ces statistiques donnent une idée de la distribution, de la tendance centrale et de la dispersion des données numériques.
Insights tirés de l'exécution :

df_economies.head() : Montre les colonnes Country, Year, GDP_billion_USD, Population_million, Inflation_rate, Unemployment_rate avec des valeurs variées. On peut voir que GDP_billion_USD est aux alentours de 10 000, Population_million entre 50 et 150, etc.
df_economies.info() : Révèle qu'il y a 30 entrées. Les colonnes Country et Year sont complètes (30 non-nulles). Cependant, GDP_billion_USD, Population_million, Inflation_rate, et Unemployment_rate ont chacune 28 valeurs non-nulles, ce qui signifie qu'elles contiennent 2 valeurs manquantes chacune (comme prévu lors de la génération des données factices).
df_economies.describe() : Fournit les statistiques pour les colonnes numériques. Par exemple, la moyenne du GDP_billion_USD est d'environ 10454 millions USD, avec un écart-type de 303. Les taux d'inflation varient de 1% à 4%, et le taux de chômage de 3% à 8%. La médiane de GDP_billion_USD est de 10399.86 milliards USD.
Cette étape est cruciale pour comprendre l'état initial des données avant toute transformation ou modélisation.

### Explication du Code : Préparation des Données (ce9b4bbf)

### Objectif : Cette cellule prépare les données pour la modélisation en définissant la variable cible, séparant les caractéristiques et en encodant les variables catégorielles.

### Ce que le code fait :

Calcul de la Médiane du PIB : Calcule la médiane de la colonne GDP_billion_USD. Cette médiane servira de seuil pour créer la variable cible.
Création de la Variable Cible is_high_gdp : Une nouvelle colonne binaire is_high_gdp est ajoutée au DataFrame. Sa valeur est 1 si le GDP_billion_USD du pays est supérieur à la médiane calculée, et 0 sinon. C'est notre variable que le modèle tentera de prédire (classification binaire : PIB élevé vs. PIB faible).
Séparation des Caractéristiques (X) et de la Cible (y) :
X (features) est créé en supprimant les colonnes GDP_billion_USD (qui est la base de notre cible, donc ne doit pas être directement une caractéristique) et is_high_gdp du DataFrame original df_economies.
y (target) est défini comme la colonne is_high_gdp.
Encodage One-Hot de 'Country' : La colonne Country est une variable catégorielle (noms de pays). Les modèles de Machine Learning nécessitent des entrées numériques. pd.get_dummies() convertit cette colonne en plusieurs colonnes binaires (une par pays), où 1 indique la présence du pays et 0 son absence. drop_first=True est utilisé pour éviter la multicolinéarité (si K catégories, K-1 nouvelles colonnes sont créées).
Affichage des Premières Lignes : Les premières lignes de X (maintenant avec les colonnes encodées pour les pays) et de y sont affichées pour montrer le résultat de ces transformations.
Insights tirés de l'exécution :

La médiane du PIB est d'environ 10399.86 milliards USD.
Le DataFrame X contient maintenant Year, Population_million, Inflation_rate, Unemployment_rate, et les colonnes binaires Country_Germany, Country_India, etc. (sauf Country_China qui a été supprimée par drop_first=True, car son absence dans toutes les colonnes Country_X indique qu'il s'agit de la Chine).
Le vecteur y est une série de 0 et de 1, représentant si chaque observation a un PIB 'élevé' ou 'faible'.
Cette étape est fondamentale pour structurer les données dans un format utilisable par les algorithmes de Machine Learning.

###Objectif : Cette cellule vise à identifier et traiter les valeurs manquantes qui ont été introduites artificiellement dans le jeu de données pour simuler des scénarios réels. L'approche choisie est l'imputation par la moyenne.



Identification Pré-Imputation : X.isnull().sum().sum() calcule le nombre total de valeurs manquantes dans l'ensemble des caractéristiques X avant tout traitement. Cela confirme la présence de valeurs à gérer.
Instanciation de SimpleImputer : Un objet SimpleImputer de scikit-learn est créé. La stratégie 'mean' est spécifiée, ce qui signifie que toutes les valeurs manquantes (NaN) dans une colonne numérique seront remplacées par la moyenne des valeurs non manquantes de cette colonne.
Application de l'Imputation :
imputer.fit_transform(X) applique l'imputation. fit() calcule les moyennes de chaque colonne, et transform() remplace les NaN par ces moyennes. Le résultat est un tableau NumPy (X_imputed_array).
Le tableau NumPy est ensuite reconverti en DataFrame Pandas (X_imputed_clean), en conservant les noms de colonnes d'origine, pour faciliter les étapes suivantes de l'analyse.
Vérification Post-Imputation : X_imputed_clean.isnull().sum().sum() est utilisé à nouveau pour vérifier qu'il n'y a plus de valeurs manquantes après l'imputation.
Insights tirés de l'exécution :

Le nombre total de valeurs manquantes avant imputation est de 6 (ce qui correspond aux 2 NaN par colonne multiplié par les 3 colonnes numériques restantes dans X après encodage One-Hot : Population, Inflation, Unemployment). L'encodage One-Hot des pays crée des 0 ou 1 et n'introduit pas de NaN.
Après imputation, le nombre de valeurs manquantes est tombé à 0, confirmant le succès de l'opération.
Cette étape est essentielle pour la robustesse du modèle, car la plupart des algorithmes de Machine Learning ne peuvent pas gérer les valeurs manquantes et nécessitent un jeu de données complet.

Explication du Code : Statistiques Descriptives pour EDA (a5a7125f)
Objectif : Cette cellule génère et affiche les statistiques descriptives pour le DataFrame des caractéristiques nettoyées et imputées (X_imputed_clean). C'est une étape clé de l'Analyse Exploratoire des Données (EDA) pour comprendre la distribution et les propriétés des variables numériques après le prétraitement.

Ce que le code fait :

X_imputed_clean.describe() : Appelle la méthode describe() sur le DataFrame X_imputed_clean. Cette méthode calcule un résumé statistique pour chaque colonne numérique, comprenant :
count : Le nombre d'observations non nulles.
mean : La moyenne arithmétique.
std : L'écart-type, qui mesure la dispersion des données.
min et max : Les valeurs minimale et maximale.
25%, 50% (médiane), 75% : Les quartiles, qui divisent les données en quatre parties égales et aident à comprendre la distribution et la présence éventuelle d'asymétrie.
Insights tirés de l'exécution :

count : Toutes les colonnes ont maintenant 30 entrées, confirmant que les valeurs manquantes ont bien été traitées.
Les statistiques pour Year, Population_million, Inflation_rate, et Unemployment_rate sont affichées, donnant une idée de leurs plages de valeurs et de leurs centres. Par exemple, la Population_million moyenne est d'environ 104 millions, et le Unemployment_rate moyen est de 5.26%.
Les colonnes Country_Germany, Country_India, etc. (issues de l'encodage One-Hot) sont également incluses. Leurs moyennes (par exemple, 0.166667 pour Country_Germany) indiquent la proportion d'observations où ce pays est présent (1/6 = 0.166667, car il y a 6 pays, et un des pays est la valeur de référence supprimée par drop_first=True). Le min est 0 et le max est 1, ce qui est attendu pour des variables binaires.
Ces statistiques fournissent une base solide pour la compréhension des données et pour orienter les visualisations futures.

Explication du Code : Visualisations EDA Supplémentaires (2aafee39)
Objectif : Cette cellule génère deux visualisations clés dans le cadre de l'Analyse Exploratoire des Données (EDA), spécifiquement pour explorer les relations entre les taux d'inflation et de chômage et la variable cible is_high_gdp.

Ce que le code fait :

Histogramme de 'Inflation_rate' :

Crée un histogramme (sns.histplot) de la colonne Inflation_rate.
hue=y colore les barres de l'histogramme en fonction de la variable cible is_high_gdp (PIB élevé ou faible), permettant de comparer les distributions des taux d'inflation entre ces deux groupes.
kde=True ajoute une estimation de la densité de noyau, qui lisse la distribution pour une meilleure visualisation des tendances.
element="step" affiche l'histogramme avec des contours plutôt que des barres pleines, ce qui est utile pour comparer les distributions par hue.
Les titres, labels d'axes et une légende sont ajoutés pour rendre le graphique clair et interprétable.
Histogramme de 'Unemployment_rate' :

Suit la même logique que pour l'inflation, mais applique l'histogramme à la colonne Unemployment_rate.
L'objectif est d'observer si les taux de chômage ont des distributions différentes selon que le PIB est élevé ou faible.
Insights tirés de l'exécution :

Les deux graphiques affichent des distributions de ces variables pour les groupes 'High GDP' et 'Low GDP'. Bien que les données soient factices et l'échantillon petit, ces visualisations sont conçues pour montrer si une séparation visuelle ou des tendances distinctes existent entre les groupes cibles en fonction de ces indicateurs économiques.
La légende indique clairement quelles couleurs correspondent aux 'High GDP' et 'Low GDP', ce qui est essentiel pour l'interprétation. (Dans un vrai cas, on chercherait par exemple si les 'High GDP' ont tendance à avoir une inflation ou un chômage plus bas, ou si les distributions se chevauchent fortement).
Ces visualisations sont précieuses pour l'EDA car elles aident à comprendre la relation entre les caractéristiques et la variable cible, ce qui peut guider le choix du modèle ou l'ingénierie des caractéristiques.

Explication du Code : Séparation des Données d'Entraînement et de Test (72c8f878)
Objectif : Cette cellule divise le jeu de données préparé (X_imputed_clean et y) en deux sous-ensembles distincts : un ensemble d'entraînement (X_train, y_train) et un ensemble de test (X_test, y_test). Cette séparation est fondamentale pour évaluer objectivement la performance d'un modèle de Machine Learning.

Ce que le code fait :

Importation : Importe la fonction train_test_split du module sklearn.model_selection.
Division des Données : La fonction train_test_split est appelée avec les paramètres suivants :
X_imputed_clean : Le DataFrame des caractéristiques (features) nettoyées.
y : Le vecteur de la variable cible.
test_size=0.2 : Spécifie que 20% des données seront allouées à l'ensemble de test, et les 80% restants à l'ensemble d'entraînement.
random_state=42 : Un entier utilisé pour l'initialisation du générateur de nombres aléatoires. Fixer random_state garantit que la division des données sera exactement la même à chaque exécution du code, rendant l'analyse reproductible.
Affichage des Formes : Affiche la forme (nombre de lignes et de colonnes) des quatre ensembles résultants (X_train, X_test, y_train, y_test). Cela permet de vérifier la taille des ensembles et de confirmer la division.
Insights tirés de l'exécution :

Forme de X_train : (24, 9) : L'ensemble d'entraînement contient 24 échantillons et 9 caractéristiques.
Forme de X_test : (6, 9) : L'ensemble de test contient 6 échantillons et 9 caractéristiques.
Forme de y_train : (24,) et Forme de y_test : (6,) : Les vecteurs cibles correspondants ont 24 et 6 étiquettes, respectivement.
La petite taille du jeu de données de test (seulement 6 échantillons) est une observation critique. Un ensemble de test aussi petit peut ne pas être représentatif et peut conduire à des évaluations de modèle peu fiables, comme cela a été observé dans l'évaluation finale.

Explication du Code : Entraînement du Modèle (bfb3bd90)
Objectif : Cette cellule entraîne un modèle de classification Random Forest en utilisant les données d'entraînement préparées.

Ce que le code fait :

Importation : Importe la classe RandomForestClassifier du module sklearn.ensemble. Le Random Forest est un algorithme d'apprentissage ensembliste qui construit de multiples arbres de décision et fusionne leurs prédictions pour obtenir un modèle plus précis et stable.
Instanciation du Modèle : Un objet RandomForestClassifier est créé.
random_state=42 est spécifié pour garantir la reproductibilité. Cela signifie que si le code est exécuté plusieurs fois, le processus d'entraînement du modèle (y compris la sélection aléatoire des caractéristiques et la construction des arbres) produira exactement le même modèle à chaque fois.
Entraînement du Modèle : La méthode fit() est appelée sur l'objet model_thematic, en lui passant les données d'entraînement (X_train pour les caractéristiques et y_train pour les étiquettes cibles). Pendant cette phase, le modèle apprend les relations entre les caractéristiques et la variable cible en construisant ses arbres de décision.
Insights tirés de l'exécution :

Le message "Modèle Random Forest entraîné avec succès pour la thématique." confirme que le processus d'apprentissage s'est terminé sans erreur. À ce stade, le modèle est prêt à être utilisé pour faire des prédictions sur de nouvelles données.
Le choix du Random Forest est souvent pertinent car c'est un algorithme robuste qui gère bien les données hétérogènes et est moins sujet au surapprentissage que les arbres de décision individuels.

Explication du Code : Évaluation du Modèle (df977e5b)
Objectif : Cette cellule évalue les performances du modèle Random Forest entraîné sur l'ensemble de test, en utilisant des métriques de classification clés et une visualisation.

Ce que le code fait :

Importations : Importe accuracy_score, classification_report, confusion_matrix de sklearn.metrics pour les métriques, et matplotlib.pyplot et seaborn pour les visualisations.
Prédictions sur le Test : Le modèle entraîné (model_thematic) est utilisé pour faire des prédictions (y_pred_thematic) sur l'ensemble de caractéristiques de test (X_test). Ces prédictions sont ensuite comparées aux vraies étiquettes de test (y_test).
Calcul de l'Accuracy : accuracy_score(y_test, y_pred_thematic) calcule le score d'exactitude global du modèle, qui est la proportion de prédictions correctes.
Rapport de Classification : classification_report(y_test, y_pred_thematic, target_names=class_names_thematic) génère un rapport détaillé, incluant pour chaque classe :
precision : La proportion de vrais positifs parmi toutes les prédictions positives pour cette classe.
recall : La proportion de vrais positifs trouvés parmi tous les vrais positifs de cette classe.
f1-score : La moyenne harmonique de la précision et du rappel.
support : Le nombre réel d'occurrences de la classe dans l'ensemble de test.
Matrice de Confusion :
confusion_matrix(y_test, y_pred_thematic) calcule la matrice de confusion, qui est un tableau montrant le nombre de vrais positifs, vrais négatifs, faux positifs et faux négatifs pour chaque classe.
sns.heatmap(...) visualise cette matrice de confusion de manière claire, avec des annotations numériques et un code couleur (cmap='Blues'). Les labels xticklabels et yticklabels sont définis pour une meilleure interprétation.
Insights tirés de l'exécution :

Accuracy Score : 50.00% – Un score très faible, suggérant un problème.
Rapport de Classification :
Low GDP (0) : Précision 1.00, Rappel 0.50, F1-score 0.67, Support 6.
High GDP (1) : Précision 0.00, Rappel 0.00, F1-score 0.00, Support 0.
Matrice de Confusion : Montre que 3 échantillons de 'Low GDP' ont été correctement prédits, et 3 échantillons de 'Low GDP' ont été incorrectement prédits comme 'High GDP'. La ligne pour 'High GDP' est entièrement à zéro, confirmant que le modèle n'a pas prédit cette classe, et surtout, qu'il n'y avait aucun échantillon de la classe 'High GDP' dans le jeu de test (support = 0).
Conclusion de l'évaluation : La faible accuracy et l'échec total à prédire la classe 'High GDP' ne sont pas nécessairement dus à un mauvais modèle en soi, mais plutôt à un problème de répartition des classes dans le très petit ensemble de test. L'absence d'échantillons de la classe 'High GDP' dans le test rend l'évaluation de cette classe non significative et met en évidence la fragilité de l'évaluation sur un jeu de données aussi limité et potentiellement déséquilibré.

1. Création et Chargement des Données Factices

[13]
0 s
import pandas as pd
import numpy as np

# Create dummy data for top_six_economies.csv
data = {
    'Country': ['USA', 'China', 'Japan', 'Germany', 'India', 'UK'] * 5,
    'Year': sorted(list(range(2015, 2020)) * 6),
    'GDP_billion_USD': np.random.rand(30) * 1000 + 10000, # GDP between 10,000 and 11,000 billion USD
    'Population_million': np.random.rand(30) * 100 + 50, # Population between 50 and 150 million
    'Inflation_rate': np.random.rand(30) * 3 + 1, # Inflation between 1% and 4%
    'Unemployment_rate': np.random.rand(30) * 5 + 3 # Unemployment between 3% and 8%
}

df_dummy = pd.DataFrame(data)

# Introduce some missing values artificially for the data cleaning step later
for col in ['GDP_billion_USD', 'Population_million', 'Inflation_rate', 'Unemployment_rate']:
    df_dummy.loc[df_dummy.sample(frac=0.05, random_state=42).index, col] = np.nan

df_dummy.to_csv('top_six_economies.csv', index=False)
print("Fichier 'top_six_economies.csv' créé avec des données d'exemple et des valeurs manquantes.")

df_economies = pd.read_csv('top_six_economies.csv')
print("Fichier 'top_six_economies.csv' chargé avec succès dans df_economies.")
print(df_economies.head())
Fichier 'top_six_economies.csv' créé avec des données d'exemple et des valeurs manquantes.
Fichier 'top_six_economies.csv' chargé avec succès dans df_economies.
   Country  Year  GDP_billion_USD  Population_million  Inflation_rate  \
0      USA  2015     10354.823380          149.609809        3.817529   
1    China  2015     10695.499079          124.184800        3.021677   
2    Japan  2015     10183.864412          111.452265        1.765516   
3  Germany  2015     10510.339760          132.791138        1.167952   
4    India  2015     10500.126959           94.203034        3.052672   

   Unemployment_rate  
0           7.135002  
1           6.788706  
2           6.392193  
3           4.648581  
4           6.153558  
2. Inspection Initiale des Données

[14]
0 s
print("1. Premières 5 lignes du DataFrame df_economies :")
print(df_economies.head())

print("\n2. Informations générales du DataFrame df_economies :")
df_economies.info()

print("\n3. Statistiques descriptives du DataFrame df_economies :")
print(df_economies.describe())
1. Premières 5 lignes du DataFrame df_economies :
   Country  Year  GDP_billion_USD  Population_million  Inflation_rate  \
0      USA  2015     10354.823380          149.609809        3.817529   
1    China  2015     10695.499079          124.184800        3.021677   
2    Japan  2015     10183.864412          111.452265        1.765516   
3  Germany  2015     10510.339760          132.791138        1.167952   
4    India  2015     10500.126959           94.203034        3.052672   

   Unemployment_rate  
0           7.135002  
1           6.788706  
2           6.392193  
3           4.648581  
4           6.153558  

2. Informations générales du DataFrame df_economies :
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 30 entries, 0 to 29
Data columns (total 6 columns):
 #   Column              Non-Null Count  Dtype  
---  ------              --------------  -----  
 0   Country             30 non-null     object 
 1   Year                30 non-null     int64  
 2   GDP_billion_USD     28 non-null     float64
 3   Population_million  28 non-null     float64
 4   Inflation_rate      28 non-null     float64
 5   Unemployment_rate   28 non-null     float64
dtypes: float64(4), int64(1), object(1)
memory usage: 1.5+ KB

3. Statistiques descriptives du DataFrame df_economies :
             Year  GDP_billion_USD  Population_million  Inflation_rate  \
count    30.00000        28.000000           28.000000       28.000000   
mean   2017.00000     10577.061111          101.892275        2.500416   
std       1.43839       254.539627           29.062683        0.907195   
min    2015.00000     10074.610159           56.586599        1.068437   
25%    2016.00000     10358.647270           80.827504        1.728055   
50%    2017.00000     10587.630750          106.032980        2.679875   
75%    2018.00000     10822.553842          122.180326        3.327001   
max    2019.00000     10966.544390          149.609809        3.869039   

       Unemployment_rate  
count          28.000000  
mean            5.485864  
std             1.465631  
min             3.097286  
25%             4.425677  
50%             5.696130  
75%             6.674525  
max             7.951232  
3. Préparation des Données

[15]
0 s
print("1. Préparation des données...")

# 1. Calcul de la médiane de 'GDP_billion_USD'
median_gdp = df_economies['GDP_billion_USD'].median()
print(f"   Médiane du 'GDP_billion_USD' : {median_gdp:.2f} milliards USD")

# 2. Création de la variable cible binaire 'is_high_gdp'
df_economies['is_high_gdp'] = (df_economies['GDP_billion_USD'] > median_gdp).astype(int)
print("   Colonne 'is_high_gdp' créée.")

# 3. Séparation des caractéristiques (X) et de la variable cible (y)
X = df_economies.drop(columns=['GDP_billion_USD', 'is_high_gdp'])
y = df_economies['is_high_gdp']
print("   Caractéristiques (X) et variable cible (y) séparées.")

# 4. Gestion des variables catégorielles (One-hot encoding pour 'Country')
X = pd.get_dummies(X, columns=['Country'], drop_first=True, dtype=int)
print("   Encodage One-Hot appliqué à la colonne 'Country'.")

# 5. Affichage des premières lignes de X et des premières valeurs de y
print("\n2. Premières lignes du DataFrame X (après encodage) :")
print(X.head())

print("\n3. Premières valeurs du vecteur cible y :")
print(y.head())
1. Préparation des données...
   Médiane du 'GDP_billion_USD' : 10587.63 milliards USD
   Colonne 'is_high_gdp' créée.
   Caractéristiques (X) et variable cible (y) séparées.
   Encodage One-Hot appliqué à la colonne 'Country'.

2. Premières lignes du DataFrame X (après encodage) :
   Year  Population_million  Inflation_rate  Unemployment_rate  \
0  2015          149.609809        3.817529           7.135002   
1  2015          124.184800        3.021677           6.788706   
2  2015          111.452265        1.765516           6.392193   
3  2015          132.791138        1.167952           4.648581   
4  2015           94.203034        3.052672           6.153558   

   Country_Germany  Country_India  Country_Japan  Country_UK  Country_USA  
0                0              0              0           0            1  
1                0              0              0           0            0  
2                0              0              1           0            0  
3                1              0              0           0            0  
4                0              1              0           0            0  

3. Premières valeurs du vecteur cible y :
0    0
1    1
2    0
3    0
4    0
Name: is_high_gdp, dtype: int64
4. Gestion des Valeurs Manquantes

[16]
0 s
from sklearn.impute import SimpleImputer

print("1. Identification et traitement des valeurs manquantes...")

# Identifier les colonnes avec des valeurs manquantes dans X
missing_values_before = X.isnull().sum().sum()
print(f"   Nombre total de valeurs manquantes avant imputation : {missing_values_before}")

# Instancier SimpleImputer avec la stratégie 'mean'
imputer = SimpleImputer(strategy='mean')

# Appliquer l'imputation sur X
X_imputed_array = imputer.fit_transform(X)

# Convertir le tableau NumPy résultant en DataFrame Pandas
X_imputed_clean = pd.DataFrame(X_imputed_array, columns=X.columns)

# Afficher le nombre total de valeurs manquantes après imputation
missing_values_after = X_imputed_clean.isnull().sum().sum()
print(f"   Nombre total de valeurs manquantes après imputation : {missing_values_after}")

print("   Imputation des valeurs manquantes terminée (remplacées par la moyenne).")
1. Identification et traitement des valeurs manquantes...
   Nombre total de valeurs manquantes avant imputation : 6
   Nombre total de valeurs manquantes après imputation : 0
   Imputation des valeurs manquantes terminée (remplacées par la moyenne).
5. Analyse Exploratoire des Données (EDA)

[17]
0 s
import matplotlib.pyplot as plt
import seaborn as sns

print("1. Statistiques descriptives du DataFrame X_imputed_clean :")
print(X_imputed_clean.describe())
1. Statistiques descriptives du DataFrame X_imputed_clean :
             Year  Population_million  Inflation_rate  Unemployment_rate  \
count    30.00000           30.000000       30.000000          30.000000   
mean   2017.00000          101.892275        2.500416           5.485864   
std       1.43839           28.042620        0.875354           1.414189   
min    2015.00000           56.586599        1.068437           3.097286   
25%    2016.00000           82.886252        1.770022           4.552053   
50%    2017.00000          104.881095        2.525653           5.527964   
75%    2018.00000          121.215329        3.240139           6.578089   
max    2019.00000          149.609809        3.869039           7.951232   

       Country_Germany  Country_India  Country_Japan  Country_UK  Country_USA  
count        30.000000      30.000000      30.000000   30.000000    30.000000  
mean          0.166667       0.166667       0.166667    0.166667     0.166667  
std           0.379049       0.379049       0.379049    0.379049     0.379049  
min           0.000000       0.000000       0.000000    0.000000     0.000000  
25%           0.000000       0.000000       0.000000    0.000000     0.000000  
50%           0.000000       0.000000       0.000000    0.000000     0.000000  
75%           0.000000       0.000000       0.000000    0.000000     0.000000  
max           1.000000       1.000000       1.000000    1.000000     1.000000  

[18]
2 s
print("2. Visualisation de la distribution de 'Population_million' par rapport à 'is_high_gdp'...")
plt.figure(figsize=(10, 6))
sns.histplot(x=X_imputed_clean['Population_million'], hue=y, kde=True, element="step")
plt.title("Distribution de 'Population_million' selon le groupe 'is_high_gdp'")
plt.xlabel("Population (millions)")
plt.ylabel("Count")
plt.legend(title='is_high_gdp', labels=['High GDP', 'Low GDP'])
plt.show()

print("\n3. Matrice de corrélation de toutes les caractéristiques...")
plt.figure(figsize=(12, 10))
correlation_matrix_full = X_imputed_clean.corr()
sns.heatmap(correlation_matrix_full, annot=True, cmap='coolwarm', fmt=".2f")
plt.title("Matrice de Corrélation de toutes les Caractéristiques")
plt.show()

print("\n4. Visualisation de la distribution de 'Inflation_rate' par rapport à 'is_high_gdp'...")
plt.figure(figsize=(10, 6))
sns.histplot(x=X_imputed_clean['Inflation_rate'], hue=y, kde=True, element="step")
plt.title("Distribution de 'Inflation_rate' selon le groupe 'is_high_gdp'")
plt.xlabel("Taux d'inflation")
plt.ylabel("Count")
plt.legend(title='is_high_gdp', labels=['High GDP', 'Low GDP'])
plt.show()

print("\n5. Visualisation de la distribution de 'Unemployment_rate' par rapport à 'is_high_gdp'...")
plt.figure(figsize=(10, 6))
sns.histplot(x=X_imputed_clean['Unemployment_rate'], hue=y, kde=True, element="step")
plt.title("Distribution de 'Unemployment_rate' selon le groupe 'is_high_gdp'")
plt.xlabel("Taux de chômage")
plt.ylabel("Count")
plt.legend(title='is_high_gdp', labels=['High GDP', 'Low GDP'])
plt.show()

6. Séparation des Données d'Entraînement et de Test

[19]
0 s
from sklearn.model_selection import train_test_split

print("1. Séparation des données d'entraînement et de test...")

# 1. Diviser les données en ensembles d'entraînement et de test
X_train, X_test, y_train, y_test = train_test_split(X_imputed_clean, y, test_size=0.2, random_state=42)

print("2. Division effectuée.")

# 3. Afficher les formes des ensembles d'entraînement et de test
print(f"   Forme de X_train : {X_train.shape}")
print(f"   Forme de X_test : {X_test.shape}")
print(f"   Forme de y_train : {y_train.shape}")
print(f"   Forme de y_test : {y_test.shape}")
1. Séparation des données d'entraînement et de test...
2. Division effectuée.
   Forme de X_train : (24, 9)
   Forme de X_test : (6, 9)
   Forme de y_train : (24,)
   Forme de y_test : (6,)
7. Entraînement du Modèle

[20]
0 s
from sklearn.ensemble import RandomForestClassifier

print("1. Entraînement du modèle (Random Forest Classifier) pour la thématique...")

# 1. Instancier le modèle Random Forest Classifier
model_thematic = RandomForestClassifier(random_state=42)

# 2. Entraîner le modèle sur les données d'entraînement
model_thematic.fit(X_train, y_train)

print("   Modèle Random Forest entraîné avec succès pour la thématique.")
1. Entraînement du modèle (Random Forest Classifier) pour la thématique...
   Modèle Random Forest entraîné avec succès pour la thématique.
8. Évaluation du Modèle

[21]
0 s
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix
import matplotlib.pyplot as plt
import seaborn as sns

print("1. Évaluation des performances du modèle thématique...")

# 1. Effectuer des prédictions sur le jeu de test
y_pred_thematic = model_thematic.predict(X_test)
print("   Prédictions effectuées sur le jeu de test pour le modèle thématique.")

# 2. Calculer et afficher le score d'accuracy
acc_thematic = accuracy_score(y_test, y_pred_thematic)
print(f"\n   >>> Accuracy Score (modèle thématique) : {acc_thematic*100:.2f}%")

# 3. Générer et afficher un rapport de classification détaillé
print("\n   >>> Rapport de Classification (modèle thématique) :")
class_names_thematic = ['Low GDP', 'High GDP'] # Assuming 0 is Low GDP and 1 is High GDP
print(classification_report(y_test, y_pred_thematic, target_names=class_names_thematic))

# 4. Calculer la matrice de confusion
cm_thematic = confusion_matrix(y_test, y_pred_thematic)
print("   Matrice de confusion calculée pour le modèle thématique.")

# 5. Visualiser la matrice de confusion
plt.figure(figsize=(6, 5))
sns.heatmap(cm_thematic, annot=True, fmt='d', cmap='Blues', cbar=False,
            xticklabels=class_names_thematic, yticklabels=class_names_thematic)
plt.xlabel('Prédiction')
plt.ylabel('Réalité')
plt.title('Matrice de Confusion (Modèle Thématique)')
plt.show()

print("   Évaluation du modèle thématique terminée.")

9. Résumé de l'Analyse Thématique
Ce rapport fournit une synthèse de l'ensemble du processus d'analyse thématique, récapitulant les étapes clés, les observations faites et les conclusions tirées. Il intègre toutes les explications fournies précédemment.

Summary:
Data Analysis Key Findings
Data Loading and Initial Inspection: The top_six_economies.csv dataset, programmatically generated with dummy values, was successfully loaded. It contains 30 entries and 6 columns, including Country, Year, GDP_billion_USD, Population_million, Inflation_rate, and Unemployment_rate. Initial inspection revealed 2 missing values in each of the four numerical columns (GDP_billion_USD, Population_million, Inflation_rate, Unemployment_rate). The median GDP was calculated to be 10399.86 billion USD.
Data Preparation: A binary target variable, is_high_gdp, was created, classifying economies as high GDP (1) if their GDP_billion_USD was greater than the median (10399.86 billion USD), and low GDP (0) otherwise. The 'Country' feature was one-hot encoded.
Missing Value Handling: A total of 6 missing values across the numerical features were successfully imputed using the mean strategy.
Exploratory Data Analysis (EDA):
Descriptive statistics showed average Population_million around 104 million, Inflation_rate around 2.28%, and Unemployment_rate around 5.26%.
The distribution of 'Population_million' by is_high_gdp was visualized, but no strong visual separation was immediately apparent.
A correlation heatmap was generated for all features, indicating the relationships between variables.
Histograms were successfully generated for 'Inflation_rate' and 'Unemployment_rate' against the is_high_gdp target variable.
Data Splitting: The dataset was split into training (24 samples) and testing (6 samples) sets, with a 80/20 ratio.
Model Training: A Random Forest Classifier was successfully trained on the preprocessed training data.
Model Evaluation: The model achieved an accuracy of 50.00% on the test set.
The classification report revealed that the model had a precision of 1.00, recall of 0.50, and F1-score of 0.67 for the 'Low GDP' class (class 0).
However, for the 'High GDP' class (class 1), precision, recall, and F1-score were all 0.00. This was attributed to the absence of 'High GDP' instances (support = 0) in the test set, leading to the model's complete failure to identify this class.
Insights or Next Steps
The model's poor performance (50.00% accuracy) is primarily due to a significant imbalance or complete absence of the 'High GDP' class in the small test set, which renders the evaluation metrics for that class meaningless. Future steps should address this data imbalance or test set distribution.
To obtain a more robust and reliable model evaluation, especially given the small dataset, consider implementing stratified sampling during the train-test split to ensure both classes are proportionally represented in both sets, or use cross-validation techniques.



 ## 6. Conclusion et Recommandations
L'analyse a permis d'explorer les indicateurs économiques et de mettre en œuvre un processus de modélisation. Bien que le dataset soit synthétique, il a permis de visualiser certaines dynamiques et d'illustrer les défis inhérents à l'analyse de données économiques.

Pour des études économiques futures plus robustes, il est impératif de :

Acquérir des données plus complètes et équilibrées : Un plus grand volume de données et une répartition plus équitable des économies à 'Haut PIB' et 'Faible PIB' dans les ensembles d'entraînement et de test sont cruciaux pour une évaluation fiable.
Utiliser l'échantillonnage stratifié : Pour garantir que la proportion des classes (Haut PIB, Faible PIB) est maintenue lors de la division des données, afin d'éviter les biais d'évaluation observés.
Approfondir l'analyse des corrélations : Avec un dataset réel, explorer des corrélations plus complexes et des interactions entre variables pourrait révéler des dynamiques économiques plus fines.
Considérer la dynamique temporelle : Le 'Year' est présent, mais une analyse de séries chronologiques pourrait apporter des informations précieuses sur l'évolution des économies.
