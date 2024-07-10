---
title: "Optimization"
teaching: 25
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions 

- How is optimization used in machine learning?
- What sort of algorithms perform optimization?
- How can optimization be performed in Python?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Define various curve fitting algorithms
- Demonstrate how to train and use curve fitting models with the lmfit library.
- Demonstrate how to code and configure a genetic algorithm.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

Fitting accepts an objective function with some number of parameters, as well as a set of observations. The assumption is that the function correctly models the physical process behind the observed points. Fitting takes a guess-and-check approach, evaluating the basis function at one point, calculating the residual, and repeating until stopping criterea are reached.

::::::::::::::::::::::::::::::::::::: callout

Follow along by importing this notebook into Colab:

http://

::::::::::::::::::::::::::::::::::::::::::::::::

## Parameters

Parameters are floating point inputs to the objective function.

## Objective Function

The objective (or basis) function takes the Parameters object and produces a numerical output. The form of the objective function must rely on domain knowledge. If multiple objective function candidates exist, they will have to be fitted separately and the results compared. 

## Parameter constraints
Constraints allow parameters to be restricted to a range or formula.

::::::::::::::::::::::::::::::::::::: callout

## Sensitivity to Starting Values

That last model in this notebook section was terrible. Why? Because the starting values for all the Gaussian function's parameters were zero. Fitting functions will being their search around the location of the first values. If those first values are very far away from any maxima, the algorithm can give up before finding anything close to a solution.

::::::::::::::::::::::::::::::::::::::::::::::::

## Levenberg-Marquardt
The Levenberg-Marquadt algorithm is essentially a combination of gradient descent and the Gauss-Newton algorithm (itself an extension of Newton's method for non-linear functions.) It comes closer to the former the less improvement the last iteration made.

## Trust Regions
A trust region is an area where a simplified approximation of the objective function has been created. Initial steps are used to create the approximation, which is minimized, and the process repeats. They can be added to other methods such as generalized Lanczos (GLTR), which is an algorithm normally used in minimizing eigenvalues and eigenvectors. 

Constrained Optimization By Linear Approximation uses linear interpolation for its approximation of the trust region.

Powell's dog leg algorithm is similar to Levenberg-Marquadt. If the Gauss-Newton method and gradient descent both lead to a next step outside the trust region, the gradient descent solution is projected to the edge of the trust region. If the gradient descent is inside, the intersection between the line of the two solutions and the boundary of the trust region is used.

## Basin-Hopping
Basin-Hopping randomly perturbs all parameters and checks if the new solution was an improvement.

## Brute Force
The Brute force method creates a grid of points around the initial values, then tests every point.

## Dual Annealing
Simulated annealing is a hill climbing method, in which the probability that a new solution is accepted is proportional to its fitness, with the probability decreasing as a function of time. Dual annealing is a specific implementation.

## Conjugate Gradient
Conjugate Gradient is a numerical method for an analytical solution by choosing gradients in each direction. It is used in fitting by approximating only a of the conjugate directions.

## Nelder-Mead
In the Nelder-Mead algorithms for an n-feature function, n+1 candidates are chosen. The worst fitting candidate is replaced by the centroid.

## Newton
The Gauss-Newton method for linear regression can be used on its own.

## Simplified Homology Global Optimization
Simplified Homology Global Optimization (SHGO) samples multiple points in the optimization function, trying to find find a convex region which it can optimize on.

## Error Calculation
Certain of the above models will have their errors naturally calculated by lmfit.

It is possible to estimate errors for the parameters by taking the logrithmic posterior probability, over the distribution via Markov Chain Monte Carlo.

## Genetic Algorithms
One class of machine learning algorithms mimics the process of evolution. Differential evolution uses a genetic algorithm solve the curve fitting problem.

Genetic algorithms consider of a population of potential solutions to an optimization problem. Each one is encoded in the form of a genome (a list of features). Every genome in the generation is evaluated for fitness via some process. The generation is then transformed to produce a new generation of candidates. The algorithm repeats for some number of cycles or until a sufficiently high scoring solution is found or operates indefinitely in anticipation of changes to the environment which will require a new kind of solution.

## Fitness

The fitness function is a vital part of a genetic algorithm. Even in scenarios where the testing process for a member of the population is more complex than a simple function evaluation, the fitness function will be the ultimate decider of what constitutes a successful genome. 

## Selection

The first step in creating a new generation involves choosing the "parent" genomes from the previous generation which will contribute genes to the "child" genome in the current generation. Normally, two genomes are selected per child, but sometimes only one will be used or, conversely, three or more will.

A simple type of selection is Roulette Wheel. In this method, each genome in the previous generation has a chance to be chosen as a parent proportional to its normalized fitness.

## Crossover

When multiple parents are selected, the crossover mechanism controls how they contribute genes to the child. 

One point crossover is a simple type of crossover. All genomes are given a universal ordering of genes at the start of the algorithm. During crossover, a random point is chosen. The first parent contributes all genes before that point, while the second contributes all genes after it.

## Mutation

While the selection and crossover operators allow one generation to exploit information from previous generations, mutation allows the exploration of new areas of the solution space. Normally, a mutation rate is chosen and each child genome after crossover has the same percentage chance to undergo mutation. If chosen, a random gene is selected and its value is perturbed. The algorithm chosen for mutation may vary from gene to gene, such as a Gaussian probability curve about a floating point number or the random selection from a list of non-numerical values. It is desired, where possible, that mutation more heavily favors genes closer in value to the pre-mutation value. Mutation rate need not be static and can vary over the course of the optimization.

## Elitism
In order to avoid forgetting a superior solution, the results with the highest fitness can be copied directly into the next generation. 

## Steady State Selection
In steady state selection, the lowest n genomes are removed from the population and the highest n receive two copies in the next generation. The rest of the population is copied directly.

## Tournament Selection
In tournament selection, n genomes are chosen at random. One genome from that set is chosen with likelihood in proportion to the the genomes' fitness.

## K Point Crossover
One point crossover can extended to an arbitrary number of points. Each point chosen changes which parent contributes genes in that region.

## Uniform Crossover
In uniform crossover, each gene, or individual bits defining a gene's value, are selected at random from each parent.

