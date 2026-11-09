if positions B or C are selected for calculations. To avoid this, use positions D or E. The center of a rectangular pocket can be determined in a similar manner.

# 11.5 Finding Angle of an Edge

Sometimes the machining program for a rectangular block is written with program zero point at, say, the lower left corner of the block, with the coordinate axes being parallel to its axes. In such a case, a very accurate (hence expensive) fixture is needed, to hold the workpiece properly. An inaccurate fixture would hold it incorrectly, as shown in Fig. 11.4, where the coordinate system used for programming (X-Y) does not coincide with the workpiece coordinate system (X<sub>w</sub>Y<sub>w</sub>). A solution to this problem would be to shift the workpiece zero point to point O, and then execute the machining program using coordinate-system-rotation feature (G68). Calling macro C0808, after placing the tool at point O, would shift the coordinate system, as done in the previous example. For commanding G68, the angle θ (in degrees) must be known. The algorithm would be

+   1. Find angle θ.
+   2. Find X- and Y-coordinates of point O.
+   3. Place the tool at point O (at a safe height from the workpiece).
+   4. Call C0808.

![](bbox=[0.136, 0.586, 0.855, 0.938])