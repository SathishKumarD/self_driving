#**Traffic Sign Recognition** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

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

[image1]: ./exploratory_analysis/1.png "Visualization"
[image12]: ./exploratory_analysis/2.png "Visualization2"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./examples/1.jpg "Traffic Sign 1"
[image5]: ./examples/2.jpg "Traffic Sign 2"
[image6]: ./examples/13.jpg "Traffic Sign 3"
[image7]: ./examples/27.jpg "Traffic Sign 4"
[image8]: ./examples/28.jpg "Traffic Sign 5"
[image9]: ./examples/35.jpg "Traffic Sign 6"

## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
###Writeup / README

####1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

###Data Set Summary & Exploration

####1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32x32x3
* The number of unique classes/labels in the data set is 43

####2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data ...

![alt text][image1]
![alt text][image12]


###Design and Test a Model Architecture

####1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because,
1) Most of the times color is not a decisive factor. There are no two signs with same edges but of different color.
2) Color information is most of the times noise. With 43 classes of data and few classes having as low as 200 examples, it is easy for the network to consider color as noise since the color distribution is not uniform.

I also clipped the dark images with bright spot was capped at 127 instead of 255 and did a contrast stretching.


As a last step, I normalized the image data to make sure the gradient is not going out of control.  

I decided not to generate additional data as the actual data with little pre processing and a small change in leNet Architecture.



####2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Greyscale image   					| 
| Convolution     		| 1x1 stride, valid padding, outputs 28x28x6 	|
| RELU					|												|
| dropout				|		keep_prob = 0.75						|
| Convolution 	     	| 1x1 stride, valid padding, outputs 24x24x6	|
| Max Pooling 	     	| 2x2 stride, outputs 12x12x6					|
| RELU					|												|
| Convolution	      	| 1x1 stride,  outputs 8x8x16					|
| Max Pooling  	     	| 2x2 stride, output 4x4x16						|
| Fully connected		| output 120   									|
| RELU 					|   											|
| dropout 				| keep_prob = 0.75								|
| Fully connected		| output 84   									|
| RELU 					|   											|
| Fully connected		| output 43   									|
 


####3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

I tried with several batch sizes like 128, 500, 1000. 128 gave the maximum accuracy
I noticed that 20 epochs gives the best validation accuracy(96 to 97%) without much overfitting (test accuracy was equally higher). To iterate faster, I kept it as 10 epochs as it was able to reach upto 96% accuracy.
I used adam optimizer and learning rate as 0.001. I tried using 0.0005 ( 25 epochs was not enough to reach above 93% accuracy). I also tried 0.05 ( reached 94% accuracy in two epochs but it was not stable)
Used keep probablity as 0.75. Tried 0.5 as well but there was no signifacnt change in the acuracy.



####4. 

For preprocessing 

My final model results were:
* training set accuracy of 99%
* validation set accuracy of 95.6% 
* test set accuracy of 92.5%

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?
Used leNet Architecture
* What were some problems with the initial architecture?
Accuracy was less than 90%
* How was the architecture adjusted and why was it adjusted? 
Added dropouts to avoid over fitting
Added one more convolutional layer
* Which parameters were tuned? How were they adjusted and why?
Epochs were changed
Added more dropouts
Learning rate was modified to see if it has any impact in the convergance rate
* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model?
Dropout layer increased the accuracy percentage from 86 to 93
Adding one more convolutional layer changed the validation accuracy from 93 to 96


###Test a Model on New Images

####1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8]

Out of 6 images three images were difficult to classify.
This was due to images having tree background.

####2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        		|     Prediction	        					| 
|:-----------------------------:|:---------------------------------------------:| 
| Speed limit (30km/h)      	| Speed limit (30km/h)  						| 
| Yield   						| Speed limit (60km/h)							|
| Speed limit (50km/h)			| Speed limit (50km/h)							|
| Pedestrians	      			| General caution					 			|
| Children crossing				| Right-of-way at the next intersection     	|
| Ahead only					| Ahead only  									|


The model was able to correctly guess 3 of the 6 traffic signs, which gives an accuracy of 50%. This is because the image I chose from the internet has various background noise.

####3. For the first image(Speed limit (30km/h) ), The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .65         			| Speed limit (30km/h)  									| 
| .12     				| Speed limit (100km/h)										|
| .11					| Speed limit (50km/h)											|
| .05	      			| Speed limit (80km/h)					 				|
| .03				    | Roundabout mandatory      							|





