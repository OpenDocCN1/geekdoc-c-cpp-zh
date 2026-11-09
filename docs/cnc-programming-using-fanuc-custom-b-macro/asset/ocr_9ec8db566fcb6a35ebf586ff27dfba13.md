```
```text
G00 Z#101;

#101 = #101 - #18;

END 1;
#103 = #4119;
G01 X#2 Z[-ABS[#7]] F[#9 / 2] S[#103]

#101 = ~ABS[#7];

WHILE [#101 LE 0] DO 1;

#102 = [[#13 * #13 * ABS[#7]] / [#13 * #13 - #2 * #2]];

#102 = #101 + #102;

#102 = [[#13 * #13 - #2 * #2] / ABS[#7]] * #102;

#102 = SQRT[#102];
X#102 Z#100;

#101 = #101 + #100;

END 1;
#104 = [[#13 * #13 - #2 * #2] / [2 * #13 * ABS[#7]] * 2];

U#104 W2;

G00 X#105 Z#106;

S#103 F#9;
M99;
```
```

(Tool positioning for the next G94 cycle. Step 6 complete)

(Z decremented by the specified roughing depth of cut. Step 7 complete)

(End of loop. Step 8 complete)

(Current rpm stored)

(Tool placed at the inner edge of the parabola. Step 9 complete)

(Z-coordinate of the inner parabola stored. Step 10 complete)

(Exit from the loop if the outer edge of the parabola is reached. Step 11 complete)

(Intermediate calculation)

(Intermediate calculation)

(Intermediate calculation)

(Intermediate calculation)

(X calculated. Step 12 complete)

(Linear interpolation to the calculated coordinates. Step 13 complete)

(Z incremented by the specified step distance. Step 14 complete)

(End of loop. Step 15 complete)

(Calculating ΔX, corresponding to ΔZ = 2 mm, at Z=0)

(Additional tangential move at the outer edge of the parabola for removing any possible kink)

(Rapid move to the original tool position)

(Original rpm and feedrate restored)

(Return to the calling program. Step 16 complete)

Though the macro O0818 does not have the feature of finishing allowance of G72, it can be easily incorporated into it. One only has to subtract the desired X-finishing allowance from the calculated X-values, and add Z-finishing allowance to the calculated Z-values, in roughing as well as in step-removal operation. Finally, the step-removal operation would be repeated without adding/subtracting finishing allowances, to be the same tool or a different tool, if desired. It is also possible to introduce two more local variables for passing the values for X- and Z-finishing allowances to the macro, through the macro-calling block. It is left as an exercise for the readers to develop such a macro.