# Unity Games by Tutorials

Notice Projection is set to Orthographic as discussed — you'll learn about the Camera's size property in a bit. The other properties will stay at their defaults.

In the Project browser, select the single-block.png sprite under the Sprites sub-folder, then take a look at the Inspector. You'll see that Pixels Per Unit is 100.

![](bbox=[0.217, 0.198, 0.782, 0.345])

What does 100 really mean?

In units, yours doesn't necessarily correspond to pixels on the screen. On some arbitrary scale, as 1 unit = 1 meter. Unity uses Pixels Per Unit to determine sprites' uncased size in units.

Consider this: An imported sprite is 500 pixels wide. The following table will give you an idea of how the GameObject's width would change on the X-axis with different Pixels Per Unit settings at various X-scales.

| Pixels to Units | X-scale | Width Calculation | Width |
| 100 | 0.5 | 500 / 100 * 0.5 | 2.5 units |
| 100 | 1.0 | 500 / 100 * 1.0 | 5.0 units |
| 100 | 2.0 | 500 / 100 * 2.0 | 10.0 units |
| 50 | 0.5 | 500 / 50 * 0.5 | 5.0 units |
| 50 | 1.0 | 500 / 50 * 1.0 | 10.0 units |
| 50 | 2.0 | 500 / 50 * 2.0 | 20.0 units |

Now consider an example from your game. The single-block sprite is 100 x 100 px with a Pix Per Unit value of 100. At a scale of 1 for X and Y, the single-block GameObject would be 1 unit wide and 1 unit tall.

Remember the Size property on the Orthographic Camera you saw a moment ago? With the Size to 5, you would need to stack ten single-block sprites atop each other to reach from bottom of the camera to the top of the camera's viewport. This is because Unity calculates the Orthographic size from the center of the screen to the top.