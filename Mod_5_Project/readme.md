# Module 5 Final Project

## Introduction
In this project, news headlines from 2012 - 2018 are classified into different categories using Natural Language Processing.

## Data:
The dataset was sourced from Kaggle and has ~ 200k news headlines that are to be classified into 1 of 40 categories.
There dataset comes in the form af a JSON file and contains the following fields:

1) category:
     - 40 unique entries
     - Examples: POLITICS, TECHNOLOGY, PARENTING, WELLNESS

2) headline
3) author
4) short_description
5) link

## Methodology:

1) Data Cleaning & Organization:
     - The different text fields are explored and common formatting problems are corrected
     - All the fields are combined into a single 'text' field

2) EDA:
     - Several areas are explored including:
          - Category Prevalence (showing class imbalance)
          - Author Prevalence (showing which authors write the most articles)
          - Word Frequency (across all categories and within, before and after removing stop words)

3) Preprocessing:
     - Need to represent the text in a way that models can understand
          - Vectorizing (strings --> tokens --> vectors)
     - There are many ways to represent the text
          - Count Vectorizaiton (binary / counts)
          - Term Frequency / Inverse Document Frequency
          - Word Embeddings (custom vs pre-built models such as GLoVE)
     - Stop Words
     - Stemming & Lemmatization
     - n-grams

4) Modelling:
     - Many different models are built including Naive Bayes, Logistic Regression, Random Forest, and Neural Networks across these different pre-processing schemes.

## EDA Findings:

### Category Prevalence:
- There is a strong class imbalance, with Politics being the most prominent category
 <img src="images/article_categories.PNG?raw=true" width="70%" height="70%">

### Most common words in categories:
- After stopwords were removed, the most common words in each category are explored, and appear to make sense!
 <img src="images/common_words_in_category.PNG?raw=true" width="75%" height="75%">

### Custom embeddings appear strong:
- Custom word embeddings are created using the articles, and the results (while not perfect) appear to capture some of the semantic meanings
 <img src="images/custom_embeddings.PNG?raw=true" width="100%" height="100%">

## Model Results
- The two best models both used tri-grams without any stemming, lemmatization, or word embeddings. The best model was a neural network with an accuracy score of ~ 80%, and the second best was a Naive Bayes classifier with ~78% accuracy. The NN has stronger performance, but is not as directly interpretable as the NB classifier!

### Neural Network Results:
 <img src="images/trigrams_nn_results.PNG?raw=true" width="70%" height="70%">
 <img src="images/nn_cr.PNG?raw=true" width="30%" height="30%">

### Naive Bayes Results:
 <img src="images/nb_cr.PNG?raw=true" width="30%" height="30%">

## Forward:
- Modelling:
     - The gap between training and validation accuracy in the NN points towards overfitting, and some attempts at regularization can be made.
     - RNNs and LSTM can also be built to try to improve accuracy
- Reframing the problem:
     - Instead of treating these labels and categories, we could treat them as tags, assigning 2-3 to each article
     - This will likely increase the accuracy of the predictions, and also provide more value to the user audience



 


