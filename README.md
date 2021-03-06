# Predicting the survival rate in Heart failure

<p align="center"><img width="450" alt="HF1" src="https://user-images.githubusercontent.com/64856136/100112228-fc418580-2e3c-11eb-9687-752e3e6de46a.png">


**GOAL** : Predict the Survival rate in Heart Failures

**INTRODUCTION:** Heart failures occurs when heart cannot pump enough blood and oxygen to support other organs in our body. The object of this project is to develop a model that predicts the survival rate of  heart failures based on variables like age, anaemia, creatinine_phosphokinase, diabetes, ejection_fraction, high_blood_pressure, serum_creatinine, serum_sodium, sex, smoking, time and Death_event.

The tools I  used are Python and the libraries- numpy, pandas, matplotlib, seaborn and sklearn.

## **Table of Contents- 4D Method**

&nbsp; &nbsp; **Define Problem**  <br />
&nbsp; &nbsp; &nbsp; -Why Predicting Survival rate in Heart Failures is important?  <br />

&nbsp; &nbsp; **Discover data**  <br />
&nbsp; &nbsp; &nbsp; -Load data  <br />
&nbsp; &nbsp; &nbsp; -Exploratory Data Analysis(EDA)  <br />
&nbsp; &nbsp; &nbsp; -Data Visualization  <br />
  
&nbsp; &nbsp; **Develop solutions**  <br />
&nbsp; &nbsp; &nbsp; -Establish a baseline  <br />
&nbsp; &nbsp; &nbsp; -Machine Learning Models  <br />
&nbsp; &nbsp; &nbsp; &nbsp;  **-Logistic Regression**  <br />
&nbsp; &nbsp; &nbsp; &nbsp;  **-Random Forest**  <br />
&nbsp; &nbsp; &nbsp;-Selecting the Best model  <br />
  
&nbsp; &nbsp; **Deploy model**  <br />
&nbsp; &nbsp; &nbsp; -Deploy solution  <br />
&nbsp; &nbsp; &nbsp; -Feature importance  <br />

&nbsp; &nbsp; **Conclusion**  <br />
## **PART 1: DEFINING THE PROBLEM** <br />

One person dies every 36 seconds from cardiovascular disease in the United States. About 655,000 Americans die from Heart disease each year- that is  1 in every 4 deaths as per the recent statistics(September 2020). Further Heart Disease costs US about $219 billion each year as estimated from 2014 to 2015, which includes cost of health care services, medicines and loss of productivity due to death , according to the Center of Disease Control and Prevention (CDC). <br />

The medical conditions that have impact on heart failures are - Diabetes, High Blood Pressure, obesity and other conditions related to heart. Machine Learning, in particular, can predict the patient's survival using the data such as-  electronic medical records of patients quantify symptoms, body features, and clinical laboratory test results. It can also individuate the most important features among those included in their medical records. <br />

**PREVENTION :** With the advancement of science and technology, if Heart failure's are diagnosied early,  it can be treated and can increase the survival rate. <br />
“The very essence of cardiovascular practice is the early detection of heart failure” - Sir Thomas Lewis, 1933 <br />

This dataset contains 299 observations and 13 variables. Death_event is the dependent variable 


<img width="607" alt="Screen Shot 2020-11-24 at 11 20 34 AM" src="https://user-images.githubusercontent.com/64856136/100122206-1aac7e80-2e47-11eb-978e-7a76ddfc1ad5.png">


## **PART 2: DISCOVER DATA** <br />

There was no cleaning necessary for this dataset. The only change was to change the data type of age from float to int. <br />

The rate at which death occured is 32% in the entire dataset. <br />

**Identifying the relationship between age, ejection_fraction and time with target variable** <br />


<img width="967" alt="Screen Shot 2020-11-24 at 11 16 23 AM" src="https://user-images.githubusercontent.com/64856136/100120960-8fcb8400-2e46-11eb-98d0-c01c1b92948d.png">



**Findings**

Analyzing the above plots reveal that:

**1. Age & Death :** patients aged above 80 have more chances of mortality. <br />
**2. Ejection_fraction & Death :** patients with low ejection fraction, that is less than 30 have more chances mortality and above 30 have higher chance of surviving. <br />
**3. Time & Death:** Patients with less follow-up period resulted in more deaths. <br />


**Cluster analysis: Time vs Age with respect to mortality**


<img width="743" alt="Cluster" src="https://user-images.githubusercontent.com/64856136/100118935-54c85100-2e44-11eb-9a82-5332cdb2f8d4.png">


There are 2 distinct clusters namely:

**Cluster 1- Mortality:** Follow-up period below 50 and any age : These have high chances of mortality.  <br />
**Cluster 2: Survival:** Patients with age less than 80 and follow-up period more than 50 - have higher changes of survival.  <br />


**Identifying the relationship between sex, diabetes, anaemia, High BP and smoking  with target variables**



<img width="767" alt="age,sex,diabetes" src="https://user-images.githubusercontent.com/64856136/100118983-63166d00-2e44-11eb-8491-2578ee26ae65.png">


<img width="767" alt="Smoking , Hbp" src="https://user-images.githubusercontent.com/64856136/100119031-6f9ac580-2e44-11eb-932b-11aff2f70f04.png">


Analysis of Categorical variables:
    
**Sex Category:** Female has higher chance of surviving than males. <br>
**Anaemia:** Patients with and without anaemia both have same chances of surviving. <br>
**Diabetes:** There is not much difference between the patients with and without Diabetes but patients without diabetes have higher chance of Mortality. <br>
**High_blood_pressure:** There are no siginificant differences between the two. <br>
**Smoking:** Patients who do smoke have higher chance of survival. 


**Correlation matrix**

<img width="1000" alt="Correlation" src="https://user-images.githubusercontent.com/64856136/100119071-77f30080-2e44-11eb-907e-7a85196818c3.png">

## **PART 3: DEVELOP SOLUTIONS** <br />


**For base line** Randomly assigned (0,1) in 70-30% using Numpy and calulated the accuracy score. 


<img width="474" alt="Screen Shot 2020-11-24 at 11 41 55 AM" src="https://user-images.githubusercontent.com/64856136/100124806-1c2b7600-2e4a-11eb-8171-bc1371e313b2.png">

**Feature Engineering :** Scaled the numeric variables using MinMaxScalar. 

**Train test split :** Split data into Training and testing in 70-30 %.

**Evaluation Metric :** Accuracy score

The confusion matrix displays the correctly predicted as well as incorrectly predicted values. 

**True negative** is an outcome where the model correctly predicts the negative class :  Patients who are correctly predicted as Survived <br> 
**True Positives** is an outcome where the model correctly predicts the positive class : patients who are correctly classified as dead <br>
**False positive** is an outcome where the model incorrectly predicts the positive class :patients who are predicted to be dead when they actually survived <br>
**False negative** is an outcome where the model incorrectly predicts the negative class : patients who are predicted to be survived when they are actually dead<br>
 
 
From the above analysis, decreasing the False positive rate is important as incorrectly perdicting a person to be dead when they are still alive, would deprive the patients from getting necessary treatment. Hence our **goal** is to reduce the False Positives. 

Hence, I chose Accuracy to be the Evaluation Metric.


**Model 1: Logistic Regression :** Found the best parameters using GridSearchCV and got an accuracy score of 86% with 5 false positives.

**Model 2: Random Forest :** Found the best parameters using GridSearchCV and got an accuracy score of 87% with 4 false positives.

<img width="528" alt="RF" src="https://user-images.githubusercontent.com/64856136/100119138-8a6d3a00-2e44-11eb-9db4-ef1974eb6976.png">

## **PART 4: DEPLOY MODEL** <br />

**Selecting the Best model:** As random forest gave the best accuracy score with less false positives and it has the best area under the curve that is 0.82 (ROC) , hence it will be selected as the best model.


**Feature Importance:**
This gives us an insights into which variables are important. For example, Time, Serum_creatininie, age, ejection_fraction  are considered as the most important variables. 

<img width="1027" alt="Feature Imp" src="https://user-images.githubusercontent.com/64856136/100119169-92c57500-2e44-11eb-8224-2a9f7890ae50.png">

**Conclusion :**

Random Forest model reduced the False positives by 85% over the baseline model. The evaluation metric considered was Accuracy. The Accuracy for Random forest model for test data set is 87%.  <br />

Notebook Url: https://github.com/manasa2093/PredictingHeartfailureSurvival/blob/main/HeartFailurePrediction.ipynb

