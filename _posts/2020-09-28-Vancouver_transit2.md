---
title: "Demographic Characters and Access to Public Transit in Greater Vancouver: Key Variables"
date: 2020-09-28
tags: [GIS, python, transit]
header:
   image: "/images/Vancouver_photo1.jpg"
excerpt: "GIS, Python, transit"
---
# Usage of public transit

Fortunately, Canada's 2016 census provides abundant information about residents' usage of public transit to the DA level. In the "Journey to Work" section, the numbers of residents falling into the following categories are provided:
- commuters (aged 15 or older, living in private housing)
- commuters using truck, car or van to go to work as drivers
- commuters using truck, car or van to go to work as passengers
- commuters using public transport
- people who walk to work
- people who cycle to work
- people who commute to work with other methods

As shown in the following chart, for most DAs, the majority of peole commute as drivers of private vehicles. However, there are a substantial number of DAs where around (or a little bit less than) half residents commute use public transit. For almost all DAs, only a tiny proportion of commuters bike, walk or use private vehicles as a passenger.

<img src="{{ site.url }}{{ site.baseurl }}/images/Vancouver_transit2/plots/DA_mode.png" alt="DA_mode">

Where do people use public transit the most? As shown in the followng map, the corridor along Highway 1A from Mount Pleasant through East Vancouver, Metrotown to New Westerminster see relatively high proportion of transit use. In addition, areas including Surrey, South Vancouver and Sunset also have relatively high proportion of people using public transit. 

<img src="{{ site.url }}{{ site.baseurl }}/images/Vancouver_transit2/plots/DA_public_prop.png" alt="DA_public_prop">

# Transit duration and destination

The census also tells us about people's transit destinations, and the average commuting time of different DAs. As shown in the following chart, people living in DAs in the west part of the metropolitan area spend relatively less time commuting, whereas people living in areas in the east, including Burnaby, Coquitlam and Surrey spend longer time in commute. 

<img src="{{ site.url }}{{ site.baseurl }}/images/Vancouver_transit2/plots/DA_commute_duration.png.png" alt="DA_commute_duration">



