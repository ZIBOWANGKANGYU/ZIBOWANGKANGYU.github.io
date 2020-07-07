---
title: "Demographic Characters and Access to Public Transit in Greater Vancouver"
date: 2020-07-10
tags: [GIS, python, transit]
header:
excerpt: "GIS, Python, transit"
---
# Abstract

Vancouver has one of the best pulic transit systems in North America. However, to what extent is access to public transit equiutable among residents in the metropolitan area? What demographic characters are related to differences in access to public transit? This project inrends to explore accessibility to Vancouver's public transit system across regions. I will use [GTFS data](https://gtfs.org/) on Vancouver's mass transit system as of June 6, 2020. 

This will be a series of blog posts and data visualizations. I will firstly explore the public transit data and present how public transit routes and stops are distributed geographically. I will then use the 2016 Census data to break the Greater Vancouer area into dissemination areas, and measure their access to public transit. I will then dig into 2016 Census data, espcially records about people's commute, trying to identify the gap betweem the demand and supply of public transit. 

The project folder can be found [here](https://github.com/ZIBOWANGKANGYU/Vancouver_transit)

# Static mapping

This static map shows the distance from each cell to the nearest road. Firstly, `dissolve` function of `geopandas` is used to combine multiple road geometries into one single multiple shape. Then, `nearest_points` of `shapely` is used to identify closet point on the roads shape that is closest to each cell (centroid used). I then used the `distance` method to calculate the minimum distances. 

I also calculated the weighted public transportation commuting time from each cell to the Railway Station. I calculated the centroid of each population cell, and got their commuting times by overlapping them with the travel time shapefile. Then I averaged average commuting time weighted by populaiton. 

The average public transportation commute time is 37.89 minutes

<img src="{{ site.url }}{{ site.baseurl }}/images/pythonDS/plots/static.png" alt="Static map: distance to road">

# Interactive mapping

I measured the convenience of public transportation by the ratio of public transportation commuting time to car commuting time. Then I used `bokeh` package to develop an [interactive](https://zibowangkangyu.github.io/pythonDS/accessibility_map_Helsinki) map showing this index. 

<img src="{{ site.url }}{{ site.baseurl }}/images/pythonDS/plots/interactive.png" alt="Interactive map: convenience of public transportation">