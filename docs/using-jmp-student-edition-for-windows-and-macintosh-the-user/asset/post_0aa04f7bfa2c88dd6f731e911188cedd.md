
## Figure 10.4 The Open Data File Dialog to Read a JMP table

![](img/a858f3b35ed4923af65c22e8829ee5a8_176_0.png)

## Macintosh

The Open window allows you to open any type of file into JMP. If you select a text document to open, the Open As menu appears in the window (see the next section for details on text importing).

![](img/a858f3b35ed4923af65c22e8829ee5a8_177_0.png)

## Importing Text Files

You import text by doing one of three things, depending on the operating system you are working with.

## Windows

Under Microsoft Windows,

Choose Text from the **Files of Type** drop-down list to import the data based on your current preferences.

Select the **Data With Preview** checkbox to see a preview of an incoming text file.

You then see the dialog shown in Figure 10.5 for specification of delimiters and other import details.

## Macintosh

On the Macintosh, select a text file to open. This displays the **Open As** menu in the lower part of the dialog. Then choose one of the three text commands:

- **Text** opens the file in a simple text editing window
- **Data (Best Guess)** opens the data in a format that JMP thinks is appropriate based on the contents of the file.
- **Data (Using Preview)** presents a dialog similar to the one shown in Figure 10.5, that lets you designate delimiters and other information, and shows a preview of the resulting data table.
- **Data (Using Preferences)** opens the file and uses default rules (set in the preferences panel) to interpret end of field and end of line delimiters to create a JMP data table

## All Platforms

JMP Student Edition attempts to discern the arrangement of text data. This is adequate for a rectangular text file with no missing fields, a consistent field delimiter, and an end-of-line delimiter

Note: If double-quotes are encountered when importing text data, JMP changes the delimiter rules to look for an end double-quote. Other text delimiters, including spaces embedded within the quotes, are ignored and treated as part of a text string.

The initial settings in the delimited import dialog are taken from the current Preferences file. The dialog also shows the column names, data types, and the first two rows of data. In Figure 10.5, preferences are set that indicate the incoming table contains column headers to be used as the column names; the column names are name, age, sex, and height. If no column names are indicated, the Name fields are called Column 1, Column 2, and so on.

One or more end-of-field delimiters, end-of-line delimiters, the option to Strip enclosing quotes, and the ability to set how many rows and columns will be read are additional options presented in the dialog.

## Figure 10.5 Import Text File

![](img/a858f3b35ed4923af65c22e8829ee5a8_178_0.png)

## Fixed-Width Text

If your data is fixed width (that is, each variable uses a set number of columns in the text file), click the Try Fixed Width button to specify the separations of each column to be imported.

## Importing Microsoft Excel Files

JMP Student Edition has the ability to directly import Microsoft Excel worksheets and workbooks under Macintosh and Microsoft Windows. Excel worksheet and workbooks are imported simply by choosing Excel Files from the Files of Type (Windows) or Enable (Macintosh) lists as shown in Figure 10.6.

Figure 10.6 Excel Open Choice

![](img/a858f3b35ed4923af65c22e8829ee5a8_179_0.png)

JMP Student Edition can also import Excel workbooks that contain several data tables inside them. After selecting Excel Files(*.xls) from the Open dialog and double-clicking on the desired workbook, JMP Student Edition opens all the worksheets in the workbook.

## Results from Platforms

The results from JMP Student Edition’s platforms can be cut and pasted into other programs using the system’s clipboard, through standard cut and paste facilities. To copy results into another program,

- Select the Selection tool ( ).
- Hold down the Shift key and click on each part of the report that needs to be copied. Note that axes frequently need to be selected in addition to the graphs they accompany.
- Select Edit > Copy.
- In the word processor, select Edit > Paste.

## The Chart Platform

The Chart platform computes and plots data and statistics about the data. Unlike the statistical platforms in JMP, the Chart platform is not intended as an exploratory device. It is used to report the results from other explorations. For that reason, the plots in the Chart platform do not “bristle with interactivity” to the degree that other platforms do. In essence, what is going to be reported should be known before the Chart platform is used.

To plot descriptions of data, complete the following steps after bringing up the Chart launch dialog (Figure 10.7)

Figure 10.7 Chart Launch Dialog

![](img/a858f3b35ed4923af65c22e8829ee5a8_180_0.png)

- Select the data column in the column list.
- Click the Statistics button (revealing the menu shown in Figure 10.8) and select the statistic to be charted.
- From the section labeled Options, use the drop-down list to select the orientation of the chart (vertical or horizontal) and the type of chart (bar, line, pie, needle, or point chart) to be generated.

Don’t worry too much about getting the orientation and chart type correct initially — they can be changed after the chart has been generated.

Optionally, include an X, Level column to be plotted on the horizontal axis, or a Grouping variable to generate separate graphs for each level of the column, either in separate windows or overlaid in the same window. Weight, Freq, and By options work as in other platforms.

Click OK.

An example bar chart, plotting the mean of Starch Content (%) using Method as Categories, X Levels is shown in Figure 10.9.

## Figure 10.8 Plottable Statistics

![](img/a858f3b35ed4923af65c22e8829ee5a8_181_0.png)

## Figure 10.9 Chart Example

![](img/a858f3b35ed4923af65c22e8829ee5a8_181_1.png)

Many of the options on the launch dialog can be changed using the platform popup menu. Platform options affect all charts in the report window. However, some options can be applied to individual charts.

## Single-Chart Options

To apply the following options to individual charts, right-click on a chart legend to see the popup menu shown in Figure 10.10. When this menu is accessed through a chart legend, the commands apply only to the individual chart. When accessed through the platform popup menu, without any legends highlighted, the commands apply to all charts.

Figure 10.10 Chart Options

![](img/a858f3b35ed4923af65c22e8829ee5a8_182_0.png)

- **Bar Chart** displays a bar for each level of the chart variables. The default chart is a bar chart.
- **Line Chart** replaces a bar chart with a line chart and connects each point with a straight line. Choose the **Show Points** option to show or hide the points.
- **Needle Chart** replaces each bar with a line drawn from the axis to the plotted value.
- **Point Chart** shows only the plot points, without connecting them.
- **Show Points** toggles the point markers on a line or needle chart off and on.
- **Connect Points** toggles the line connecting points on and off, leaving a point chart.
- **Std Error Bars** overlays needles at plus or minus one standard error from the mean.
- **Overlay Color** assigns color to a variable to identify it when overlaid with other charts.
- **Overlay Marker** assigns plot points a marker to identify them in overlaid charts.
- **Overlay Pattern** assigns bars a fill pattern to identify them in overlaid charts.
- **Pen Style** allows the choice of a line style from the palette shown in Figure 10.10.

## Frame Options

Frame options allow control of the plot frame’s elements as a whole.

Figure 10.11 Frame Options

![](img/a858f3b35ed4923af65c22e8829ee5a8_183_0.png)

- **Background Color** colors the background of the plot with the color chosen from the JMP Student Edition color palette.
- **Marker Size** allows selection of the marker from a palette of six point sizes that range from dot to very large. The **Preferred Size** is set in the **Preferences.** The marker size applies to the plot point and its associated rows.
- **Marker Drawing Mode** lets you adjust the way markers are drawn. Fast mode is useful for graphs with large number of points, so that they re-draw quickly after adjustments. Outlined mode is often used in presentations.
- **Border** lets you turn border lines on or off.
- **Size/Scale** allows changes in axes and plot frames. **X Scale** is only active on platforms where the X axis is numeric (the X axis for the Charts platform is categorical). **Y Scale** shows the standard axis scale dialog, which can also be shown by double-clicking in the Y axis. The axis scale dialog allows the specification of the maximum, minimum, increment, and tick marks for the axis, and draws tailored reference lines or a grid on the plot. The **Frame Size** command displays a dialog to enter the exact pixel size for the plot frame.
- **Add Graphics Script** displays a text entry box to enter JSL commands, usually to tailor the graphics output in ways not provided with commands and options. See the *JMP Scripting Language Guide* for documentation of JSL commands.
- **DisplayBox** lists the commands to conveniently select and deselect the plot area, and redraw the plot.
