```
~~~
Y0 F60;                (Groove along the Y-axis, at the current depth)
X60;                   (Groove along the X-axis, at the current depth)
X0 Y60;                (Groove at 45°, at the current depth)
M99;                   (Return to the calling program)
~~~
```

# ### 6.3 Multiple Call of a Subprogram

It is possible to call the subprogram a desired number of times repeatedly, that is, one after another. Up to 999 repetitions are permitted. The argument of P in M98 block must contain seven digits (or minimum five digits) for this. Four digits from the right are considered the (sub)program number, and the remaining digits (maximum three) to the left indicate the number of repetitions. And if eight digits are specified in the P-word, the eighth digit from the right is ignored:

```
~~~
M98 P50001;         (Calls program number 1, five times, which is
                    equivalent to five consecutive blocks of M98 P0001
                    or M98 P1)
M98 P050001;        (Same as above)
M98 P050001;        (Same as above)
M98 P9990001;       (Program number 1 is called 999 times)
M98 P12340001;      (Program number 1 is called 234 times. The eighth
                    digit from right is ignored)
~~~
```

A subroutine also can be repeatedly called by inserting an L-word in the M98 block. The argument of the L-word is the number of repetitions. The advantage of using this method is that up to 9999 repetitions would be possible, compared to only 999 with the earlier method:

```
~~~
M98 P0001 L9999;    (Program number 1 is called 9999 times)
M98 P1 L9999;       (Same as above)
M98 P1 L10000;      (Illegal L-word)
~~~
```

If the repeated call of a subprogram simply retraces the toolpath, the repetition would be unnecessary and meaningless. Repetition would be useful only in incremental mode where it is possible to have different toolpaths in the subsequent executions of the same subprogram. For example, program O0004 repeatedly calls program O0005 five times in incremental mode, making for the groove of Fig. 6.1.

```
~~~
O0004;              (Program number 4)
G21 G94;            (Millimeter mode and feedrate in millimeter
                    per minute)
G54;                (Workpiece coordinate system)
G91 G28 X0 Y0 Z0;   (Reference point return)
M06 T1;             (Tool number 1)
M03 S1000;          (CW rpm 1000)
G90 G43 H01;        (Tool length compensation)
~~~
```