# CaptionBot-Image-Caption-Generator
CaptionBot uses computer vision and natural language processing to generate captions from the image.

## Dataset:
[FLICKR_8K](https://forms.illinois.edu/sec/1713398).
This dataset includes around 8000 images along with 5 different captions written by different people for each image. The images are all contained together while caption text file has captions along with the image number appended to it. The zip file is approximately over 1 GB in size.

## Flow of the project
#### a. Cleaning the caption data
#### b. Extracting features from images using VGG-16
#### c. Merging the captions and images
#### d. Building LSTM model for training
#### e. Predicting on test data
#### f. Evaluating the captions using BLEU scores as the metric

![](images/dataset.PNG?raw=true)
<br>

## Steps to follow:

### 1. Cleaning the captions
This is the first step of data pre-processing. The captions contain regular expressions, numbers and other stop words which need to be cleaned before they are fed to the model for further training. The cleaning part involves removing punctuations, single character and numerical values.  After cleaning we try to figure out the top 50 and least 50 words in our dataset.

![](images/top50.PNG?raw=true)
<br>

### 2. Adding start and end sequence to the captions
Start and end sequence need to be added to the captions because the captions vary in length for each image and the model has to understand the start and the end.

### 3. Extracting features from images
* After dealing with the captions we then go ahead with processing the images. For this we make use of the pre-trained  [VGG-16](https://github.com/fchollet/deep-learning-models/releases/download/v0.1/vgg16_weights_tf_dim_ordering_tf_kernels.h5) weights.

![](images/vgg16.PNG?raw=true)
<br>

### 5. Merging the caption with the respective images
* The next step involves merging the captions with the respective images so that they can be used for training. Here we are only taking the first caption of each image from the dataset as it becomes complicated to train with all 5 of them. 

### 6. Splitting the data for training and testing
The tokenized captions along with the image data are split into training, test and validation sets as required and are then pre-processed as required for the input for the model.

### 7. Building the LSTM model
LSTM model is been used beacuse it takes into consideration the state of the previous cell's output and the present cell's input for the current output. This is useful while generating the captions for the images.<br>

### 8. Predicting on the test dataset and evaluating using BLEU scores
After the model is trained, it is tested on test dataset to see how it performs on caption generation for just 5 images. If the captions are acceptable then captions are generated for the whole test data. 

![](images/pred2.PNG?raw=true)
<br>


#### Good Captions

![](images/good.PNG?raw=true)
<br>

## Conclusion
Implementing the model is a time consuming task as it involved lot of testing with different hyperparameters to generate better captions. The model generates good captions for the provided image but it can always be improved.

## Use cases
* Some detailed usecases would be like an visually impaired person taking a picture from his phone and then the caption generator will turn the caption to speech for him to understand. Doctors can use this technology to find tumors or some defects in the images or used by people for understanding geospatial images where they can find out more details about the terrain.
