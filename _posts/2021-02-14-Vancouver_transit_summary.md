---
title: "Public Transportation in Vancouver: Suggestions from Machine Learning Models"
date: 2021-12-1
tags: [GIS, python, transit]
header:
   image: "/images/Vancouver_photo4.jpg"
excerpt: "GIS, Python, transit"
---

For the Jupyter Notebook with full analysIs, please see [here](https://nbviewer.jupyter.org/github/ZIBOWANGKANGYU/Vancouver_transit/blob/master/Report.ipynb). The GitHub repo of this analysis is located [here](https://github.com/ZIBOWANGKANGYU/Vancouver_transit).  

A series of in-depth posts about this project include [data sources](https://zibowangkangyu.github.io/Vancouver_transit1/), [key variables](https://zibowangkangyu.github.io/Vancouver_transit2/), [machine learning modeling](https://zibowangkangyu.github.io/Vancouver_transit3/), and [model analyses and recommendations](https://zibowangkangyu.github.io/Vancouver_transit4/). 

The city of Vancouver [aspires to](https://vancouver.ca/files/cov/transportation-2040-plan.pdf) have 33% of its residents using public transportation to commute by 2040, and pledges to "advance new and improved" local and rapid transit. How can the public transit authority in the Greater Vancouver Area (GVA) best allocate its resources across the region to increase the number of residents using public transit? I gathered data from Canada's 2016 census and [TransLink](https://developer.translink.ca/servicesgtfs/gtfsdata) to analyze people's access to, and usage of public transit. Using Random Forest and LASSO regression models, I modeled the relationship between number of public transit services accessible and proportion of residents using public transit to commute. Then, I identified areas where a fixed amount of increase in transit access leads to the most increase in proportion of people using transit. These are the areas where GVA's new public transportation development should focus on. 

Putting resources into priority neighborhoods identified in the models instead of randomly selected areas, GVA can potentially see a significantly increased number of people using public transit. For example, if we target regions with a combined population of 100,000 and increase the number of transit services per capita in these regions and surrounding areas by 10%, we are expected to see 0.5 percentage point increase in proportion of people using transit, which translates into 500 more people using transit. By contrast, if we randomly select regions also with a combined population of 100,000, we are only expected to see 80 more people using transit.

The following chart shows percentage point increase of public transportation use, in average, as a function of population in the neighborhoods where GVA pours resources to increase the number of public transit services by 10%.

<img src="{{ site.url }}{{ site.baseurl }}/images/Vancouver_transit4/plots/X_2_percentage_point_increase_compare.png" alt="Chart: Scenario 2 PC Point Compare">

The following map highlights priority areas if GVA wants to target 10% of its neighborhoods, and increase the number of public transit services by 10%. 

<img src="{{ site.url }}{{ site.baseurl }}/images/Vancouver_transit_4_summary/plots/X_2_LASSO.png" alt="Map: LASSO Scenario 2">
