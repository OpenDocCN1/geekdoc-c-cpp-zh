Unity Games by Tutorials

Chapter 12: Beginning Unity 2D

Select SuperSoyBoySprite.png under the Sprites folder in the Project browser. Click the expansion triangle to reveal the sliced sprites.

![](bbox=[0.218, 0.143, 0.779, 0.222])

Click and drag the run_0 sprite into the Scene view to create a new GameObject with the run_0 sprite. In the Hierarchy, set the name to SoyBoy. This GameObject is the size main for your character.

Create one more sprite in the scene by dragging the top-left-small.png sprite into the Scene view. Enter the value 59443CFF in the color picker.

Position the sprites side-by-side, ensuring they are within the camera's area view in the Scene view, and start the game. You will see the three sprites floating in space — they don't interact with the physics engine, so they know no gravity.

![](bbox=[0.313, 0.446, 0.684, 0.503])

You just completed Sprites 101. Well done!

# ## The 2D orthographic camera

By default, 2D projects use an orthographic camera. Generally, you'll want to stick with it instead of using a perspective camera. Remember: orthographic cameras just render the game view so that objects near and far are the same size — perfect for 2D!

These are the properties of the current Camera in the scene.

![](bbox=[0.238, 0.735, 0.746, 0.876])

raywenderlich.com 334