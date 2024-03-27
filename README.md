# Algo Trading Bot
This project seeks to optimize the performance of a machine learning algo-trading bot.

## Tuning Steps
### Tuning training data
In an effort to improve our model scores, the DateOffset parameter was changed from 3 months to 6. In effect, doubling the amount of training data for our model.

Also, the short_window and long_window were increased from 4 and 100 respectively, to 10 and 200. This increases the SMA input features for our model in an effort to increase the model's scores.

Tuning Questions
#### What impact resulted from increasing the training window?
Increasing the training window of our model impacted the precision score of our model.

Here is the base line Classification Report

          precision    recall  f1-score   support

    -1.0       0.43      0.04      0.07      1804
     1.0       0.56      0.96      0.71      2288

accuracy                           0.55      4092
macro avg 0.49 0.50 0.39 4092 weighted avg 0.50 0.55 0.43 4092

Here is the Classification Report with our adjusted Training data.

          precision    recall  f1-score   support

    -1.0       0.52      0.03      0.06      1732
     1.0       0.56      0.98      0.71      2211

accuracy                           0.56      3943
macro avg 0.54 0.50 0.39 3943 weighted avg 0.54 0.56 0.43 3943

As you can see, no significant impact was made on accuracy, or recall. We did see an increase in precision of 0.9 which is an overall improvement considering the stability of other factors.

Here is the graph of our Cumulative Actual Return vs. Strategy Returns.



This model is a poor fit due to the irratic underperformance of our strategy returns vs. actual returns.

#### What impact resulted from increasing or decreasing the SMA Windows?
Adjusting the SMA windows does not seem to significant impact the model one way or the other. Here is our Classification Report with a short_window of 6 and long_window of 120:

          precision    recall  f1-score   support

    -1.0       0.47      0.03      0.05      1793
     1.0       0.56      0.97      0.71      2284

accuracy                           0.56      4077
macro avg 0.51 0.50 0.38 4077 weighted avg 0.52 0.56 0.42 4077

As you can see, adjusting the SMA does not significantly impact the Report. Increasing the training data size remains our best option for improving the model's scores.

Optimized Model
Considering the above, in order to optimize our model, we will increase the amount of training data from 6 months to 8. Now our model will train on a year's worth of data.

Here is the Classification Report with the original SMA values and 8 months of training data:

          precision    recall  f1-score   support

    -1.0       0.43      0.16      0.24      1670
     1.0       0.56      0.83      0.67      2142

accuracy                           0.54      3812
macro avg 0.50 0.50 0.45 3812 weighted avg 0.50 0.54 0.48 3812

As you can see, although the accuracy of the model dropped by 0.02, the model's recall scored for -1.0 (sell orders) from 0.03 to 0.16. This score is still far from ideal, but it is a significant improvement for our model. What this low value means for our model is it will miss a significant number (84%) of negative instances (sell opportunities). However, the model will only miss (17%) of buying opportunities.

Our Precision scores are more balanced, though still not ideal. 0.56 precision for buying opportunites means the model will execute 44% of false positives. Similarly, 0.43 precision for sell opportunities means the model will execute 57% of false positive selling opportunities. These metrics are not ideal for deploying this model with real money.

### Using a New Model
To add additional context to understanding our model. We tried a new Machine Learning Classifier. Specifically, we implemented a Logistic Regression. This improved the model's scores on the Classification Report:

          precision    recall  f1-score   support

    -1.0       0.56      0.02      0.04      1670
     1.0       0.56      0.99      0.72      2142

accuracy                           0.56      3812
macro avg 0.56 0.50 0.38 3812 weighted avg 0.56 0.56 0.42 3812

Here is the graph of our Actual Returns vs. Strategy Returns



As you can see, the Logistic Regression Model strategy outperforms our Actual Returns by a small percentage. This means that the Logistic Regression Model is our best bet of the trials undergone in this project.

## Conclusion
After several trials adjusting our input features for out machine learning algorithm, the Logistic Regression Model with 8 months of training data is our best fit. It is the only model tested in this project which consistently outperforms our actual data and is the best bet to deploy into actual use.