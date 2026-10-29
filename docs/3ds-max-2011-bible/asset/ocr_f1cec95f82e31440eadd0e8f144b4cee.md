# ## FIGURE 7.9

Transformation buttons and the Transform Gizmos were used to position this spaceship.

![](bbox=[0.077, 0.165, 0.788, 0.562])

# ## Using Pivot Points

An object's pivot point is the center about which the object is rotated and scaled and about which most modifiers are applied. Pivot points are created by default when an object is created and are usually created at the center or base of an object. You can move and orient a pivot point in any direction, but repositioning the pivot cannot be animated. Pivot points exist for all objects, whether or not they are part of a hierarchy.

# ## Caution

**Try to set your pivot points before animating any objects in your scene. If you relocate the pivot point after animation keys have been placed, all transformations are modified to use the new pivot point.**

# ## Positioning pivot points

To move and orient a pivot point, open the Hierarchy panel in the Command Panel and click the Pivot button. At the top of the Adjust Pivot rollout are three buttons; each button represents a different mode. The Affect Pivot Only mode makes the transformations buttons affect only the pivot point of the current selection. The object does not move. The Affect Object Only mode causes the object to be transformed, but not the pivot point. The Affect Hierarchy Only mode allows an object's links to be moved.

The pivot point is easily identified as the place where the Transform Gizmo is located when the object is selected, as shown in Figure 7.10.