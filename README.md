This repo is for Metis project 3 - McNulty

# Understanding financial inclusion in East Africa: Predicting bank account holding in Kenya, Rwanda, Tanzania and Uganda

## Background

Across Sub Saharan Africa, formal financial inclusion is low. 

This is important because bank accounts provide a convenient and secure place for storing money and making transactions.  Bank accounts also enable individuals to save for retirement and plan for recurring expenses such as education or rent. Finally, bank accounts serve as a gateway to other financial services - such as credit - which also enables individuals to invest in income-generating activities.

## Objective

Predict who is __unbanked__ in order to identify the most important features linked to financial inclusion. The focus on the unbanked population is important, given financial inclusion efforts aim to increase access to financial services for underserved and unserved populations. 

Understanding the nature of financial *exclusion* can enable development agencies to design targeting strategies and programs to reach the most underserved. It can also be used by banks and fintechs to design products that directly respond to opportunities and areas of need.

## Methods

* **Exploratory daata analysis** on FinMark Trust National Surveys data and the World Bank Global Findex Database
* **Predictive analysis** on FinMark Trust National Surveys data using logistic regression and Naive Bayes

### Features
* Age
* Gender
* Location (rural / urban)
* Cellphone access
* Household size
* Relationship to head of household
* Marital status
* Education level
* Type of job

### Target
* Bank account (yes / no)

## Tools Used
* Pandas
* Numpy
* Sklearn
* Matplotlib
* Seaborn
* Tableau

## Insights

![alt text] (https://github.com/tawney-kirkland/03-mcnulty/blob/main/02-ghimages/tableau_shot.png)

The results provide important insights on opportunities to advance financial inclusion

* For the unbanked, Informally employed single women have higher odds of being unbanked - development agencies should consider special programmes for this demographic, and participants can be targeted through engagement with departments of social development and women’s economic empowerment

* While individuals who have completed primary school have lower odds of being unbanked than those with no formal education, the majority of primary school level individuals are still unbanked and would benefit from financial inclusion outreach

* Individuals with a cell phone are more likely to be banked - banks and fintechs should consider extending financial products through mobile channels
