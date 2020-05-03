# Syriatel Customer Churn Analysis


This project is centered around a Telecommunications company called SyriaTel. SyriaTel is one of the two major telecommunications companies in Syria. One of the biggest issues that companies in the Telco industry face is to identify potentially unsatisfied clients before they decide to go to another provider. In advertising/marketing, users leaving a specific provide is also known as 'churning'. Customer churning leads to a huge loss of potential profits and thus it follows that a telco company seeking to improve their bottom line (i.e profits) will want to prevent this from happening as much as possible.

The aim of this project is to adopt machine learning techniques in order to make predictions on what customers are more likely to churn. Having this information would allow SyriaTel to create actionable plans around different type of customers.

# Table of Contents

1. [ File Descriptions ](#file_description)
2. [ Methods Used ](#methods_used)
3. [ Technologies Used ](#technologies_used)
4. [ Executive Summary ](#executive_summary)
    * [ Dataset Description ](#dataset_info)
    * [ Data Cleaning ](#data_cleaning)
    * [ Business Questions ](#business_questions)
    * [ Modelling ](#modelling)
    * [ Cost Evaluation and Insights ](#insights)
  


<a name="file_description"></a>
## File Descriptions
- .ipynb_checkpoints: different notebooks version going from preprocessing to modelling
- index_101.ipynb: notebook where the models were made, tuned and evaluated.
- data: contains dataset used for the analysis
- references: links to the source material referenced in the notebook
- images: jpg images taken from the jupyter notebook
- syritael_presentation: pdf format of a presentation with key insights for non-tecnhical stakeholders

<a name="methods_used"></a>
## Methods Used
- Data exploration, visualisation and cleaning
- Feature engineering
- Machine learning

<a name="technologies_used"></a>
## Technologies Used
- Python
- Pandas
- Numpy
- Scikit-learn
- Matplotlib

<a name="executive_summary"></a>
## Executive Summary
As previously mentioned, the main objective of this project is to help Syriatel identify in advance people who are about to unsubscribe from Syriatel services. On top of this, in the exploratory analysis stage will also try to answer some business questions that could be beneficial to Syriatel.


<a name="dataset_info"></a>
## Dataset information
Although we are performing this study on behalf of Syriatel, we are actually given a dataset comprised of US telco datapoints. These include information on 3333 users over a span of 256 days. Geolocation and zipcodes will have to be dropped when selecting predictors for the algorithms. The main reasonable assumption here is that all other data signals can be safeluy used to make inferences on the Syrian telco market. 

<a name="data_cleaning"></a>
## Data Cleaning

Luckily, there are no missing values in this dataset and no significant outliers to work on. The only initial remark would be on a clear class imbalance in our target variable since only 14.49% of the users have churned.


<p align="center">
  <img src="https://github.com/matteomm/syriatel_customerchurn_project/blob/master/images/class_imbalance.png" width=550>
</p>

We'll deal with class imbalance by constanly adjusting for the parameter 'class_weight' in our modelling. No SMOTE or undersampling have been applied in this instance.


<a name="methods_used"></a>
## Business Questions

**When are customers more likely to churn in terms of days after activation?**

We found out after grouping the relevant data that the highest percentage of churners is concentrated in 100-125 days since activation bracket. As a consequence, increased attention should be given to this group by checking in on the quality of the service provided.

<p align="center">
  <img src="https://github.com/matteomm/syriatel_customerchurn_project/blob/master/images/when.png" width=550>
</p>

**What are the highest and lowest states in terms of chrun rate?**


<p align="center">
  <img src="https://github.com/matteomm/syriatel_customerchurn_project/blob/master/images/state.png" width=750>
</p>

Although state data cannot be used as predictors, it would be still beneficial to identify the top/lowest states in terms of churn rate. A deeper analusys will be required in order to see if there are any underlying common traits across the worst and best performing states.

Highest Churn Rate: New Jersey 3.7%

Lowest Churn Rate: Arkansas 0.7%

<a name="modelling"></a>
## Modelling

Since we are dealing with a binary classification problem with heavy class imbalance, we have used roc_score as the main metric to assess good performance in the modelling stage. Upon selection of winning model, we have then evaluated in the final confusion matrix other metrics such as accuracy and f1. However, we'll explain in teh next section how, in this specific case, recall would be probably the most important metric after evaluating potential costs.

Due to the relatively small size of the dataset (3333), we have performed a single split into training and testing with validation done throughout the modelling with a stratified k-fold object with size 10.

Baseline model used was Naive Bayes, followed by a Decision Tree, Random Forest and lastly a logistic regression.
Hyperparameters tuning have been applied to all models with GridSearch CV.

Despite Random forest having the highest roc_auc_score out of all of them (0.90% roc_score) , we decided to opt for **Decision Tree** as the winning model due to much higher interpretabilty of the features while having only a slightly worse performance (0.88%). Attaching below a snapshot of the Decision Tree winning model:

<h5 align="center">Decision Tree</h5>
<p align="center">
  <img src="https://github.com/matteomm/syriatel_customerchurn_project/blob/master/images/decision_tree.png" width=750>
</p>

<a name="insights"></a>
## Cost Evaluation and Insights

After some research we have estimated the potential costs associated with the predicting power of our model. We have found out the 'False Negatives' predictions (that in our case would be associated with the model incorrectly labeling someone as a non-churner when they would) has the highest possible cost. **That's because finding a new prospect is on average 5X times more expensive than sucessfully retaining an exisiting one.** Our model will then be more sensitive to this specific class (more explanations on this in the notebook, see threshold selection). This is aso why 'Recall or TPR' is the most important metric in this instance.

After running our model on the test set, we have relatively good results with an overall accuracy of 87% and 83% Recall.
Our model is basically capable of successfully identifying a potential churner 8 times out of ten (due to recall).

A brief final estimation has been carried out, quantifying the benefit of implementing this model. By implementing this model, Syriatel could potentially save **$24,915** every 1000 customers by correctly identifying future churners and acting upon them to convince them to stay. 

Also, a feature importance graph based on the Decision Tree most important predictor has been put together, attached below:

<p align="center">
  <img src="https://github.com/matteomm/syriatel_customerchurn_project/blob/master/images/feature_importance.png" width=750>
</p>

The graph clearly showcases the features that have most impact on someone churning with customer service calls, international plan and total day charge having 3x more weight than any other feature in teh dataset.

In the final section, we have written some custom function to further investigate the magnitude and direction of these 3 features. 4 customer service calls seem to be the cut off point for churn percentage to go significantly up. Syriatel should flag this event as a potential signal for provider disservice and closely monitor anyone making more than number of calls within 256 days.
