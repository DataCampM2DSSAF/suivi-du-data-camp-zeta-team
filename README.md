
# Read Me : Zeta Team 
## Equipe : 
- Ayoub Abraich
- El Mehdi Bouchouat
- Hoang Dung NGUYEN
- Mohamed Tounsi

## Github structrure
- Personal works : inclut toutes les versions de code de chaque membre dans un premier temps
- Code merged works : un dossier bien structuré qui comprend les versions finales de notre projet
- References : L'ensemble des références pour notre travail

## Sujet : 
Dans le monde électronique d'aujourd'hui, presque tout le monde fait une transaction dans un centre commercial ou lors de la réservation de billets de cinéma ou de billets d'avion, etc. Une transaction frauduleuse peut se produire dans l'un de ces endroits, ce qui pénalisera fortement le client ainsi que les entreprises. Améliorant ainsi l'efficacité des alertes de transactions frauduleuses pour des millions de personnes dans le monde et aidant des centaines de milliers d'entreprises à réduire leurs pertes de fraude et à augmenter leurs revenus.
## Source/Useful Links
L'IEEE-CIS fonctionne dans une variété de domaines de l'IA et de l'apprentissage automatique, y compris les réseaux de neurones profonds, les systèmes flous, le calcul évolutif et l'intelligence en essaim. Aujourd'hui, ils s'associent avec la plus grande société de services de paiement au monde, Vesta Corporation, à la recherche des meilleures solutions pour l'industrie de la prévention de la fraude.
Les données ont été collectées à partir des transactions de commerce électronique de Vista dans le monde réel et contiennent un large éventail de fonctionnalités, du type d'appareil aux fonctionnalités du produit.
Source : https://www.kaggle.com/c/ieee-fraud-detection
## Data Overview
- The data contains 2 csv file one for transaction and another for identity.
- Train file of identity contains 144233 rows and 41 features.
- Train file of transaction contains 590540 rows and 394 features.

### Categorical Features - Transaction
- ProductCD
- emaildomain
- card1 - card6
- addr1, addr2
- P_emaildomain
- R_emaildomain
- M1 - M9
### Categorical Features - Identity
- DeviceType
- DeviceInfo
- id_12 - id_38
### The TransactionDT feature is a timedelta from a given reference datetime (not an actual timestamp).
## Problématique
Les exigences commerciales sont les suivantes: 
+ Si une fraude survient lors de la transaction, l'entreprise doit immédiatement bloquer la carte. 
+ Le modèle devrait éviter de ne pas commettre une fraude de transaction qui est en réalité une transaction légitime. 
+ Le modèle devrait fournir l'estimation de la probabilité qu'une transaction soit frauduleuse.

En langage de ML, notre objectif et nos contraintes sont la mesure de performance utilisée dans cette étude de cas, c'est l'aire sous la courbe ROC. Parce que nous voulons améliorer la précision des deux classes, la courbe roc est donc une bonne option. 
Contraintes: 
- Le modèle doit fournir une sortie probabiliste (Le modèle doit indiquer quelle est la probabilité que la transaction appartienne à la classe de fraude)
- Exigences de faible latence (Étant donné que les problèmes commerciaux indiquent que si le système trouve une transaction inhabituelle, il doit immédiatement bloquer la carte)
- Minimiser les faux positifs et les faux négatifs (signifie minimiser à la fois la légitimité faussement prédite comme fraude et la fraude comme transaction légitime).

## Plan
- Data Cleaning,Data Analysis and Feature Engineering
- Building Model and hyperparameter tunning
- ? 
- ?

## Data Cleaning,Data Analysis and Feature Engineering
+ De nombreuses covariables ont une grande quantité de valeurs nulles spécifiquement pour les celles d'identité. Maintenant, pour la distribution des étiquettes de fraude, cela montre que 96,5% des données contiennent des transactions légitimes alors que seulement 3,5% sont des fraudes, ce qui signifie qu'il s'agit de données très déséquilibrées.
+ L'une des covariables importantes de cet ensemble de données est TransactionDT. Il s'agit d'une variable liée au temps et l'heure est en seconde 
+ Les données de test sont en avance sur le temps des données du train, nous ne ferons pas de répartition aléatoire sur les données, nous utiliserons la répartition temporelle.
+ Imprtances des variables avec LGB : 
![](https://image.noelshack.com/fichiers/2020/05/5/1580507871-importance.png)


## Code Colab
### Submissions :

- First : V features only with model=LGBM >>> Public SCORE = 0.844118
- 2nd : All features without : Drop=['TransactionID','ProductCD','card4','card6','P_emaildomain','R_emaildomain','DeviceInfo','DeviceType' and 'id_1 --> id_38']
with model=LGBM >>> Public SCORE = 0.893450
- 3rd : All features without Drop
with model=Light Gradient Boosting (LGB) >>> Public SCORE = 0.910894
![](https://image.noelshack.com/fichiers/2020/05/5/1580507610-sub.png)

### 24/01 - 31/01 :
- [Abraich V1](https://drive.google.com/file/d/1uMhY40rdWBZgDtl1fB02W3i_mjHnLPHE/view?usp=sharing)
- [Bouchouat V1](https://drive.google.com/file/d/1Tlj7by_njwV1bbtp3oOiDu2cQRqhX6Wq/view?usp=sharing)
- [Hoàng V1](https://)
- [Tounsi V1](https://)
### 31/01 - 07/02 :
- [Abraich V2](https://drive.google.com/file/d/1EnnFj_tLB6ma8uypxrK1D88gFgE6DqMk/view?usp=sharing)

### 14/02 : 

- Voir l'influence de la variable dist 2 (dont les données manquantes > 90%) sur isFraud.
- Groupby (P_email et R_email)
- Tester l'influence de (NA P_email) sur isFraud.
- 2nd approche --> remplacer les valeurs manquantes de card(2,3,5,6) par "mode".
- card 1 et 4 pair.
- Addr = Addr1 + Addr2 (voir package tick).
- Supprimer les variables (>80% de NA) et remplacer les variables qualitatives par Mode, et quantitatives par Med.

Pre-processing : 
- One hot code.
- supprimer outliers.
- Multi colinéarité.
## 28/02 :

- Mehdi & Mohammed : 
        ◦ Lasso pour sélection de variables + modèles simples 
        ◦ Regrouper les variables importantes
        ◦ One hot coding  :
- Ayoub :
        ◦ Analyse des variables importantes avec XGB , LGB ~~ variables cachées 
- Hoang :
        + Catboost : 
        + Variables cachées
+ Une référence qui montre la différence entre les tâches de Hoang et Ayoub : https://towardsdatascience.com/catboost-vs-light-gbm-vs-xgboost-5f93620723db

## 06/03 : 
### Abraich : 
+ LGBM & XGB score :
![](https://image.noelshack.com/fichiers/2020/10/6/1583545162-resultats.png)
+ Features importance : 
        ++ LGBM : 
        ![](https://image.noelshack.com/fichiers/2020/10/6/1583545353-lgb-im.png)
        ++ XGB : 
        ![](https://image.noelshack.com/fichiers/2020/10/6/1583545406-xgb-im.png)

## Lundi 16 Mars : 
- Rapport : https://www.overleaf.com/read/cjzknkcsmbbf  (you can view only this project)

## 16/03 :
L'objectif pour la semaine : 
- Finir tous les modélisations, le contenu pour le rapport
- Finir la rédaction de la première partie sur l'analyse des données.

Organisation :
- Hoang, Mehdi & Mohammed : Commencer directement sur le rapport
- Ayoub : Finir le contenu pour la modélisation simple : Ridge, LASSO, GLM, ... pour 2 jours. Intervenir sur le rapport dès le 19 mars.

Quelque submissions pour les modèles utilisés :
- elastic net + knn : 
![](https://image.noelshack.com/fichiers/2020/14/2/1585659492-knn-elnet.png)

- elastic net + random forest :
![](https://image.noelshack.com/fichiers/2020/14/2/1585659731-rf-elnet.png)

- lasso + random forest : 
![](https://image.noelshack.com/fichiers/2020/14/2/1585659796-rf-lasso.png)

## 17/03
A first plan for the report 

0.	Introduction
Purpose of the competition
Structure of the report and Summary of used techniques and their results
 
1.	Data description
Copy full description of the data with modification
Add some points if needed 

2.	Exploratory data analysis
Explain that we analyze variables in group by their meaning  and want to deduce some cross effect if possible
a.	Target variables: very short but needed
b.	Transaction DT and Delta variables: need to explore more because no 
c.	TransactionAmt and ProductCD: already included in the notebook
d.	Card variables: already included in the notebook but need to shorten 
e.	Address, distance and email domain variables: same as above
f.	C-counting variables: same as above
g.	M-matching variables: same as above 
h.	Ensemble of Vega variables: need to release 1 graphique on their PCA

3.	Data preparation 
Summary all the preparation based on the 2nd section
New engineering variables: those variables are based on personal view, experience or kaggle notebook reference with explaination
Quick talk about the possible modeling on this problem regrading of the data structure -> Deep learning may not a good choice. Tree model should work, also the classical model should be tested in order to see their performance, their weakness and strength in a real problematic. 
4.	Classical Machine Learning models
Present shortly the result -> conclude on the performance
Analyze the result -> Even the bad performance by comparing with the leaderboard, we may find some interesting points that could be useful for the preprocessing of the next advanced modeling
5.	Boosting tree-based models
Brief introduction of the theorical party. Linked the traditional GB with the 2  (or 3) advanced boosting model : LGBM, catboost (XGB)
a.	LGBM
The context depending on intervener
b.	catboost
		The context depending on intervener
6.	Final model (if enough time) combine all the modeling and the engineering above to build the best model
7.	Conclusion

### 18/03
L'objectif pour la fin de la semaine : 
+ Mohammed and Mehdi : finir la modélisation classique et la rédaction du point 3.4 - 3.8
+ Hoang et Ayoub : le reste jusqu'à la fin de la section 4 
+ Introduction pourrait être complétée après. 
