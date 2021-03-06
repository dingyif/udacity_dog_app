# Dog Breed Classifier App in Pytorch

This is the repository for second project of Udacity Deep Learning Nanodegree
The code is implemented with Pytorch librabry.
Udacity Provided the Starter Code and the original repo is [HERE](https://github.com/udacity/deep-learning-v2-pytorch/tree/master/project-dog-classification).

[//]: # (Image References)

[image1]: ./images/sample_dog_output.png "Sample Output"
[image2]: ./images/vgg16_model.png "VGG-16 Model Layers"
[image3]: ./images/vgg16_model_draw.png "VGG16 Model Figure"


## Project Overview

Welcome to the Convolutional Neural Networks (CNN) project in the AI Nanodegree! In this project, you will learn how to build a pipeline that can be used within a web or mobile app to process real-world, user-supplied images.  Given an image of a dog, your algorithm will identify an estimate of the canine’s breed.  If supplied an image of a human, the code will identify the resembling dog breed.  

![Sample Output][image1]

Along with exploring state-of-the-art CNN models for classification and localization, you will make important design decisions about the user experience for your app.  Our goal is that by completing this lab, you understand the challenges involved in piecing together a series of models designed to perform various tasks in a data processing pipeline.  Each model has its strengths and weaknesses, and engineering a real-world application often involves solving many problems without a perfect answer.  Your imperfect solution will nonetheless create a fun user experience!


# Brief Summary of what I did:

## - Build Own CNN using Pytorch with the structure below. 
1. Convolutional Layer <br />
(conv1) nn.Conv2d(3,16,kernel_size= 3,stride=1,padding=1) <br />
(relu)  nn.ReLU() <br />
(pool1) nn.MaxPool2d(2,2) <br />
(conv2) nn.Conv2d(16,32,kernel_size=3,stride=1,padding=1) <br />
(relu)  nn.ReLU() <br />
(pool2) nn.MaxPool2d(2,2) <br />
(conv3) nn.Conv2d(32,64,kernel_size=3,stride=1,padding=1) <br />
(pool3) nn.MaxPool2d(2,2) <br />
2. Fully Connected Layer <br />
 Flatten the image <br />
(fc1) nn.Linear(28*28*64,1024) <br />
(relu)nn.ReLU() <br />
(dropout) nn.Droupout(0.2) <br />
(fc2) nn.Linear(1024,133) <br />

### For Loss and Optimizer choices:
I choose the Loss to be CrossEntropy Loss and SGD with momentum as my Optimizer. The random guess of prediction is **0.75%**, and with only 10 epochs of training my model reached performance of **11%**. I believe with long enough epochs, this will reach a decent accurarcy.

## Transfer Learning
I selected the **VGG16** pertrained framework and changed the last layer of 1000 into 133 classes, and with just 8 epochs of retrain the classificaiton layer the accuracy of the model reached **85%** on test dataset. It performed extremely well compared to the CNN from scratch.

## Model Evalution:

I randomly selected few photos from website to test the model. Here're some results:

![dog1](./images/dog_result_1.png)
![dog2](./images/dog_result_2.png) 
![dog3](./images/dog_result_3.png)
![Human1](./images/human_result_1.png)
![Human2](./images/human_result_2.png)

# Suggestions from Udacity:

1. Consider using transforms.Resize(256) and transforms.CenterCrop(224) instead of RandomResizedCrop for train dataset also.
The reason is RandomResizedCrop crop the image from random (centre, corner etc) so it might miss the face of dogs <br />
2. CNN from scratch:
   - Consider using Batch Normalization after each convolution layer (number of conv layer = number of batch normlization layer)
   - Consider using ELU or LEAKY_RELU activation function
   - Consider adding weight initialization parameter in conv2d operation
   - Set Dropout rate between 0.4-0.5
3. Transfer Learning:
   - Try experiment with Inception and Xception net which is more power than VGG and Resnet



## Project Instructions

### Instructions

1. Clone the repository and navigate to the downloaded folder.
	
	```	
		git clone https://github.com/udacity/deep-learning-v2-pytorch.git
		cd deep-learning-v2-pytorch/project-dog-classification
	```
	
__NOTE:__ if you are using the Udacity workspace, you *DO NOT* need to re-download the datasets in steps 2 and 3 - they can be found in the `/data` folder as noted within the workspace Jupyter notebook.

2. Download the [dog dataset](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/dogImages.zip).  Unzip the folder and place it in the repo, at location `path/to/dog-project/dogImages`.  The `dogImages/` folder should contain 133 folders, each corresponding to a different dog breed.
3. Download the [human dataset](http://vis-www.cs.umass.edu/lfw/lfw.tgz).  Unzip the folder and place it in the repo, at location `path/to/dog-project/lfw`.  If you are using a Windows machine, you are encouraged to use [7zip](http://www.7-zip.org/) to extract the folder. 
4. Make sure you have already installed the necessary Python packages according to the README in the program repository.
5. Open a terminal window and navigate to the project folder. Open the notebook and follow the instructions.
