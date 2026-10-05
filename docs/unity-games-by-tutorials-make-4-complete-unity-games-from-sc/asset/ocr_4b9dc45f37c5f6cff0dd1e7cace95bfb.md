Since you are in Animation mode, you can think of this as "time traveling" to what the animation will look like at the 1:00 mark. You can see what it will look like in the Unity editor, and modify the values.

Note that if you don't move the scrubber exactly over the keyframes at the 1:00 mark, Unity will create new keyframes at the scrubber's current position.

Make sure that just **Outer_Wall_003** is selected, and in the Inspector, set the **y position** to **-0.48**. In the Scene view, you'll see the wall drop down.

![](bbox=[0.306, 0.266, 0.691, 0.458])

Do the same for **Outer_Wall_004** and **Outer_Wall_006**. The walls should look as follows:

![](bbox=[0.306, 0.515, 0.691, 0.696])

Now, **click** the animation **Play** button (in the Animation window, not the normal Play button). Just like that, you have moving walls!

| Animation | | | | | 0:00 | 0:10 | 0:20 | 0:30 | 0:40 | 0:50 | 1:00 |
|---|---|---|---|---|---|---|---|---|---|---|---|n| Walls | | | | | | | | | | |
| Outer_Wall_003 | Position | | | | | | | | | |
| Outer_Wall_004 | Position | | | | | | | | | |
| Outer_Wall_006 | Position | | | | | | | | | |
| Add Property | | | | | | | | | | |

Hit the animation **Play** button again to stop the looping animation. Note you can also move the scrubber on the timeline to see the interpolated values at any point.

When you finish, **click** the **Record** button to stop Record mode.