---
title: "Deep Phenotyping using K-means Clustering"
date: 2018-04-23
tags: [unsupervised learning, k-means, clustering, R]
excerpt: "Unsupervised learning for Deep Phenotyping"
---

## Data

It is important to identify the drinking/smoking patterns of women during pregnancy in order to better understand the risk of possible postnatal outcomes.

For this project, I analyzed data from the Safe Passage Study, also known as the PASS study. This is a multi-center, prospective pregnancy cohort study that collected data from women living in the Northern Plains, US and Cape Town, South Africa. Both populations are at high risk for drinking and smoking during pregnancy. The goal of the study was to investigate the role of prenatal drinking and smoking on postnatal outcomes - specifically stillbirth and SIDS.


Because of the dynamic behavior of the women's drinking and smoking habits, the first step was to define the exposure variable by clustering the women based on their drinking and smoking patterns. I accomplished this through the use of k-means clustering. The data is longitudinal, therefore I used the 'kml3d' package in R to create trajectories. The variables used to cluster are "TotalCigsSmoked" per trimester and "TotalStandardDrinks" per trimester. It was pre-determined that the number of clusters would 4.

Next,

## Sample

Because results may differ by site, the analysis was stratified. The following tables

<img src="{{ site.url }}{{ site.baseurl }}/images/table1_SA.png" alt="">
