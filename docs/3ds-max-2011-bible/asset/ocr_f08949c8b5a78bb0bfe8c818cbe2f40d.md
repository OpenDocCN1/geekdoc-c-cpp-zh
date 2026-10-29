# Part III: Modeling Basics

# FIGURE 11.10

The Bend modifier can be used to bend trees.

![](bbox=[0.086, 0.159, 0.796, 0.559])

# Caution

In order for the Displace modifier to work, the surface requires a dense mesh, which can lead to very high polygon counts. ■

The Displace modifier parameters include Strength and Decay values. You can also specify the dimensions of the gizmo. A cylindrical-shaped gizmo can be capped or uncapped. The alignment parameters let you align the gizmo to the X-axis, Y-axis, or Z-axis, or you can align it to the current view. The rest of the parameters deal with displacing the surface using a bitmap image. Figure 11.11 shows a Quad Patch with the Plane-shaped gizmo applied with a Strength value of 25. To the right is a Quad Patch with the Sphere-shaped gizmo.

# Cross-Ref

The Displace modifier can also alter an object’s geometry using a grayscale bitmap image. This is similar to a Displacement map, which is covered in Chapter 17, “Adding Material Details with Maps.” In many ways, the Displace gizmo works like the Conform compound object. You can learn about the Conform compound object in Chapter 27, “Working with Compound Objects.”