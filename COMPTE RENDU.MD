## EL BAKRAOUI Hayat École Nationale de Commerce et de Gestion (ENCG) - 4ème Année
<img src="EL BAKRAOUI Hayat (1).jpg" style="height:164px;margin-right:132px"/>

## appogé d'etudiant:24010285
## Classe:CAC2
  ---
## Rapport Thématique : Analyse des Indicateurs Économiques des Six Premières Économies Mondiales
  ---
## 1. Contexte et Objectif
Ce rapport présente une analyse des indicateurs économiques clés pour un échantillon de six des plus grandes économies mondiales. L'objectif principal était de comprendre les relations entre des variables telles que le PIB, la population, l'inflation et le chômage, et de développer un modèle capable de classer une économie comme ayant un 'Haut PIB' ou un 'Faible PIB' en fonction de ces indicateurs. Le dataset utilisé est un ensemble de données factices, conçu pour simuler un scénario économique et mettre en lumière les dynamiques potentielles.

## 2. Aperçu des Données Économiques
Le dataset top_six_economies.csv simule des données annuelles pour les États-Unis, la Chine, le Japon, l'Allemagne, l'Inde et le Royaume-Uni sur une période de 5 ans (2015-2019). Il comprend les indicateurs suivants :

GDP_billion_USD (Produit Intérieur Brut)
Population_million (Population)
Inflation_rate (Taux d'inflation)
Unemployment_rate (Taux de chômage)
La variable cible is_high_gdp a été construite en classifiant les économies selon que leur PIB annuel dépassait la médiane de l'ensemble des observations (établie à 10399.86 milliards USD).

 ## 3. Statistiques Descriptives des Indicateurs Clés
Après traitement des valeurs manquantes par imputation (moyenne), les statistiques descriptives des données ont révélé :

Population : Une moyenne d'environ 104 millions d'habitants, avec une dispersion notable reflétant la diversité démographique des pays inclus.
Taux d'inflation : Une moyenne autour de 2.28%, suggérant une période de stabilité relative des prix ou une gestion monétaire uniforme dans ce dataset simulé.
Taux de chômage : Une moyenne d'environ 5.26%, indiquant des niveaux d'emploi variés parmi les économies.
 ## 4. Analyse des Relations entre Indicateurs (EDA)
L'Analyse Exploratoire des Données a cherché à identifier des tendances et des corrélations :

Population et PIB : Les visualisations ont montré que les économies classées 'High GDP' tendaient à avoir des populations légèrement plus élevées que celles classées 'Low GDP'. Bien que le chevauchement soit présent, il y a une indication que la taille de la population pourrait être un facteur contributif au niveau de richesse mesuré par le PIB.

Inflation, Chômage et PIB : Les distributions du taux d'inflation et du taux de chômage par rapport à la classification 'High GDP'/'Low GDP' n'ont pas révélé de séparations claires ou de tendances prononcées. Cela pourrait indiquer que, dans ce dataset spécifique, ces variables n'ont pas un impact discriminant direct et simple sur la distinction entre 'High GDP' et 'Low GDP' ou que d'autres facteurs interagissent.

Matrice de Corrélation : La matrice de corrélation a permis de visualiser les relations linéaires entre les variables. Par exemple :

Year a une faible corrélation avec la plupart des indicateurs, ce qui est attendu car l'année est une variable de temps et non un indicateur économique direct.
Population_million montre une légère corrélation positive avec certains indicateurs, mais pas de manière écrasante.
Les variables encodées par pays (Country_Germany, Country_India, etc.) sont, comme prévu, corrélées négativement entre elles, car l'activation d'une annule les autres. Elles montrent également diverses corrélations (positives ou négatives) avec les indicateurs économiques, suggérant que la situation économique varie d'un pays à l'autre.
 ## 5. Modélisation et Interprétation Économique des Performances
Un classifieur Random Forest a été entraîné pour prédire si une économie aurait un 'Haut PIB' ou un 'Faible PIB'. L'évaluation du modèle sur un petit ensemble de test (6 échantillons) a donné une accuracy de 50%.

L'analyse détaillée des métriques de classification et de la matrice de confusion a révélé une limitation critique :

Le modèle a montré une bonne performance pour la classe 'Low GDP' (Précision de 1.00, Rappel de 0.50), ce qui signifie qu'il a correctement identifié 3 des 6 économies à 'Faible PIB' et que toutes ses prédictions comme 'Low GDP' étaient correctes.
Cependant, le modèle a échoué à prédire la classe 'High GDP' (Précision, Rappel, F1-score de 0.00). La raison principale est que l'ensemble de test ne contenait aucune instance réelle de la classe 'High GDP'. Cela rend impossible pour le modèle de démontrer sa capacité à reconnaître les économies à 'Haut PIB' sur ces données de test.
Interprétation Thématique : Ce résultat ne signifie pas nécessairement que les indicateurs ne sont pas pertinents pour la classification du PIB, mais plutôt que l'échantillon de test était insuffisant et non représentatif. Dans un contexte économique réel, un tel déséquilibre ou l'absence d'une catégorie clé dans l'évaluation fausserait l'interprétation de la capacité d'un modèle à identifier les économies performantes.
## Summary:

### Q&A
1.  **A histogram showing the distribution of 'Inflation\_rate' according to the 'is\_high\_gdp' target variable.**
    A histogram visualizing the distribution of 'Inflation\_rate' for both 'High GDP' and 'Low GDP' groups was successfully generated using the dummy dataset.
2.  **A histogram showing the distribution of 'Unemployment\_rate' according to the 'is\_high\_gdp' target variable.**
    A histogram visualizing the distribution of 'Unemployment\_rate' for both 'High GDP' and 'Low GDP' groups was successfully generated using the dummy dataset.

### Data Analysis Key Findings
*   **Exploratory Data Analysis (EDA)**: Histograms were successfully generated for the dummy dataset, visualizing the distributions of 'Inflation\_rate' and 'Unemployment\_rate' against the `is_high_gdp` target variable.
*   **Data Split**: The dataset was divided into training (24 samples) and testing (6 samples) sets, with the test set representing 20% of the total data.
*   **Model Performance**: The Random Forest Classifier achieved an overall accuracy of 50.00% on the test set.
*   **Class Prediction Discrepancy**: The model demonstrated perfect precision (1.00) for the 'Low GDP' class but only a 0.50 recall. Critically, the model completely failed to predict any instances of the 'High GDP' class, resulting in 0.00 for precision, recall, and F1-score. This was due to the 'High GDP' class having 0 support in the test set, indicating its absence from the evaluation subset.

### Insights or Next Steps
*   The small size of the dataset (30 total samples) and the resulting very small test set (6 samples) likely led to an unrepresentative test split, specifically the complete absence of 'High GDP' samples. This renders the evaluation of the 'High GDP' class unreliable.
*   To obtain a more robust and reliable model evaluation, especially given the small dataset, consider implementing stratified sampling during the train-test split to ensure both classes are proportionally represented in both sets, or use cross-validation techniques.


 ## 6. Conclusion et Recommandations
L'analyse a permis d'explorer les indicateurs économiques et de mettre en œuvre un processus de modélisation. Bien que le dataset soit synthétique, il a permis de visualiser certaines dynamiques et d'illustrer les défis inhérents à l'analyse de données économiques.

Pour des études économiques futures plus robustes, il est impératif de :

Acquérir des données plus complètes et équilibrées : Un plus grand volume de données et une répartition plus équitable des économies à 'Haut PIB' et 'Faible PIB' dans les ensembles d'entraînement et de test sont cruciaux pour une évaluation fiable.
Utiliser l'échantillonnage stratifié : Pour garantir que la proportion des classes (Haut PIB, Faible PIB) est maintenue lors de la division des données, afin d'éviter les biais d'évaluation observés.
Approfondir l'analyse des corrélations : Avec un dataset réel, explorer des corrélations plus complexes et des interactions entre variables pourrait révéler des dynamiques économiques plus fines.
Considérer la dynamique temporelle : Le 'Year' est présent, mais une analyse de séries chronologiques pourrait apporter des informations précieuses sur l'évolution des économies.
