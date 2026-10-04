Then, either choose any currently active RGL devices or clear the background of the one in focus. A call to plot3d starts the plot with appropriately colored spheres.

```
plot3d(x=pwid,y=plen,z=swid,type="s",size=1.5,col=cols[slen.cols],
      aspect=(1.1,75,1),xlab="Petal width",ylab="Petal length",
      zlab="Sepal width")
```

You supply a vector of length 3 to the aspect argument, describing the relative lengths of the x, y, and z axes, in that order. By changing the order to 1.7, you're lengthening the y-axis relative to the others. This creates the stretched-out effect along the y-axis. The colors are assigned by vector indexing using the slen.cols factor vector, and xlab, ylab, and zlab are used to tidy up the axis titles.

Now, to add a vertical line from the x-plane to each observation, use its base counterpart, segments3d doesn doesn't separate the "from" and "to" coordinates into different arguments (recall the use of x0, y0, x1, and y1 in segments and arrows). it takes each pair of observations provided to the x, y, and z arguments to be the beginning and end of each line, in that order.

So, draw the vertical lines on the existing RGL device, you first need to set up these vectors containing a "from" location and a "to" location in the 3D space. Consider the following code:

```
xfromto <- rep(pwid,each=2)
yfromto <- rep(plen,each=2)
zfromto <- rep(min(swid),times=2*nrow(iris))
zfromto <- seq(2,length(zfromto),2)] <- swid
```

The first two lines set up the vectors for the x and y-components, xfromto and yfromto, respectively, by replicating each observation twice. These are easy, the "from-to" values don't change in these coordinate directions. The z-component does change, however. You create the zfromto vector by replicating the smallest width value, min(swid), by twice the size of the data set, so you have a vector that matches xfromto and yfromto in length. Every second position of zfromto is overwritten using the elements of the se width vector. This gives you "from" z values for all observations, min(swid), matched (in the pairwise fashion as required for segments3d) with the "to" z values in swid itself. with xfromto and yfromto, you'll end up with lines that go from the bottom x-y plane of the plot (the vertical position of which is automatically leveled at min(swid)) up to the actual swid value (which is of course the corresponding z value of each sphere).

Interactive 3D Plots 695