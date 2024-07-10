---
title: "Using Google Colab"
teaching: 10
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do you use Google Colab to run code?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Demonstrate using Google Colab
- Show how to import a notebook from Github

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

For coding demonstrations, we will be using Google Colab notebooks. A notebook is a GUI environment in which Python code can be run. You can access Google Colab [here](https://colab.research.google.com/)

## Using Colab

Colab is much like Jupyter. Each cell in the notebook is contains a block of Python code. Clicking the cell to select it and then either pressing the triangular start button to the cell's left or typing ctrl + Enter will cause the code to run. Output will appear directly beneath the cell.

## Installing Packages

In addition to standard Python, Colab supports some custom instructions for interacting with the workspace in which the notebook is run. Of particular interest is the ability to install new packages:

`!pip install foo`

This line will install the package `foo` just as running pip from the command line would. When working with a notebook, you should generally run the cells in order the first time so that packages are installed and variables instantiated as the later cells expect. 

## Opening a Notebook

When you first enter Colab, and whenever you press ctrl + o, you will see the dialogue to open a notebook. You'll see a list of notebooks you have already used, but to open a notebook hosted on Github, click the Github link on the left hand side. Then copy and paste the link to the notebook in the provided box.

## Saving a Notebook Locally

If you want to run a notebook on your own computer instead of Google's servers, you can click File -> Download -> Download .ipynb. This is the same format used by Jupyter, and can be opened in your own Jupyter instance.

::::::::::::::::::::::::::::::::::::: keypoints 

- Press the start button at the left of a cell to run the cell's contents.
- Install packages with `!pip install (package name)`
- Import a notebook by pressing ctrl + o, selecting Github, and pasting the notebook's address.

::::::::::::::::::::::::::::::::::::::::::::::::


