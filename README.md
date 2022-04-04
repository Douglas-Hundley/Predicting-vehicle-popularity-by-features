# Predicting Vehicle Popularity by Features
_by Douglas Hundley_
___

### Problem Statement
___

I am working for General Makers who is developing a new car. My goal is to predict the popularity of the car if it goes to the market and also to help identify what features make a car popular. In order to do this I will be cleaning the dataset shown below and using regression models for my predictions. I will gauge success by creating a predictive model that has atleast an 80 percent R2 score and beats the null model in RMSE.

### Data Dictionary
___
|Feature|Type|Dataset|Description|
|---|---|---|---|
|**make**|*object*|cars.csv|The car manufacturer|
|**model**|*object*|cars.csv|Model of the car|
|**engine_fuel_type**|*object*|cars.csv|Type of fuel the car takes|
|**engine_hp**|*float*|cars.csv|Car Horsepower|
|**engine_cylinders**|*integer*|cars.csv|Number of cylinders|
|**transmission_type**|*object*|cars.csv|Transmission type of car|
|**driven_wheels**|*object*|cars.csv|Drive type of car|
|**number_of_doors**|*float*|cars.csv|Total count of words in title column|
|**market_category**|*object*|cars.csv|Marketing type of car|
|**vehicle_size**|*object*|cars.csv|Size type of car|
|**vehicle_style**|*object*|cars.csv|Style of car|
|**highway_mpg**|*integer*|cars.csv|Highway miles per gallon|
|**city_mpg**|*integer*|cars.csv|City miles per gallon|
|**popularity**|*integer*|cars.csv|Popularity rating of car|
|**msrp**|*integer*|cars.csv|Manufacturer suggested retail price|

### Summary of Analysis
___
In order to answer my problem statement I first had to clean up my dataset and clean up any nulls. I first started off this process by removing the "market_category" feature from the data as it had 3,742 nulls and I felt there was no appropriate way to impute this many missing values in this set. From there I imputed the rest of my nulls using KNNImputer. With my nulls imputed I then proceeded to drop all of the duplicate rows in the dataset. With my data fully cleaned I then moved on to visualizing my data to look for any connections between my features and my target of "popularity". I started off by creating a heatmap to compare my numerical features to "popularity". From this I could see that all of the numerical features had a very low correlation. For me to consider anything to be highly correlated I look for atleast a value of 0.40 but in this data set the highest value was "year" at 0.085. Moving on I created bar plots to check vehicle makes that have the highest and lowest popularity. The top three vehicle makes in popularity are Ford, BMW, and Audi while the least popular vehicles are Spyker, Genesis, and Oldsmobile. However one thing to note is that Genesis and Spyker both only hold 2 to 3 spots in the dataset. 
![Most Popular Cars](https://git.generalassemb.ly/douglas-h91/capstone/blob/master/Images/popular_bar.jpg)
![Least Popular Cars](https://git.generalassemb.ly/douglas-h91/capstone/blob/master/Images/not_popular_bar.jpg)
Next I created scatter plots to check for any relation between "MSRP" and "popularity". What I found was that most vehicles with a popularity of over 3,000 tended to have a max price of around 200,000 or less with the most popular vehicles staying at around 70,000 or less. After this it was on to modeling. At this stage I had dropped the "model" column this was due to it adding 914 columns to the dataset.
With my dataset trimmed down to 87 columns I started off by creating a Lasso model and checking the coefficients it returned. Although the model's R2 scores of 99 over 99 were unrealistic the coefficients it returned made sense based off of my EDA. The model showed that features in the "make" column were seeing the biggest moves in "popularity". After this I decided to try some modeling without the "make" feature due to it adding 48 columns to my data. After gridsearching several models the best scores I received were from my Regression Tree Model. Although the model was over fitting by around 10 percent it was returning the most realistic results and I believe that it can be tuned further to reduce overfitting. The scores of each model are listed below. 

|Model|Train Score|Test Score|RMSE|
|---|---|---|---|
|**Null**|NA|NA|1445.6989|
|**1st Lasso Model**|0.9999|0.9999|4.1932|
|**2nd Lasso Model**|0.1347|0.1331|1385.5655|
|**Linear Model**|0.1335|0.1350|1385.9820|
|**Ridge Model**|0.1336|0.1353|1385.8341|
|**Regression Tree Model**|0.9809|0.8764|524.0349


### Conclusion and Recommendations
___
To answer my problem statement I would say based on my EDA of this dataset it appears that the feature that most affects popularity is the brand of the vehicle. Ford, Audi, and BMW seem to have the most postive affect on popularity. While Oldsmobile, Lincoln, and Buick appear to be the car brands to avoid. Knowing what vehicle brand is popular can absolutley be useful. General Makers could consider reaching out to any of the popular brands mentioned above and create a collaborative vehicle. This could help boost brand recognition as well as popularity by appealing to an already large audience. As for the features besides make there are no discernible patterns in the data that I could detect except for msrp. If a vehicle is to expensive it won't be available to the general public and won't receive as much exposure. I would also deploy my random forest model to predict the popularity of the cars as they come out.

In the future to improve the efficacy of modeling I would recommend bringing in more outside data such as user reviews for each vehicle type or condensing the "make" feature into their parent companies to reduce the overall number of features without losing the information from that column. I would also like to further tune the model with additional gridsearching.
 
