Even if such a special gauge is available, it will be too late to find out that the cone is out of tolerance. The method of using a trial cut is to provide a special flat area (diameter) that can be easily measured, before the final cone is machined, following a few simple rules.

Normally, a cone machined from round stock, such as the 5.0 inch diameter used in the following example, will include G71 roughing cycle and G70 finishing cycle in the part program:

```
N1 G20 T0100 (ROUGHING TOOL)
N2 G96 S300 M03 (CUTTING SPEED)
N3 G42 G00 X5.2 Z0.1 T0101 M08 (START POINT FOR CYCLE)
N4 G71 U0.15 R0.025
N5 G71 P6 Q8 U0.07 W0.02 F0.015
N6 G00 X2.8 (CONE START)
N7 G01 X4.6 Z-3.5 F0.008 (CONE END)
N8 U0.2 (RETRACT FROM PART)
N9 G40 G00 X10.0 Z4.0 T0100 (CLEAR POSITION)
N10 M01

N11 T0300 (FINISHING TOOL)
N12 G96 S500 M03 (CUTTING SPEED)
N13 G42 G00 X5.2 Z0.1 T0303 M08 (START POINT FOR CYCLE)
N14 G70 P6 Q8
N15 G40 G00 X10.0 Z4.0 T0300 (CLEAR POSITION)
N16 M30
%
```

Although correct, the program above does not offer any means to measure the conical part efficiently. By adding several blocks of trial cut in the program and using the finishing tool (T03), a suitable straight cut can be machined first.

When measured, various offsets can be adjusted as necessary — all this is done before any roughing cuts take place.