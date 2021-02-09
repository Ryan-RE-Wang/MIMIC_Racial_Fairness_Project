# MIMIC_Racial_Fairness_Project

This project is aim to find out bias contain in deep learning-based machine learning model, and remove such bias. 

Dataset we use is MIMIC-CXR, and there are about 220,000 frontal-viewed chest X-ray images. These images were done with histogram equalization, and removed the unnecessary parts in images. Hance, what we need to do is resize the images to 256*256 and store them into TFrecords, which is a data type provided by Tensorflow.

we use two method to define the bias in machine learning model

1. Use convolutional neural network (CNN) features of filters to train several classifiers for classifying 4 races
DenseNet121 is a CNN based model architecture, we remove the last layer of Dnet_disaese, and freeze Dnet_disaese to get 1024 features of CNN filters. We use these 1024 features to train several classifiers, such as k-nearest neighbor (KNN), logistic regression (LR), to classify 4 races.  We also use same training and testing set as Dnet_disaese and put images into Dnet_disaese to get 1024 features. 
After training and testing, we found that LR seems to be a better classifier for this task, LR significantly outperform KNN and performance shows in following figure. In this experiment, we found that when classifying 14 labels of diseases, the CNN filters would generate some features about race, which is the cause of racial bias.

![image]()

2. Train a DenseNet121 model to classify 4 races on MIMIC-CXR dataset
We use chest X-ray images to train a DenseNet121 based model, Dnet_race, to classify 4 races, and evaluate Dnet_race’s performance of classifying races as a benchmark. We use same set of training and testing as Dnet_disaese, and optimizer we use is Adam with categorical-cross-entropy loss for training 10 epochs and batch size is 32 images. Following figure shows the AUC score of classifying 4 races can achieve at least 0.732 for Hispanic/Latino, while at most 0.917 for Black/African American. The result shows that chest X-ray images contain racial characteristics, so that machine learning model can classify them.

![image]()
