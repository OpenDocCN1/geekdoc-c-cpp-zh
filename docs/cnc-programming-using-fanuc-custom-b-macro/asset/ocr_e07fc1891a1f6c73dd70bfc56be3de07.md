style was recommended earlier in this text. It is being reiterated here because it is so important.

This is not an example of a macro involving a complex logic. Therefore, a flowchart or an algorithm is not really necessary. It is, however, recommended to at least write down how the toolpath is to be generated, which would streamline the thought process:

+   1. Send the turret to its home position, and select tool number 1 with offset number 1.
+   2. Place the tool at (X54 Z2), and face up to Z−0.5 using G94, in a single pass.
+   3. Place the tool at (X50 Z2), and rough out using G71, leaving suitable finishing allowances.
+   4. Send the turret to its home position, and select tool number 3 with offset number 3.
+   5. Place the tool at (X50 Z2), and finish by G70, at reduced feedrate and increased rpm (CSS, with radius compensation). (Since it is a right-hand turning tool, the tool-tip number on a rear-type lathe would be 3 that has to be entered in the third row of the geometry or wear offset table. The radius of the tool tip is entered in the geometry offset table.)

The defined profile, which is same for both G71 and G70, is shown in Fig. 9.2.

![](bbox=[0.328, 0.538, 0.749, 0.746])

+   **Note:**
+   1. Refer to Fig. 9.1 for dimensions not shown.
+   2. The profile definition starts at P and ends at Q.
+   3. The X- and Z-coordinates of P are (−9) and (−2), respectively.
+   4. The X- and Z-coordinates of Q are (54 and 5), respectively.
+   5. The extended toolpath at the start of the profile is at the angle of the chamfer (45°). This makes a better-quality corner.
+   6. The Z-coordinate of Q includes 3 mm extra length on the larger diameter, which is needed for part-off operation.

Figure 9.2  Defined profile for G71 and G70, for the pin of Fig. 9.1.