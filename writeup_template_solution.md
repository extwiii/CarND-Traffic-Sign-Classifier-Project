# **Traffic Sign Recognition** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/extwiii/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

I added an exploratory visualization of the data set inside the code. Please see [project code](https://github.com/extwiii/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)


### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because one dimensional model better and easier than three dimensional RGB color pictures.

Here is an example of a traffic sign image before and after grayscaling. Please see [project code](https://github.com/extwiii/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)


As a last step, I normalized the image data because it makes every value between 0 and 1


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Gray image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x6 	|
| RELU					|							tf.nn.relu					|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 				|
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 10x10x16 	|
| RELU					|							tf.nn.relu					|
| Max pooling	      	| 2x2 stride,  outputs 5x5x16 				|
| Flatten	    | From  5x5x16 to 400   				|
| Fully connected		| shape=(400, 120)        									|
| RELU					|							tf.nn.relu					|
| Fully connected		| shape=(120, 84)       									|
| RELU					|							tf.nn.relu					|
| Fully connected		| shape=(84, 43)      									|
| One Hot				| tf.one_hot(y, 43)        									|
|	Cross Entropy			|	tf.nn.softmax_cross_entropy_with_logits											|
|	Loss_operation				|				tf.reduce_mean(cross_entropy)								|
|	Optimizer				|				tf.train.AdamOptimizer(learning_rate = rate)								|
|	Training_operation				|				optimizer.minimize(loss_operation)							|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

-To train the model, I used an tf.train.AdamOptimizer and my metrics were like below;
* EPOCHS = 30
* BATCH_SIZE = 300
* mu = 0
* sigma = 0.1
* rate = 0.008

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 0.99008593095
* validation set accuracy of 0.916468735121
* test set accuracy of 0.942176879263


If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?
- I simply used LeNet architecture and the reason I picked because during the CNN class we implemented same architecture, so easy to implement.
* What were some problems with the initial architecture?
- Different dimensions
* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.
- I kept layers as it is just changed epochs and batch size to see differences
* Which parameters were tuned? How were they adjusted and why?
- I also changed Learning Rate
* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model?
- CNN works because we are using images, if we use text we would use completely different model.

If a well known architecture was chosen:
* What architecture was chosen?
- LeNet
* Why did you believe it would be relevant to the traffic sign application?
- We used same architecture for hand-written digits
* How does the final model's accuracy on the training, validation and test set provide evidence that the model is working well?
- I passed the minimum level :) Over 90% for all level.
 

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

Please see [project code](https://github.com/extwiii/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

The last image might be difficult to classify because similar to right or left sign.

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Stop      		| Stop   									| 
| No entry     			| No entry 										|
| General caution					| General caution											|
| 30 km/h	      		| 30 km/h				 				|
| Ahead only			| Ahead only     							|


The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100%. This compares favorably to the accuracy on the test set of German traffic signs.

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

All images, and their probabilities;

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 1.00      		| Stop   									| 
|  1.00     			| No entry 										|
|  1.00					| General caution											|
|  1.00	      		| 30 km/h				 				|
|  1.00			| Ahead only     							|

 ### Rating :full_moon::full_moon::full_moon::full_moon::full_moon::full_moon::full_moon::full_moon::full_moon::full_moon:
### Difficulty :full_moon::full_moon::full_moon::full_moon::full_moon::full_moon::full_moon::full_moon::full_moon::full_moon:

### Bilal Cagiran | [E-Mail](mailto:bcagiran@hotmail.com) | [Github](https://github.com/extwiii/) | [LinkedIn](https://linkedin.com/in/bilalcagiran) | [CodePen](http://codepen.io/extwiii/) | [Blog/Site](http://bilalcagiran.com) | [FreeCodeCamp](https://www.freecodecamp.com/extwiii)



