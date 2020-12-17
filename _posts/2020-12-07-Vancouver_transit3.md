---
title: "Demographic Characters and Access to Public Transit in Greater Vancouver: Machine Learning Modeling"
date: 2020-12-07
tags: [GIS, python, transit]
header:
   image: "/images/shap.png"
excerpt: "GIS, Python, transit"
---

# Preprocessing

Now that we have tabular data of demographic characters, transit access and transit usage down to the DA level, I will pre-process the data so that it is ready to be put into machine learning algorithms. Firstly, columns with all NA data are removed (in fact there are two such columns). Then, I remove rows that have irregular, or extreme values for important variables, as shown in the following table:

| Removal Criteria                                                    | Number of DAs removed     |
|---------------------------------------------------------------------|---------------------------|
|DAs with zero population in 2016                                     |                         8 |
|DAs with zero land size in 2016                                      |                         1 |
|DAs with with land size 2 standard deviations above the mean         |                         8 |
|DAs with with population density 2 standard deviations above the mean|                        37 |
|DAs with with population density 2 standard deviations below the mean|                       165 |
|DAs without transit service or stops in the neighborhood area        |                        49 |
|DAs whose proportions of residents using transit are invalid (NAs)   |                         2 |

The following map shows in brown color DAs that have been removed from our next steps of analyses. 

<img src="{{ site.url }}{{ site.baseurl }}/images/Vancouver_transit3/plots/DA_removed.png" alt="Map: DA removed for analyses">