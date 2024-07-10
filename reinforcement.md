---
title: "Reinforcement Learning"
teaching: 5
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is reinforcement learning?
- How can reinforcement learning be performed in Python?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Demonstrate how to train and use reiforcement learning models with the stable-baselines library.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

Reinforcement learning consists of time steps, actions, and observations. During a time step, a model is given an observation. It then selects an action, which may be discrete or continuous. The cycle repeats, with the model learning the consequences of its actions via new observations. 

::::::::::::::::::::::::::::::::::::: callout

Follow along by importing this notebook into Colab:

http://

::::::::::::::::::::::::::::::::::::::::::::::::

## Environment

An environment consists of the code the model will interact with. A common pattern is to use a simulation environment during training, then switch to a real environment afterwards.

Environments consist of a set of actions which can be taken on them and one or more data points which are returned.

## Models

Neural networks are commonly used as the models in reinforcement learning. A common pattern is to train two models simultaneously, an actor model which makes decisions on what action to take and a critic model that learns a value function. This are similar to the explore/exploit divide in strategies between the selection/crossover and mutation operators previously seen in genetic algorithsm.

## Online Learning

Reinforcement learning differs from other machine learning algorithms in that it often makes use of continual updates to the model even in its final usage scenario. This is done so that it can learn a new environment after initial training or adapt to changes in the environment over time.