
![](img/1341ce50369ce8fcfb8dc3539d51c52f_241_0.png)

Figure 11.2 Probing a socket on a milling machine.

The length/width of the part can be measured. The length of the pocket can be measured by touching the pocket at, say, positions C and E, and then taking the difference in the stored X-positions. As is clear from the geometry, the diameter of the ball would need to be added to the obtained length. On the other hand, when the length of the part is measured by touching it at positions A and F, the diameter of the ball would need to be subtracted from the obtained value.

The dimensions of the pocket are not important for explaining the probing principle. However, for the purpose of writing a program, it is assumed that the “expected” size of the block and the pocket are 90 mm × 36 mm × 20 mm and 50 mm × 16 mm × 10 mm, respectively, with their centers at (45, 18, 18). It is also assumed that the probe occupies the position of tool post number 1, with 01 offset number for length compensation. The diameter of the ball is assumed to be 5 mm. The program for this problem is intentionally not made for a general case since its only aim is to explain the probing principle, without involving additional complications:

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

The Y-dimensions of the pocket and the block can be determined in a similar manner. This has been left as an exercise for the readers. Probing a hole is done in a similar manner, where the probe is generally held like an internal tool.

## 11.4 Finding Center of a Hole

Sometimes the workpiece is a cast part with a preexisting hole, and the part program is written with workpiece zero at the center of the hole. This requires that the spindle be exactly aligned with the axis of the hole, for determining work offsets along the X- and the Y-axis. This is typically done with the help of a spindle-type dial indicator. The end of the lever is made to touch the hole at some point, and the spindle is given a very low rpm. The X- and/or Y-positions are adjusted so as to get the same dial reading in all angular positions, which locates the center of the hole. Though this method is theoretically correct and is used quite often, it involves trial and error. As a result, the time taken in datum setting largely depends on the skill of the operator. We will now see how this can be done automatically, using a touch probe.

Consider the hole shown in Fig. 11.3. The principle involved in locating the center is very simple. The center would lie on the point of intersection of the perpendicular bisectors on any two chords. As a special case, if the two chords are chosen to be parallel to the X- and Y-axes, respectively, then the X-coordinate of the center would be same as that of the mid-point of the chord that is parallel to the X-axis. Similarly, the Y-coordinate of the center would be same as that of the mid-point of the chord that is parallel to the Y-axis. When the end-points of the chords are found using a touch probe, its diameter comes into the picture, because the circle is not touched by the same point on the ball. (The points on the ball, which touch the circle, are shown by dots in Fig. 11.3.) This, however, does not affect our calculations because of symmetry, as can be observed in the figure.

![](img/1341ce50369ce8fcfb8dc3539d51c52f_244_0.png)

A macro, based on this principle, will be developed now. To locate the center of a hole, one simply has to place the ball of the probe somewhere inside the hole (say, position A), and then call the macro. After locating the center, the macro would place the workpiece zero point at that point, by editing the associated system variables.

If positions B or C are selected for calculations, to avoid this, use positions D or E. The center of a rectangular pocket can be determined in a similar manner.

## 11.5 Finding Angle of an Edge

Sometimes the machining program for a rectangular block is written with program zero point at, say, the lower left corner of the block, with the coordinate axes being parallel to its axes. In such a case, a very accurate (hence expensive) fixture is needed, to hold the workpiece properly. An inaccurate fixture would hold it incorrectly, as shown in Fig. 11.4, where the coordinate system used for programming (X-Y) does not coincide with the workpiece coordinate system (X<sub>w</sub>Y<sub>w</sub>). A solution to this problem would be to shift the workpiece zero point to point O, and then execute the machining program using coordinate-system-rotation feature (G68). Calling macro C0808, after placing the tool at point O, would shift the coordinate system, as done in the previous example. For commanding G68, the angle θ (in degrees) must be known. The algorithm would be

- 1. Find angle θ.
- 2. Find X- and Y-coordinates of point O.
- 3. Place the tool at point O (at a safe height from the workpiece).
- 4. Call C0808.
- 5. Command `G17 (G68 X0 Y0 R<θ>)` (X0 Y0, which is the center of rotation, can be left blank because the current tool position automatically becomes the center of rotation, if it is not specified).
- 6. Execute machining program.
- 7. Command `G69` (cancel coordinate rotation).
- 8. End of program.

![](img/1341ce50369ce8fcfb8dc3539d51c52f_246_0.png)

The X- and Y-coordinates of point O, and the angle θ, can be determined using touch probes. For this, the probe would need to touch the orthogonal edges of the workpiece at three points, as shown in Fig. 11.4. Let the coordinates of each of the points be $(x_A, y_A)$, $(x_C, y_C)$, and $(x_D, y_D)$, respectively, corresponding to points A, C, and D. The equation given below can be used for necessary calculations. (Try to derive these, using coordinate geometry.)

The equations of lines CD and AB (which is orthogonal to CD) would be:

$$y_{CD}=\frac{y_D-y_C}{x_D-x_C}(x-x_C)+y_C$$

$$y_{AB}=-\frac{x_D-x_C}{y_D-y_C}(x-x_A)+y_A$$

The coordinates $(x_B, y_B)$ of the point of intersection of these lines (point B) can be found out by solving these equations simultaneously, which gives:

$$x_B=\frac{m^2x_C-my_C+x_A+my_A}{m^2+1}$$

$$y_B=\frac{-mx_C+y_C+mx_A+m^2y_A}{m^2+1}$$

where

$$m=\frac{y_D-y_C}{x_D-x_C}$$

Angle θ would be given by

$$\theta=\tan^{-1}m$$

Finally, the coordinates of the program zero point O would be

$$x_O=x_B+\sqrt{2}\,r\cos(\theta+45)$$

$$y_O=y_B+\sqrt{2}\,r\sin(\theta+45)$$

where r is the radius of the ball of the probe.

```text
G28 W0;                         (Z-home)
T#20;                           (The probe becomes the current “tool”)
G00 Z[#26 - #7 / 2];            (Center of the probe at the specified Z-coordinate, where measurement is to be made. The radius of the probe has been subtracted from the specified value, assuming that the tip of the probe is its reference point)
X[#24 + #7 + 4];                (Probe at a clearance of 2 mm from the diameter to be measured. Make necessary changes in positioning too, if an internal diameter machine is being probed. Moreover, both the plus signs would change to minus signs, for an internal measurement)
#103 = #4005;                   (Stores 98 or 99, depending on which one of G98 and G99 is currently active)
G98;                            (Since the spindle is stationary, this macro would not work in G99, the feed per revolution mode, because the feedrate would become zero when zero rpm)
G31 U-10 F10;                   (Stops at the surface, where the diameter is to be measured)
#104 = #5061;                   (X-coordinate of the center of the probe ball stored when it touches the part)
#105 = #104 - #7;               (Diameter of the part calculated. In the case of an internal diameter, the diameter of the ball would have to be added here. Step 2 complete)
#106 = #105 - #24;              (Error due to wear calculated. This quantity would be negative if probing is being done for an internal tool. Step 3 complete)
#107 = 10000 + #102;            (The system variable for wear offset, corresponding to the offset number being used, is determined. Replace 10,000 by 2000, if only 64 offset numbers are available. 10,000 series is for 99 offset numbers. Step 4 complete)
#[#107] = #[#107] - #106;       (Error subtracted from the current wear offset value. This expression is also correct for internal measurement, since the sign of #106 would automatically become negative. Step 5 complete)
G28 U0;                         (X-home)
G28 W0;                         (Z-home)
T#100;                          (Original tool called, with the updated wear offset value)
G#103;                          (Modal G-code restored)
M99;                            (Return to the calling program. Step 6 complete)
```
