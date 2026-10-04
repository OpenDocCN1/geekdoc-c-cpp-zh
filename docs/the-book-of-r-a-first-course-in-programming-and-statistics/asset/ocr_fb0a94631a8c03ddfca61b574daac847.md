# 13.1.3 Univariate and Multivariate Data

When discussing or analyzing data related to only one dimension, you're dealing with univariate data. For example, the weight variable in the earlier example is univariate since each measurement can be expressed with one component—a single number.

When it's necessary to consider data with respect to variables that exist in more than one dimension (in other words, with more than one component or measurement associated with each observation), your data are considered multivariate. Multivariate measurements are arguably relevant when the individual components aren't as useful when considered on their own (in other words, univariate quantities) in any statistical analysis.

An ideal example is that of spatial coordinates, which must be considered in terms of at least two components—a horizontal x-coordinate and a vertical y-coordinate. The univariate data—for example, the x-axis values only—aren't especially useful. Consider the quakes dataset (like chicks is automatically available through the datasets package), which contains observations on 1,000 seismic events recorded off the coast of Fiji. If you look at the first five records and read the descriptions in the help file quakes, you quickly get a good understanding of what's presented.

```
R> quakes[1:5]
lat long depth mag stations
1 -20.62 181.62 562 4.8 41
2 -20.62 181.03 650 4.2 15
3 -26.00 184.10 42 5.4 43
4 -17.97 181.66 626 4.1 19
5 -20.42 181.96 649 4.0 11
```

The columns lat and long provide the latitude and longitude of the event, depth provides the depth of the event (in kilometers), mag provides the magnitude on the Richter scale, and stations provides the number of observation stations that detected the event. If you're interested in the spatial dispersion of these earthquakes, examining only the latitude or the longitude is rather uninformative. The location of each event is described with two components: a latitude and a longitude value. You can easily plot these 1,000 events; Figure 13-1 shows the result of the following code:

```
R> plot(quakes$long,quakes$lat,xlab="Longitude",ylab="Latitude"
```