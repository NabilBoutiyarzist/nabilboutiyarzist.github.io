---
title: Computer vision project
publishDate: 2024-03-04 00:00:00
img: /assets/computer_vision.svg
img_alt: Title of the project with a motherboard background
description: |
  We have developed a neural network that detects handwritten numbers. In addition, we have created an application that allows users to write a number on a canvas, and we then detect what the user has written.
tags:
  - Data Science
  - Neural Network
  - Python
---

### Project Overview & Objectives 

We had a dataset of 42,000 images of handwritten digits, ranging from 0 to 9, our database consisted of 42,000 rows and 785 columns, with each row representing an image and the columns representing the pixels linked to the image, ranging from 0 to 255 (white and black images) and one column determining the number.

The idea will be to design the best possible handwritten digit recognition model, in order to determine with the greatest precision the digit to be expressed. 

To provide the best possible answer to this problem, we will proceed as follows: 
- Carry out a statistical analysis of the data at our disposal
- Design a clustering analysis to check whether our data can be broken down into 10 segments (digits 0 to 9).
- Designing a recognition model
- Design an interactive application where it will be possible to write a number and then make the prediction.   

---

### Technologies Used  
- **Python** (Pandas for data processing, ) 
- **Excel** (For the statistical analysis)
- **R** (For the clustering)

---

### Statistical analysis 

The idea here was to explore the dataset that we have to be sure that every number was well represented. 
First we measured the distribution of digit occurrences : 

<img src="/assets/distribution_digits.png" alt="distribution_digits">

We saw that the distribution of figures were relatively uniform, with each figure appearing with a frequency of between approximately 7.5% and 11%. No figure significantly dominates the others, which could indicate the absence of bias in the generation or selection of figures in the data source.

Next, we wanted to know if each digit was written in different ways, so as to detect as far as possible any digit with an “weird” representation (for the clever who want to fail our model with intentional unintelligible handwriting ^^)

Here's an example of different writing styles from number 2: 

  <img src="/assets/representation_number2.png" alt="number2" >

The visualization represents the average pixel variation for each digit (label) in our dataset. These values illustrate the average variability among images of each digit, revealing differences in digit representations.

  <img src="/assets/variance.png" alt="number2" >

Here are some key observations:
- Digit 2 has the highest average pixel variance, indicating that digit 2 images vary considerably in their representation.
- In contrast, digit 1 has the lowest average variance, suggesting that images of digit 1 are relatively more consistent or less varied in their representation.
- The digits 0, 3, 5, 8 also have relatively high variances, indicating a fair amount of variation in the way these digits are drawn.


### Clustering 

The aim of setting up a cluster is to ensure that the data can be broken down into 10 categories (0 to 9) **without the data labeling that we have.** We therefore need to use an unsupervised clustering algorithm. 

The clustering was build with R and we used the Kmeans algorithm.
The k-means method is an unsupervised clustering algorithm that aims to partition a data set into K distinct clusters. Each observation is assigned to the nearest cluster, based on the Euclidean distance between the observation and the cluster center, or centroid. These centroids are initially chosen at random, and the algorithm then iterates to optimize their position in order to minimize intra-cluster variance. The process continues until the centroids stabilize and the assignment of observations to clusters no longer changes significantly.

<img src="/assets/clustering.png" alt="number2" >

Principal component analysis (PCA) combined with the k-means algorithm provides us with a sophisticated tool for identifying the handwritten digits that are closest in terms of visual characteristics. For example, the analysis reveals a notable proximity between the clusters of digits 2 and 7, as well as between those of digits 6 and 9. 


### Convolutional neural networks

> History of the CNN method

*Computer vision competitions are held every year to evaluate and compare the performance of different algorithms and techniques in specific scenarios. In 2012, a revolution occurred at the ILSVRC, the annual computer vision competition, where a new Deep Learning algorithm broke all records! It's a convolutional neural network known as AlexNet. **This is the algorithm that we will use***

We won't explain how it works here, but we can simply say that it's a similar methodology to traditional supervised learning methods: they receive input images, detect features in each of them, then train a classifier on these images.

#### Results: 
We trained the model with a precision score of 99,4 % on the training data, and a score of 98,3 % on the test data. Classification performance was excellent, with precision, recall and F1 score all rated at 0.983. 

### Interactive application

The aim of the application was to design an application that would allow a user to write a number on a sketchpad and then submit it to our neural network to make a prediction. 

To do that, we have exported the model with JobLib (python library), in this case, it has enabled us to serialize our convolutional neural network model so that we don't have to retrain it each time we use it. 

In order to build our application, we used the Gradio library, which enables us to 
create user-friendly interfaces for machine learning models. 

Here an example of the app : 

<img src="/assets/app_cnn.gif" alt="number2" >