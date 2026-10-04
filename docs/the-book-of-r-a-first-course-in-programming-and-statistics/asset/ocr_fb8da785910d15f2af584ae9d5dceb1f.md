8. To draw lines connecting the coordinates in x and y, you use lines. Here you've also set lty to 4, which draws a dash-dot-dash style line.

```
R> lines(x,y,lty=4)
```

9. The ninth line of code adds the arrow pointing to the sweet spot. The function arrows is used just like segments, where you provide a "from" coordinate (x0, y0) and a "to" coordinate (x1, y1). By default, the head of the arrow is located at the "to" coordinate, (and other options such as the angle and length of the head) can be altered using optional arguments described in the help file?

```
R> arrows(x=8,y=14,lwd=11,y1=2.5)
```

10. The tenth line paints a label on the plot at the top of the arrow. As per the default behavior of text, string supplied as labels is centered on the coordinates provided with the arguments x and y.

```
R> text(x=8,y=15,labels="sweet spot")
```

As a finishing touch, you can add the label with the legend, which gives you the final product in Figure 7-6.

```
legend("bottomleft"
```

The first argument where the legend should be placed. There are various ways to do this (including setting x- and y-coordinates), but it often suffices to pick a corner using one of the four following character strings: "topleft","topright","bottomleft" or "bottomright". You supply the labels as a vector of character strings to the legend. Then you need to supply the remaining argument values in vectors of the same length so that the right elements match up with each label.

For example, for the first label ("overall process”), you want a line of type 4 with thickness and Color. In the first positions of the remaining argument values, you set pt.cex=NA,lty=4,col="black",lwd=1, and pt.cex=NA (all of these are default values, except for lty). Here cex refers to the cex parameter when calling points (using just cex in legend would expand the text, not).

Note that you have to fill in some elements in these vectors with NA when you don't want to set the corresponding graphical parameter. This is just to preserve the equal lengths of the vectors so R can track that parameter values correspond to each particular reference. As you work through this book, you'll see plenty more examples using legend.