# Module 1 Final Project

## Introduction
In this project, data for several thousand films is scraped from IMDB's website and used to generate a high level analysis. The goal is to provide some insight into the current trends of the industry.

A blog post about this project can be found [here](https://johnodonnell123.github.io/pages/page_blogpost_1.html)

## Data:
Scrapy Crawlers are used to retrieve data from IDMB's website. The Scrapy project folder can be found [here](fill_this_in). ~85,000 movies were scraped and the fields include:
- Title
- Release Date
- IMDB Star Rating
- Number of Ratings
- Genres
- Director
- Writer
- Stars
- Budget
- Cumulative Worldwide Gross
- Production Company

## Methodology:
Once the data was scraped and stored in a local .csv file, Pandas is used to import the data into a DataFrame structure for cleaning and analysis. 
- Dates are cleaned and cast to datetime objects
- Run Times are converted from hour and minute strings into minute integers
- Genres and stars are cast to lists for querying
- Budget and Gross values are cleaned and cast to integers

The data is then grouped by genre and writers to uncover trends within the data.

## Findings:

### Larger Budgets show a positive correlation with gross revenue:

 <img src="images/Budget vs Revenue Box Plot.PNG?raw=true" width="75%" height="75%">
 
### Twentieth Century Fox appears to do a better job of generating revenue for a given budget than Warner Brothers 
##### (showing ols best fit line)

<img src="images/Budget vs Revenue by Studio Scatter Plot.PNG?raw=true" width="75%" height="75%">

 
### Animation, Adventure, and Family are the genres with the most favorable distributions of Revenue:

 <img src="images/Revenue by Genre Box Plot.PNG?raw=true" width="75%" height="75%">
 
 ## Recommendations:
 1) For the desired gross revenue, choosing an appropriate budget is important. Our revenue target should be within the IQR of the revenues observed given our budget. 
 2) Have at least one of the following themes in the film: Animation, Adventure, Family
 3) If Animation is chosen, one of the top writers should be recruited: John Lasseter, Cinco Paul
 4) If Animation is chosen, one of the top voice actors should be recruited as film they appear in have been very successful: Tom Hanks, Mike Myers






