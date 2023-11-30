# In this section i gonna show three examples how we can improve accuracy by implementation of some techniques
# [Example 1: Dropout Regularization](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Dropout_Regularization.ipynb)
* I start with the simplest example, it will be (dropping neurons tehnic)
* I need to do only simple preparation of data for my model, because it is fully numerical
* I show the most popular activation function for (Neural net), which is relu and also sigmoid which i use in output layer
#
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/Relu.png)
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/Sigmoid.png)
* And then i build simple sequential model
* I allow the situation when occurs the overfitting
* **(accuracy is 0.8077 and loss 0.7854)** despite that during training it achive (accuracy: 1.0000 and loss: 0.0021)
* When i check classification report (f1-score for both calsses is 0.82 and 0.79)
# So i build another model, but now with dropout layers
* Now the (accuracy reaches around 0.9 and loss 0.30)
* After evaluation the score is **(0.82 and loss 0.42)**
* We can clearly see that the accuracy is higher and loss is lower, that's all the good signs

# [Example 2: Data Augmentation CNN](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Data_Augmentation_Overfitting__CNN.ipynb)
# In this example i show data augmentation in form of layer insite Convolution Neural Net
* First i download the dataset which contains images of flowers
* I prepare them using **(Pathlib and cv2)**, then convert them into dictionary and set labels
* Then i create function which return me two lists of **(resized and converted into numpy array)**
* Next i create (train and test sets) and scale them in range 0 to 1

# I build first model to measure accuracy and compare it later with (augmented model)
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/Model_before_augmentation.png)
* We can see that **(accuracy is pretty low 0.63 and the loss is pretty high 2.64)**

# Then i create the layer with data augmentation
* And place it at the first place in my another model
* I measure the parameters of this model and i get improvement
# The accuracy is now 0.70 and loss 0.95
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/Model_after_augmentation.png)

# [Example 3: Customers Churn](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/imbalanced_dataset_customers_churn.ipynb)
# In this example i gonna show how different sampling methods can affect the accuracy of the model
* And we are gonna mesure which is the better in our case
# First i start of data preparation
* I search for unique values in columns 

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/unique_values_function.png)

 # Then i convert all objects into full numerical data 
 * I use replacement of **(yes and no into 1 and 0)** or **(No internet service to No)**
 * And create dummy variables from much complicated columns
 * Finally i get fully numerical dataset and i can now create (train and test set) for my model

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/data_types_numerical.png)

# I create function (ANN) which i gonna train with different variants of the data (undersampling, oversampling, Smote, ensemble)

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/ANN_model_function.png)
* First i train my model with imbalanced dataset
 ![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/report_class_imbalance.png)
* Accuracy seems to be good, but when we see (f1-score) there is big class imbalance
* Our goal is to improve the score from class nr. 1

# Next i train my model with dataset balanced by undersampling
* We create equal number of samples in our both classes **(our class with lower number of samples)**
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/report_under_sampling.png)
* Accuracy is lower than previous, but we improve score in our class number 1

# Then we train the model with over-sampling balanced dataset
* In this case we balance our dataset making equal number of samples in both classes, but to **(class with higher number of samples)**
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/report_over_sampling.png)
* We see that the score of class number 1 is much higher than lastly
