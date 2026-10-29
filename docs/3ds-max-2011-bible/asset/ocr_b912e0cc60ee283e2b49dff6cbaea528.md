# Chapter 11: Introducing Modifiers and Using the Modifier Stack

# Wave modifier

The Wave modifier produces a wavelike effect across the surface of the object. All the parameters of the Wave Parameter are identical to the Ripple modifier parameters. The difference is that the waves produced by the Wave modifier are parallel, and they propagate in a straight line. Figure 11.26 shows the Wave modifier applied to a simple Quad Patch with values of 5 for Amplitude 1 and a Wave Length value of 50. The right Quad Patch also has an Amplitude value of 20.

![](bbox=[0.016, 0.277, 0.576, 0.438])

The Wave modifier produces parallel waves across the surface of an object.

# Tutorial: Waving a flag

The Wave modifier can add a gentle wave to an object such as a flag. If you animate the Phase value, you can show a flag unfurling in the breeze.

# Cross-Ref

For a more realistic-looking flag, you can apply a Cloth modifier. See Chapter 29, “Adding and Styling Hair and Fur, and Using Cloth,” for more information on the Cloth modifier.

To animate a flag waving with the Wave modifier, follow these steps:

+   1. Open the Waving US flag.max file from the Chap 11 directory on the DVD.
+   
+      This file includes a simple flag and flagpole made from primitive objects.
+   
+   2. With the flag selected, select the Modifiers > Parametric Deformers > Wave menu command to apply the Wave modifier to the flag.
+   
+   3. Notice how the waves run from the top of the flag to the bottom. You can change this by rotating the gizmo. Click the plus sign to the left of the Wave modifier in the Modifier Stack and select the Gizmo subobject. With the Select and Rotate tool (E), rotate the gizmo 90 degrees and then scale the gizmo with the Select and Scale tool (R) so it covers the flag object. Click the Gizmo subobject again to deselect gizmo subobject mode.
+   
+   4. Set Amplitude 1 to 25, Amplitude 2 to 0, and the Wave Length to 50. Then click the Auto Key button (N), drag the Time Slider to frame 100, and set the Phase value to 4. Click the Auto Key button (N) again to exit key mode.

Figure 11.27 shows the waving flag.