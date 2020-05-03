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
    * [ Business Questions ]((#business_questions)
    * [ Modelling ](#modelling)
    * [ Insights ]((#insights)
  


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

Luckily, there are no missing values in this dataset and no significant outliers to work on. The only initial remark would be on a clear class imbalance in our target variable since only 14% of the users have churned.

<h5 align="center">Number of Fights in the UFC Each Year</h5>
<p align="center">
  <img src="https://github.com/ravimalde/ufc_fight_predictor/blob/master/images/number_of_fights.png" width=850>
</p>

We'll deal with class imbalance by constanly adjusting for the parameter 'class_weight' in our modelling. No SMOTE or undersampling have been applied in this instance.




