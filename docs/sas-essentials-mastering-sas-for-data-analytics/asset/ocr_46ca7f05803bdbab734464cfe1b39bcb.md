(continued)

```
OUT=CARDATA; BY CYLINDERS;
PROC BOXPLOT DATA=CARDATA;
PLOT HWYMPG*CYLINDERS CBOXFILL=LIGHTGREEN;
WHERE CYLINDERS GT 1;
```

Note when comparing side-by-side boxplots, you must sort the data on the grouping variable before running the PROC BOXPLOT procedure. Also note that the WHERE statement is necessary because one car (the Mazda RX-8) is listed as -1 cylinders as it uses a rotary engine. You could have also recoded the -1 as a missing value to obtain the same result.

2. Run this program and observe the output in Figure 18.10.

![](bbox=[0.15, 0.365, 0.84, 0.673])

Figure 18.10 Boxplots showing highway MPG by cylinders

3. Change the PLOT statement to include the following:

```
PLOT HWMPG*CYLINDERS/
CBOXFILL=VLIGB
CBOXES=BLACK
BOXSTYLE=SCHEMATIC
NOTCHES;
```

The CBOXFILL and CBOXES options specify the fill color and outline color of the boxes, respectively. BOXSTYLE requests the SCHEMATIC style plot, which specifies the type of outliers displayed in the plot. The SCHEMATIC option defines outliers as