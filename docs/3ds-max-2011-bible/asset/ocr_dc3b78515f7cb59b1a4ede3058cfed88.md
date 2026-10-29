# FIGURE 26.1

The Paint Deformation brush looks like a circle that follows the surface.

Paint Deformation brush

![](bbox=[0.085, 0.255, 0.845, 0.71])

Dragging the Paint Deformation brush over the object surface deforms the surface by moving the vertices within the brush's area. The direction that the vertices are moved follows the surface normals by default, or you can have the deformation follow a deformed normal or along a specified transform axis. For example, if you select to deform vertices along the X-axis, then all vertices underneath the brush are moved along the X-axis as the brush is dragged over the surface.

# Note

Deformations created using the Paint Deformation brushes cannot be animated. For objects with the Edit Poly modifier applied, the Paint Deformation brushes are disabled when in Animate mode.

The Push/Pull value determines the distance that the vertices are moved, thereby setting the amount of the deformation. The Brush Size sets the size (or radius) of the brush and determines the area that is deformed. The Brush Strength value sets the rate at which the vertices are moved. For example, if the Push/Pull Value is set to 100 mm, then a Brush Strength value of 1.0 causes the vertices directly under the brush center to move 100 mm; a Brush Strength value of 0.4 causes the same vertices to move only 40 mm.

# Tip

Holding down the Shift and Alt keys while dragging in the viewports lets you interactively change the Brush Strength value.