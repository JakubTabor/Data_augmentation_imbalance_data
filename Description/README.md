**DROPOUT REGULARIZATION**
# This dataset is made on (sonar data), it is full numerical data, so there is no need to preprocess it, only simple processing
* I only need to check if there is any null values and class imbalance
* Then i separate last column, it will be my (y) target feature
* And i convert my (y) into dummy column, because it is not numerical

# Now i split my data into train and test sets and check their shape and i can see class imbalance
* In this case i can ignore it and show only (dropping of neurons method) for improvement in accuracy

# But first i will show how the most popular activation function (RELU) look like 
*It activates when it get positive input, but when it get negative input it become zero

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/RELU.png)

# So i import tensorflow and keras to create my (neural net)
* I create first layer with (60 neurons) and (60 dimensions) with activation as relu
* Next i create another two (hidden layers) with (30 and 15 neurons) and same activation (relu)  
* And final (output layer with only 1 neuron) and activation as (sigmoid)

# Then i compile my model with loss as (binary_crossentropy), because of binary output
* The best optimizer in this case (adam) and i want metrics as (accuracy)

# Then I train my model with my (train sets), then (100 epochs) and (8 samples)
* Accuracy reaches 1.0 which is the sign of overfitting, but after evaluation accuracy is (0.8077)
* Then i also prepare ypred for confusion matrix and check my model predictions
* I can see that my model with (accuracy 0.8077) make good predictions and fits in the data
* Now I call (classification report) and see that (true and predicted classes) have different values
* It means that it is not a balance model, but (F1 score) is not that different which is a good sign
* The average score is (0.81), i gonna compare it with next model which gonna have (dropping neurons layers)

![https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/Report_first_model.png]

# Next i create another model, this one gonna have (dropout layers)
* First i create layer with (60 neurons and size of input dimensions as 60, with activation relu)
* And now i add (Dropout layer) which gonna drop (0.5 of neurons after pass)

# Then i create another layers with (30 and 15 neurons), after every layer i add (Dropout layers)
* And final output layer with one nueron
* I compile my second model with the same parameters as in my previous model, there is no need to make any changes
* Next i train my model with same (train sets and parameters as previous)

# I can see that my accuracy never reach accuracy (1.0) which is a good sign, there is no overfitting
* After evaluation i get accuracy (0.8269), so there is improvement in comparison to my previous model
* I check also predictions of my model and it seems that it fit the data and work good

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/Report_secound_model.png)

# When i call (classification report) i can see statistic improvement
* I see that the average score is around (0.83)

# That was only simple example to show how we can improve ouraccuracy with adding or removing some parameters
