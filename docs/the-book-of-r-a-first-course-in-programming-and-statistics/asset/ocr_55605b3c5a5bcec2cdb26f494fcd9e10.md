is to calculate and visualize a density estimate of the same spatial earthquake data, but this time to do so based on the trivariate coordinates of longitude, latitude, and depth, in 3D space.

# Raw Data

First, let’s look at the raw observations. The following code creates a copy of the quakes data, extracting those three variables and rendering depth negative. I do this so that, when plotted, earthquake depth corresponds to moving down the vertical axis to give the impression of depth below sea level.

```
R> quak <- quakes[,c("long","lat","depth")]
R> quak$depth <- -quak$depth
```

In the usual rgl fashion, you create a point cloud of the raw data with the following:

```
R> plot3d(x=quak$long,y=quak$lat,z=quak$depth,
    xlab="Longitude",ylab="Latitude",zlab="Depth")
```

Figure 26-13 shows the result. If you spin the plot so that you’re looking down directly from the top with a bird’s-eye view, you’ll recognize the 2D spatial patterning that you’ve plotted already; see, for example, Figure 13-1 (page 265), Figure 23-1 (page 578), or Figure 25-12 (page 662).

![](bbox=[0.22, 0.6, 0.75, 0.88])

Figure 26-13: Viewing the 3D spatial dispersion of the earthquake occurrences—latitude, longitude, and depth