---
title: "Overview of Machine Learning"
teaching: 10
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is machine learning?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain the general concept behind machine learning
- Show how to pose scientific questions in a format amenable to machine learning
- Learn the categories of machine learning algorithms

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

Machine learning algorithms tackle problems in two, possibly cyclical steps. 

 1. `Training` involves the input of new information into the algorithm. This data is used to create or update a `model` which stores the state of the algorithm's knowledge. 
 2. `Output` is the process by which an algorithm utilizes the information in the model to make some type of decision, such as providing a label to a new data point or enacting some change upon the environment.
 
## Defining Expected Outputs

In order to choose a fitting machine learning algorithm for your application, it is neccesary to have a firm idea of what precisely is sought as an answer the model can provide in a given situation. Possibilities include:

 1. A label for an unknown data point.
 2. A numerical rating for some quality of an unknown data point.
 3. An input which will optimize (or at least provide a high value for) some well defined metric.
 4. An action to take given a current environment.
 5. Plausible values for missing sections of a piece of data.
 
Just because a problem does not fit perfectly into one of these categories at first glance, that does not mean that machine learning techniques are a lost cause. For example, determining the likelihood of a hypothesis can be considered an example of case 1. The set of data points are a given kind of hypotheses and relevant evidence and the potential labels are "true" and "false." 

## Defining Inputs

Once you've determined what precise output you can expect from your machine learning algorithm, you can begin defining what data is available to feed into it as input. Consider the following formats:

 1. Numerical quantities.
 2. Values out of a set.
 3. A graph of relationships between nodes.
 4. Image data.
 
Of the four, only numerical and qualitative features are easy to combine in one model.

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Defining inputs and outputs

You have a database of XY data read off a given instrument for a variety of different liquids. You want to leverage this data to automatically identify unknown liquids which have been analyzed by instrument. What will your inputs and outputs be? When will you train your model?

:::::::::::::::::::::::: solution 

## Output
 
Your inputs numerical data. How much data you use will be something you will likely experiment with as you develop your process. You may bin the data into exactly 100 numbers based on the average of 100 equally sized regions of the x axis, for example. 

Your outputs will be a label identifying the unknown liquid as belonging to a class. Depending on your scenario, labels may be an explicit chemical formula, or you may have multiple models that detect individual classes. For an example of the latter, you may decide to train one model to recognize the labels "contains ethanol" versus "does not contain ethanol" or perhaps the three labels "contains ethanol" versus "contains nitrogen" versus "contains sodium".

You will only train your final model once. You will probably wind up training many times over the development of your software, as you ascertain what produces the best results for your particular problem, but by the end you will have a model which you trained only once, using all of your available data. That model will then be used repeatedly to assign labels to all future unknown samples as you conduct multiple experiments with your instrument. Any new training would be done irregularly, such as when you expand your database of data available for training.

:::::::::::::::::::::::::::::::::


## Challenge 2: Defining inputs and outputs

You are tasked with configuring many servers, each with the same software installed and with load balancing being used so that each one has roughly the same amount of requests being sent in. You want to provide high quality service, meaning that requests are replied to promptly and that service is not interrupted. Reconfiguration is expensive, requiring a server to be rebooted, and thus you are only allowed to do it once a day at midnight when the servers are not being used. What are your inputs and outputs? When will you train your model?

:::::::::::::::::::::::: solution 

Your inputs will be a set of configuration options for your software. Some of these will be numerical (eg the number of seconds before a request times out) while others will be qualitative (eg whether a certain kind of optional buffering is to be used.) 

Your output will be a decision as to what input will maximize performance. This will require a mathematical definition of what you consider "performance" to entail. This may be a formula of the average time each user waits for their request to finish, with a large penalty added to this average for each minute the server spends unavailable. (That is, you would prefer a server that takes a long time to process requests over a server that keeps crashing.)

Training will occur every night. Since you have the ability to redeploy and try new inputs only at midnight, it makes sense to perform training every night, using the previous day's performance data to learn more about what makes a well configured server.

:::::::::::::::::::::::::::::::::

## Challenge 3: Defining inputs and outputs

You are writing software for a drone equipped with atmospheric sensors and a GPS. It is intended to fly around a forested area for a day, searching for concentrations of environmental pollution. You want the drone to stay in the forest, to search as much of the forest as possible, to spend extra time in areas of pollution to obtain more detailed readings on these areas of interest, and to return to you before the day ends (when it will run out of energy.) What are your inputs and outputs? When will you train your model?

:::::::::::::::::::::::: solution 

Your inputs will be the readings from the sensors, the GPS, and the time. All will be numerical data. Because the actual size and shape of the true deployment location and test location(s) will likely differ, it will be important to ensure the GPS data is scaled to a position relative to the area's boundary.

Your output will be a decision for whether the drone should move and, if so, in what direction and at what speed.

Training will likely occur over several test flights over one or more areas. It may be neccesary to use fake sensors to emulate the detection of pollution if real pollution can't be found for a test. The entire training flight may even take place in simulation, model learning on solely emulated data before ever being given control of a physical machine.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Categories of Machine Learning

Machine learning algorithms are broadly broken down into three categories. These determine the broad class of question a given algorithm is intended to address. These categories are:

 1. `Supervised Learning` is used for labeling problems or calculating numerical values. A set of training data is prepared, with each item being assigned a label for what class it belongs to or a number by a human. A model is trained on this data, then used to predict the class or value of new points. This is referred to as `classification` when the labels are qualitative and `regression` for numerical values.
 2. `Unsupervised Learning` contrasts with supervised learning in that training data points are not given any labels or values. The model is left to define one or more groups of data based solely on how similar data points are to each other during training. The model will then predict new data points as belonging to one group of data. It is up to the user to determine what the semantic meaning of a group is, if such information is desired.
 3. `Reinforcement Learning` exposes the model to an environment made up of variables. The algorithm then makes some choice(s) and calculates the utility of its new state. This process repeats in a loop, allowing the model to learn which actions produce positive outcomes in which scenarios. Optionally, at some point updates to the model may be halted, locking in its current knowledge and preventing new situations from altering what it has learned.

::::::::::::::::::::::::::::::::::::: keypoints 

- Precisely defining what data you can provide a model and what you expect to get out of it are key to algorithm selection.
- Supervised Learning accepts data points and labels/values as training data and returns a label/value.
- Unsupervised Learning accepts data points as training data and returns a group of data points.
- Reinforcement Learning accepts data from an environment and a utility function and returns an action to perform.

::::::::::::::::::::::::::::::::::::::::::::::::
