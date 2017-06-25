---
layout: post
title: R Markdown and Leaflet
author: Saul Cruz
tags: leaflet
type: post
published: true
status: publish
---
 

June 25 2017
Saul Cruz
 
## Objective
 
The objective of this post is to do an exploratory analysis of crime in Atlanta, Georgia. I recently moved to Atlanta from Houston, and found a very nitty tool called Leaflet, in this post I will show a simple use case of this library.
 
## Pre-requisites
 
install.packages(leaflet)
library(leaflet)
 
## Dataset
 
The dataset used for this exploratory analysis can be found in [University of Georgia Police Department ](https://moto.data.socrata.com/dataset/Georgia-Institute-of-Technology/nd8h-v3b5)
 
The last update was on May 10, 2017, it contains 10.4 K records
 
We use the  lubridate package to convert datetime fields
 

 
 
 
## Data Cleansing
These are the steps followed to clean the data, make it more readable and relevant. This is not feature selection since we're not predicting yet.
 
Since we are only interested in crimes which take place in Atlanta, we need to restrict the data set. As stated in Kahle & Wickham's [article](https://journal.r-project.org/archive/2013-1/kahle-wickham.pdf) To determine a bounding box, we use google maps to define the top and bottom boundaries (lats and lons), then we create the map using [qmap from ggmap package](https://cran.r-project.org/web/packages/ggmap/ggmap.pdf)
 

    atlanta<-data[-84.43743<=data$longitude & data$longitude<=-84.36238 & 33.70419<=data$latitude & data$latitude<=33.76848,]
 
 
## Exploratory Analysis using Leaflet
 

    crimeLatLong<-data.frame(lat=atlanta$latitude,lng=atlanta$longitude)
    crimeTitles<-atlanta$incident_type_primary
     
    crimeLatLong%>% 
      leaflet()%>%
      addTiles()%>%
      addMarkers(clusterOptions = markerClusterOptions(), popup = crimeTitles )

    ## Error in file(con, "rb"): cannot open the connection
 
 
##References
Coursera Week 2 (R Markdown) Product Development Tools
 
