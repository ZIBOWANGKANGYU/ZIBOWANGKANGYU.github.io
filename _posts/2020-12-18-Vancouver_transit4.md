---
title: "Demographic Characters and Access to Public Transit in Greater Vancouver: Analyses and Recommendations"
date: 2020-12-18
tags: [GIS, python, transit]
header:
   image: "/images/Vancouver_photo3.jpg"
excerpt: "GIS, Python, transit"
---

# Feature importance

Both LASSO and Random Forest models give easy access to measurements of global feature importances. For LASSO model, I use the magnificence of coefficients to roughly estimate each variable's importance. For Random Forest model, I use the impurity measurement of each variable's importance.

In addition, the three types of input variables, namely categorical_features, numeric_features, and proportion_features are scaled differently in the preprocessing step. Therefore, I will review the important variables for all three categories separately.

## Categorical features

### LASSO Model

The table below shows the five categorical features that mostly strongly predict proportion of transit use among residents. They are ADA or CCS areas.

|     |         feature |   coeffs |
|----:|----------------:|---------:|
| 148 | ADAUID_59150117 | 0.097663 |
|   7 |  CCSUID_5915022 | 0.069961 |
|   8 |  CCSUID_5915025 | 0.065468 |
| 138 | ADAUID_59150107 | 0.053888 |
| 114 | ADAUID_59150082 | 0.048754 |

<img src="{{ site.url }}{{ site.baseurl }}/images/Vancouver_transit4/plots/output_16_0.png" alt="Map: high transit use categorical LASSO">


As shown in the map above, areas in the city of Vancouver tend to have high proportions of people using public transit.

<img src="{{ site.url }}{{ site.baseurl }}/images/Vancouver_transit4/plots/output_19_0.png" alt="Map: low transit use categorical LASSO">

Somehow unexpectedly, areas that most strongly predict low public transit use are also in the downtown area. They are distributed along Thurlow Street. It is important they are also in the CCS which predicts high transit use. In other words, these areas may have lower transit use than their immediate neighbors, but not necessarily compared to other ares in GVA.

### Random Forest Model

The table below shows the five categorical features that mostly strongly impact proportion of transit use among residents. They are CSD or CCS areas. It is worth noting that we cannot know the direction of impact from these impurity measures.

|     |         feature | impurity_importance |
|----:|----------------:|--------------------:|
|  18 |  CSDUID_5915022 |            0.008434 |
|   8 |  CCSUID_5915025 |            0.005865 |
|   2 |  CCSUID_5915001 |            0.004445 |
|   7 |  CCSUID_5915022 |            0.003664 |
| 148 | ADAUID_59150117 |            0.001297 |

<img src="{{ site.url }}{{ site.baseurl }}/images/Vancouver_transit4/plots/output_23_0.png" alt="Map: low transit use categorical LASSO">

If we can take a guess, however, areas in the city of Vancouver probably tend to have higher rates of transit use. By contrast, The east part of Langley city and Aldergrove probably have low transit use. We will know more details about each feature's impact later using SHAP.

For the Jupyter Notebook with full analyses, please see [here](https://nbviewer.jupyter.org/github/ZIBOWANGKANGYU/Vancouver_transit/blob/master/book/Model_analysis.ipynb). The GitHub repo of this analysis is [here](https://github.com/ZIBOWANGKANGYU/Vancouver_transit).  

