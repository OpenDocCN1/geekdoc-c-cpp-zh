```
{
  series.Points[pointIndex].CustomProperties += "Exploded=true";
}
}
```

Code file [OnClickDataPointsSample.aspx] available for download at Wrox.

Setting either the PostBackValue or the LegendPostBackValue of a series will initiate a postback when the series' data points (or any legend item associated with the series) is clicked. The code in Listing 16-14 sets these properties to #index so that the data point index is posted back when the click event is set to Chart_1's OnClick event parses the postback to obtain the index of the data point, clicked and sets the Exploded custom property of the slice clicked to true. Figure 16-14 shows what happens when you click on the Tumumble slice.

![](bbox=[0.53, 0.25, 0.93, 0.53])

FIGURE 16-14: A slice of the doughnut chart is

You can also click on the legend items to explode the appropriate data point slice.

# Interactivity With Ajax

Ajax (Asynchronous JavaScript and XML) is a group of interrelated web development techniques used on the client-side to create interactive web applications. Ajax, web applications can retrieve data from the server asynchronously in the background without interfering with the display and behavior of the existing page.

This section explores how easy it is to combine a chart's interactivity features with Ajax to improve the user experience.

> This chapter is definitely not about Ajax and related techniques. You can read a more detailed overview about Ajax and its improvements in .NET Framework 4.0 in Chapter 19. Chapter 20 introduces you to the Ajax Control Toolkit. This chapter only examines a few examples that may wet your appetite, but definitely won't present you with the full menu Ajax offers.