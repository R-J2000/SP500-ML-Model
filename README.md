# ML Model Forecasting Tomorrow's S&P 500 Index

#### This project uses scikit-learn's **RandomForestClassifer** and a **backtesting engine** to train a forecasting model on 30+ years of data, predicting whether the S&P 500 index will go up or down tomorrow.

### Implementation Steps

1. Import the Yahoo Finance API (yfinance) and query the historic index prices of the S&P 500.
2. Clean and visualize the DataFrame
    - Remove extraneous columns
    - Remove particularly old data; anything older than 1990 was be removed.
    - Visualize data for the S&P 500 index  
![image.png](attachment:9038b028-23f6-4bdb-9a0b-632e8f33d610.png)
3. Set Target, which is an additional column indicating whether tomorrow's price went up (Target = 1) or not (Target = 0). This can be done by comparing the index price of a particular row $n$ with the index price corresponding to row $(n+1)$.
4. Initialize the RandomForestClassifier (after importing it) with tentative inputs. Partition dataset into training and testing dataset.
5. Establish predictors. Use the predictors and target values to get a model fit. 
6. Import and use precision_score (from scikit-learn) to assess your model. Test, in particular, the accuracy of the your models positive predictions, as the client will primarily be interested in investing when the price is anticipated to go up.
7. Implement a Backtesting system. The value for the first 10 years of data was taken as the training set, and was used it to predict the values for the 11th year. Then the values for the first 11 years was taken and used to predict the values of the 12th year...so on and so further, until the model reached the current year.
8. Use rolling average for different time horizons to set new columns in your DataFrame. Qualitatively these new column will assess the general trend of our index (how the S&P 500 index price is doing) over different time horizons. **These will be our new predictors**. 
**KEY INSIGHT**: This is where we are encoding some human intution into the code. If the times are good we may anticipate them to be good for longer and vice versa. The model with these new predictors will be able to assess the state of the market in a manner losely aligned with a human analyst.
9. Clear rows with "NaN" values. 
10. Improve the model by being more selective with your positive classification. Only set prediction to 1 if the model is 60% certain that the price will go up.



### Future Improvements
- Use Trading Platforms Open at "Night" to correlate to S&P 500 values
- Add News
- General Macro-Economic Stats

