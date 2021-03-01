---
title: "Combating America's Other Infodemic"
date: 2021-3-1
tags: [python, regressions, COVID-19]
header:
   image: "/images/Infodemic.png"
excerpt: "python, regressions, COVID-19"
---

This projects won the First Place Prize at 2021 West Coast Regional Datathon sponsored by Citadel and CItadel Securities and Correlation One. The GitHub repository of this project can be found [here](https://github.com/Twenty-One-Spring-Citadel-WestCoast/Datathon). I am honored to have worked with three fantastic team members [Ben](https://www.linkedin.com/in/ben-huckell/), [Jason](https://www.linkedin.com/in/jskzhou/) and [Peter](https://www.linkedin.com/in/zhipeng-peter-ye/).

The submitted version of the report can be downloaded [here](https://github.com/Twenty-One-Spring-Citadel-WestCoast/Datathon/raw/main/team_2_report.pdf).

## Summary: misconception, misinformation and COVID-19 pandemic control

Since the beginning of the pandemic, governments and technology companies around the world have prioritized combating false information about the COVID-19, along with public health measures, to ensure that people take adequate caustion and change their behavior to slow down the spread of the virus. In this project, we demontrated strong statistical relationships between people’s increased physical mobility and worse outcomes of COVID, as measured by infection, hospitalization and death at the state level. Moreover, we discovered that the incorrect information problem to COVID-19 containment turns our to be broader than misinformation from social or traditional media and extends to a lack of basic knowledge about the cause, spread and prevention of COVID-19 (misconception). Misconception is associated with higher non-essential mobility and worse disease outcomes.

Based on our models, we identified US states where, by geographic and demographic characters, where people are most vulnerable to the COVID-19 misconception or misinformation. We believe that the dissemination of correct information to people who are not necessarily exposed to much misinformation from the media, but nonetheless have more misconceptions about the basics of COVID-19.

## Data source, preprocessing and EDA

We confine the time span of this study from March 2020 to January 2021. 

### Physical mobility

We use people's physical movement at non-residential venues as a measurement of compliance to pandemic containment policies in the population. Google has made public datasets on movement of people available since February 15, 2020 to help combat COVID-19. As shown in the map below, states in Southern US, along with New York and small states in the northeast saw the most dramatic drop in non-residential mobility, By contrast, states in the northwest saw little change, or even increase in non-residential mobility. 

<img src="{{ site.url }}{{ site.baseurl }}/images/infodemic/plots/Mobility_change.png" alt="Map: Mobility change">

It turns out that in addition to differences in strictness of government policies and levels of compliance, Google Mobility data should also be used along with temperature and urbanization rate to get a more accurate picture. The baseline data was taken in January/February 2020, and residents of northern and colder states are naturally more stagnant during the winter months, and are thus more likely to be more mobile in the summer period. In addition, rural and urban residents also show different movement patterns.

### Misconception and exposure to misinformation