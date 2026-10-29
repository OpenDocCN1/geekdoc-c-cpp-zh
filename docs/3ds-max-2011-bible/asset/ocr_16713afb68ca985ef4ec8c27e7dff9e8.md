# Part VI: Advanced Modeling

# FIGURE 27.16

The Loft compound object rollouts

![](bbox=[0.06, 0.16, 0.53, 0.42])

# TABLE 27.1

# Path Rollout Buttons

| Toolbar Button | Name | Description |
|---|---|---|
| Pick Shape | Selects a new cross-section spline to be inserted at the specified location |
| Previous Shape | Moves to the previous cross-section shape along the Loft path |
| Next Shape | Moves to the next cross-section shape along the Loft path |

# Setting skin parameters

The Skin Parameters rollout includes many options for determining the complexity of the Loft skin. You can specify whether to cap either end of the Loft using the Cap Start and/or Cap End options. The caps can be either Morph or Grid type.

This rollout also includes the following options for controlling the look of the skin:

+   - Shape and Path Steps: Sets the number of segments that appear in each spline's cross-sectional shape and between each division along the path. The straight segments are ignored if the Optimize Path option is selected.
+   - Optimize Shapes and Paths: Reduces the Loft's complexity by deleting any unneeded edges or vertices.
+   - Adaptive Path Steps: Automatically determines the number of steps to use for the path in order to maintain a smooth curve.