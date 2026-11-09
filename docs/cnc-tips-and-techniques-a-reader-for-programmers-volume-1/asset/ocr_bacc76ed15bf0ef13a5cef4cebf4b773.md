vector also requires a positive or negative direction. The example below shows the previous example modified to cut an R0.1 blend radius:

```
    N1 T0100 (R0.1 FILLET - MANUAL RADIUS)
    N2 G96 S300 M03
    N3 G00 G42 X4.0 Z0.1 T0101 M08
    N4 G01 Z-2.0 F0.01
    N5 X5.8
    N6 G03 X6.0 Z-2.1 R0.1
    N7 G01 Z-3.0
    ...
```

Using the automatic corner radius, the program is much easier to write:

```
    N1 T0100 (R0.1 FILLET - AUTOMATIC RADIUS)
    N2 G96 S300 M03
    N3 G00 G42 X4.0 Z0.1 T0101 M08
    N4 G01 Z-2.0 F0.01
    N5 X6.0 R-0.1 (SHARP CORNER)
    N6 Z-3.0 (CONTINUES IN Z-NEGATIVE DIRECTION)
    ...
```

Both methods are based on the same principles and use the same rules:

+   - The chamfer must have a 45-degree angle and the radius must have
+     a 90-degree sweep angle, in a single quadrant.
+   - The programmed amounts of corner vectors are always *per side*, not
+     diameter.
+   - The cutting direction *before* a corner break must be perpendicular to
+     the cutting direction *after* the corner break.
+   - The cutting direction following the corner break must continue
+     along a single axis only. It must be at least as long as the
+     corner amount — it cannot reverse.