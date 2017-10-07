#**Traffic Sign Recognition** 

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./hist.png "Distribution of traffic sign classes"
[image2]: ./pics/1.png "Picture 1"
[image3]: ./pics/2.png "Picture 2"
[image4]: ./pics/3.png "Picture 3"
[image5]: ./pics/4.png "Picture 4"
[image6]: ./pics/5.png "Picture 5"

## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
###Writeup / README

####1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it, and here is a link to my [project code](https://github.com/szokezsolt/CarND-Project2/blob/master/Traffic_Sign_Classifier.ipynb)

###Data Set Summary & Exploration

####1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32x32
* The number of unique classes/labels in the data set is 43

####2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the traffic signs are distributed among their 43 classes.

![alt text][image1]

###Design and Test a Model Architecture

####1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc.

As a first step, I normalized the pictures with zero mean and equal variance. Since the signs were already padded, that was all preprocessing I have done.

####2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model, MyNet consisted of the following layers, based on the LeNet architecture:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x16 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x16 				|
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 10x10x36 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x36 				|
| Flatten     | outputs 900x1x1
| Fully connected		| 900 --> 320        									|
| RELU					|												|
| Fully connected		| 320 --> 120        									|
| RELU					|												|
| Fully connected		| 120 --> 43        									|
| Softmax				|


####3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used Adam optimizer, 20 epochs, 256 batch size and 0.001 learning rate.

####4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model result had 94.1% validation accuracy.

The basics of the LeNet architecture was chosen. This has been proven to be ideal for simple image recognition purposes. The traffic signs were similar to the digits, however a bit more complex: 43 classes instead of 10 and I took also the colors into consideration. Due to the increased complexity, I was pointing towards a longer, 900x1x1 flattened tensor on the border of the convolutional and the fully connected layers. I also tuned the parameters on both sides of this to more reasonable values. The longer flattened tensor was the point at my experiment, when the accuracy drastically increased from a few percents to 80%+.
 

###Test a Model on New Images

####1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image2] ![alt text][image3] ![alt text][image4] 
![alt text][image5] ![alt text][image6]

All images might be difficult to classify because they are "sterilized" pictures, not realistic shots, like the ones in the training-validation set.

####2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set.

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| General Caution      		| General Caution   									| 
| Yield     			| Speed Limit 60km/h 										|
| Dangerous Curve to the Left					| Speed Limit 60km/h											|
| Ahead Only	      		| Speed Limit 60km/h					 				|
| Speed Limit 60km/h			| Speed Limit 60km/h      							|


The model was able to correctly guess 2 of the 5 traffic signs, which gives an accuracy of 40%. This is much less compared to the accuracy on the validation set of 94%.

####3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability.

For the first image, the model is relatively unsure that this is a general caution sign (probability of 0.29), and the image does contain a general caution sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .29         			| General Caution   									| 
| .48     				| Speed Limit 60km/h 										|
| .40					| Speed Limit 60km/h										|
| .51	      			| Speed Limit 60km/h					 				|
| .65				    | Speed Limit 60km/h      							|


Interestingly, all other predictions were speed limit 60km/h, relatively surely, however only one of them was correct. 
