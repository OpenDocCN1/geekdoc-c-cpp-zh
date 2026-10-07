
PATTERN2 VALUE=R1 COLOR=BLUE;
RUN;
QUIT;

The added SUBGROUP= statement. This tells SAS to color the bars for each subgroup using a different color. The PATTERN2 statement specifies the color for males because the patterns are assigned in alphabetical order.

![](img/6113440fee6085d6edba5f406f541c12_420_0.png)

- 4. Run the program and observe the output. Note that the bars for each GENDER are now in different colors. The PATTERN remains the same because of the VALUE=R1 specification in both PATTERN statements.

- 5. Change the statement in PATTERN1 to VALUE=X4 and rerun the program to see how that alters the output.

- 6. Change VBAR to VBAR3D. Note that the colors for the bars remain, but the PATTERN option no longer has any effect.

If you want the bars to appear in an order other than alphabetical, you can create a format for the variable and apply that format to the variable for the PROC GCHART statement.

## 18.4 CREATING STACKED BAR CHARTS

Another often-used type of bar chart is a stacked bar chart. To create stacked bar charts, you do not use the GROUP option. This is illustrated in the following Hands-on Example.

### HANDS-ON EXAMPLE

This example illustrates how to create stacked bar charts using PROC GCHART.

- 1. Open the program file AGRAPH7.SAS.

```
GOPTIONS RESET=ALL;
PATTERN1 V=R1 C=RED; * FOR BUS;
PATTERN2 V=R2 C=BLUE; * FOR CAR;
PATTERN3 V=R3 C=BLACK; * FOR WALK;
TITLE C=RED 'Stacked Bars, Method of Arrival';
PROC GCHART DATA=MYASLIB.SURVEY;
VBAR GENDER /SUBGROUP=ARRIVE WIDTH=15;

RUN;
QUIT;
```

Note that this plot is set up a little differently from previous GCHART examples, in that the PATTERN statement occurs before the PROC GCHART statement. The PATTERNs are set up for the three arrival types that will be graphed: Bus, Car, and Walk.

- 2. Run this program and observe the output in Figure 18.7.

![](img/6113440fee6085d6edba5f406f541c12_421_0.png)

Figure 18.7 Stacked bar chart

- 3. Suppose that for a publication that doesn’t print in more than one color, you want the bars to be in different shades of gray. Change the PATTERN and V statements to read as follows:

```
PATTERN1 V=S C=GRAYAA; * FOR BUS (Dark Gray);
PATTERN2 V=S C=GRAYCC; * FOR CAR (Medium Gray);
PATTERN3 V=S C=GRAYEE; * FOR WALK (Light GRAY);
```

V=S indicates solid, and the various shades of gray are given as GRAYAA, GRAYCC, and so on to GRAYFF, which is white.

- 4. Change the GCHART code to

```
PROC GCHART DATA=MYSASLIB.SURVEY;
VBAR GENDER / GROUP=ARRIVE SUBGROUP=GENDER WIDTH=10;
RUN;
```

Rerun the program and observe the difference.

- 5. For further enhancement to the bar chart, open the program AGRAPH7A.SAS and observe the additional code defining a plot key and an enhancement to the vertical axis.

```
OPTIONS RESET=ALL;
PATTERN1 V=R1 C=RED; * FOR BUS;
PATTERN2 V=R2 C=BLUE; * FOR CAR;
PATTERN3 V=R3 C=BLACK; * FOR WALK;
LEGEND1
ACROSS=1 LABEL=("Gender")
POSITION=(top inside left)
VALUE=(H 'Male' 'Female');
AXIS1 label=a 90 Color=RED H=2 f="Swiss/Bold "Count"\n
TITLE C=RED "Example Bar Chart";
PROC GCHART DATA=MYSASLIB.SURVEY;
VBAR GENDER / GROUP=ARRIVE SUBGROUP=GENDER WIDTH=10
LEGEND=LEGEND1 RAXIS=AXIS1
OUTSIDE=FREQ;
RUN;
QUIT;
```

- The LEGEND1 and AXIS1 statements. The LEGEND1 statement creates a key named "Gender" that appears at the top, inside left in the graph frame, with the key items "Male" and "Female" listed. The ACROSS option specifies that the key has items listed once.
- The AXIS1 statement defines an axis to use as the vertical axis where the name "Count" will be displayed at 90 angle using the Swiss font, in red, with a height of 2 units (default is 1).
- In the PROC GCHART statements, note the LEGEND=LEGEND1 and RAXIS=AXIS1 statements. These statements apply the legend and axis to the chart.
- Note the statement OUTSIDE=FREQ. This tells the program to display the count (FREQ) for each bar, and to display outside the bar.
  a. Run this program and observe the results shown in Figure 18.8.
  b. Take out the ACROSS=1 option and rerun. How does this change the legend?
  c. Change the legend position to the top right. Rerun the program to see if your change worked.

![](img/6113440fee6085d6edba5f406f541c12_423_0.png)

There are many options for customizing these plots, only a few of which have been discussed. Several of the options (e.g., AXIS and LEGEND) are similar to those used in PROC CHART.

## 18.5 CREATING MEAN BARS USING GCHART

An often-used graphic is one that displays means as bars with error bars around the mean indicating a level of variability. PROC CHART can produce this graph with a little help. The following Hands-on Example shows how.

### HANDS-ON EXAMPLE

In this example, will produce a bar chart with error bars representing means by group.

- 1. Open the program GRAPH8.SAS.

```
PATTERN1 V=L3 COLOR=LIGHTBLUE;
AX1 LABEL=(A=90 F="SWISS" "OBSERVATION" C=BLUE);
AX2 LABEL=(H=1.5 F="SWISS" "GROUP");
TITLE 'Mean Displayed with Error Bars';
PROC GCHART DATA=MYSASLIB.DATA;
VBAR / WIDTH=10
TYPE=MEAN
SUMVAR=TIME
INSIDE=MEAN
CLM=99
ERRORBAR=TOP
RAXIS=AX1 MAXIS=AX2
OUTLINE=SAME WOUTLINE=2;
RUN;
QUIT;
```

Note the following statements and how they are used:
- The PATTERN statement makes the bars light blue with L3 (left stripe).
- The AX1 statement is used to specify the RAXIS (which is Response axis), and AX2 statement is used to specify the MAXIS (Midpoint Axis). RAXIS is rotated by 90°. Both are displayed with a height of 1.5.
- The SUMVAR tells SAS which variable is used to calculate the mean (as specified by INSIDE).

![](img/6113440fee6085d6edba5f406f541c12_424_0.png)

Figure 18.9 Means with error bars

- INSIDE=MEAN causes the mean values to be displayed within the bars.
- The CLM=99 specifies 99% confidence interval on the mean.
- The TYPE= specifies the type of statistic used in the ERRORBAR option.
- The ERRORBAR=TOP takes the CI bars to be displayed on the top of the bars.
- COUTLINE and WOUTLINE specify a black outline with width 1.

Run this program and observe the output, as shown in Figure 18.9.
2. Change the AXIS1 statement to control attributes of the major and minor axes on the response scale.

```
AXIS1 LABEL=(A=90 H=1.5 F="SWISS" "OBSERVATION" C=BLUE)
MAJOR=(COLOR=BLUE HEIGHT=3 WIDTH=2)
MINOR=(NUMBER=4 COLOR=RED HEIGHT=1);
```

3. Change the ERRORBAR, TYPE, and CLM statements to observe the changes.
4. Take off the ERRORBAR, TYPE, and CLM statements and change INSIDE=MEAN to OUTSIDE=FREQ (ERRORBAR, TYPE and CLM do not work with FREQ), rerun and observe the changes.

## 18.6 CREATING BOXPLOTS

Examples in earlier chapters have shown how default SAS creates boxplots. This section provides information on methods for creating and enhancing boxplots. The abbreviated syntax for this procedure is follows:

```
PROC BOXPLOT <DATA=dataset>; <options>;
PLOT <devpar=>groupvar(s)</options>
<statements>;
```

The PLOT statement is required. For example, a typical use (group must first be sorted):

```
PROC BOXPLOT DATA = MYDATA;
PLOT HEIGHT*GROUP;
RUN;
```

There are numerous options for PROC BOXPLOT. Some commonly used statements are listed in Table 18.10. Options for the PLOT statement appear after a slash. For example:

```
PROC BOXPLOT DATA=CARDATA;
PLOT HWYPG*CYLINDERS/BOXFILL=LIGHTGREEN;
```

Some common options for the PLOT statement associated with PROC BOXPLOT are listed in Table 18.11. A number of other options are available, many similar to those listed for PROC CHART (see SAS documentation for more details).

### TABLE 18.10 Common Statements for PROC BOXPLOT

| Statement | Explanation |
| --- | --- |
| DATA=dataname | Specifies which data set to use |
| PLOT <depvar*>groupvar(s); | Typically, a dependent variable and grouping variable such as PLOT AGE*GROUP |
| INSET | Specifies an inset key similar to those previously described for histograms. See Chapter 9 |
| ID variables; | Specifies which variables will be used to identify observations |
| BY, FORMAT, LABEL, WHERE | These statements are common to most procedures and may be used here |

### TABLE 18.11 Common Options for the BOXPLOT Statement (Follow a Slash /) in PLOT Statement

| Option | Explanation |
| --- | --- |
| CBOXES=color | Specifies outline color for boxes. For example, CBOXES=RED |
| CBOXFILL=color | Specifies the fill pattern for boxes. For example, CBOXFILL=LIGHTBLUE |
| NOTCHES | Species that boxes will be notches. For an explanation for notches, see McGill, Tukey, and Larsen (1978) |
| BOXSTYLE= | Specifies the style of the boxplot. Options include SCHEMATIC, SCHEMATIC SKELETAL (default). SCHEMATIC displays labels for outliers according to the ID variable specified in the ID statement. SKELETAL does not display outliers. (See example for more explanation.) |

### 18.6.1 Creating a Simple Boxplot

The basic plot request consists of indicating the variables used for the analysis and grouping in the statement:

```
PLOT analysisvariable*groupingvariable;
```

### HANDS-ON EXAMPLE

This example illustrates a simple use of PROC BOXPLOT.
1. In the Editor window, open the file AGRAP9.SAS.

```
GOPTIONS RESET=ALL;
Title "Simple Box Plot";
* You must sort the data on the grouping variable;
PROC SORT DATA=MYSASLIB.CARS
```
