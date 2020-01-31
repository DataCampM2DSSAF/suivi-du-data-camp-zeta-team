
# Read Me : Zeta Team 
## Equipe : 
- Ayoub Abraich
- El Mehdi Bouchouat
- Hoang Dung NGUYEN
- Mohamed Tounsi 
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

## Code Colab
### Submissions :

- First : V features only with model=LGBM >>> Public SCORE = 0.844118
- 2nd : All features without : Drop=['TransactionID','ProductCD','card4','card6','P_emaildomain','R_emaildomain','DeviceInfo','DeviceType' and 'id_1 --> id_38']
with model=LGBM >>> Public SCORE = 0.893450
- 3rd : All features without Drop
with model=Light Gradient Boosting (LGB) >>> Public SCORE = 0.910894
![](blob:https://pasteboard.co/a3ccafaa-ab3e-47f1-9bfa-ab3ab16e2b4b)

### 24/01 - 31/01 :
- [Abraich V1](https://drive.google.com/file/d/1uMhY40rdWBZgDtl1fB02W3i_mjHnLPHE/view?usp=sharing)
- [Bouchouat V1](https://drive.google.com/file/d/1Tlj7by_njwV1bbtp3oOiDu2cQRqhX6Wq/view?usp=sharing)
- [Hoàng V1](https://)
- [Tounsi V1](https://)
### 31/01 - 07/02 :
- [Abraich V2](https://drive.google.com/file/d/1EnnFj_tLB6ma8uypxrK1D88gFgE6DqMk/view?usp=sharing)

