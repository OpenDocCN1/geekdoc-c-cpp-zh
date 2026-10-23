
# Level Options

Click on a value in the legend to highlight it. Right-clicking on a highlighted legend shows the commands for the Colors and Markers palettes, which are identical to their Overlay equivalents in Figure 10.10. The commands affect only the highlighted level and its associated rows in the data table.

# Platform Options

After the charts appear, their drop-down menu has the following options.

- **Overlay** displays a single overlaid chart when the chart has more than one Y (statistics) variable. Each chart can have its own chart type, which can be overlaid. For example, the chart shown in Figure 10.12 has two overlaid variables, with one as a bar chart and one as a needle chart. When Overlay is not checked, the platform shows duplicate axis notation for each chart.

Figure 10.12 Different Chart Types

![](img/a858f3b35ed4923af65c22e8829ee5a8_184_0.png)

- **Vertical** changes a horizontal bar chart or a pie chart to a vertical bar chart.
- **Horizontal** changes a vertical bar chart or a pie chart to a horizontal bar chart
- **Pie** changes a horizontal or vertical chart into a pie chart.
- **Y Options** accesses the options described in “Single-Chart Options,” p. 182. These options affect the variable whose legend is highlighted.
- **Level Options** accesses the color, marker, and pattern palettes options described in “Level Options,” p. 184. These options affect highlighted bars.
- **Separate Axes** duplicate the axis notation for each chart when there are multiple charts. By default, the axis notation only shows for the last chart displayed if the charts are not overlaid. Separate Axes is only enabled on the menu when there are multiple Y variables that are not overlaid.
- **Script** has a submenu of commands available to all platforms that redo the analysis, or save the JSL commands for the analysis to a window or a file. (See “Script Submenu,” p. 66.)

# The Overlay Plot Platform

The Overlay Plot platform overlays numeric Y variables with a single numeric or character X variable. Optionally, the values of the X variable appear in ascending order, with points plotted and connected in that order.

The Overlay Plot platform has platform plotting options accessed by the popup menu icon on the Overlay Plot title bar. There is also a single-plot options menu for each Y variable, which show when the Y variable legend beneath the plot is right-clicked. The individual plot options are the same as those in the **Y Options** submenu at the platform level. When one of these options is selected at the platform level, it affects all plots in the report if no legends are highlighted. If one or more plot legends are highlighted, the options affects all those plots.

## Platform Options

Platform options affect every plot in the report window.

- **Overlay** overlays plots for all columns assigned the Y role. Plots initially appear overlaid with the **Connect Points** option in effect. When Overlay option is turned off, the plots show separately.
- **Separate Axes** lets the X axis scale values be printed only once, on the last plot in the window. When **Separate Axes** is selected, the X axes for other Y variables show tick marks but show no scale values.
- **Uniform Y Scale** makes the Y scales the same on grouped plots.
- **Connect Through Missing** connects adjacent points in the plot, regardless if there are missing values between them.
- **Range Plot** connects the lowest and highest points at each X value with a line with bars at each end.

  *Note:* The **Needle** option, described below, and **Range** option cannot be selected at the same time.
- **Y Options** has a submenu of options that apply to *all* variables and plots in the report window when selected from the main platform window. The section “Single-Plot Options,” p. 186, describes Y options for each individual variable.
- **Ungroup Plots** creates a separate chart for each level of a grouping variable
- **Arrange Plots** allows you to specify the number of plots in each row
- **Script** has a submenu of commands available to all platforms that redo the analysis or save the JSL commands for the analysis to a window or a file. (See “Script Submenu,” p. 66.)

## Single-Plot Options

Each Y variable is labeled beneath the plot, showing its name and symbol. Each Y variable’s plot can be modified by right-clicking on the variable name to bring up a menu.

- **Show Points** alternately shows or hides points.
- **Connect Points** is a toggle that alternately connects the points with lines. **Connect Points** can be activated when **Show Points** is not, allowing for greater flexibility in plot displays.
- **Needle** draws a vertical line from each point to the X axis.
- **Step** joins the position of the points with a discrete step by drawing a straight horizontal line from each point to the X value of the following point, and then a straight vertical line to that point. **Step**, without showing points, is illustrated in Figure 10.13.

*Note:* Only one of **Connect Points**, **Needle**, and **Step** can be chosen at a time.

# Figure 10.13 Overlay Step Plot

![](img/a858f3b35ed4923af65c22e8829ee5a8_186_0.png)

- **Function Plot** plots a formula (stored in the Y column) as a smooth curve. To use this function, store a formula in the Y column that is a function of a single X column. For example, the following column contains a formula involving the sine function. When used in an overlay plot, the function is plotted as a curve rather than individual points.

![](img/a858f3b35ed4923af65c22e8829ee5a8_186_1.png)

Note: Overlay Plot normally assumes you want a function plot when the Y column contains a formula. However, formulas that contain random number functions are more frequently used with simulations, where function plotting is not often wanted. Therefore, the Function Plot option is off (by default) when a random number function is present, but on for all other functions.

- **Connect Color** displays the standard JMP color palette (see Figure 10.10) for assigning colors to lines that connect points.
- **Overlay Marker** assigns markers to plotted points using the standard JMP marker palette (see Figure 10.10).
- **Overlay Marker Color** lets you select the color of the overlay marker.
- **Line Style** and **Line Width** let you adjust the appearance of the lines drawn on the plot.

The completed dialog is shown in Figure 11.1.

# Figure 11.1  Full-Factorial Example Response and Factors Panels

![](img/a858f3b35ed4923af65c22e8829ee5a8_190_0.png)

- 6. Click **Continue** to see Output Options panel. A full factorial design includes runs for all combinations of high and low factors for the five variables, giving 32 runs.
- 7. Click **Make Table**.

The design data table (Figure 11.3) contains a run for every combination of high and low values for the five variables. Since there are five variables, there are 2⁵ = 32 runs. This covers all combinations of a five factors with two levels each. Initially, the table has an empty Y column named Percent Reacted for entering response values when the experiment is complete.

The values in your table may be different from those shown below.

# Figure 11.2  2⁵ Factorial Reactor Data

![](img/a858f3b35ed4923af65c22e8829ee5a8_190_1.png)

To see the completed experiment and continue following this example, open the folder **Sample Data** that was installed when you installed JMP. Within this folder, open **Design Experiment > Reactor 32 Runs.jmp**.

# Figure 11.3  Reactor 32 Runs.jmp

![](img/a858f3b35ed4923af65c22e8829ee5a8_191_0.png)

Begin the analysis with a quick look at the data before fitting the factorial model.

- 1. Select **Analyze > Distribution**.
- 2. Highlight **Percent Reacted** and click **Y, Columns**. Then click **OK**.
- 3. Click the red triangle icon on the Percent Reacted title bar and select **Normal Quantile Plot**. The results are shown in Figure 11.4.

# Figure 11.4  Distribution of Response Variable for Reactor Data

![](img/a858f3b35ed4923af65c22e8829ee5a8_191_1.png)

Start the formal analysis with a stepwise regression. The data table has a script stored with it that automatically defines an analysis of the model that includes main effects and all two-factor interactions, and brings up the Stepwise control panel.

- 1. Click the red triangle icon next to the Fit Model script and select **Run Script**.
- 2. The probability to enter a factor (Prob to Enter) in the model should be 0.05.
- 3. The probability to remove a factor (Prob to Leave) should be 0.1.
