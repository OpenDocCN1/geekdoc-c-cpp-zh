# # The Overlay Plot Platform

The Overlay Plot platform overlays numeric Y variables with a single numeric or character X variable. Optionally, the values of the X variable appear in ascending order, with points plotted and connected in that order.

The Overlay Plot platform has platform plotting options accessed by the popup menu icon on the Overlay Plot title bar. There is also a single-plot options menu for each Y variable, which show when the Y variable legend beneath the plot is right-clicked. The individual plot options are the same as those in the **Y Options** submenu at the platform level. When one of these options is selected at the platform level, it affects all plots in the report if no legends are highlighted. If one or more plot legends are highlighted, the options affects all those plots.

# ## Platform Options

Platform options affect every plot in the report window.

+   - **Overlay** overlays plots for all columns assigned the Y role. Plots initially appear overlaid with the **Connect Points** option in effect. When Overlay option is turned off, the plots show separately.
+   - **Separate Axes** lets the X axis scale values be printed only once, on the last plot in the window. When **Separate Axes** is selected, the X axes for other Y variables show tick marks but show no scale values.
+   - **Uniform Y Scale** makes the Y scales the same on grouped plots.
+   - **Connect Through Missing** connects adjacent points in the plot, regardless if there are missing values between them.
+   - **Range Plot** connects the lowest and highest points at each X value with a line with bars at each end.
+   
+     *Note:* The **Needle** option, described below, and **Range** option cannot be selected at the same time.
+   - **Y Options** has a submenu of options that apply to *all* variables and plots in the report window when selected from the main platform window. The section “Single-Plot Options,” p. 186, describes Y options for each individual variable.
+   - **Ungroup Plots** creates a separate chart for each level of a grouping variable
+   - **Arrange Plots** allows you to specify the number of plots in each row
+   - **Script** has a submenu of commands available to all platforms that redo the analysis or save the JSL commands for the analysis to a window or a file. (See “Script Submenu,” p. 66.)

# ## Single-Plot Options

Each Y variable is labeled beneath the plot, showing its name and symbol. Each Y variable’s plot can be modified by right-clicking on the variable name to bring up a menu.

+   - **Show Points** alternately shows or hides points.
+   - **Connect Points** is a toggle that alternately connects the points with lines. **Connect Points** can be activated when **Show Points** is not, allowing for greater flexibility in plot displays.
+   - **Needle** draws a vertical line from each point to the X axis.