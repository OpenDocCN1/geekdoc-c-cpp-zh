![](bbox=[0.082, 0.061, 0.849, 0.527])

**FIGURE 5.14** Flowchart for an algorithm to drill holes on the plate shown in Fig. 5.13, using a nested WHILE statement.

```
```text
(#3 @ TOTAL NUMBER OF HOLES ALONG X);
(#4 @ TOTAL NUMBER OF HOLES ALONG Y);
(#5 @ DEPTH OF HOLE);
(#6 @ PITCH ALONG X);
(#7 @ PITCH ALONG Y);

#3 = 4;                    (Four holes along the X-axis to be made)
#4 = 3;                    (Three holes along the Y-axis to be made)
#5 = 5;                    (Depth of hole is 5 mm)
#6 = 20;                   (Pitch along a row is 20 mm)
#7 = 25;                   (Pitch along a column is 25 mm)
;
G21 G94 G90 G54;           (Initial settings)
M06 T1;                    (Tool number 1 placed in the spindle)
M03 S1000;                 (Clockwise rpm 1000 starts)
G43 H01;                   (Tool length compensation invoked)
```
```