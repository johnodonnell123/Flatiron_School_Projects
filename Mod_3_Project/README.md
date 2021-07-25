# Module 3 Final Project

## Introduction
In this project, cell phone usage data for 3,333 customers is explored and is used to predict customer churn. The dataset comes from the Syria based cell phone service company SyriaTel, and is limited to their users in the United States. Unfortunately this is not time-series data, the dataset is indexed by the unique user id. A blog post reviewing the impact of churn on the subscription business can be found [here](https://johnodonnell123.github.io/pages/page_blogpost_3.html). The dataset contains the following features: 



## Data:
- user_id
- state
- account_length
- area_code
- phone_numver
- international_plan (boolean)
- voicemail_plan
- number_vmail_messages
- total_day_minutes
- total_day_calls
- total_day_charge
- total_eve_minutes
- total_eve_calls
- total_eve_charge
- total_night_minutes	
- total_night_calls
- total_night_charge	
- total_intl_minutes	
- total_intl_calls	
- total_intl_charge	
- customer_service_calls	
- churn (boolean)

## Methodology:
Fortunately this data set was very tidy and did not require any cleaning whatsoever, allowing the focus to remain on feature engineering, balancing, modelling, and interpretation. I began with some simple EDA looking at churn rate by state to see if there was a trend that existed. I then moved on to same very basic feature engineering. This dataset (as with all churn related datasets) was heavily unbalanced, therefore SMOTE was used to oversample the minority class. A random forest model was constructred and iteratively retrained with the least important feature being dropped until the least important feature explained at least some predefined level of varaince. This allows for not only a faster model but also a more interpretable prediction structure. After the final model was constructed, a confusion matrix was used to determine the efficacy of the model. Finally, the feature importances are viewed and a few simple statistical visualizations are created using the most important features to show how strongly they impact churn. 

## EDA Findings:

### There are strong differences in churn rate that lie at the state level.
- This could be due to differences in user demographics, or it might be the result of the *quality and or configuration of the service in that state*. 
- Further work is warranted here in data gathering

 <img src="images/churn_rate_by_state.PNG?raw=true" width="50%" height="50%">

## Model Findings:
 
### The random forest model was able to achieve > 95% accuracy:
- Due to the imbalance of churn/no churn in the original dataset, simply guessing that no customers would churn would yield an accuracy of ~ 84%. Random forest was able to beat this random guess by ~ 10%
- The top left hand corner represents the accuracy of the models prediction for users that **actually did not churn**, and it is very high
- The bottom right corner represents the accuracy of the models prediction for user that **actually did churn**. While it is still high, it has room for improvement

<img src="images/confusion_matrix.PNG?raw=true" width="35%" height="35%">

### The variables that explained the most variance in churn were total charge, number of customer service calls, and total day charge:
 
 <img src="images/feature_importances.PNG?raw=true" width="75%" height="75%">

### The feature that explained the most variance was the total amount the customer was charged:
- Here we see two histograms (one for churn, one for no churn) for an enngineered feature totalling the day/evening/night charges
- There appears to be a threshold at ~ $75 at which once crossed we see many more customers churn 

 <img src="images/total_charge_vs_churn.PNG?raw=true" width="75%" height="75%">
 
 ### The feature that explained the second most variance was the total number of customer service calls. 
 - This is intuitive, as more service calls likely means a poorer UX and therefore a high risk of churn
 - It is very rare to see a retained customer make more than 3 service calls, however many of the customers that have churned have made > 3 calls

 <img src="images/customer_service_calls_vs_churn.PNG?raw=true" width="75%" height="75%">
 
### Using both total charge and the number of customer service calls, we can limit our dataset to more clearly separate out these populations. 
- Here we are seeing distributions for total charge *for customers that placed at least 3 service calls*
- The combination of charging a frustrated customer too much creates a very high probability of customer churn
- Understanding this relationship allows the provider to take action on these customers that are at risk

<img src="images/total_charge_and_customer_service_calls_vs_churn.PNG?raw=true" width="75%" height="75%">



 


