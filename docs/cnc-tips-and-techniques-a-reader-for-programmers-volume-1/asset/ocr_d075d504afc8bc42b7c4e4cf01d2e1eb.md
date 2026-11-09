```
```
N12 Y300.0
N13 G15 G80 Z10.0 M09 (POLAR COORDINATES OFF)
N14 G52 X0 Y0  (RESET BACK TO WORK OFFSET G54)
N15 G28 Z10.0 M05
N16 M01
```
```

The programming itself is very simple. Although the X60.0 (radius) does not change in this case, the Y (angle) increases by the amount of angle between holes (360/6 = 60.0), starting at zero degrees (Y0). No special calculations are required; the program is easy to understand and easy to change, if necessary.

There are several important features used in the program that require explanation:

As a precautionary measure, G15 has been programmed at the program beginning (N2), to cancel the polar coordinate mode, if active.

The first major tool motion should be to the pole — the bolt hole circle center (N3).

For a bolt hole pattern where the X-radius does not change, only the Y-angle increment (N8 to N12) is programmed

Either absolute or incremental mode can be used while polar coordinates are in effect.

Programming the angle with 0.001 accuracy makes a better program (three decimal places for an angle, if needed, for example, when programming a seven hole bolt circle).

In the less common situations that would require you to program polar coordinates in a plane other than G17, the meaning of addresses changes:

```
```
G17 plane XY => X = Radius, Y = angle
G18 plane ZX => Z = Radius, X = angle
G19 plane YZ => Y = Radius, Z = angle
```
```