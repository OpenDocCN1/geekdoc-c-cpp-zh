As you can see, two LEDs are missing from the grid. If we had the full set of 3x9 LEDs, we would have 27 while a 5x5 array only needs 25. The micro:bit V2 makes use of the additional GPIO lines to create a simpler 5x5 layout:

![](bbox=[0.173, 0.153, 0.762, 0.563])

The GPIO assignments are:

# LED MATRIX COLS

V1
COL1 = p0_4
COL2 = p0_5
COL3 = p0_6
COL4 = p0_7
COL5 = p0_8
COL6 = p0_9
COL7 = p0_10
COL8 = p0_11
COL9 = p0_12

V2
P0_28
P0_11
P0_31
P1_05
P0_30