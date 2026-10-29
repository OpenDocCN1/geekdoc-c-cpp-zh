# Chapter 22: Animating with Constraints and Simple Controllers

Figure 22.2 shows the tire as it moves down the hill. In the Top view, you can see the function curves for this motion.

# FIGURE 22.2

The Surface constraint can animate one object moving across the surface of another.

![](bbox=[0.02, 0.27, 0.78, 0.81])

# Path constraint

The Path constraint lets you select a spline path for the object to follow. The object is locked to the path and follows it even if the spline is changed. This is one of the most useful constraints because you can control the exact motion of an object using a spline. With Max's spline features, you can control very precisely the motions of objects that are constrained with the Path constraint. A good example of this constraint is an animated train following a track. Using a spline to create the train tracks, you can easily animate the train using the Path constraint.

When you choose the Animation ⇔ Constraints ⇔ Path Constraint menu command, you can select a single path for the object to follow. This path is added to a list of paths in the Path Parameters rollout.

The Path Parameters rollout also includes Add and Delete Path buttons for adding and deleting paths to and from the list. If two paths are added to the list, then the object follows the position centered between these two paths. By adjusting the Weight value for each path, you can make the object favor a specific path.

The Path Options include a % Along Path value for defining the object's position along the path. This value ranges from 0 at one end to 100 at the other end. The Follow option causes the object to be aligned with the path as it moves, and the Bank option causes the object to rotate to simulate a banking motion.