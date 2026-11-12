in Unity. Or, create a plane for a wall that was completely invisible in Unity. Turning this on will give you a better idea of how things will appear in Unity.

# ## Roof Creation

**Step 22:** Create a roof. Figure 2.22 shows a collection of cubes with one big plane across the top. The exact shape of this is unimportant, so don’t worry about that (although it’s safe to assume that the long vertical beams are paired 2×6s and the shorter horizontal ones are 2×4s). The importance of this is how we are going to optimize this form.

![](bbox=[0.515, 0.378, 0.735, 0.466])

FIGURE 2.22 *Untitled, document1.mb*

# ### Tips and Tricks

The roof shown in Figure 2.22 has a few additional extrusions (extruding edges instead of faces to get the outcropping bits), but to start with it was a single 1 Subdivision × 1 Subdivision plane. Working with planes (like the top of this roof unit) can be among the most efficient uses of polys available (a 1×1 subdivision plane is one—yes one—four-sided poly). However, remember that this one polygon has a front and a back. Since Backface Culling is turned on, quickly it will become apparent that the plane disappears if being viewed from the “wrong” side. Remember that we will be below this roof looking up, so make sure and either rotate the roof so its face is facing down, or use Polygons>Normals>Reverse to make sure the plane can be seen when the player is beneath it and looking up.

# ### Tips and Tricks

When working with something with regular repetitions like this roof has, use Maya’s Duplicate (Edit>Duplicate) and Duplicate With Transform (Edit>Duplicate With Transform). Create one cube. Ctrl-D will duplicate it, and if you move immediately in one move (with one click and drag) and press Shift-D, Maya will duplicate again, offsetting the new duplicate by the same amount as the last copy was moved. It’s a quick way to create lots of equally spaced copies.