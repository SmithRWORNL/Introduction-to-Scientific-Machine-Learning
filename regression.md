---
title: "Regression"
teaching: 25
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions 

- What sort of algorithms perform regression?
- How can regression be performed in Python?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Define various regression algorithms
- Demonstrate how to train and use regression models with the Scikit Learn library.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

Regression is a kind of supervised learning in which data points associated with numerical values are used to train a model, then the model makes a prediction about the value of an unidentified new piece of data. 

::::::::::::::::::::::::::::::::::::: callout

Follow along by importing this notebook into Colab:

http://

::::::::::::::::::::::::::::::::::::::::::::::::

## Linear Regression

In linear regression, a linear function is fitted to the data by reducing the residuals between the line and each training point.

## Performance Evaluation

Most performance metrics for regression focus on either the degree to which independent variables explain dependent variables or the residuals between predicted and actual values. The R2 value or coefficient of determination. A value of 1 indicates a perfect fit for the test data. A value of 0 performs equally well as ignoring the independent variables entirely and always guessing the mean of the test values.

::::::::::::::::::::::::::::::::::::: callout

Feature selection, data weighing, and outlier removal from classification can all apply equivalently to regression.

::::::::::::::::::::::::::::::::::::::::::::::::

## Ridge

The Ridge algorithm is linear regression with an added penalty for complexity, which is the square of the coefficients of the linear function. Bayesian Ridge uses a Gaussian prior for the distribution of possible coefficients instead.

## Polynomial Fitting

Fitting of polynomial data can be achieved, even using a linear regression model, by transforming the features into a Vandermonde matrix: [x, y] becoming [1, x, y, x * x, x * y, y *y].

## Kernels

A kernel function projects the space under consideration into a higher dimension, with the goal that a non-linear relationship be expressible linearly (eg by a hyperplane) within the higher dimensional space.

## Classifier Algorithms

Many classifier algorithms from the previous section can also be used for regression. Often, the equivalence is simply that the classifier is a special case where the classes are treated as values 0 and 1. Nearest neighbors, decision trees, ensemble methods, Gaussian process, support vector machines, and neural networks are all equally applicable to regression problems as they are to classification.

## Algorithmic feature selection

Previously discussed methods of feature selection consider the idea of removing features as a preprocessing step, providing the regressor with only features believed to be useful. Some regressor algorithms are instead designed such that they prefer sparse solutions to fitting the training data. That is, they tend to assign coefficients of zero or near zero during training, combining the feature selection and training steps into one. 

## Lasso
The Lasso algorithm is a linear model with a regularization term added.

## ElasticNet
ElasticNet is similar to Ridge, having two regularization parameters combined with a least squares linear regression

## Least Angle Regression
Least Angle Regression (LARS) begins with all coefficients in the linear model equal to 0. It increases the absolute value of the coefficient which most correlates with the label, until another coefficient has equal correlation to the residual, at which point it increases both. The process repeats until all features have been used. LARS can also be applied to fit other kinds of models, such as Lasso.

## Orthogonal Matching Pursuit
Orthogonal Matching Pursuit (OMP) is another forward feature selection algorithm like LARS. At each step, the residual is calculated orthogonal to the current model. The feature with the highest correlation to the residual is added to the set of chosen features. 

## Automatic Relevance Determination
Automatic Relevance Determination (ARD) is similar to Bayesiand Ridge, but replaces the spherical Gaussian prior with an elliptical Gaussian, with each feature having its own standard deviation.

## Multi-task Regression
Algorithms can be fitted to multiple values simultaneously, minimizing the combined residuals between the model output and each of the individual dependent variables.

::::::::::::::::::::::::::::::::::::: callout

## Multi-label Classification

Classification is also not relegated to learning a single label at once.

::::::::::::::::::::::::::::::::::::::::::::::::