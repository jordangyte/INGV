# INGV - Prédiction d'éruptions volcaniques

<img src="https://www.thoughtco.com/thmb/RvU_4FHKmqJe691ZsLZCQSpMqmU=/2260x1271/smart/filters:no_upscale()/GettyImages-608873707-f359835d93ea4f0b95a50cbeeb839c05.jpg" height="200" />

[Lien de la compétition](https://www.kaggle.com/c/predict-volcanic-eruptions-ingv-oe/data)
## Description

**Objectif** : Prédire une éruption volcanique à moyen/long terme.
Les scientifiques identifient souvent le temps avant une éruption en surveillant les secousses volcaniques à
partir des signaux sismiques. Dans certains volcans, ces secousses s'intensifient lorsque les volcans se
réveillent et se préparent à entrer en éruption. L'algorithme doit ainsi être en mesure d'identifier les
signatures des formes d'ondes sismiques qui caractérisent le développement d'une éruption pour prédire le
temps avant la prochaine éruption.

Dans ce contexte, les données proviennent de 10 capteurs placés autour d'un même volcan. Une instance
de donnée correspond à plusieurs séquence de données. Au sein de cette séquence de données de dix
minutes (6001 valeurs), on retrouve les valeurs détectées par 10 capteurs (sismomètres) placés autour du
volcan. À chaque instance de donnée est associée un temps avant éruption exprimé en centième de
secondes.

## Process
La démarche statistique adoptée :
1. **Preprocessing du dataset** : Imputation des valeurs manquantes par 0 lorsque qu'une série de mesure est manquante et par la moyenne lorsqu'il manque seulement quelques valeurs, features engineering à partir de statistiques usuelles (moyenne, max, min, quantiles etc..) et des versions modifiées du signal (FFT, filtre médian). Réduction de la dimension par la méthode **Lasso**.
2. **Modélisation** : **XGBOOST**, **Random Forest** et **Support Vector Regression**. XGBOOST affiche un meilleur résultat.
3. **Entraînement et optimisation des hyperparamètres** : Ajustement des hyperparamètres par **optimisation bayésienne** et validation croisée K-Fold.
4. **Résultat et score** : Le score de la compétition est l'**erreur absolue moyenne**. Mon score avec la modélisation par XGBOOST est de 6102018.

## Améliorations
Liste non exhaustive des expériences à envisager pour améliorer le score :
- Appliquer un **filtrage du bruit** et une **détection des anomalies**.
- Approfondir l'analyse et l'**imputation** des valeurs manquantes.
- Réduction de la dimension par **ACP**.
- Tester **LightGBM, CatBoost** (méthodes récentes et très utilisés lors de compétitions Kaggle).
- Tester les **modèles de mélange** (utiliser les prédictions de différents modèles et puis prédire à nouveau à l'aide d'un dernier modèle à partir des prévisions).
- Utiliser d'autres **modifications du signal** (MFCC/Cepstrum, STA/LTA...).

## Références
[XGBoost: A Scalable Tree Boosting System](https://arxiv.org/pdf/1603.02754), [Algorithms for Hyper-Parameter Optimization
](https://papers.nips.cc/paper/2011/file/86e8f7ab32cfd12577bc2619bc635690-Paper.pdf), [Random Decision Forests](https://web.archive.org/web/20160417030218/http://ect.bell-labs.com/who/tkh/publications/papers/odt.pdf), [Understanging Support Vector Regression](https://www.mathworks.com/help/stats/understanding-support-vector-machine-regression.html), [Basic Feature Engineering and Modeling](https://www.kaggle.com/altprof/basic-feature-engineering-and-modeling)
