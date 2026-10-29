# Part III: Modeling Basics

Thickness, the number of Sides, and the Angle values; for the Rectangular option, you can specify Length, Width, Angle, and Aspect values.

The Radial Thickness is the diameter of the renderable spline. The number of Sides sets the number of sides that make up the cross section of the renderable spline. The lowest value possible is 3, which creates a triangle cross section. The Length and Width values set the size along the Y-axis and X-axis, respectively, of the rectangular sides. The Angle value determines where the corners of the cross section of sides start, so you can set a three-sided spline to have a corner or an edge pointing upward. The Aspect value sets the ratio of the Length per Width. If the Lock icon to the right of the Aspect value is enabled, then the aspect ratio is locked, and changing one value affects the other.

# Note

**By default, a renderable spline has a 12-sided circle as its cross section.**

You can choose different rendering values for the viewport and for the renderer using the Viewport and Renderer options above the Radial option. Each of these settings can be enabled or disabled using the Enable in Renderer and Enable in Viewport options at the top of the Rendering rollout. Renderable splines appear as normal splines in the viewport unless the Enable in Viewport option is selected. The Use Viewport Settings option gives the option of setting the spline render properties different in the viewport and the renderer.

The Auto Smooth option and Threshold value offer a way to smooth edges on the renderable spline. If the angle between two adjacent polygons is less than the Threshold value, then the edge between them is smoothed. If it is greater than the threshold value, then the hard edge is preserved.

The Generate Mapping Coordinates option automatically generates mapping coordinates that are used to mark where a material map is placed, and the Real-World Map Size option allows real-world scaling to be used when mapping a texture onto the renderable spline.

# Cross-Ref

**To learn more about mapping coordinates and real-world scaling, see Chapter 17, “Adding Material Details with Maps.”**

# Interpolation rollout

In the Interpolation rollout, you can define the number of interpolation steps or segments that make up the shape. The Steps value determines the number of segments to include between adjacent vertices. For example, a circle shape with a Steps value of 0 has only four segments and looks like a diamond. Increasing the Steps value to 1 makes a circle out of eight segments. For shapes composed of straight lines (like the Rectangle and simple NGons) the Steps value is set to 0, but for a shape with many sides (like a Circle or Ellipse) the Steps value can have a big effect. Larger step values result in smoother curves.

The Adaptive option automatically sets the number of steps to produce a smooth curve by adding more interpolation points to the spline based on the spline’s curvature. When the Adaptive option is enabled, the Steps and Optimize options become disabled. The Optimize option attempts to reduce the number of steps to produce a simpler spline by eliminating all the extra segments associated with the shape.

# Note

**The Section and Helix shape primitives have no Interpolation rollout.**