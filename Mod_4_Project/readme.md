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
          - "Popularity Score" = average rating * number of ratings
          - "Controversial Score" = ratings stdev * number of ratings

3) EDA:
     - More detail can be seen below, but the takeaways were:
          - Ratings distribution is negtaively skewed, with most ratings falling between 3 and 4
          - Older movies (< 1980) tend to have higher ratings 
          - The most common genres are Drama and Comedy
          - The highest rated genres are Film Noir, War, Documentary, Crime, Drama, and Mystery
          - Most users (in this dataset) create 20 - 170 ratings
          - Most movies have less than 10 ratings
          - Most user tags are unique to one movie, making them useless (unless similarity matched to other tags, not done here)
          - There are some movies that are trends much more strongly than others

4) Addressing Cold Start
     -  For new users: 
          - Take a generalized approach and recommend:
               - Best Movies This Year
               - Best Movies of All Time
               - Recently Added*
               - Love It or Hate It (based on controversial score)
               - Trending (based on trend in popularity)
               - Top rated movies from the top genres
     - For new movies:
          - Surface them on platform as "Recently Added"*
          - Order them by their similarity to the Best Movies of All Time
               - Similarity = Closest manhattan distance

5) Build a recommendation system with SVD:
     - Constructed an efficient and simple 1 factor low epoch model
     - When the users had sufficient ratings, the model was used to:
          - Change the order of movies shown to the user in the generalized approach
          - Create a "Recommended for You" section, listing the top movies the user should like according to the model (that they haven't seen yet)

6) Synthesize into a final function:
     - The final function create a dataframe that is a rough outline for a users homepage, and will be different for each user

## EDA Findings:

### Distrbution of Ratings:
- Many of our ratings are between 3 and 4, with 3.5 being the median
- There is a significant negative skew to the data
- Most of the ratings are whole numbers
 <img src="images/distribution_of_ratings.PNG?raw=true" width="50%" height="50%">

### Highest Rated Genres:
- The genres with the most favorable distributions are:
     -Film-Noir, War, Documentary, Crime, Drama, and Mystery
- 3 other genres have a notably strong negative skew with the bulk of ratings being 4s:
     - Animation, IMAX, and Western
- The rest of the genres look very similar
- Horror and movies without a genre have the widest range of outcomes
- <img src="images/genre_ratings.PNG?raw=true" width="50%" height="50%">

### Positively Trending:
- Many of our ratings are between 3 and 4, with 3.5 being the median
- There is a significant negative skew to the data
- Most of the ratings are whole numbers
 <img src="images/distribution_of_ratings.PNG?raw=true" width="50%" height="50%">

### Distrbution of Ratings:
- Ratings were mean normalized, scores above the mean are additive, scores below the mean drag it down
- Some movies are trending much stronger than others
 <img src="images/trending_movies.PNG?raw=true" width="50%" height="50%">


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



 


