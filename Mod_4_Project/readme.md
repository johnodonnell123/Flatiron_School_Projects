# Module 4 Final Project

## Introduction
In this project, an outline for a homepage is built for an online movies streaming service. For personalization, a recommender system is built with SVD for movies using data from the MovieLens dataset. The dataset contains are 100,000 user ratings for various films. A blog post reviewing diferent types of recommendation systems can be found [here](https://johnodonnell123.github.io/pages/page_blogpost_4.html). 

## Data:
The data comes in 3 different csvs:
1) user_tags.csv
     - userId
     - movieId
     - tag (a string a user assigned to a movie)
     - timestamp (when the user created the tag)
     
2) ratings.csv
     - userId
     - movieId
     - rating 
     - timestamp (when the rating occurred)

3) title_and_genre.csv
     - movieId
     - title
     - genres (string of multiple genres)

## Methodology:
1) Data Cleaning & Organization:
     - The first thing I wanted to do was clean and organize the data to make it more accessable. 
     - I started with some typecasting of timestamps, and extracting the year filmed from the movie titles (as they all included one). 
     - I cast the string of genres to a list, and ensured that all of the users tags for movies were lower case and unique to each film. 
     - Once all of this was complete, I reorganized the data into 3 primary dataframes centered around the User, Movie, and Ratings. 
2) Feature Engineering:
     - For users:
          - The number of tags and ratings created, along with the average and stdev of their ratings
     - For movies:
          - Number of ratings, average rating, ratings stdev
          - "Popularity Score"

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



 


