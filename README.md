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







