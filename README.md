# Online News Popularity Prediction
## Problem statement
The marketing team of Mashable is responsible identifying popular articles and accordingly sell ads on these articles to incur large profits. Currently the team uses heuristics to predict articles popularity and has flat rate for ads irrespective of the popularity. The team lacks a framework to identify article popularity based on historical data of articles published on the website.
## Goal 
Determining the popularity of articles prior to its publication by training machine learning models on various features and implement new pricing strategy with help of cost based analysis (cost matrix) and help mashable's marketing to maximize their profit.

## Dataset
Instances – 39,000

Features – 61

Target variables (No. of shares) - Determine the popularity of articles based on the shares

Source – UCI Data Repository

Link -  https://archive.ics.uci.edu/ml/datasets/online+news+popularity

## Exploratory Data Analysis (Univariate, Bivariate, Multivariate)

1. Understand the target variable (shares)
Shares – Determine the popularity of articles based on the shares
Number of shares – Continuous

2. Converted this problem to a classification problem based on the percentile (median) of the target variable which was 1400 but we chose 1500 to eliminate the problem of class
imbalance and therefore imposes less challenges when building ML models.

     • Shares > 1500 – Popular (1)
   
     • Shares < 1500 - Unpopular (0)

    Reason for choosing 1500

    • Closer to median (50th percentile)

    • The problem of class imbalance would be resolved 

3. Performed correlation analysis using heatmap, scatter plot, bar chart to understand variable relationship and identify highly correlated features.

<img width="323" alt="image" src="https://user-images.githubusercontent.com/99356847/204112760-aab66b30-d937-4aa9-b7d0-d971c4e627fa.png"> <img width="323" alt="image" src="https://user-images.githubusercontent.com/99356847/204112732-31fb7bbd-928e-4d53-a12c-aa54ce7357dc.png">
 
## Insights Obtained after EDA
• Articles with titles that include a fair number of words are more likely to be shared and short titles articles aren’t appreciated by people.

• It was observed that articles with more number of videos were shared fewer times, probably because people don’t have the option to skim read the articles.

• It is observed that if rate of negative words in the content increases the count of shares decreases.

• The number of shares for articles posted on weekends is less than those posted on weekdays, pet the proportion of popular articles is higher on weekends.

<img width="600" alt="image" src="https://user-images.githubusercontent.com/99356847/204113105-cc41b48c-37c5-453a-ae56-7e75654bf332.png">  <img width="600" alt="image" src="https://user-images.githubusercontent.com/99356847/204113143-64279e88-a1f6-4473-b26a-2d678ac129dd.png">

## Preprocessing
• Removed dump articles – articles with no words as they won’t be helpful for model building

• Removing non-predictive features like URL of article and time delta 

• Removed highly correlated attributed with help of correlation matrix: n_non_stop_unique_tokens, n_non_stop_words, kw_avg_min, self_reference_avg_shares_new, avg_negative_polarity_new, avg_positive_polarity_new

• Removed weekday_is_saturday and weekday_is_Saturday with help of cross plots chi-square values 

<img width="650" alt="image" src="https://user-images.githubusercontent.com/99356847/204113293-c9f618f5-6b01-4de0-a908-d6a4dbb12539.png">
<img width="600" alt="image" src="https://user-images.githubusercontent.com/99356847/204113473-31c776c3-539f-4dc7-a63b-47b23ebecded.png">

## Dealing with Skewness and Outliers

• Most of the features are right skewed – In order to deal with this, we performed power transformation techniques imported from pre-processing package 

• Box Cox Transformation: This transformation can be performed when we have values greater than 0 in our dataset. As we had many negative values in our dataset we first converted these negative values into positive and then proceeded with the box cox transformation.

• Most of the features in our dataset contained outliers and after performing box cox transformation we partially took care of the outlier and further performed capping 

Lower bound = less than 1st percentile (outliers below lower bound)
Upper bound = above 99th percentile (outliers above upper bound)

<img width="500" alt="image" src="https://user-images.githubusercontent.com/99356847/204113650-e9acd841-20ba-489a-bd75-6ae8f5d6df3e.png"> <img width="500" alt="image" src="https://user-images.githubusercontent.com/99356847/204113678-3bd47b61-c2bb-41f3-8043-012b9d66b8d2.png">


## Machine Learning Model and Evaluation

Naïve Bayes

Logistic Regression

KNN

Random Forest

Performance metrics 
AUC & ROC Curve, F1 Score and Accuracy to evaluate these models 

It was observed that random forest model gave the highest accuracy, AUC score so we performed hyperparameter tunning on it and observed that its performance increase significantly

<img width="568" alt="image" src="https://user-images.githubusercontent.com/99356847/204113789-ac396048-b569-4537-819a-67edf5483c50.png">

## Cost-based Analysis using cost matrix

Based on the problem statement and our research on the advertisement selling we created a cost matrix where we added the profits and loss of the following cases :

• Identifying popular articles correctly will help in increasing the cost at which Advertisements are sold (True Positive)

• While identifying unpopular articles will decrease the ad cost, it will increase the number of Advertisement sold although at lower cost (True Negative)

• Loss will be incurred when a Popular article will be predicted as Unpopular, as ads will be sold at lower cost (False Negative)

• Loss will be incurred when an Unpopular article will be predicted as Popular, as ads will be sold at a higher cost but eventually, we might lose potential future ads (False Positive)

<img width="634" alt="image" src="https://user-images.githubusercontent.com/99356847/204114038-2e87dd84-ea8b-46ae-bd2a-1bccc3b516ac.png">

## Model Profitabilty Analysis

• Profitability by cost matrix, Random Forest has the highest profitability

• Profitability in no model scenario, with flat rate of $400 for all articles irrespective of popularity

• The red line indicates - No Model Scenario

• Naive bayes cost performance gives negative lift, based on the cost matrix 

• Form the 4 supervised learning models, random forest has the best profitability. (6.47 mil from 3 mil)

 <img width="450" alt="image" src="https://user-images.githubusercontent.com/99356847/204114122-d39bcac5-7cd8-483c-b870-b227926280b5.png">

## Conclusion
Random Forest shows the highest accuracy, AUC, and profitability but it isn't the most interpretable model. While there is a recurrent dilemma between performance and interpretation our goal is to create a more interpretable model. While KNN is a good model in our case, it might be slow when the data size increases as it generates hypotheses on the fly. The logistic regression model gives almost the same lift as the KNN model, however, it is more interpretable and would work even with increased data size. One of the major takeaways from the project is that accuracy is not the only metric we need to look forward to while we are building the model, there are parameters that need careful consideration based on the use case. In the future, we could build ensemble models to get higher accuracy, precision, and AUC for the data. Additionally, the research could be extended to building multiclass classification, this will help in identifying the Most Popular, Popular, Neutral, Unpopular, and No Popularity articles.

