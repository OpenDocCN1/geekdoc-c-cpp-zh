those values greater than the absolute value of 1.5*(interquartile range) from the top or bottom of the box. Run the program and observe the output in Figure 18.11. Note that outliers are marked at the top of two of the boxplots.

# ### Distribution of HwyMPG cylinders

![](bbox=[0.212, 0.201, 0.755, 0.463])

### Figure 18.11 Boxplots with enhancements

+   4. To display the IDs of outliers, change the style to SCHEMATICID and include the statement ID MODEL using the code shown here. Rerun and observe the results. (In this case, some of the ID text overlaps so that it is hard to read some of the results.)

```
PLOT HWYMPG*CYLINDERS/
CBOXFILL=VLIGE
CBOXES=BLACK
BOXSTYLE=SCHEMATICID
NOTCHES;
ID MODEL;
```

+   5. To display summary statistics on the graph, include an INSETGROUP statement as the code shown here. Rerun and observe the results.

```
INSETGROUP (5.1) MIN MAX /
header = 'Mean and Extremes';
```

The notches are a way to measure the difference between two medians. If there is no overlap in the corresponding notches for two plots, it indicates a significantly different in the group medians at approximately the 0.95 confidence level.