---
title: Computer vision project
publishDate: 2024-12-04 00:00:00
img: /assets/computer_vision.svg
img_alt: Title of the project with a motherboard background
description: |
  Can a model read handwriting as reliably as a human? We built a CNN that classifies handwritten digits with 98.3% test accuracy, and shipped it as an app you can test by drawing a number yourself.
tags:
  - Data Science
  - Neural Network
  - Python
---

### The Problem
Can a model read handwritten digits as reliably as a human? That's the practical question behind OCR and document digitization. We used the classic Kaggle "Digit Recognizer" dataset to answer it end-to-end, from raw pixels to a small app anyone can test by drawing a number themselves.

<img src="/assets/app_cnn.gif" alt="Interactive digit recognition demo: draw a digit, get a live prediction">

### The Data
42,000 handwritten digit images, each flattened into 785 columns: 784 pixel values (a 28x28 image, 0 = white to 255 = black) plus the true label. Before touching any model, we checked two things: are all 10 digits equally represented, and is each digit written consistently enough to be learnable?

<img src="/assets/distribution_digits.png" alt="distribution_digits">

Digit frequency turned out close to uniform (roughly 7.5% to 11% each), no obvious bias in how the dataset was built.

<img src="/assets/representation_number2.png" alt="number2">

<img src="/assets/variance.png" alt="number2">

Pixel variance per digit hinted at where the model would struggle: digit 2 has the highest variance (many different ways to write it), digit 1 the lowest (a very consistent shape). Digits 0, 3, 5 and 8 also showed above-average variance, an early signal of which digits would be easiest to confuse.

### Checking the Structure Before Modeling
Before training a supervised model, we tested something else: **without using the labels**, can the images naturally be grouped into 10 separate clusters? We ran K-means on the pixel data in R, combined with PCA for dimensionality reduction.

<img src="/assets/clustering.png" alt="number2">

The clusters for digits 2/7 and 6/9 overlapped the most, consistent with how visually close those shapes are, and a preview of where a classifier would likely make mistakes too.

### Why a CNN
We picked a Convolutional Neural Network (the AlexNet-style approach that won ILSVRC 2012) instead of a classical ML model because CNNs learn spatial features (edges, curves, loops) directly from pixels, instead of treating each pixel as an independent, unrelated feature. For handwriting, where the same digit can be shifted, rotated, or thicker/thinner, that spatial awareness matters more than raw feature count.

### Result
- **99.4%** accuracy on training data, **98.3%** on test data.
- Precision, recall and F1-score all at **0.983**, consistent performance across all 10 classes, not skewed by one easy digit.

### Shipping It
A model on paper isn't proof it works end-to-end. We exported it with Joblib to avoid retraining on every use, then wrapped it in a Gradio app: draw a digit on a canvas, get a live prediction from the CNN behind it.