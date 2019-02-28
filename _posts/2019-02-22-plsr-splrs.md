---
title: "Exploring Associations Between Cortical Thickness and Subvolume Measures Using Partial Least Squares Regression and Sparse Partial Least Squares Regression"
date: 2018-10-14
tags: [neuroimaging, splsr, plsr, R, regression]
excerpt: "Applying partial least squares regression and sparse partial least squares regression to the Alzheimer's Disease Neuroimaging Initiative data to identify networks of correlations between cortical thickness measures and subcortical volume measures"
header:
---

### Introduction
Experts agree that Alzheimer's Disease is caused by abnormal buildup of beta-amyloid protein within the brain. The amyloid protein destroys brain cells and as Alzheimer's progresses, both the cortical and hippocampus shrink and ventricles are enlarged. Understanding the progression of the brain deterioration and the correlations of deterioration between parts of the brain is a crucial part of understanding where there is room for any possible remedy for patients. Brain atrophy, measured by MRI, and hypometabolism, measured by PET, are primary diagnostic biomarkers for Alzheimer's disease. Currently, the field is moving towards multi-modal brain imaging. Rather than using data from only one medical measure, such as MRI, Multi-modal analysis incorporates data from different medical tools including MRI, FMRI, PET, WMHI, and others.

The goal of this projects is to use data from the Alzheimer's Disease Neuroimaging Initiative (ADNI) and the Reference Ability Neural Network (RANN) study to explore correlations between the subcortical volume and cortical thickness structures of the brain for both sets of participants. Both of these measures are T1 images that come from MRI. Ultimately, I hope to expand the analysis to incorporate other measures, ideally WMHI data.

Partial least squares regression was used to identify significant cortical thickness predictors of subcortical volume.

### Data
The Alzheimer's Disease Neuroimaging Initiative (ADNI) is a multisite study that aims to improve clinical trials for the prevention and treatment of Alzheimer’s disease. Many techniques were used to study the participants such as MRI scanning, PET scanning, and neuropsychological tests. The Reference Ability Neural Network (RANN) Study collected similar data on cognitively normal young and old patients. ADNI participants consist of people diagnosed with Alzheimer's disease while RANN participants are healthy patients.

### Methods
Partial least squares regression (plsr) optimizes the latent components describing the global correlation of the images treated as multi-dimensional arrays. Essentially, this enables the model to identify significant correlations between voxels in images of different modalities. The model is allows for the user to choose the number of latent components that should be used. Part of my analysis includes calculating the optimal amount of latent components to be used for the model based on mean squared error of the predictions (MSEP).

My approach is as follows:

* Bootstrap the data 100 times
* On each data set, run the plsr model using 1 through 10 latent components (i.e. run the model 10 times for each dataset) where subcortical volume is the outcome and cortical thickness is the predictor. This is multivariate analysis - there are 50 subcortical volume variables and 68 cortical thickness variables.
* Using 5-fold cross validation, calculate the MSEP for each model and choose the optimal number of components based on that with the smallest MSEP
* Using the model with the optimal number of components (i.e. smallest MSEP), calculate the average of the beta coefficients for each variable across the different datasets
* Calculate the z-score for each beta coefficient and identify any significant Associations

### Summary Statistics for ADNI
Included are some summary statistics for the ADNI data:

<p align="center">
<img src="{{ site.url }}{{ site.baseurl }}/images/plsr_table1.png" alt="" align="middle">
</p>

Because these are patients with Alzheimer's disease, then it is understood that they are primarily old (>).

### Summary Statistics for RANN

###
