of burning an amount of fuel and determining the CO emissions released. The experimental unit is the portion of a standard fuel required for one run, and the response, y, is the carbon monoxide (CO) emissions concentration in grams/meter^3 determined from that run. Factor A is the amount of ethanol added to an experimental unit or portion of the standard fuel, and factor B is the fuel-to-air ratio used during the burn of that fuel.

# Table 3.3 Data from Ethanol Fuel Experiment
A=ethanol additions B=air/fuel ratio y=CO emissions

| A=ethanol additions | B=air/fuel ratio | y=CO emissions |
|---|---|---|
| 0.1 | 14 | 66, 62 |
| 0.1 | 15 | 72, 67 |
| 0.1 | 16 | 68, 66 |
| 0.2 | 14 | 78, 81 |
| 0.2 | 15 | 80, 81 |
| 0.2 | 16 | 66, 69 |
| 0.3 | 14 | 90, 94 |
| 0.3 | 15 | 75, 78 |
| 0.3 | 16 | 60, 58 |

The SAS commands to read in this data and produce the analysis are shown below.

```
Data CO;
input Ethanol Ratio CO;
datalines;
.1 14 66
.1 14 62
... etc.
;
proc glm;
class Ethanol Ratio;
model CO=Ethanol Ratio Ethanol*Ratio/solution;
lsmeans Ethanol Ratio Ethanol*Ratio;
estimate '13 vs 0.1' Ethanol -1 0 1;
estimate '16 vs 14' Ratio -1 0 1;
run;
ods graphics off;
```

The resulting ANOVA table is shown on the next page. There it can be seen that proc glm produces a table of the type I sums of squares, as described earlier, and a table of type III sums of squares. For the case where there is an equal number of replications in each cell, these two tables will always be identical. It can be seen from the tables that the two effects and their interaction are significant as indicated by the P-values to the right of the F-values.

The result of the /solution option on the model statement produces the table of parameters shown below the ANOVA table. SAS labels these estimates