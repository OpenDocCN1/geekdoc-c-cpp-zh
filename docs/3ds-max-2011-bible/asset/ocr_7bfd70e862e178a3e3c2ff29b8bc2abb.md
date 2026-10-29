# Part III: Modeling Basics

# Mirror

You can use the Mirror button to mirror a spline object horizontally, vertically, or along both axes. To use this feature, select a spline object to mirror and then locate the Mirror button. To the right of the Mirror button are three smaller buttons, each of which indicates a direction—Mirror Horizontally, Mirror Vertically, and Mirror Both—shown in Table 12.4. Select a direction, and then click the Mirror button. If the Copy option is selected, a new spline is created and mirrored. The About Pivot option causes the mirroring to be completed about the pivot point axes.

**TABLE 12.4**

**Mirror Button Options**

| Button | Description |
|---|---|
| [Mirror horizontally icon] | Mirror Horizontally |
| [Mirror vertically icon] | Mirror Vertically |
| [Mirror both icon] | Mirror Both |

Figure 12.32 shows a little critter that has been mirrored horizontally, vertically, and both. The right image was horizontally mirrored with the About Pivot option disabled. Notice that the eye spline was mirrored about its own pivot.

![](bbox=[0.074, 0.548, 0.755, 0.7])

# Trim and Extend

The Trim button cuts off any extending portion between two overlapping splines. The splines must be part of the same object. To use the Trim feature, select the spline that you want to keep, click the Trim button, and then click the segment to trim. The spline you click is trimmed back to the nearest intersecting point of the selected object. This button works only in Spline subobject mode. The trimming command is dependent on the viewport that is active. When the Perspective or a Camera view is active, this command uses the Top viewport to trim.

Figure 12.33 shows a circle intersected by two ellipse shapes. The Trim button was used to cut the center sections of the ellipse shapes away.

The Extend button works in the reverse manner compared to the Trim button. The Extend button lengthens the end of a spline until it encounters an intersection. (There must be a spline segment to intersect.) To