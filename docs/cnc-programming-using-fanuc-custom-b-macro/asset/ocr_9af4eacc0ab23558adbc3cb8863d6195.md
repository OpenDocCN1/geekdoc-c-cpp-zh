```
```text
#103 = #24 + #102 * COS[#101 + #1];
#104 = #25 + #102 * SIN[#101 + #1];
G90 X#103 Y#104 F#13;
#101 = #101 + #100;
END 2;
#105 = #5043;
G00 Z2;
X[#24 + #19 * COS[#1]] Y[#25 + #19 * SIN[#1]];
Z[#105 + 1];
G01 Z#105 F#9;
#107 = #107 - 3;
END 1;
G91 G01 Z-#107 F#9;
#100 = #17;
#101 = #100;
WHILE [ABS[#101] LE ABS[#4]] DO 3;
#102 = #19 + [[#8 - #19] * ABS[#101] / ABS[#4]];
#103 = #24 + #102 * COS[#101 + #1];
#104 = #25 + #102 * SIN[#101 + #1];
G90 X#103 Y#104 F#13;
#101 = #101 + #100;
END 3;
G00 Z2;
M99;
```
```

(Xr calculated)

(Yr calculated)

(Move to (Xr, Yr) with the specified milling feedrate)

(Angle θ incremented/decremented by the chosen step)

(End of WHILE loop. Arc made)

(The current absolute Z-coordinate of the tool stored in #105)

(The tool is now at the end point B of the arc. Here, it is retracted to 2 mm above the workpiece)

(Tool brought back to the start point A)

(Rapid to 1 mm above the previous Z-level)

(Feed motion in the last 1-mm travel)

(Calculates the remaining depth of the slot, to be machined further)

(Loop back to the start of step 2. Step 2 complete)

(Plunge entry to the final depth, at the start point A, with the specified plunge feedrate)

(Δθ set to the specified value. This statement is redundant, because #100 is already defined)

(θ set equal to Δθ)

(Exit from the loop if the magnitude of θ is greater than the magnitude of the included angle of the arc. Since it is not a nested WHILE loop, one may choose to use even 1 or 2, in place of 3, as loop identification number)

(r calculated)

(Xr calculated)

(Yr calculated)

(Move to (Xr, Yr) with the specified milling feedrate)

(Angle θ incremented/decremented by the chosen step)

(End of WHILE loop. Arc made. Step 3 complete)

(The tool is now at the end point B of the arc. Here, it is retracted to 2 mm above the workpiece. Step 4 complete)

(Return to the calling program. Step 5 complete)