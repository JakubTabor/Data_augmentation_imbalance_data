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
