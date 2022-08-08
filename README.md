The Ames housing dataset is a feature-rich dataset, documenting over 80 features and their relation to sales price of homes.
My goals are twofold:
First, I am trying to create a machine learning model that uses some subset of these approximately 80 features to optimally predict sales prices of houses for data it has not been exposed to.
Second, I am trying to create an informative model for real estate buyers to know which features to invest in that would lead to the greatest sales price.

I started off by looking through and cleaning my data. I identified data types and null values for both datasets and identified any anomolies in the data.
I noticed many columns that were categorical in terms of their data. Rather than individually change these columns, I just applied .getdummies to the whole dataframe, and it correctly dummied all columns that could be dummied. I filled any nullvalues with the mean of the column, as dropping rows with null values would lead to almost all the dataset being lost.

I next plotted some graphs to show the relationships between different features and Sale Price.
Using a heatmap I've identified those columns most correlated with SalePrice, and used this information to fit my first model. I also created pairplots of those variables most highly correlated with SalePrice, and saw that there is a mostly linear relationship to sale price for most of these features (with the exception of Kitchen Qual_TA and Exter Qual_TA).

I next started fitting and testing models.
I played with adding and removing a whole variety of features from X. My original R2 score of .78 was from a normal linear regression model of only the top 10 most highly correlated features to sale price. The variance of this model was medium to low, and the effectiveness of the model could be improved.

I noticed the more features I removed, the lower the score of the model, so just to try it, I made a model where I used every feature in the data set besides "SalePrice" as my X. The R2 score for both training and testing were excellent, and were close to one another. As such, this model has low variance and low bias. Additionally the RMSE was 23,452, meaning the model predicts within $23,452 of error

I am happy with this model, but will attempt some more complex data processing to see if i can improve my score.

I played around with 3 other models, a polynomial, lasso, and ridge. Using polynomials on all the features resulted in a higher R2 score for training than in my next best model (.975), but an extremely low one for testing (.337). The RMSE was very high as well: 6.303484430052246e+20. This was a highly overfit model. So, since variability in this model was exceptionally high, so I decided to use ridge and lasso on it to see if I could decrease variability.

Lasso increases the train score, but overfits it. Better than poly on its own, but far more variable than the original linear regression.

Ridge is better than lasso, much less variability. However, it runs into similar RMSE problems as lasso: 1.3968882620002243e+18. The train scoe was .99, and test score was .916, which shows the model is probably overfit, and that is the reason for the very high RMSE score.

I only showed my second linear regression model, as it was my final model, and the other models I tried gave worse RMSE scores, and would effect readibility of my notebook.


CONCLUSIONS
This process revealed that utilizing all the data provided and a simple linear regression yielded my most predictive model.
However, this model utilized nearly all features on the dataset, which would be hard for someone to make real estate decisions according to.

RECCOMENDATIONS
As such, I would use my first model to recommend to people to invest in houses that scored well in Overall Quality, Garage Area, Number of Cars per Garage, Total Basement Surface Area, 1st Floor Surface Area and Year Built. This is because these features all have high correlation with sales price.

FURTHER CONSIDERATIONS
With more time to optimize my models, I would take two paths.
First, when trying to submit to Kaggle, I had to match up the column names of the train dataset and test dataset, forcing me to drop 20 columns of data in the train dataset. This worsened my models RMSE by about $4,000. I would in the future try and add 20 columns of data in the test dataset instead, and hopefully maintain my models predictive strength.
Second, I would try and iron out the reason my Ridge model had reasonable R2 scores, but such horrendous RMSE, which I imagine is due to some error in my processing of the data.

