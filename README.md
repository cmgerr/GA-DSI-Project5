# GA-DSI-Project5
Predicting survival on the Titanic

# Introduction
The goal of this exercise is to demostrate modeling capability for disaster management scenarios as a selling point for a hypothetical research consultancy to pitch to clients.

For this project, we have a dataset with attributes of 891 passengers on the Titanic, including whether or not they survived. Our goal is to build a classification model to predict survival based on passenger attributes. After removing observations with missing data, there are 712 passengers that I can use to build and test models. Of these, 61.6% died and 38.4% survived.

My hypothesis is that attributes such as gender, age, and class can be used to predict survival more accurately than guessing alone (if we were to guess 'died' as the outcome for all passengers, we would be correct 61.6% of the time). As a criteria for success, I will aim for 75% accuracy in predicting survival outcomes.

The modeling techniques used are Logistic Regression and K Nearest Neighbors. They are used in conjunction with GridSearchCV to find the optimal model parameters, and with SelectKBest to limit the model features.

# Risks and Assumptions
One assumption is that the 891 lines in our dataset are a representative sample of the 2208 total Titanic passengers. A risk is missing data: not all characteristics are available for all passengers in the dataset, so the method of imputing the missing data could lead to inaccurately identified relationships. For the purpose of this analysis, then, I will exclude the rows with missing values. This leaves 712 observations for modeling.

# Results
The three most valuable variables in predicting survival were determined to be Passenger Class, Gender, and whether the passenger boarded at Southampton. As we might expect, Passenger Class has an inverse relationship with survival (ie 1st class passengers were more likely to survive than 2nd or 3rd class passengers), and female passengers were much more likely to survive than male. Surprisingly, passengers who boarded at Southampton were more likely to survive than those who boarded at other ports.

I tested logistic regression models based on these 3 features as well as based on 7 total features, and found that the 3-feature model had only slightly lower accuracy. Therefore the 3-feature model is preferable for simplicity and to avoid overfitting. The best 3-feature logistic regression model has an accuracy score of 79%, above my 75% threshold. However, while this model has very high precision rate of 94%, meaning almost every passenger we predicted to survive in fact did, it has quite low recall at 51%, meaning many of the passengers we predicted would die in fact survived. If our clients are concerned with minimizing the number of people they do not assist in a disaster because of misclassifying them as not being at high risk, then this tradeoff may be acceptable. This would likely only be the case if resource constraints are not a problem. However, if clients are more concerned with ensuring that their resources are dedicated to recipients who truly are at higher risk, then a model with higher recall would be more appropriate.

With k Nearest Neighbors, I found that the optimized 7-feature model has much better recall (67%) than the 3-feature logistic regression model(51%) or the 3-feature kNN model (57%). This 3-feature kNN model accuracy is 81%, so it also meets my threshold requirement. This model would be more appropriate for clients who want to make sure resources are dedicated to truly high-risk individuals in disaster management.

Thus, we have two acceptable models (accuracy>75%) for predicting survival in the Titanic. 3-feature Logistic Regression model that will be appropriate for clients without resource constraints in helping at-risk individuals, and the 7-feature kNN model for clients whose resource constraints mean they want to minimize the misclassification of non-high-risk individuals as high-risk (and therefore minimize allocation of resources to individuals who do not need them).

