(continued)

+   2. Change HBAR to VBAR and rerun the analysis to see a vertical bar chart version of this plot.

+   3. Change the bar code to read

```
VBAR RACE_CAT/ GROUP=GENDER;
```

Resubmit the code and observe the stacked vertical bar chart created.

+   4. Change the code again to read

```
VBAR RACE_CAT/ GROUP=GENDER GROUPDISPLAY=CLUSTER;
```

![](bbox=[0.233, 0.3135, 0.766, 0.575])

Submit this code and observe the vertical bar chart with bars clustered.

+   5. To illustrate manipulating the legend and axis labels add this to code:

```
KEYLEGEND / LOCATION=INSIDE POSITION=TOPLEFT;
XAXIS LABEL="Race";
```

Resubmit this code and observe the results.

+   6. To produce a grayscale version of this plot, place the code.

```
ODS RTF STYLE=GRAYSCALEPRINTER;
```

```
Before PROC SGPLOT, and
```

```
ODS RTF CLOSE;
```

after the RUN; statement, run the revised code. Observe the results as shown in Figure 18.17.