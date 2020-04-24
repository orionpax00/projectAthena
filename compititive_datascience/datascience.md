## Compititive Data Science
Some important points about data science compititions.

### Structure of any competitions

data $\rightarrow$ model $\rightarrow$ submission $\rightarrow$ Evaluation $\rightarrow$ Leaderboard 

#### Some important Websites to practice
* Kaggle
* Driven Data
* CrowdAnalityx
* Codalab
* DataScienceChallenge.net
* Datascience.net

#### Real World vs Competitive pipeline ML Pipeline

* ~~Understanding of Business problem~~
* ~~Problem Formalization~~
* ~~Data Collecting~~
* Data Preprocessing
* Modelling
* ~~Way to evaluate model in real life~~
* ~~Way to deploy model~~

#### Types of model 
* Linear model
* Tree based model
    * Decision Tree
    * Random Forest
    * Gradient Boosted Decision Tree
* KNN
* Neural Network
***Refer :***  https://scikit-learn.com


### Data Preprocessing

#### Feature Preprocessing
* Depends on model choosen for prediction

#### Feature Generation
* Choose of very tricky
* Feature generation is a very powerful technique
* Depends on model choosen for prediction

#### Scaling (Pre processing)
* Feature scaling has very significant impact on prediction.
    * MinMaxScalar
        $$X=\frac{X-X_{min}}{X_{max}-X_{min}}$$
    * StandardScaler
        $$X=\frac{X - X_{mean}}{X_{std}}$$

#### Outliers Removal (Pre processing)
* Linear model are very much effected by outliers

#### Rank transformation (Pre processing)
* log transformation
* Sqrt tranformation

#### Data Type
* Rational
* Categorical (use encoding methods like onehot, etc)
* ordinal
* Ratio

#### Encoding
* label encoding
* frequency encoding

#### Handling Data and Time feature for feature genration
* Periodicity
* Time Since
* Difference between dates