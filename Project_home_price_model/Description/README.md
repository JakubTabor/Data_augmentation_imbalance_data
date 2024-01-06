* I start from simpified my data into few columns: **(location, size,	total_sqft,	bath,	price)**
* I check if there are any non-values and drop them

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images/isnull.png)
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images/dropna.png)
* Then i create separate column for **(bhk- bedroom, hall and kitchen)** using lambda function
* I can see that in this dataset i have outliers with bhk greater that 20
* Its good to notice, i will deal with it later
# I see that column (total_sqft) have values with two composites
* So i create a function to search for this values
* And then create function **(convert_sqft_to_num)** 
* Which search for values with length of two tokens and take intermediate value

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images/sqft_to_num_function.png)
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images/convert_sqft_to_num%20.png)
* Next i create **(price_per_sqft column)** which is the price column multiply by 100 000
* I want to know the number of location occurrence, and i see that the distribution is very divergent
* I have **(1287 different locations)** and there are **(1047 locations with occurrence greater than 10)** and**(1047 with occurrence less than 10)**
* And i also check how many for my (bhk loumn) are outliers, so with less that 300
# And next i write the function to remove outliers for (price_per_sqft cloumn)

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images/remove_pps_outliers.png)
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images/pps_values.png)
* First i iterate over **(location column)** and take **(mean and std)** for price_per_sqft column
* Then i can create **(variable reduced_df)** which is first **(difference between mean and std)** in price_per_sqft column 
* I take values greater than this difference
* And i also define **(sum between mean and std of price_per_sqft)** and **(take values lower or equal)** from it 
* I concatenate it into DataFrame and create new dataset without outliers
# Next i gonna revome outliers from bhk column
* First i create function **(plot_scatter_chart)** which take **(columns for bhk 2 and 3 their total sqft and prices)**
* I see outliers far beyound the rest of the datapoints

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images/plot1_outliers.png)

# So i create function to remove this outliers from bhk column

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images/remove_bhk_outliers_function.png)
* I gonna exclude this data by its indices and put them into numpy array
* I iterate over **(location column and then in same loop over bhk column)** 
* It **(acumulate bhk stats as mean, std with price_per_sqft and counts)**
# Now its part for outliers: in previous for loop i make another loop for bhk
* It **(iteration over all stats and if they take value greater that 5 there indices are excluded)**

#
#
#
# [2. Model tuning](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Description/Model_tuning)
# In this section i gonna first call Linear model and then tune its parameters to achieve the best accuracy
* I start from creating X and y variables and put them into (train_test_split) and get train and test sets
* My dataset is ready for training, so i put it into Linear regression model
* And reach high accuracy, but we can achieve better score
# First i gonna try to shuffle the data and put it into 5 subsets, with it i gonna train my model

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images_model/cross_val_score.png)

* I reach four scores that are fairly better than in previous evaluation
* And now if i want i can use **the highest, which is (0.860)**

# Next i use GridSearchCV to train some models with different parameters it will be hyperparameter tuning

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images_model/linear_regression.png)

* I start from putting Linear Regression model and two ways for coefficients to be negative or positive (False, True) 
* Next will be lasso, i set alpha parameter to 1 and 2, it  is strength of regularization

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images_model/lasso.png)

* Also i put **selection parameter and set for random and cyclic**
* **cyclic loop over features sequentially** and **random do updated of random coefficient every iteration**
* And next is **decision_tree Regressor and parameters are:**

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Images_model/decision_tree.png)

* First **criterion which is measurement parameter set to squared_error, so mean squared error**
* And **friedman_mse which is mean squared error with Friedman's improvement**
* And also **splitter parameter, which set the split at each node** i set them to **best and random for type of split**
# Then i **create list for scores in which will append first model and then parameters all in dataframe format**
* I use **5 combinations of parameters and put my data into GridSearchCV to train it**
# Scores append and we can see that Linear Regression model is the best in that case, also with a little improvement to previous one
* Other model are not performing that bad, but they are far below Linear Regression model
# Next i gonna create predict_price function which from given informations return me estimated price
* First i include all parameters which are needed, so location, sqft, bath and bhk
* Then i define location index of certain element
* And add position of columns that are included and set order of parameters
* And then i try some predictions, it seems working good
# So i put my model and its functionalities into pickle format, so i can use it if future development
