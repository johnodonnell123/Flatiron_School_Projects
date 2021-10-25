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
 <img src="images/distribution_of_ratings.PNG?raw=true" width="80%" height="80%">

### Highest Rated Genres:
- The genres with the most favorable distributions are:
     -Film-Noir, War, Documentary, Crime, Drama, and Mystery
- 3 other genres have a notably strong negative skew with the bulk of ratings being 4s:
     - Animation, IMAX, and Western
- The rest of the genres look very similar
- Horror and movies without a genre have the widest range of outcomes
<img src="images/genre_ratings.PNG?raw=true" width="80%" height="80%">

### Positively Trending:
- Many of our ratings are between 3 and 4, with 3.5 being the median
- There is a significant negative skew to the data
- Most of the ratings are whole numbers
 <img src="images/trending_movies.PNG?raw=true" width="80%" height="80%">

## SVD Model results
- Most of the models predictions are off by less than 2 points, with 50% of them being less then 0.5 points off. The median error is 0.07.
- The distribution looks to have a slight negative skew, meaning the model is slightly optimistic (tends to predict higher ratings for users)
 <img src="images/model_error.PNG?raw=true" width="70%" height="70%">

## Resulting Outline
- The resulting homepage outline look like the image below for users with >20 ratings
     - "Recommended For You" is based off of the SVD model
     - "Recently Added" is based off of the similarity (lowest manhattan distance) to the users most highly recommended movies
     - All other films are the top ***n*** rated films in their category, ordered by the users predicted preference for them
 <img src="images/homepage_outline.PNG?raw=true">




 


