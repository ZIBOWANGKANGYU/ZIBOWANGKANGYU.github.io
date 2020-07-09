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

# Data

I used two main data sources for this project. Detailed information on Vancouver's mass transit system is obtained through [Open Mobility Data](https://transitfeeds.com/) in the GTFS form. Canada's [2016 Census](https://www12.statcan.gc.ca/census-recensement/2016/dp-pd/index-eng.cfm) data gives detailed informaion on the demographic characters of neighborhoods across the Greater Vancouver area. 

## GTFS Data

According to the [official website](https://gtfs.org/gtfs-background) of GTFS, it was originally known as Google Transit Feed Specification, a format of public transit data that is now used by urban transit agencies around the world. 

GTFS provides two types of public transit information, namely `Static` and `Realtime`. `Static` data, generally speaking, provides information on how the transit system are **plannd** to run in a period. By contrast, `Realtime` data gives information about how the transit system is **actually running** in real time. This project only uses the `Static` part of GTFS data.

There are various tables in the `Static` part of GTFS data. I mainly used five of them: `routes`, `shapes`, `stops`, `stop_times` and `trips`. 

- Routes

A route is a group of trips that are displayed to riders as a single service. There are 233 routes in Vancouver's public transit system, according to the data. Different modes of transportation are identified: Among all routes, 3 are subways, 1 is rail, 228 are buses, and 1 is ferry.

- Trips

A trip is a sequence of two or more stops that occur during a specific time period, adn one route usually has multiple trips. 122746 trips are identified in Vancouver: among them, route Expo Line has 4778 trips, which is the most among all routes, and route Dunbar/Downtown has 13 trips, which is the least among all routes.

As shown in the histogram below, each route has in average about 200 trips. Routes with more than 1,000 trips are rare.

<img src="{{ site.url }}{{ site.baseurl }}/images/Vancouver_transit/plots/stops_cnt_trips_hist.png" alt="Histogram: number of trips per route">

- Shapes

A trip is geographically linked with a shape, which describes the path that a vehicle travels along a route alignment. According to GTFS, stops on a trip should "lie within a small distance of the shape for that trip."

From the shape table, we can get more information on the length of each trip. For Vancouver, the median trip distance is 12.00 km. Route West Coast Express is 67.9 kms long, which is the longest route. Its map is presented below.

<img src="{{ site.url }}{{ site.baseurl }}/images/Vancouver_transit/plots/lines_max.png" alt="Histogram: longest route">

- Stops

GTFS defines stops as places where vehicles pick up or drop off riders. Vancouver 

- Stop-times


his static map shows the distance from each cell to the nearest road. Firstly, `dissolve` function of `geopandas` is used to combine multiple road geometries into one single multiple shape. Then, `nearest_points` of `shapely` is used to identify closet point on the roads shape that is closest to each cell (centroid used). I then used the `distance` method to calculate the minimum distances. 

I also calculated the weighted public transportation commuting time from each cell to the Railway Station. I calculated the centroid of each population cell, and got their commuting times by overlapping them with the travel time shapefile. Then I averaged average commuting time weighted by populaiton. 

The average public transportation commute time is 37.89 minutes

<img src="{{ site.url }}{{ site.baseurl }}/images/pythonDS/plots/static.png" alt="Static map: distance to road">

# Interactive mapping

I measured the convenience of public transportation by the ratio of public transportation commuting time to car commuting time. Then I used `bokeh` package to develop an [interactive](https://zibowangkangyu.github.io/pythonDS/accessibility_map_Helsinki) map showing this index. 

<img src="{{ site.url }}{{ site.baseurl }}/images/pythonDS/plots/interactive.png" alt="Interactive map: convenience of public transportation">