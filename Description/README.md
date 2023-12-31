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

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/Report_first_model.png)

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
* That was only simple example to show how we can improve ouraccuracy with adding or removing some parameters
#
#
#
#
# **MORE ADVANCE EXAMPLE (OVERFITTING_CNN)**
#
**Data_Augmentation_Overfitting__CNN**
# First I need to download dataset from tensorflow
# So i save "url", then I use method "get_file" on "flower_photos" from my saved url "dataset_url"
* I save it in directory and unzip, using "untar"

# Then I need to convert my data into "pathlib"
* Thats because it will be more proper to use (Path of my data_dir), it looks like this **(pathlib.Path(data_dir))**
* Now i convert my data_dir into list, i want five samples, so i make them global **(list(data_dir.glob('*/*.jpg'))[:5])**
* I want to get length of my dataset, so i take len of my global images and save it as variable (image_count)
* Then I check roses images in my dataset, so I use **(PIL.Image)** to open first image and save my roses images as variable **(roses)**

# Next I gonna create one list for my images to sort "every type" of them and secound list for my images labels

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/flower_images_dictionary.png)

# Then I convert my images into numerical 3D numpy arrays, next i resize then to the same dimension for training purpose
* First i create two empty lists **(X, y = [], [])**, then i make for loop **(for flower_name, images in flowers_images_dict.items())** and with acces to items
* Then in that loop i create another loop **(for image in images)** i create **img** variable which is **(cv2.imread and str on my image)** 
* It will convert into **(3D np.array)** then i resize img using **cv2.resize** img variable and set size which is **(180,180)**
* Then I fill my **(X and y variables, X with resized_img as 3D array and y with flowers_labels_dict)** so numbers of my **labels of flower_name**

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/convertion_of_all_images.png)

# And i convert my (X and y into numpy arrays) i have (X and y) prepared
* Next i import (train_test_split) and get **(train and test sets)**
* I check length of my sets and scaled them in range **(from 0 to 1 for training in my CNN)**

# Now i gonna build CNN, i create variable to keep all visually good (num_classes = 5), then i start building (Sequential model)
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/CNN_model.png)

* First layer have 16 filter detectors **(filter size is 3)** padding means adding **one layer of zeros** to my image while processing
* And **(padding = same)** return **same output shape as my input shape** 

# Then i add (pool layer after every conv. layer), and i also add two (hidden conv. layers) with 32 and 64 neurons
* Purpose of adding (pool layer) is to reduce the dimensions the layers

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/maxpool.gif)

# Next i add "Flatten layer" to convert it into (1D array) 
* And also one **(Dense layer with 128 neurons)** **(My output layer have 5 classes)**
* Then i compile my model with **optimizer as adam** and loss as **SparseCategoricalCrossentropy**, because my output is **exact value**
* **metrics is accuracy**

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/Flatten_layer.png)

# Next training of my model, so i use (X_train_scaled, y_train and set number of epochs at 30)
* During the training appears **(accuracy close to 1.00)** it means that my model is overtrained
* When I evaluate my model with **(X_test Scaler, y_test)** so brand new data it return me pretty low accuracy in comparison to accuracy during trainning 
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/Model_before_augmentation.png)

* I also check predictions, but i need to return index of my prediction (np.argmax(score))

# Now i gonna (augment) my data with new samples by (rotating and zooming) my original data, i can also (flip it)  

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/data_augmentation_process.png)

# I show how my data is changing after (augmentation), it is zoomed and rotated
* I also need to convert it into **(numpy and int type)**  **plt.imshow(data_augmentation(X)[0].numpy().astype("uint8"))**

# Once again I create my "Sequential model" but first i add (data_augmentation function) 

![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/CNN_augmented.png)

* Then **thre convolutial layers** after every layer i put also **pool layer** 
* And i add also **dropout layer** which will **drop 0.2 of neurons** for better **accuracy score**
* After that Flatten layer to fit all **conv layers** into my **neural net**
* Then additional **Dense layer with 128 neurons** and output **Dense layer with five classes** 

# I compile my model with this same parameters, because there is no need to change anything in there
* And next training my model with **X_train_scaled and y_train and 20 epochs**
* Now accuracy of my model during the training reaches **88**
* After evaluation of my model with my **test sets accuracy is 70**
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/Model_after_augmentation.png)
* in my previous model **it was 63**
* So we can notice the difference, by adding new samples to our data and drop some neurons we can achieve better accuracy
* Its because our model is trained on more possible variants of images
#
#
#
#
# **(Complex example of boosting accuracy and deal with class imbalance)**
#
#
#
# Customer_Churn_description
* In this project i gonna examine **Customer churn dataset**
* Then create a proper model and finally try to **resolve the problem of class imbalance**
* And search for **the best sampling method**

# First i make simple data preprocessing
* I take care of **TotalCharges column**, i change the type **from object** to **float64 with double precision**
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/dtype_float64.png)

# Now i plot customer churn in relation to tenure of customers
* Conclusion is that if customers have more tenure they are more likely to stay
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/customer_churn_plot.png)

# Next when i have idea when the customers are more willing to go and stay
* I gonna deal with all of my columns that are object columns
* So i create function that show the type of my columns
* At this stage i have a lot of object columns
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/unique_values.png)

* I take care of them by replacing complex informations (No internet service) to simple answer (No)
* And now i can convert (yes and no) columns into (binary form) 1 and 0
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/binary_form.png)

* I also replace (Female and Male) into (1 and 0)
* Then i  apply dummy variables to more complex columns
* Now my dataset is expanded into new columns, but it keep the complexity of the data
* There is no losse of informations 
* And choose number of epochs, same in every case

# Now my data types are changed from almost fully object types
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/data_types_object.png)

# To fully numerical (float and int)
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/data_types_numerical.png)

# Now i gonna scale my columns into range (0 - 1), it will help my model in training process

# Next i prepare the data for my model
* Then i create (train and test sets) and show the class imbalance
* And show how it affect the (f1 score), which is an important measurement

# Next i create function that will be a (Neural Net model) with simple 3 (Dense layers)
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/ANN_model_function.png)
* Then i compile my model with (adam optimizer)
* And i set the loss during training process
* Also i include evaluation in this function 
* The prediction and (classification report)
* This function will help me automatized all training and evaluation process

# I get my first model evaluation and (the accuracy is 0.7846) which is fine, but we can boost it
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/report_class_imbalance.png)
* The loss is low, it is (0.4490) which is also fine
* But we can see very high class disproportion (true and predicted are 0.86 and 0.54)
* This is bad sign, we are gonna try to reduce disproportion in both classes 

# First i gonna check number of the values in both classes of the (Churn)
* The first class (Yes) is obviously smaller (1869 samples to 5163(No) samples)

# Now i gonna use method (undersampling) to see how it affect the score of my model
* So first i equalize my (0 class) to the size of (1 class) and then concatenate them
* Next i create from them (train and test sets)
* When i check (value counts) in my train set there is no class imbalance
* I train my model with this sets and check (Classification Report)
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/report_under_sampling.png)
* We can see that the (accuracy is lower and loss higher)
* But in (f1 score measurement we reach similar results for both classes)
* This is a better model, trained on balanced dataset, my model is more reliable 

# Now i gonna do oversampling method
* So i fill my first class with samples, to make it equal as my (0 class)
* Now both calsses have (5163 samples)
* Then after creation of both sets, my (train set have 4130) and (test set have 1033)
* I gonna see how larger number of samples affect the model score
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/report_over_sampling.png)
* We can clearly see that more samples for training and evaluation affect positively the accuracy and loss
* Which are now (accuracy score to almost 0.80), that's higher than in my original model
* And the (f1 score is high 0.78 and 0.81 in both calsses)

# Now i gonna use (Smote over sampling method)
* This thechnic reproduce synthetic samples from (in our case) minority class
* I start from creating two sets (X smote and Y smote)
* And then creating from them (train and test sets), we can see that number of samples are same that in (oversampling method)
* Next i train my neural net with them and look at results
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/report_smote.png)
* We can see that (accuracy reaches 0.82) which are the highest from all of my models
* And loss also droped from (0.4583 in over-sampling to 0.4094)
* This is our greatest improvement at this point, the average accuracy is now (0.82)

# Next i gonna try ensemble method, i gonna split my data into three batches form our majority class
* So i create function to create this three batches and then concatenate them
* Then we create three models and we are gonna choose the majority vote, the average score
* And then i create function that will vote for the best model of them all
![](https://github.com/JakubTabor/Data_augmentation_imbalance_data/blob/main/Images/ensemble_final_report.png)
* There is no much improvement, only in average score there in no big spread

# The conclusion is that our best model is (Smote model), we reach the best f1 score 
* Average is not that important when there is class imbalance
* Our goal was to improve the (score for our class 1) and we reach (0.83) with smote tehnic



