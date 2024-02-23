### Tasks and Deliverables for the Project

- EDA: 
    Reports describing univariate and bivariate analyses.

- Modeling: 
    The goal is to predict whether customers/handraisers purchase a Vehicle or Not.

### Data Source:

The data sources considered for use in this study are:

*	Demo graphic table (demos.csv)

*	Engagement data  (email_sends.csv) – used to communicate to Individuals 

    | Column_Name | Desc |
    | ------ | ------ |
    | Id | Customer id |
    | Timets | Number of days since email engagement. |
    | Opened | Whether the person opened the mail or not |
    | Clicked | Whether the person opened the mail and clicked the link or not|

* Disposition table (disposition.csv) 

    | Column_Name | Desc |
    | ------ | ------ |
    | Id | Customer id |
    | Timets | Number of days since hand raising. |
    | Y | Whether or not a person had purchased – “1” indicates purchased. ( Example: Customer id = 1 purchased 5 days after hand-raising, Customer id = 3 purchased 7 days after hand-raising, Customer id = 5 hand raised 17 days ago, but has not purchased ) |


### Approach:

**Data Preprocessing:**

- Merged the 'demos' and 'disposition' tables.
- Excluded the entire 'emails_sends' table due to insights from Exploratory Data Analysis (EDA).
  - Found high correlation between 'timets' (demo) and 'days since handraise.'
  - Observed a relatively low open rate (29%) and click rate (3.01%), with only half of those who opened the email survey making a vehicle purchase.
- Created a new column indicating people who received email engagement (1 for recipients and 0 for non-recipients).
  - Noted that 27% of customers who purchased vehicles were engaged through email.

**Feature Engineering:**

*Encoding:*

- Applied label/ordinal encoding for columns ['gender', 'education', 'income', 'age', 'years_in_workforce'] due to relationships between categories.
- Utilized one-hot encoding for other categorical variables.

*Feature Selection:*

- Removed the 'ID' column as it is irrelevant for modeling.
- Used Pearson's correlation to eliminate correlated columns.
- Established a dictionary with all columns as keys, initializing values to 0.
  - Updated values based on features selected by:
    1. SelectKBest module with Chi2, mutual_info_classif (k = 25 columns).
    2. ExtraTreesClassifier for determining important features.
- Selected features with values 2 or above from the dictionary for modeling.

**Model Selection:**

- Also performed Standard Scaling on the features
- Chose classification models suitable for the predominantly categorical data:
  1. Logistic Regression model.
  2. Decision Tree model.
  3. Random Forest Classifier model.1

**Model Training:**

- Split data into a 70-30 split using shuffling and a random state of 42.
- Employed grid search CV for hyperparameter tuning.
- Utilized StratifiedKFold for cross-validation.

**Model Evaluation:**

- Evaluated models based on accuracy.
  1. Logistic Regression:60%
  2. Decision Tree Accuracy: 62%.
  3. Random Forest Accuracy: 62%.

**Assumtion's Made**

- We have 2 types of population 
  1. A set of people who raise hand with out email engagement.
  2. A set of population who raise hand after email engagement.

- The conversion steps are 
  1. Email engagement.
  2. Hand rasie 
  3. Purcahse.
