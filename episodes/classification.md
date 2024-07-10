---
title: "Classification"
teaching: 25
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions 

- What sort of algorithms perform classification?
- How can classification be performed in Python?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Define various classification algorithms
- Demonstrate how to train and use classification models with the Scikit Learn library.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

Classification is a kind of supervised learning in which labeled data points are used to train a model, then the model makes a prediction about the label of an unidentified new piece of data. 

::::::::::::::::::::::::::::::::::::: callout

Follow along by importing this notebook into Colab:

http://

::::::::::::::::::::::::::::::::::::::::::::::::

## Nearest Neighbors

The nearest neighbors algorithm calculates the distance between the unknown data point and each training data point, feature by feature and assembles a list of the top K closest training points. The probability that the unknown is of class X is equal to the percentage of the closest K neighbors which belong to class X.

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Nearest Neighbors by Hand

A data point is submitted to a 3 Nearest Neighbors classifier. The ten training data points are, by ascending distance from the unknown data point, of classes: class 3, class 2, class 2, class 1, class 1, class 2, class 3, class 1, class 1, class 1.

What is the probability that the unknown belongs to class 3? 


:::::::::::::::::::::::: solution 

## Answer
 
33.33...%

Of the three closest points, 0/3 were of class 1, 2/3 were of class 2, and 1/3 were class 3. Thus the model's confidence in the unknown belonging to class 2 is equal to 1 divided by 3. 

:::::::::::::::::::::::::::::::::

## Performance Measurement

Consider the sample dataset of iris flower characteristics and species provided by scikit-learn. The features of each data point are length of the sepal, width of the sepal, length of the petals, and width of the petals, while there are three species (setosa, versicolor, and virginica). In order to determine how well a classifier is performing, the available data is partitioned. One part will be used to train the classifier, then the rest will be classified by the trained model. The results of the model can then be compared to the known classes of the test data, showing how well the given algorithm can correctly identify unknown (to it) data points.

A confusion matrix bins each test data point according to both its true and predicted labels. A True Positive was correctly identified as belonging to the class, while a False Positive was incorrectly identified as belonging to the class. True Negatives and False Negatives are equivalent for data points identified as not belonging to the class. Many metrics can be calculated from these, such as accuracy:

$accuracy = \dfrac{TN + TP}{FN + FP + TN + TP}$

One particularly common metric is the F1 score:

$F1 = \dfrac{2*TP}{(2*TP)+FN+FP}$

## Decision Trees

Decision trees create a set of binary rules which partition the data. Unknown data points traverse the tree until they reach a leaf, at which point the proportion of members of a class in the training data also contained in that leaf node is the percentage confidence that the unknown is also a member of the class.

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 2: Decision Trees by Hand

A very simple decision tree has only one layer and one feature. It splits the feature at 5, such that anything less than 5 goes to leaf node 0 (containing 38 positive data points and 2 negative) and anything greater than or equal to 5 goes to leaf node 1 (containing 8 positive data points and 71 negatives). What is the confidence that a data point with feature 0 is positive?


:::::::::::::::::::::::: solution 

## Answer
 
95%

0 < 5, so the tree sorts it into leaf node 0. 38 out of the 40 training points in leaf 0 are positive. Thus, 38/40 = 0.95.

:::::::::::::::::::::::::::::::::

## Overfitting

You may have noticed that creatinga Decision Tree with 25 layers performed worse than only allowing 5. This is an example of overfitting. A model that approximates the training data too closely is susceptible to creating needlessly complex rules that will only apply to individual points in your training data.

## Ensemble Methods

In an ensemble method, many small classifier models are trained seperately. Unknown data points are submitted to each one in turn, and their results are aggregated either by having each one vote for the single best class and counting the proportion which voted for each class or by taking the average of the percentage confidence from each model for each class.

The AdaBoost algorithm trains classifiers sequentially. The first classifier is trained on the original training data. Then, each training point that is incorrectly classified by the current ensemble is given a higher weight and a new classifier is trained against the weighted training data. The process repeats until the ensemble is completed.

## Bayesian Classification

Bayes' theorem calculates the likelihood of an event given prior knowledge. Combined with a prior distribution describing your belief about the distribution of the data, it can be used to determine the probability of membership in a given class.

## Discriminant Analysis

Discriminent Analysis (either Linear Discriminent Analysis or Quadratic Discriminant Analysis) is an expansion of Bayesian classification. Gaussian Naive Bayes is equivalent to QDA when QDA's covariance matrices are diagonal and inputs are assumed conditionally independent from all classes. LDA is another special case, in which only one covariance matrix is used for all Gaussian distributions.

## Support Vector Machines

A Support Vector Machine (SVM) draws a hyperplane such that it separates the two classes and the parallels that touch the closest data point(s) of each class are maximally far away from it. Distance from the line correlates to probability of belonging to the class.

::::::::::::::::::::::::::::::::::::: callout

Why does the example SVM classifier have three lines in its output?

By the definition above, there should only be one line. In truth, most classification methods can only solve binary problems (ie ones with exactly two classes). Some, like Decision Trees, are inherantly able to process data with arbitrary numbers of labels. For the rest, we use an ensemble of models. The algorithm is repeated, considering only the training data from each pair of classes. To classify a new data point, we use all these as though they were classifiers in an Ensemble Method.

::::::::::::::::::::::::::::::::::::::::::::::::

Most real non-trivial cases will not be linearly seperable. For these cases, we use a kernel function which transforms the space in which classification occurs.

## Neural Networks

Neural networks take inspiration from the brain. A multi-layer perceptron is a series of nodes arranged in layers. Each layer of nodes takes as input all outputs from the previous layer. The initial features of the data point are the first "layer" of inputs. The final layer is a single node whose output is instead the final class label. Each node applies some weight to each input and sums them as its output.

Training a neural network involves experimenting with possible weight values for different nodes to apply to their inputs. That is, training a multi-layer perceptron is itself an optimization machine learning problem as in section five.

## Choosing Features

When there are very many features, restricting the model to only consider those which are most relevant to classification can improve performance in both classification accuracy and calculation time.

Alternitavely, you perform feature down-selection after training. Recursive feature elimination is an algorithm in which a trained model's features are compared to the model's predictions. The least important feature is removed from the training data and the process repeats until a specified number of features is left.

One method to determine the number of features for recursive feature elimination selects a set of features of every size, then performs cross-validation (splitting the available data into K bins, then performing K different sets of training and metric calculation in which each bin is used as test data once) on each and selects the feature set that performed best.

## Weighing Samples

Certain data points may deserve special consideration. They may contain measurements which are more certain or represent objects for which it is more critical for the model to classify correctly. Most classification algorithms allow training data to be assigned a weight in order to bias the model towards that sample.

## Outliers

Not all data is useful. Some data may be in error or represent unlikely edge cases.

Unsupervised Learning allows for the detection of clusters. Training data that is far from any cluster are potentially damaging to a model's performance. Identifying potential outliers in the training data and removing them before training can improve performance.

::::::::::::::::::::::::::::::::::::: callout

Before removing outliers, carefully consider how such unusual data points may have arisen.

Your domain knowledge will be crucial in this determination. Do the outliers violate well known laws of the domain or show artifacts characteristic of measurement errors? Conversely, is there some reasonable edge case to which the irregular data points could belong? The temptation to get a well performing model by potentially cherry picking data should be guarded against.

If there is a potential explanation, all is not lost. If removing flamingos and penguins from your dataset of birds allows for clean seperation of classes, you can dub that model a classifier for only birds capable of flight, then try to train a second one to recognize the label(s) of interest in flightless birds.

::::::::::::::::::::::::::::::::::::::::::::::::

A Local Outlier Factor classifier calculates the probability density of each data point's nearest neighbors. Points with unusually low probability may be considered outliers.

## Challenge 2: how do you nest solutions within challenge blocks?

:::::::::::::::::::::::: solution 

You can add a line with at least three colons and a `solution` tag.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Figures

You can use standard markdown for static figures with the following syntax:

`![optional caption that appears below the figure](figure url){alt='alt text for
accessibility purposes'}`

![You belong in The Carpentries!](https://raw.githubusercontent.com/carpentries/logo/master/Badge_Carpentries.svg){alt='Blue Carpentries hex person logo with no text.'}

::::::::::::::::::::::::::::::::::::: callout

Callout sections can highlight information.

They are sometimes used to emphasise particularly important points
but are also used in some lessons to present "asides": 
content that is not central to the narrative of the lesson,
e.g. by providing the answer to a commonly-asked question.

::::::::::::::::::::::::::::::::::::::::::::::::


## Math

One of our episodes contains $\LaTeX$ equations when describing how to create
dynamic reports with {knitr}, so we now use mathjax to describe this:

`$\alpha = \dfrac{1}{(1 - \beta)^2}$` becomes: $\alpha = \dfrac{1}{(1 - \beta)^2}$

Cool, right?

::::::::::::::::::::::::::::::::::::: keypoints 

- Use `.md` files for episodes when you want static content
- Use `.Rmd` files for episodes when you need to generate output
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
