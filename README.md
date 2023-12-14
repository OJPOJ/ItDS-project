# Predictive Model LCSF1: Lung Cancer Survival Forecasting for 1 Year

## Description
Predictive Model LCSF1 is a groundbreaking project that focuses on predicting 1-year mortality in lung cancer patients using synthetic medical data. This initiative is a critical step towards enhancing healthcare by providing accurate and early patient prognosis.

## Team Members
Shao Ci Weng | Teele Kuri | Jan Petersen

## Provide the motivation and goal of the project
Our project uses a synthetic dataset that includes patient IDs, treatment IDs, and treatment times(Unit:Year). This data is critical for training and validating our predictive model.<br>
Our team believe that the relationship between data science and medical predictive models is pivotal in transforming healthcare. By harnessing the power of data, these models have the potential to enhance patient care, moreover can use predictive models to assess patient populations' health risks and implement preventive measures. This synergy between data science and healthcare has far-reaching implications for both patients and the medical community, driving innovation and better healthcare outcomes.
Our team's goal for this project:<br>
(1.)To develop a predictive model that can accurately forecast 1-year mortality in lung cancer patients based on treatment data.<br>
(2.)To achieve and surpass an AUC-ROC value of 0.75,  model's performance is evaluated using metrics like accuracy, precision, recall, and F1-score.<br>
(3.)Analyzing which features are most predictive of mortality can provide insights and validate the clinical relevance of the model.<br><br>
Business Analysis CRISP-DM: F2_report.pdf <br>

## Guide to the contents of the repository

In the beginning we focused on the analysis of the data: Visual_Exploratory.ipynb <br> Unfortunately most of the detailed analysis is not included anymore. <br>
We tried many difference methods, such like AdaBoost, XGBoost& Light BGM...etc.) Through discussion, we decided to work focus on Random forest and Cox Proportional Hazards Model with Logistic Regression(Teele's_models.ipynb)<br>
###1. (workflow.ipynb)
DEFINITION_ID' into two new columns, 'CATEGORY' and 'CATEGORY_ID,' and pivot this data to create a wider format where each 'CATEGORY' becomes a separate column, then concatenate these new category columns back to the original dataset.<br>
Handle the 'death' column, interpreting the values accordingly (converting to integer type)<br>
Next, split the unique subjects into training and testing sets, moreover handle the 'death' column, interpreting the values accordingly (converting to integer type) to reflect whether a patient has died.
In order to handling imbalanced classes, we used SMOTEENN, a combination of over-sampling and under-sampling techniques to address class imbalance.<br>
For feature selection, we also set up a Logistic Regression estimator and potentially other estimators (SVC, Naive Bayes) for Recursive Feature Elimination with Cross-Validation (RFECV) and SelectKBest
Finally, Model Training and Model Evaluation.(2_SHAO_edited.ipynb) also tried the similar way but with RandomForest Regression.<br>

###2.(_COX_Model_SHAOCI(FINAL VERSION_visual Chart) Group-F2):
A new column 'CATEGORY' is created by splitting 'DEFINITION_ID' and keeping only the prefix( condition,	drug,	measurement,	observation,	procedure), next, counts of each category by 'SUBJECT_ID' are calculated, which will use for further analysis and feature engineering.<br>
Survival Analysis(Create and drop Column)<br>
Time-to-Event Calculation: The maximum time for each subject is determined, representing the time to event or censoring.<br>
Event Encoding: A binary 'event' column is created where '1' represents an event occurrence (death) and '0' represents censoring.<br>
Dataframe Preparation: The 'death' column is dropped from the data, leaving the categories, time, and event status.<br>
Importing Cox Proportional Hazards Model, we used 'TIME' as the duration and 'event' as the event occurrence indicator, and gain the'Risk Scores'.<br>
The survival function is predicted at 1 year for all subjects( For Survival Probability Prediction we had asked GPT4)<br>
Finally importing logistic regression model is trained using risk scores and 1-year mortality probabilities as features, and 'event' as the target.(Model Performance can see from  accuracy, precision, recall, and F1-score, AUC-ROC)<br>

## Explain how it is possible to take the code and replicate the same analysis that the authors have done

The main steps are included in the workflow.ipynb.<br>
This file expects data in the original format of the synthetic_data_lung_cancer.csv<br>
There are multiple options for selection of models and preprocessing of the data. Depending on these the final model will be different. <br>

For the statistical analysis you can refer to _COX_Model_SHAOCI(FINAL VERSION_visual Chart) Group-F2.ipynb. 

