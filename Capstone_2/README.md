# Movie ratings vs Return on Investment

When companies make movies, they want to know that they can make a profit. The goal of this project is to take movie parameters such as ratings, genres, release date, and budget to predict if a movie will be successful.

## 1. Data

The data was taken from Kaggle and includes 507 movies. The columns are Title, MPAA Rating, Budget, Gross, Release Date, Genre, Runtime, Rating, Rating Count, and Summary.

## 2. Data Cleaning

The original data had 7545 entries. Most rows were removed from the original data. Those rows contained null values or were actors and not movies. Also, two movies were removed because they had no Rating or Rating count. A duplicate entry for Jurassic Park III was averaged.
The data was looked at graphically to see if there were any outliers or other abnormalities. There are two, Titanic and Avatar, but we know those values are accurate.
There are 4 MPAA rating levels, and 16 genres. Also, all currencies appear to be in USD.

## 3. EDA

An ROI column was created by dividing Net Profit by the Budget.

The genre categories were not evenly distributed which would cause the model to be skewed. A genre frequency column was created to help standardize the genre counts.

The Net profit was analyzed to look for negative values. None of the movies were flops. I think we can assume that this data set only includes blockbuster successes. This means future models using this data assume the movie will succeed.

Avatar and Titanic were removed from the data set because they are outliers based on net profit. 

The Blair Witch Project was removed because it had an ROI of over 4000 and was an outlier.

You can see that the most successful movies are released in the May, June, July, November and December.

## 4. Modeling

The data was scaled using a standard scaler and dummy variables were created for MPAA rating, and Genre categories. The Release Date category was encoded into sine and cosine features due to its cyclical nature. Also, the Gross column was changed to a log scale due to having a skewed distribution. The Summary, Title, Release Date, genre_Frequency, Net Profit, and ROI columns were also removed from the data. Then the data was split into training and test sets.
Random Forest, XGBoost, Linear Regression, and SVR were tested as potential models.


There were three predictive features to choose from: ROI, Gross, and Net Profit. Gross performed best overall when testing data. Ergo, the log of Gross was used as the predictive value. However, I believe that the ROI would be a more useful predictive value, but it could be easily calculated from the final model.

Random Forest and SVR performed best. SVR had a lower mean absolute error, so it was chosen as the final model.

After a grid search, SVR best hyper parameters were found to be the following: C = 1, degree = 2, gamma = auto, kernel = RBF.

These parameters were used for the final SVR model. The metrics table shows that the best hyper parameters increased the R squared value to 0.63, however they also increased the mean absolute error to 0.42.


## 5. Discussion

This data set is of Hollywood blockbusters. It shows that successful movies have more critic reviews, higher ratings, and higher budgets. Movies released in the fall or summer also have a better chance of being more successful.
This data has no movie flops which makes it extremely biased. The model will most likely not report a movie as a flop and if it did, there is no model data to support that hypothesis.

The final model created with this data had a R squared value of .63 which shows there is correlation between features, but it s not the best. Also, the mean absolute error for the model was 0.42 based on the log of the Gross. That number looks small but represents millions of dollars. A small budget movie would not be predictable with this model.

I think the most helpful information in this project is found in the data analysis, not the modeling. The general correlation between release month, ratings and genre potentials are the most important thing when looking at how successful a movie could be.

Future study on this subject should include more robust data of a larger sample size and movie flops as well as blockbuster hits. Future features could also include directors, production companies, production time, cast members ect. The list goes on.
