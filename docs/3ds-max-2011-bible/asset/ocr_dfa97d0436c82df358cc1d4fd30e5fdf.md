# Cross-Ref

For more on Maps and the various map types, see Chapter 17, “Adding Material Details with Maps.”

# FIGURE 16.2

The Blinn Basic Parameters rollout lets you select and control properties for the Blinn shader.

![](bbox=[0.03, 0.294, 0.681, 0.681])

Active map

Locked colors

Locked maps icon

Inactive map

Self-illumination can use a color if the Color option is enabled. If this option is disabled, a spinner appears that enables you to adjust the amount of default color used for illumination. Materials with a Self-illumination value of 100 or a bright color like white lose all shadows and appear to glow from within. This happens because the self-illumination color replaces the ambient color, but a material with self-illumination can still have specular highlights. To remove the effect of Self-illumination, set the spinner to 0 or the color to black. Figure 16.3 shows a sphere with Self-illumination values (from left to right) of 0, 25, 50, 75, and 100.

The Opacity spinner sets the level of transparency of an object. A value of 100 makes a material completely opaque, while a value of 0 makes the material completely transparent. Use the Background button (located on the upper-right side of the Material Editor) to enable a patterned background image to make it easier to view the effects of the Opacity setting. Figure 16.4 shows materials with Opacity values of 10, 25, 50, 75, and 90.