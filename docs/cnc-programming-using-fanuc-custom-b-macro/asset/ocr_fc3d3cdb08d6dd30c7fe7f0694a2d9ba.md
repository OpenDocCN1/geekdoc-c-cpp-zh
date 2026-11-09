```
```text
G90 X0 Y Z100;                 (Tool placed 100 mm above hole 1)
#1 = 1;                         (COUNTER1 initialized)
WHILE [#1 LE #3] DO 1;          (The outer loop starts. It is executed once
                                 for every column of holes)
G90 G81 G99 Z-[ABS[#5]] R2 F30; (The use of ABS function makes the pro-
                                 gram work even if a negative value is
                                 specified for the depth of the hole)
                                 (COUNTER1 incremented for drilling
                                 holes in the next column of holes)
                                 (COUNTER2 initialized)
#1 = #1 + 1;
#2 = 1;
WHILE [#2 LE [#4 - 1]] DO 2;    (The inner loop starts. It makes the
                                 required number of holes in each column
                                 of holes)
G91 G00 Y#7;                     (The tool shifted along the Y-axis to the
                                 center of the next hole in the current col-
                                 umn of holes)
G90 G81 G99 Z-[ABS[#5]] R2 F30;  (Hole drilled)
#2 = #2 + 1;                     (COUNTER2 incremented for counting
                                 and drilling the required number of holes
                                 in the current column of holes)
END 2;                           (The inner loop ends)
IF [#1 GT #3] GOTO 10;           (Shift to the base of the next column of
                                 holes is not needed after the last column)
G91 G00 X#6 Y-[#7 * [#4 - 1]];   (Tool shifted to the base of the next
                                 column of holes)
N10;                             (A blank NC statement)
END 1;                           (The outer loop ends)
G80;                             (Canned cycle cancelled)
M05;                             (Spindle stops)
G90 G00 Z100;                    (Tool retracted to Z = 100 mm)
M30;                             (Program end and control reset)
```
```

While it may appear that the use of the [WHILE statement] in this case is too complex a method for too simple a problem, this method would definitely be preferable for a large number of holes. In fact, even if the number of holes increases, the program remains essentially the same; only the two variables (#3 and #4) for the numbers of holes along the X- and Y-directions would need to be redefined, as per requirement. While the use of a loop, especially a nested loop, makes a simple program complex, it does make a complex problem pretty simple! Anyway, the basic purpose here was to explain the use of the nested WHILE statement. Moreover, this happens to be our first program which involves machining, and which is also a common practical application.