# Introduction

The intent of this project is to supplement the work I am doing researching energy. 

- This dataset was found on Kaggle: https://www.kaggle.com/datasets/vstacknocopyright/electricity
- Data explanation: 
    - We have 9 variables: date, day, period, nswprice, nswdemand, vicprice, vicdemand, transfer, class
    - Period: time of the measurement (1-48) in half-hour intervals over 24 hours. Here normalized between 0 and 1
    - NSWprice: New South Wales electricity price, normalized between 0 and 1
    - NSWdemand: New South Wales electricity demand, normalized between 0 and 1
    - VICprice: Victoria's electricity price, normalized between 0 and 1
    - VICdemand: Victoria electricity demand, normalized between 0 and 1
    - transfer: scheduled electricity transfer between both states, normalized between 0 and 1
    - class label: identifies the change of the price (UP or DOWN) in New South Wales relative to a moving average of the last 24 hours (and removes the impact of longer-term price trends).

# Analysis of data
- Split of labels 
    - We have a perfect slit of labels 50-50 
- Distribution of frequency of price
  <img width="748" alt="Screenshot 2023-07-02 at 11 14 50 PM" src="https://github.com/LucasMazza42/Energy-Price-Movement-Modeling/assets/47802441/dcc2c149-0f5f-4046-b2db-157ece48d598">
    - most of the prices sit above 4,000

- Relationships between variables: correlation
  <img width="912" alt="Screenshot 2023-07-02 at 11 16 01 PM" src="https://github.com/LucasMazza42/Energy-Price-Movement-Modeling/assets/47802441/59ef82fc-d697-4f61-bbc5-49cd603932d9">
      - vicedemand and nswdemand show a little bit of a correlated relationship
- Encoding season based on date:
    <img width="731" alt="Screenshot 2023-07-02 at 11 18 21 PM" src="https://github.com/LucasMazza42/Energy-Price-Movement-Modeling/assets/47802441/e66f49a6-73f4-4885-8918-f85da81d9aa2">
<img width="741" alt="Screenshot 2023-07-02 at 11 18 35 PM" src="https://github.com/LucasMazza42/Energy-Price-Movement-Modeling/assets/47802441/e04c64d5-73ca-43d0-b10e-99c1cd786edb">


# Base model accuracy
- An XGBoost model was trained on the data as is and achieved an accuracy of .91
- Very high

# Exploration of methods to gain higher accuracy and fit: 
    - Feature engineering: 
        - The first thing I decided to do here was break the normalized data into the actual dates of when the measurements were taken. 
        - My thought was maybe we could find some kind of pattern from the seasons. 
            - Winter and Summer have higher energy usage.... 
        - Second, I made a new feature that showed the interaction between 
            - df['price_demand_interaction'] = df['nswprice'] * df['nswdemand']
            - df['price_transfer_interaction'] = df['nswprice'] * df['transfer']
    - Hyperparameter adjustments: 
        - I used a grid search to try and find the best parameters for this model.
        - These were the best parameters that the search came up with Best Parameters: {'learning_rate': 0.1, 'max_depth': 7, 'n_estimators': 300}
# Results of adjustments
    - Obviously, our accuracy was already extremely high so these efforts only resulted in a new accuracy of about .92 
    - Next, we can take a look at some feature importance using feature importance scores: 
        Feature: date, Score: 5461.0
        Feature: nswprice, Score: 2615.0
        Feature: period, Score: 1895.0
        Feature: nswdemand, Score: 1432.0
        Feature: day, Score: 1397.0
        Feature: price_transfer_interaction, Score: 1238.0
        Feature: vicdemand, Score: 1138.0
        Feature: price_demand_interaction, Score: 1104.0
        Feature: vicprice, Score: 916.0
        Feature: transfer, Score: 864.0
        Feature: Season, Score: 22.0
    - We have some really powerful metrics in this model. The only thing to note here is that season doesn't really make a difference and had our lowest value. I attempted to train a model without season just to avoid the noise, and it didn't really make a difference. 
    - I am still looking into why this might be the case because as you can see the date column was a massive predictor for us in our model and this was not the result I was expecting. 
        - My guess is that our labels have to do with the moving average of the last 24 hours, and when we have a lot of data points from the same month which isn't necessarily the time frame window we are looking at. 
        - In other words, if we have two days that are in the same month, or season, knowing the season won't really make a difference because the price points are relative to the month. 
    - Next, I did K-fold cross-validation to evaluate the model over different sets of validation data - 5 folds
        - Here are the results: 
            Cross-Validation Results:
            Average Accuracy: 0.9121203513900454
            Standard Deviation: 0.0021014886293994734
        - These are great results, basically, we can say our model is solid over different sets of test data. 
    - F1 score: represents the mean score of the precision and recall of the model = 2 * (precision * recall) / (precision + recall)
        - Score ranges between 0 and 1. We have a score of .91 which is extremely good. 
    - Finally, we have the confusion matrix: 
        <img width="861" alt="Screenshot 2023-07-03 at 8 43 00 PM" src="https://github.com/LucasMazza42/Energy-Price-Movement-Modeling/assets/47802441/3c523eb5-254f-4902-ad08-f86b493e7b7d">

        - 572 false positives
        - 515 false negatives 
# Conclusion
    - Our model is extremely powerful. High value. 






