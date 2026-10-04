
hex code created by the first line in the previous example and turns it into a 40 percent opaque version (the third line in the previous code):

```R
R> adjustcolor(rgb(cbind(255,0,0),maxColor=255), alpha.f=0)
[1] "#FF000066"
```

You briefly came across this command in Section 24.2.1, when creating a transparent gray confidence interval for a LOESS-smoothed trend using base R graphics. This approach is also applicable to hex colors generated after you have used a built-in or custom palette function to obtain a vector of colors.

You'll put opacity to the test using the built-in quakes frame, which consists of data on 1,000 seismic events near Fiji. Let's re-create the plot in Figure 13-6 on page 284 showing "number of detecting stations" against "event magnitude" and dress it up using color to identify the continuous "depth" data. Since there are many overlapping regions, reducing opacity of individual individuals would be a good idea for visualization. The code

```R
R> keycols <- c("blue","red","yellow")
R> depth.pal <- colorRampPalette(keycols)
R> depth.pal2 <- colorRamp(keycols)
```

sets up a custom three-color palette both ways (in other words, as a function expecting an integer, depth.pal, and as a function expecting a value between 0 and 1, depth.pal2 refers to Sections 25.1.3 and 25.1.4). Then, the following line uses the normalization approach, with the normalize function defined in Section 25.1.4, to obtain the appropriate colors for the points to be plotted, according to the "depth" variable of the data:

```R
R> depth.cols <- rgb(depth.pal2(normalize(quakes$depth)),maxColorValue=255,
alpha=0.6*255)
```

The request for 60 percent opacity is made through alpha in the call to R. You can create this plot with the following frame, which assigns the colors stored in depth.cols:

```R
R> plot(quakes$stations
```

This plot affords another opportunity to showcase the colorlegend function from the shape package. Assuming you have shape already loaded in the R session, the next line draws a corresponding color legend inside the plot region (on a default-size device):

```R
R> colorlegend(adjustcolor(depth.pal(20)
```

Here you can see another demonstration of the use of adjustcolor, where the color sequence generated with the call to depth.pal(20) is reduced to 60 percent opacity to match the plotted points. Again, posx and posy are set to use the position, and the optional argument left is set to TRUE to match the ticks and color legend labels appear on the left side of the strip. Figure 25-6 shows the final result.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_678_0.png)

Figure 25-6: Altering the color opacity in a custom palette, used to index the continuous "event depth" observations in a plot of "number of stations" against "magnitude" for the quakes data set, and a corresponding color legend using colorlegend from the shape package

## 25.1.7 RGB Alternatives and Further Functionality

RGB triplets aren't the only color can be represented in R. Other specifications include hue-saturation-value (HSV) and hue-chroma-luminance (HCL), available through the built-in hsv and hcl functions. These work in the same way as rgb, where you specify the strength of influence of the three components and out pop corresponding character hex codes that form valid R for any relevant plotting command. In fact, the HSV parameterization is what's used internally by the built-in palettes detailed in Section 25.1.2, using rainbow and heat-colors.

Contributed functionality offers even more flexibility. The colorspace package (Ihaka et al., 2015), which translates between different color formats, is worth noting, as is RColorBrewer (Neuwirth, 2014), which is based directly on the well-received color schemes by Cynthia Brewer (see http://colorbrewer2.org/). RColorBrewer provides more options for creating palettes than are supplied by the built-in functionality colorRampPalette and colorRamp. That said, from an introductory perspective, you should find the use of RGB and the base R functionality as discussed here sufficient for visual explorations of your data and models.

## Exercise 25.1

Ensure the car package is loaded. The Salaries data frame you looked at in Exercises 24.1 (page 622) and 24.2 (page 628) and take a look at the help file? $Salaries to remind yourself of the variables. Your task is to use color, point size, opacity, and point character type to reflect "years since Ph.D.," "sex," and "rank" in a scatterplot of "salary" over years of service, by completing the following steps:

- a. Set up a color palette that goes from "black" to "red" to "yellow2". Create two versions of this palette—one that expects a number of colors and one that expects a vector of normalized values between 0 and 1.
- b. Create two vectors that will control point character and character expansion following the guidelines in (i) and (ii). Each of these can be achieved in a single line by vector subsetting/repetition of the corresponding factor vector in the data frame.
- i. Use the point characters 19, 17, and 15 to reference the three increasing academic ranks in that order.
- ii. Use a character expansion of 1 for females and a character expansion of 1.5 for males.
- c. Use the normalize function defined in Section 25.1.4 to create a [0,1] normalized version of the range of values of the "years since Ph.D." variable. Use the appropriate palette from (a) along with rgb to convert these to the required hex codes.
- d. Modify the vector of colors you just created in (c), adjusting opacity. Colors in the vector that correspond to females should be reduced to 90 percent opacity; colors that correspond to males should be reduced to 30 percent opacity.
- e. Now, start the plot; alter the default figure margins to be 5, 4, 4, and 6 lines on the bottom, left, top, and right. Plot salary on the y-axis against years of service.
- f. Incorporate two separate legends following the guidelines in:
    - i. Place the first legend at x=-5 and y=0. It should use the levels of "rank" factor.
    - ii. Place the second legend at x=4 and y=0. It should show two points of type 19.
- g. Lastly, ensure the shape package is loaded and use the appropriate palette from (a) to reference "years since Ph.D." The tick marks should be a sequence in steps of 10. After this, my version of this plot is here:

![](img/b2cfc85cbb129f60fe595a2bae074fe4_680.png)

Your next task is a little different. The goal is to plot a standard probability density function but use color to shade in the curve to denote "distance from mean." To achieve this, complete the following:

- h. Generate a vector of 25 colors from terrain.colors and name it tcols. Then, using a reversed version of it obtained via25:1, append the two vectors together to form a new vector of length 50 containing the first 25 colors shading one way and the same 25 shading the opposite way.
- Next, create and store an evenly spaced sequence of exactly 51 values between -3 and 3 inclusive; name it vals. Use norm to calculate and store the corresponding 51 values of the normal density curve; name it normals.
- Draw the normal density curve by plotting the values in i) as a line (recall type="1"). In the same call to plot, use knowledge from Chapter 23 to set the x-axis and y-axis to be type "i"; suppress axis titles with empty strings; change the surrounding box to be an L shape; and suppress the drawing of the x-axis. Give the plot a suitable main title.
- To shade the colors underneath the curve, use a for loop, iterating through the integers 1 to 50. Each iteration, the loop should call polygon (refer to Section 15.2.3). Assuming your index is i, the vertices of each polygon should be formed by the vectors rep(c(i,i+1),2) and c(0,normals[(i,i+1)]). Each polygon should suppress its border and be colored according to the relevant ith in your color vector of length 50.
- Lastly, ensure the shape package has been loaded and use your length 50 color vector to produce a color legend with default placement to reference "distance from mean." You can easily set the zlim and zval arguments in the call to colorlegend using vals. Include an appropriate title for the legend. For reference, my result is here:

N(0,1) density

![](img/b2cfc85cbb129f60fe595a2bae074fe4_681_0.png)
