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

# First i train my model with imbalanced dataset
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/report_class_imbalance.png)
* Accuracy seems to be good, but when we see (f1-score) there is big class imbalance
* Our goal is to improve the score from class nr. 1

# Next i train my model with dataset balanced by undersampling
* We create equal number of samples in our both classes **(our class with lower number of samples)**
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/report_under_sampling.png)
* Accuracy is lower than previous, but **(we improve score in our class nr.1 (0.72))**

# Then we train the model with over-sampling balanced dataset
* In this case we balance our dataset making equal number of samples in both classes, but to **(class with higher number of samples)**
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/report_over_sampling.png)
* We see that the **(score of class nr.1 is much higher than lastly (0.81))**
* And even we get **(better accuracy after model evaluation, than in our original imbalanced dataset)**

# Another technique of balancing your dataset is SMOTE
* With this technique we are gonna create synthetic sample from our minority class
* We create number of synthetic samples to the number of bigger class (5163)
* We train our model and check the results
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/report_smote.png)
* We achieve at this point **(the best accuracy score 0.82)** and **(the best f1-score for the class nr.1 (0.83))**

# Next technique is called ensemble learning, we are gonna train the model with three batches of data from majority class
* I create the function to get those batches and next i gonna provide number of samples to define those batches
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/get_batch_function.png)

# I divide my data into three batches and train my model with it
* All give me different results and final will be chosen as average of them
* Final will be chosen by the votes, which are 0 or 1, so i create function from all (y_preds)

# The final results are not impressing, in this case ensemble learning is not so effective
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/ensemble_final_report.png)
* But we were able to improve f1-score from class nr.1 (previous was 0.54 now it is 0.61)
