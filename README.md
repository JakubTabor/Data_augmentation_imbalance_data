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

