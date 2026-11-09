```
```text
X0;
X50;
Z-10;
G31 X-100 F200;                 (Approaches the right side of the block)

X2;
G31 X-5 F10;
#104 = #5061;                    (X-coordinate at position F stored)
X5;
Z10;
X-120;
Z-10;
G31 X100 F200;                   (Approaches the left side of the block)
X-2;
G31 X5 F10;
#105 = #5061;                    (X-coordinate at position A stored)
#502 = #104 - #105 - 5;          (Length of the block calculated, in which diameter of the ball has been taken into account)

X-5;
G28 Z0;
G28 X0 Y0;
M30;
```
```

The Y-dimensions of the pocket and the block can be determined in a similar manner. This has been left as an exercise for the readers. Probing a hole is done in a similar manner, where the probe is generally held like an internal tool.

# 11.4 Finding Center of a Hole

Sometimes the workpiece is a cast part with a preexisting hole, and the part program is written with workpiece zero at the center of the hole. This requires that the spindle be exactly aligned with the axis of the hole, for determining work offsets along the X- and the Y-axis. This is typically done with the help of a spindle-type dial indicator. The end of the lever is made to touch the hole at some point, and the spindle is given a very low rpm. The X- and/or Y-positions are adjusted so as to get the same dial reading in all angular positions, which locates the center of the hole. Though this method is theoretically correct and is used quite often, it involves trial and error. As a result, the time taken in datum setting largely depends on the skill of the operator. We will now see how this can be done automatically, using a touch probe.

Consider the hole shown in Fig.11.3. The principle involved in locating the center is very simple. The center would lie on the point of intersection of the perpendicular bisectors on any two chords. As a