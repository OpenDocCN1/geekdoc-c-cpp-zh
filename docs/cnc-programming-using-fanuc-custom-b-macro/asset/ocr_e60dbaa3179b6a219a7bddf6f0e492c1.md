```
#103 = #103 + #4;
IF [#103 LT #13] THEN #103 = #13;

G00 Z[#102 + 1];

G01 Z[#102 - #103];

#102 = #5043;

G00 Z#18;

#101 = #101 - #103;

END 1;

G00 Z[#102 + 1];
G01 Z#26;

GOTO 20;

N10 G01 Z#26 F#9;

N20 G00 Z#18;
IF [#4010 EQ 99] GOTO 30;

G00 Z#100;

N30 M99;
```

(New peck length calculated. Step 11 complete)

(Rapid motion up to 1 mm above the Z-position at the end of the previous peck. Step 12 complete)

(Feed motion to increase the depth by the calculated peck length. Step 13 complete)

(Current Z-position stored. Step 14 complete)

(Rapid retraction to R-point. Step 15 complete)

(Required depth updated. Step 16 complete)

(Jump to the WHILE block to check the loop condition again. Step 17 complete)

(Remaining depth drilled. Step 18 complete)

(Jump to N20 for final retraction. Step 19 complete)

(Single feed motion to reach the final depth. Step 20 complete)

(Retracts to R-point)
(Jumps to program end if G99 is active)
(Retracts to the initial Z-level, if G98 is active. Step 21 complete)
(Return to the calling program. Step 22 complete)

The given macro uses millimeter mode, and can be called only in the absolute coordinate mode. Though it is easy to make it suitable for inch mode as well, it would require a little more effort to use it in incremental coordinate mode (G91). This is being left as an exercise for the readers.

To illustrate the use of this macro, consider the part shown in Fig. 10.5, where it is assumed that the holes are so deep (i.e., with a large length to diameter ratio) that these require the use of regressive peck drilling cycle (G183). The G183 blocks are shown highlighted for easy identification:

```
G21 G94 G54;
G91 G28 Z0;
G28 X0 Y0;
M06 T01;
G90 G00 X0 Y0;
```