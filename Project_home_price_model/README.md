# [Home price prediction](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/bengaluru_home_price_model.ipynb)
# In this project i gonna create Linear model for home price prediction
# Remove outliers
# And search for the best parameters
#
#
#
# [1. Preprocessing](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Project_home_price_model/Description/Preprocessing)
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
