# Airbnb Price Analysis

**Analyst**: JF Roberts

## Overview
I have been contracted by a boutique real estate firm out of Manhattan Beach California to help them optimize the Airbnb branch of their business. With hundreds of properties across Los Angeles, this firm wants to ensure that they are maximizing return on each of their properties by setting an optimal per night price point. With detailed information numerous written reviews for each of their properties, they wish to uncover whether these written reviews along with other features can be used to set optimal price points.

## Business Understanding
To perform this analysis, I have chosen to use Natural Language Processing (NLP) to build a classification model to explore whether Airbnb written reviews are reliable predictors for the ‘price per night’ of a given Airbnb listing. Specifically, for one bedroom listings as they occupy the majority of Airbnb listings in the greater Los Angeles. Based on the results, this analysis will aim to communicate clear recommendations on how to utilize this model to optimize Airbnb price listing strategy.

## The Data
For this price analysis we pulled two data sets from [Inside Airbnb](http://insideairbnb.com/get-the-data/). "Inside Airbnb" is a website that sources Airbnb data quarterly for cities around the world. It includes data on _listings_, _reviews_, _neighborhoods_ and _calendar information_. The first data set includes detailed information such as **price, number of bedrooms, neighborhoods, property type and ratings** from over 44,000 Airbnb listings in greater Los Angeles. The second data set includes over 1.5 million **written reviews** corresponding to the listings in the first data set.  In the "Data Preparation" section below we will merge these two data sets and filter them down to the features of interest.

**How To Get The Data:** Apart from the cleaned and processed data (_processed_data.csv_), the data sets were too large to push to GitHub. Find the relevant download links below:

[Airbnb Listings & Reviews](http://insideairbnb.com/get-the-data)

## Data Preparation

**Listings Data Set:** To make our analysis as granular as possible, we decided to focus on listings with a specific number of bedrooms. As you can see from the graph below, 1-bedroom listings made up the majority of the data. As a result, we dropped all listings with more than 1 bedroom. To make our **target variable, price**, easier to work with we converted the price to feature to a price range based on the inter quartile range of price in this data set. As a result, our target variable was broken down into 4 classes of prcie points.

**Reviews Data:** Our first task with the written reviews was to group reviews by their respective listings reducing the data from 1.5 million reviews to 33,000. After cleaning our features of interest and joining the data sets we pre-process our text data to prepare it for modeling.

**Text Processing:**
1. Dropping symbols, numbers and non-English characters
2. Converting all characters to lowercase
3. Tokenizing our words
4. Part of Speech Tagging (POS tagging)
5. Lemmatizing using _WordNetLemmatizer_

## Evaluation Metric
It’s often the case, in a business problem, that we focus on either minimizing false negatives or false positives. In other words, we focus on precision or recall as our evaluation metric.

In this case, there’s no distinction between the two as both a false positive and a false negative reflect an inaccurate per-night price point prediction. Because of this, we chose accuracy as our evaluation metric. Accuracy in this case is how well our model predicts the actual per-night price point range of one bedroom listing.

## MODELING

## Modeling Overview
We used three different combinations of features for our modeling. Within each combination of features we then ran multiple different types of classfication models. Using GridSearchCV we itterated over each model to get the best possible combination of hyperparamters in order build the most accurate predictive model possible.

**1. Model Features: Reviews**

In this first group of models, the only feature used as a predictor are the tokenized written reviews for each listing.

Models Used:
- Logistic Regression (Baseline Model)
- Random Forest Classifier
- K-Nearest Neighbors
- Naive Bayes

**2. Model Features: Ratings, Reviews & Neighborhoods**

Models Used:

- Logistic Regression
- Random Forest Classifier

**3. Model Features: All Ratings, Reviews, Neighborhoods, Property Type & Bathrooms**

Models Used:

- Logistic Regression
- Random Forest Classifier

**FINAL MODELS:**

1. Logisitc Regression #3 - Tuned
- **Train Accuracy Score: 83%**
- **Validation Test Accuracy Score: 54%**

2. Random Forest Classifier #3 - Tuned
- **Train Accuracy Score: 100%**
- **Validation Test Accuracy Score: 52%**

## Feature Importances
Let's extract the top 10 feature importances from our best-performing Random Forest Classifier. Specifically, we are looking at the feature importance of our reviews - text data - therefore our features will be specific words. In our top 10, we find words like _nice_, _beautiful_, _great_, and _clean_ which all have positive connotations. This indicates that our model relies more heavily on these positive words when making predictions about price.

## Evaluation
- Typically, in a classification problem, a regression estimator such as Logistic Regression is less suited as it assumes a linear relationship. Its classifier counterparts such as Decision Trees and Random Forests on the other hand, are well suited for classification as they focus on feature selection - weighing important features more heavily. It is interesting then that our Logistic Regression had the highest accuracy score.
- That said, as we increased the number of features in our model to improve on our cross-validation test scores, our Logistic Regression training scores actually dropped from 99% down to 83% whereas our second-best model, Random Forest's, training score remained at 100%. This suggests that as we pull in more features and data, our Random Forest Classifier may outperform the Logistic Regression.
- Our best model has a low accuracy score of 55%. This means that our model accurately predicts the actual price of a listing 55% of the time based on the chosen features.
- Though our test scores were low, an important thing to note is that our training scores were as high as 100%. This means we could potentially get to a decent predictor by continuing to tune our model to increase our accruacy score.

## Conclusion
**Recommendations & Next Steps:**

**1. Unreliable Model** - At this point in time, this predictive model is not reliable enough to solve The Manhattan Beach Group's business problem of optimizing per night price point setting.

**2. Potential for a good predictor** - That said, as noted above, there is potential for a good model to be developed. The biggest barrier that we faced was extremely long model tuning times. Given more time we are confident we can improve our model enough to make it a good price predictor.

**3. Parallel Analysis** - Seeing at there are over 70 distinct features in Airbnb Listings data, we recommend funding a parralel analysis that focuses on these features rather than the written reviews for each listing.




