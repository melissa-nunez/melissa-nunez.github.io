---
title: "Deep Phenotyping using K-means Clustering"
date: 2018-04-23
tags: [unsupervised learning, k-means, clustering, R]
excerpt: "Unsupervised learning for Deep Phenotyping"
header:
---

## Data

It is important to identify the drinking/smoking patterns of women during pregnancy in order to better understand the risk of possible postnatal outcomes.

For this project, I analyzed data from the Safe Passage Study, also known as the PASS study. This is a multi-center, prospective pregnancy cohort study that collected data from women living in the Northern Plains, US and Cape Town, South Africa. Both populations are at high risk for drinking and smoking during pregnancy. The goal of the study was to investigate the role of prenatal drinking and smoking on postnatal outcomes - specifically stillbirth and SIDS.

Because results may differ by site, the analysis was stratified. The sample size tables for each site are included.

Insert Sample size tables
<img src="{{ site.url }}{{ site.baseurl }}/images/Table1_SA.png" alt="" class="center">

Some participants did not have data for all three trimesters available. For this analysis, only those who did have all trimester data available were included.

## Clustering

Since the women demonstrate dynamic drinking and smoking habits, the first step was to define the exposure variable by clustering the women based on their drinking and smoking patterns. I accomplished this through the use of k-means clustering. There is also depression and anxiety data available for the women.  At the beginning of the study, each participant was given the Edinburgh postnatal depression scale questionnaire and a depression score was calculated. After some discussion, it was decided that a depression variable could be used for clustering as well. The data is longitudinal, therefore I used the 'kml3d' package in R to create trajectories. The variables used to cluster are

* Total Cigarettes Smoked Per Trimester
* Total Standard Drinks Per Trimester
* A "mood" variable made up of the women's fedinburgh, state anxiety, and trait anxiety scores

It was pre-determined that the number of clusters should be 4. Prior to clustering, we wanted to establish a "non-exposed" group. Therefore, those who did not drink or smoke throughout their pregnancy were considered non-exposed and were not included in the clustering. The cut off for the fedinburgh depression variable is 13, and for state and trait anxiety variables is 40. Those below the cut off are non-exposed (i.e not depressed). I included sample code for both the clusters and the visualization of varibles per cluster. The ggplot code is the same for both the drinking and smoking variables and per site.

```r
cld.joint.fedinburgh <- cld3d(pass.US.completers.fedinburgh[pass.US.completers.fedinburgh$Exposure ==
1,], timeInData = list(grep('TotCigsT',names(merge)),grep('TotalStdDrinksT',names(merge)),rep(181,
3)), time = c(1,2,3))
kml3d(cld.joint.fedinburgh,nbClusters = 4:9)
```

### South Africa

```r
ggplot(melt(pass.US.completers.fedinburgh[,c("patid","Cluster.TotalJoint",
cigvars)], id=c('patid','Cluster.TotalJoint')), aes(x=variable,y=value,
group=patid, colour=Cluster.TotalJoint)) +
ggtitle("Total Cigarettes for Joint Cluster") +
stat_summary(aes(y = value,group = Cluster.TotalJoint), fun.y=mean,
geom="line",size=2) +
scale_x_discrete(labels=c("T1","T2","T3")) +
facet_grid(. ~ Cluster.TotalJoint)
```
<img src="{{ site.url }}{{ site.baseurl }}/images/kml_SA.png" alt="" class="center"> <img src="{{ site.url }}{{ site.baseurl }}/images/kml_SA2.png" alt="" class="center">

### US

Insert US cluster ggplot
