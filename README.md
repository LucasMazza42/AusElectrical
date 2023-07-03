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
- 



