3. Finally, you do the actual turn by using Lerp(). Remember, Lerp() is used to change a value (which as rotation in this place) smoothly over time. To learn more about Lerp(), check out the Appendix, "Unity API."

Save your changes and go back to Unity. In the Hierarchy, select the SpaceMarine GameObjectObject. Look for the Player Controller script in the Inspector, and select Floor in the drop-down.

| Player Controller (Script) |
|---||
| Script | PlayerController |
| Move Speed | 50 |
| Head | BobbleMarine-Head (Rigidbody) |
| Layer Mask | Floor |

The last thing to do is assign the floor physics layer to the, er, floor. In the Hierarchy, expand the BobbleArenaand and select World_Centre. In the layer drop-down, select floor.

Play your game like you mean it.

![](bbox=[0.323, 0.447, 0.676, 0.683])

Now, the marine follows your mouse cursor and turns on a dime. Now you're playing with power! :)]

# Where to go from here?

Wow! That was quite a chapter! As you can see, the physics engine has a stockpile of features and does a lot of cool stuff. In this chapter, you learned about:

+   - Character Controllers and how they help simplify your code.