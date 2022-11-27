# Online News Popularity Prediction
## Problem statement
The marketing team of Mashable is responsible identifying popular articles and accordingly sell ads on these articles to incur large profits. Currently the team uses heuristics to predict articles popularity and has flat rate for ads irrespective of the popularity. The team lacks a framework to identify article popularity based on historical data of articles published on the website.
## Goal 
• Determining the popularity of articles prior to its publication by training machine learning models on various features like days on which article was published, no. of images in the article, no. of words in the article and other features thus helping publishers to generate profit.

• Implement new pricing strategy with help of cost based analysis (cost matrix) and help mashable's marketing in increasing revenue.
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

<img width="638" alt="image" src="https://user-images.githubusercontent.com/99356847/204113105-cc41b48c-37c5-453a-ae56-7e75654bf332.png"> <img width="639" alt="image" src="https://user-images.githubusercontent.com/99356847/204113125-f70be976-e494-4c8f-81e1-ab4347ff89fd.png">

<img width="638" alt="image" src="https://user-images.githubusercontent.com/99356847/204113143-64279e88-a1f6-4473-b26a-2d678ac129dd.png">

## Preprocessing
• Removed dump articles – articles with no words as they won’t be helpful for model building

• Removing non-predictive features like URL of article and time delta 

• Removed highly correlated attributed with help of correlation matrix: n_non_stop_unique_tokens, n_non_stop_words, kw_avg_min, self_reference_avg_shares_new, avg_negative_polarity_new, avg_positive_polarity_new

• Removed weekday_is_saturday and weekday_is_Saturday with help of cross plots chi-square values 

<img width="1000" alt="image" src="https://user-images.githubusercontent.com/99356847/204113293-c9f618f5-6b01-4de0-a908-d6a4dbb12539.png">
<img width="600" alt="image" src="https://user-images.githubusercontent.com/99356847/204113473-31c776c3-539f-4dc7-a63b-47b23ebecded.png">



