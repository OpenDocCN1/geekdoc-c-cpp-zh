When shadows are displayed for any chart element, you can also smooth the shadows by setting the Chart.IsSoftShadows property to True.

Figure 14-42 shows the effect of anti-aliasing with a zoom factor of two.

![](bbox=[0.143, 0.187, 0.796, 0.526])

FIGURE 14-42: Using anti-aliasing with text and graphics

The top part of the figure turns off antialiasing options, while the bottom part turns them on.

# Axes and Related Chart Elements

You can customize the appearance and behavior of axes belonging to your chart. A ChartArea instance contains a property called Axes that is an array of Axis. The definition of Axes suggests that you can read and write this property, but you should use it as read-only. You can index the element of Axes with the AxisName enumeration, which has values summarized in Table 14-7.

TABLE 14-7: Values for the AxisName Enumeration

| VALUE | DESCRIPTION | POSITION FOR BAR AND STACKED CHARTS | OTHER CHARTS |
|---|---|---||
| X | Primary X-axis | Left vertical axis | Bottom horizontal axis |
| Y | Primary Y-axis | Bottom horizontal axis | Left vertical axis |
| X1 | Secondary X-axis | Right vertical axis | Top horizontal axis |
| Y1 | Secondary Y-axis | Top horizontal axis | Right vertical axis |