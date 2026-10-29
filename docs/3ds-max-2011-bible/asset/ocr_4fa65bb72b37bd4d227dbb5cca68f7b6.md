# Conform

The Conform Space Warp pushes all object vertices until they hit another target object called the Wrap To Object, or until they’ve moved a preset amount. The Conform Parameters rollout includes a Pick Object button that lets you pick the Wrap To Object. The object vertices move no farther than this Wrap To Object.

You can also specify a Default Projection Distance and a Standoff Distance. The Default Projection Distance is the maximum distance that the vertices move if they don’t intersect with the Wrap To Object. The Standoff Distance is the separation amount maintained between the Wrap To Object and the moved vertices. Another option, Use Selected Vertices, moves only a subobject selection.

# Cross-Ref

The Conform Space Warp is similar in function to the Conform compound object that is covered in Chapter 27, “Working with Compound Objects.”

Figure 42.15 shows some text being deformed with the Conform Space Warp. A warped quad patch has been selected as the Wrap To object.

# FIGURE 42.15

The Conform Space Warp wraps the surface of one object around another object.

![](bbox=[0.07, 0.55, 0.92, 0.84])

# Bomb

The Bomb Space Warp causes an object to explode from its individual faces. The Strength value is the power of the bomb and determines how far objects travel when exploded. The Spin value is the rate at which the individual pieces rotate. The Falloff value defines the boundaries of faces affected by the bomb. Object faces beyond this distance remain unaffected. You must select Falloff On for the Falloff value to work.