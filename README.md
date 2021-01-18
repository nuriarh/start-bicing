<p align="center">
  <a href="https://www.bicing.barcelona/">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a1/Bicing_logo.svg/1024px-Bicing_logo.svg.png" alt="Bicing" width="300" height="125">
  </a>
</p>

<h3 align="center">Occupancy Trends and Availability Prediction for Barcelona's Bike-Sharing System</h3>
<p align="center">By Núria Romero Herreros</p>
<p align="center">
  AllWomen Data Science Bootcamp Capstone Project
  <br>
  <a href="https://www.allwomen.tech/"><strong>Check their programs here! »</strong></a>
  <br>
</p>


## What's Bicing?

Since 2007 the city of Barcelona has been operating one of the largest bike sharing systems called [Bicing](https://www.bicing.barcelona/). Now, with about 6000 mechanic bikes and 1000 e-bikes distributed in about 400 station across the entire city, it's a 24/7 service with high demand, which makes a lot of sense - mild winters and no bad-weather in Barcelona :)

However, if you have ever tried to go to the beach on the bicing on a Sunday morning, once you finally arrive there, all the stations are likely full, and there’s a line of people waiting to return their bike. Believe me, that's pretty annoying! On the other hand, if you live in north-neighbourhoods of Barcelona, you will probably find your closest station completely empty - very easy to go down the hill but not the other way - uhum. Although there's a public service that collects and brings bikes from full stations to empty ones, the problem still remains there.

With the aim of improving the quality of the service and make it more reliable for the users, in this work I've tried to make predictions about the statuses of the stations of the public bicycle service in Barcelona using publicly available data applying Time Series Analysis and Random Forest Regression models. But, before that, I've deeply analysed and mapped the data in order to observe different patterns and behaviours of each station.

<p align="center">
  <a href="https://www.bicing.barcelona/nou-servei-bicing">
    <img src="https://www.maxpixels.net/static/photo/1x/Movement-Spain-Barcelona-Bicing-Urban-City-5402204.jpg" alt="Bicing" width="800" height="500">
  </a>
</p>


## Table of contents

- [Open Data BCN](#open-data-bcn)
- [Goal](#goal)
- [Project steps](#project-steps)
- [Outcomes](#outcomes)
- [Future improvements](#future-improvements)
- [References and inspiration](#references-and-inspiration)
- [Contact](#contact)
- [Thanks](#thanks)


## Open Data BCN

Open Data or Public Sector Information Openness is a movement driven by public administrations with the main objective of maximize available public resources, exposing the information generated or guarded by public bodies, allowing its access and use for the common good and for the benefit of anyone and any entity interested.

The [Open Data BCN](https://opendata-ajuntament.barcelona.cat/en) service, managed from the Department of Statistics and Data Dissemination of the Municipal Data Office, is transversal to several of the pillars of the city's strategy, is based on the main standards and international recommendations, adopting certain characteristics that summarize the principles of this movement: open data by default, quality and quantity of information, data for the whole world, data to improve governance and promotion of innovation.

The following datasets are the ones used in this project:
- [New Bicing stations status of Barcelona city](https://opendata-ajuntament.barcelona.cat/data/en/dataset/estat-estacions-bicing)
- [New Bicing stations information of the city of Barcelona](https://opendata-ajuntament.barcelona.cat/data/en/dataset/informacio-estacions-bicing)

The information available in these two datasets is about the current status of the stations: name, whether they are operating normally or not, number of bikes available, number of free slots, timestamp, etc (`first dataset`). This information is updated almost once a minute. This information has been split up into different datasets - one dataset per month (more than 3.000.000 samples per month!). I decided to analyse the month of October of 2019.
Besides the information about the bike system status, I accessed another source of data that contain information about the station itself: location, altitude, total capacity, etc (`second dataset`).


## Goal

There are two main objectives in this project:

- Bike stations occupancy trends: Exploratory data analysis and mapping of bike availability.
- Bike availability prediction: Number of bikes available and number of free slots are limited in each station. A prediction of the availability in each station may improve the system's reliability and increase its usage.


## Project steps

#### Data pre-processing: Cleaning and transformation of the raw data to make it suitable for future analysis and building predictive models.

Data cleaning (`drop of duplicates, check missing values`)
Converting timestamp into datetime (`month, day, day_of_week, hour, minute, second`)
Merging datasets
Feature selection

#### Exploratory data analyses and mapping: Performing initial analyses on the data to discover patterns. Mapping bike availability.

Mapping with folium (`marker clusters`)
Occupancy trends per station (`seaborn factorplot`)
Occupancy trends per station (`plotly scatterplot`)
Detecting those stations with persistent 0-bike availability and/or 0-free slots availability
Detecting rush hours with interactive maps (`density map with folium - time slice 20-minute interval`)
Animating intreractive maps (`bike availability map - green:full station, blue:almost full, yellow:bikes and docks available, orange:almost empty, red:empty`)
Creating gifs from frames
Dataset final selection for time series analysis and machine learning building models.

#### Model building:

Time Series Analysis: Time series methods are widely used to predict one-dimensional data.
· Stationarity analysis (select time period of interest, visualize target variable, creat box and whisker plots, decomposition of the time series data, autocorrelation function and partial autocorrelation function, rolling statistics)
· ARIMA model for weekly predictions (generate rolling predictions and results for each station)

Random Forest Regression: In complex environments, such as this one, there exist a high number of parameters which may have an impact on the system that is going to be studied. Considering multiple sources of data and different features can produce more accurate predictions.
· Variable taken into account: day, day of week, hour, is week day, is demonstration day.


## Outcomes

- Availability of bikes and free docks strongly depend on the hour of the day as well as on the altitude of the station.

- Some stations also show a big difference on the availability of bikes regarding if it’s a working day or not.

- Weekly predictions using ARIMA models have showed pretty accurate results for those stations that have a very similar pattern every week. However, the model doesn’t take into account variations such as protests or bank holidays.

- Similar problems have been noted when applying Random Forest Regression algorithms. However, this kind of models may improve their performance by adding external information such as weather prediction, close connections to other public transports, etc.


## Future improvements

- Perform Random Forest Regression with the following changes:
· Using data of a whole year for a specific station in order to detect other patterns such as seasonality within a year.
· Adding external information: Weather, good connection or not with other public transports, etc.

- Perform Random Forest Classification models: Instead of predicting exactly the number of bikes, we can classify the station in:
· Full
· Almost full
· Bikes and docks available
· Almost empty
· Empty
To do so we need a huge amount of data per station, so we would need to have at least one year of data in order to get a decent classification model.


## References and inspiration

 - https://opendata-ajuntament.barcelona.cat/en/
 - https://medium.com/@abhireddy/mapping-citi-bike-availability-during-rush-hour-b4d7cb9d1069
 - https://blog.prototypr.io/interactive-maps-with-python-part-1-aa1563dbe5a9
 - https://towardsdatascience.com/data-visualization-with-python-folium-maps-a74231de9ef7
 - "Predicting Occupancy Trends in Barcelona’s Bicycle Service Stations Using Open Data", Gabriel Martins Dias, Boris Bellalta and Simon Oechsner
 - https://github.com/inescsv/air_quality_madrid
 - https://github.com/shashankvmaiya/Bike-Sharing-Demand-Prediction
 - "Traffic Forecasting in Smart Cities", Juan Jose Vazquez Gimenez
 - "Sensing and Predicting the Pulse of the City through Shared Bicycling", Jon Froehlich, Joachim Neumann, Nuria Oliver
 - https://www.kaggle.com/rajmehra03/bike-sharing-demand-rmsle-0-3194
 - "Urban cycles and mobility patterns: Exploring and predicting trends in a bicycle-based public transport system", Andreas Kaltenbrunner, Rodrigo Meza, Jens Grivolla, Joan Codina, Rafael Banchs
 - http://bcnanalytics.com/visualizing-barcelonas-public-bikes-usage/
 - https://towardsdatascience.com/understanding-arima-models-using-valenbisi-valencias-bike-share-system-dcbe13b3e8a


## Contact

Please, reach me at nuria.romero.herreros@gmail.com for suggestions on how to improve the project and the code! I hope you enjoy this project as much as I did :)


## Thanks

I would like to say thanks to the [AllWomen Community](https://www.linkedin.com/school/allwomentech/) for giving me the opportunity to enroll in this [Data Science Bootcamp](https://www.allwomen.tech/academy/data-science-immersive-program/) and especially thanks to [Idoia Martí](https://github.com/idoiama), who helped me and spent countless hours assisting me and my classmates in our research, both in theoretical and practical work. And finally thanks to my wonderful classmates [Anna](https://github.com/amascasadesus), Núria, [Daria](https://github.com/dariaminsky), [Cynthia](https://github.com/CVPO), [Valeria](https://github.com/valtereshchenko), Maddie, [Oyi](https://github.com/oyidiyaoji), [Gina](https://github.com/gdiezve) and Cece. It's been an amazing experience!

