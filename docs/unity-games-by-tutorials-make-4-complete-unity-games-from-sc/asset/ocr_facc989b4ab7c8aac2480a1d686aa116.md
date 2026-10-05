You'll do this now to assemble your marine.

Select BobbleMarine-Body, and in the Inspector, set Position to (0, 0, 0). Go select BobbleMarine-Head and set Position to (-1.38, 6.16, 1.05) in the Inspector.

Congratulations! Your hero is assembled.

# Positioning the marine

Now it's time to place the space marine in its proper starting position. Select BobbleArena, and in the Inspector, check the box next to the name to re-enable it.

Select SpaceMarine, and in the Inspector, set the position to (-4.9, 12.54, 5.87). Also, set the rotation to (0, 0, 0). Your marine should end up directly over the hatch. If this isn't the case, feel free to tweak the values until that is the case.

Once the hero is in place, press F in the Scene view you can see him standing proud.

![](bbox=[0.271, 0.408, 0.727, 0.643])

The hero should now be positioned precisely over the elevator, ready to rock. Unfortunately for him, his grandiose rock party will degrade into a bug hunt.

# Creating a prefab

This game features crawly bugs and, like the hero, they're composed of many pieces. Some assembly is required.

In the Hierarchy, click the Create button and select Create Empty from the drop-down menu. Single-click the GameObject to name it Alien.