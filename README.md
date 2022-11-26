# Online News Popularity Prediction
## Problem statement
The marketing team of Mashable is responsible identifying popular articles and accordingly sell ads on these articles to incur large profits. Currently the team uses heuristics to predict articles popularity and has flat rate for ads irrespective of the popularity. The team lacks a framework to identify article popularity based on historical data of articles published on the website.
## Goal 
1. Determining the popularity of articles prior to its publication by training machine learning models on various features like days on which article was published, no. of images in the article, no. of words in the article and other features thus helping publishers to generate profit.

2. Implement new pricing strategy with help of cost based analysis (cost matrix) and help mashable's marketing in increasing revenue.
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

Shares > 1500 – Popular (1)
Shares <1500 - Unpopular (0)

Reason for choosing 1500
1. Closer to median (50th percentile)
2. The problem of class imbalance would be resolved 



