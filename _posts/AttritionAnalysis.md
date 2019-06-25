---
layout: post
title:  "Attrition Analysis"
date:   2019-03-20
excerpt: "A project to predict employee attrition and identify influential factors to reduce employee attrition."
project: true
tag:
- python 
- colabnotebook
- attrition
- machinelearning
comments: true
---

CLICK HERE:
[Colab Notebook Version](https://github.com/lmei33/trial/blob/master/Employee_Attrition_Analysis.ipynb)

CLICK HERE:
[Full PDF Version](https://github.com/lmei33/Miscellaneous/blob/master/Lan%20Mei%20-%20Final%20Project.pdf)


      
## Overview
Attrition, in Human Resource terminology, refers to the phenomenon of the employees leaving the company. Employee attrition is always the focus of Human Resource Management. This project aims to  predict employee attrition and identify influtial factors to reduce employee attrition. 

The original data is from:
[IBM HR Analytics Employee Attrition & Performance](https://www.kaggle.com/pavansubhasht/ibm-hr-analytics-attrition-dataset)
![0](https://mk0at44uvaxh7f73.kinstacdn.com/wp-content/uploads/2017/12/Topic-1.png)    

## Steps of Analysis  

### Data Ingest
After Inspecting the dataset, I found that there is no null values in the data, which means the data is clean. I also created a dataset with categorical values casted to numeric values.

### EDA 
The general overview of data and correlations between different factors: Attrited employees account for 16% of the data; Only factor “Overtime” showed a strong correlation with the target: “Attrition”.

* Attrition Factors Heatmap
![1](https://raw.githubusercontent.com/lmei33/lmei33.github.io/master/assets/img/2.png) 

#### Objective Factors
The objective factors such as age, years at company and gender show patterns as:
![2](https://raw.githubusercontent.com/lmei33/lmei33.github.io/master/assets/img/final/objective.PNG) 
Focusing on the red area (distribution of Attrition), we can find that 'younger' employees (Age/
YearsAtCompany) tend to attrite, which is not surprising. Also, those who have worked in more than 5
companies tend to attrite. Gender has nearly no influence on attrition.

#### Return and Bonus
Seen from the plot, we can identify that Income together with JobInvolvement strongly influence attrition. It is always those with similar job involvement but also with lower income tend to attrite.

![3](https://raw.githubusercontent.com/lmei33/lmei33.github.io/master/assets/img/final/return.PNG)    
Stock Option affects attrition, and a small level of option will help retain the employees.
![4](https://raw.githubusercontent.com/lmei33/lmei33.github.io/master/assets/img/final/return2.PNG)

#### Satisfaction
It is obvious that employee with lower satisfaction in Job/Environment/Relationship tend to attrite.
![5](https://raw.githubusercontent.com/lmei33/lmei33.github.io/master/assets/img/final/satisfaction.PNG)

#### Model
I split 22% of the data as test data, and find out that generally Logistic Regression showed the best accuracy with an accuracy score of 87.35. However, improvement is needed for the precision, because the model didn’t perform well in False Negative part (left bottom). The top 6 influential factors are as follows:
![6](https://raw.githubusercontent.com/lmei33/lmei33.github.io/master/assets/img/final/result.PNG)
See the original Python code here:

---

{% highlight yaml %}
from sklearn.model_selection import train_test_split

predictors = IBM_Attrition_Nu.drop(['Attrition'], axis=1)
target = IBM_Attrition_Nu["Attrition"]
x_train, x_val, y_train, y_val = train_test_split(predictors, target, test_size = 0.22, random_state = 0)

from sklearn.metrics import accuracy_score
from sklearn.linear_model import LogisticRegression

logreg = LogisticRegression()
logreg.fit(x_train, y_train)
y_pred = logreg.predict(x_val)
acc_logreg = round(accuracy_score(y_pred, y_val) * 100, 2)
print(acc_logreg)
87.35
{% endhighlight %}

---


## Conclusion
### Based on the influtial factors analysis
* Don't make them work overtime, they do care!
* Communicate the vision 
* Increase employee engagement, especially young employees
* Enhance recognition and rewards programs - Stock option can be a good choice 
* Create a pleasant workspace and increase satisfaction

### Since the model still need improvement in predicting attrition...
* Stay interview...
   e.g.
   “What kind of feedback or recognition would you like about your performance that you aren’t currently receiving?”

* Survey or interview with employees that decided to leave, identify the things employees care.
