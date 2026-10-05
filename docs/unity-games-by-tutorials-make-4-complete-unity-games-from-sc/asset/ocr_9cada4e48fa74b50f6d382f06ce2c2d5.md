Unity Games by Tutorials

Chapter 6: Animation

You'll now have a new empty state.

![](bbox=[0.312, 0.129, 0.687, 0.233])

Select this new state and name it WallsRaise in the Inspector. Next, drag the Walls animation from the Animations folder to the Motion property. Finally, set the speed to -1.

![](bbox=[0.312, 0.323, 0.687, 0.556])

The Motion property references the actual animation clip. In this case, you're using the same animation clip that you used in WallsLower. The Speed property lets designate how fast the clip will play. Setting the speed to 1 indicates that it will play at normal speed. Higher numbers make the clip run slower, whereas lower numbers make it run faster.

Why - 1? Negative numbers play the clip in reverse. In this case, you're using the same clip playing it in reverse at normal speed.

You need one more state: An idle state. Open the Animation window, making sure the BobbleArena is selected in the Hierarchy. You'll see the name of the currently displayed animation in the property list, which will be walls.

Click Walls and select Create New Clip... from the drop-down.

raywenderlich.com

163