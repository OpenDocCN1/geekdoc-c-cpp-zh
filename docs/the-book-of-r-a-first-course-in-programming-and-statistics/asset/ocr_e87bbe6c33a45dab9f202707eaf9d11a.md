Let’s make that an R function by writing the following in the R editor:

```
normalize <- function(datavec){
  lo <- min(datavec,na.rm=TRUE)
  up <- max(datavec,na.rm=TRUE)
  datanorm <- (datavec-lo)/(up-lo)
  return(datanorm)
}
```

Based on a vector datavec as its only argument, normalize implements Equation (25.1), using the optional na.rm argument to ensure any missing values in datavec don’t contaminate the calculation of the minimum and maximum values (see Section 13.2.1).

Import normalize and enter the following, which shows the original non-writing handspan values (from the object surv you created earlier) and their corresponding normalized values (output snipped for brevity):

```
R> surv$NW.Hnd
  [1] 18.0 20.5 18.9 20.0 17.7 17.7 17.3 19.5 18.5 17.2 16.0 20.2
  [13] 17.0 18.0 19.2 20.5 20.9 22.0 20.7  --snip--
R> normalize(surv$NW.Hnd)
  [1] 0.50000000 0.72727273 0.58181818 0.68181818 0.47272727
  [6] 0.47272727 0.43636364 0.63636364    --snip--
```

Now, you need to create a new version of the color palette with colorRamp.

```
R> NW.pal2 <- colorRamp(colors=c("red4","yellow2"))
```

Generate the corresponding colors for each observation based on the normalized data.

```
R> ryc2 <- NW.pal2(normalize(surv$NW.Hnd))
```

If you actually look at the returned object in ryc2, you’ll note it’s a matrix of RGB triplets corresponding to each normalized value you supplied to your colorRamp function NW.pal2 (noninteger values end up being coerced to integers). These need to be converted to hex codes before you can use them in plotting. Using rgb just as you saw in Section 25.1.1, you get the vector you need (snipped for print).

```
R> NW.cols2 <- rgb(ryc2,maxColorValue=255)
R> NW.cols2
  [1] "#BC7700" "#D3AD00" "#C48A00" "#CEA200" "#B97000" "#B97000"
  [7] "#B66700" "#CA9700" "#C18100" "#B56500"    --snip--
```

Note the difference between the hex codes you obtain here in NW.cols2 and those in NW.cols. Here, you get a hex code for each unique value, but