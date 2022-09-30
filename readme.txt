# Spotify skipped prediction

In this project, we are going to predict whether the song will be skipped or not and this model will be deployed on heroku.

# The dataset

We will be having 2 csv files from track features and 1 from the training set. Datasets from the track features and training set will be merged on the basis of “track_id” column. 
After merging the columns, we will be having 167880 rows and 50 columns. 

# Preprocessing and feature engineering

New column “skipped” is created by adding “skip_1”, “skip_2” and “skip_3” columns, which shows whether a song is skipped or not.
“skip_1”, “skip_2” and “skip_3” columns were removed, as they were not required.

“track_id” column was also removed and “session_id” column was set as an index.

As there were no missing values or garbage data, we moved towards feature engineering.

When analyzing the dataset, we get to know that “session_id”, “date”, “context_type”, “hist_user_behavior_reason_start”,”hist_user_behavior_reason_end” and “mode” having object data type, so by applying label encoder we encode these columns.
“not_skipped”, “hist_user_behavior_is_shuffle”, “premium” and “skipped” columns were having bool data type, so we changed their datatype to integer so that our model can understand.


###Random Forest Classifier 

Random Forest is a classifier that contains a number of decision trees on various subsets of the given dataset and takes the average to improve the predictive accuracy of that dataset.
1: Extracting dependent and independent variables
There were 13 independent columns placed in X and 1 dependent column was placed in Y.
X = 'hist_user_behavior_is_shuffle','context_switch','hist_user_behavior_n_seekfwd','hist_user_behavior_n_seekback','context_type','no_pause_before_play','session_length','hour_of_day','session_position','hist_user_behavior_reason_start','hist_user_behavior_reason_end','date','premium'
Y = 'skipped'
2: Splitting the dataset into training and test set
We kept the test size 0.3 and random state 42
3:Training & predicting the test set result  
4: Calculating ccuracy score
The accuracy_score() method of sklearn.metrics, accept the true labels of the sample and the labels predicted by the model as its parameters and computes the accuracy score as a float value. The accuracy achieved is 98.0%

# Flask

We created our app using flask, then it was deployed it to heroku.
An api predict was created in which all the input were taken. These values were converted into integer values and then in to an array.
Pickle is used to store the model building, so that it can be used to predict.
Then the model will predict our value.

# Heroku
Heroku is a cloud platform where we will deploying our flask app, so that everyone can access it.
Files which will be needed to deploy our app our:
•	app.py
•	spotify.py
•	model.pkl
•	request.py
•	requirements.txt
•	index.html
Our web application can be accessed by this link:

 https://spotify-prediction-flask.herokuapp.com/



###User Interface 

We designed a UI for our spotify prediction app using both HTML & CSS in which we used the "POST" method in form to send the data from UI to the flask app. We applied an image as a background in UI and the top bar has a heading of "Spotify Prediction" with spotify's logo. We placed labels for all 13 columns and the user has to select the input through the dropdown.
To distinguish the labels and user input, we placed the labels and input into a box, having opacity so that the background image is all visible. Once the user has selected the required inputs, user has to click on the submit button on which "predict_api" is called. The predict_api is getting all the inputs of UI and passing it to the "predict" method of the model. 
The final result is being displayed to the user on the app, showing 0(Not skipped) and 1(Skipped)
