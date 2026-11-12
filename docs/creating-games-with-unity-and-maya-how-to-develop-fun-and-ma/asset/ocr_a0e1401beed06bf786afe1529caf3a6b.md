If Transform's Position X is 0.5, the bottom-left corner of the image will be in the middle of the screen horizontally. Then, if the Pixel Inset for X is set to the negative value of half the size of the image (offsetting the image half the width of the image to the left), the center of the image will be sitting at exactly halfway on the screen horizontally. So if the image is 512 pixels wide, having the Transform's Position X = 0.5 and the Pixel Inset X = -256, the center of the image (horizontally) will be at the horizontal center of the screen.

If the assumption is that the screen will be split about in half with the left half being Aegis spinning and the interface on the right half (or a little more than the right half), we can align the left corner of the image in the center of the screen (Transform's Position X = 0.5). Then, if it should be at the top we can change the Transform's Position Y = 1. Then change the Pixel Inset Y = -200 (this pulls it 200 pixels off the top of the screen).

![](bbox=[0.19, 0.4, 0.65, 0.75])

**Step 9:** Rename the GameObject to Incursion_Logo.
**Step 10:** Create another GUITexture and assign the texture Button_Mission to it. Change its Pixel Inset Width to 256 and Height to 64. Rename New Texture to Button_Mission.
**Step 11:** Change the Transform Position X=0. 5 and Y=0.

# Why?

This will roughly place this button at the bottom center of the screen. From here we can finesse its placement on the screen.