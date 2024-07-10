---
title: "Latent Variable Generation"
teaching: 5
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is latent variable generation?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Describe diffusion models

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

Latent variable generation calculates a full set of variables, given a sample of only some. Diffusion models perform this task for an image by relating observed noise to a prior distribution of images. This can be used to sample probable low frequencies of an image given the high frequencies, or a segment of an image given neighboring parts. 

## A Novel Area of Research

These models are still quite new and are an emerging area of technology. Generalized libraries for solving them are not available, and even libraries in areas where they are common (image and audio processing, text generation) are large, computationally expensive, and idiosyncratic. Usage in other scientific domains 