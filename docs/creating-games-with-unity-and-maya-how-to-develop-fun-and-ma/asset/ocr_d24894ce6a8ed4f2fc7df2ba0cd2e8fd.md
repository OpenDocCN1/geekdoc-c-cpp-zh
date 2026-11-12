# Tutorial 16.2: Keys

Hopefully, this will be a fun tutorial. In the process of this tutorial, we'll make use of the techniques we've covered in the past tutorials. By assembling these skills in a new way, we'll have a new mechanism in the game.

The process will go like this: First we'll need to create a trigger that checks to see if the player has the key when the player enters it. If the player does indeed have the key, the door will open; if the player does not, a text prompt will pop up to alert the player that he needs the key. We'll create a PickUpKey function that fires when the player's ray is cast upon the key and the player clicks it. When the player clicks the key, we'll make the key disappear from the scene, but create a GUI element to indicate that the key is on the player's person. It's going to be fun!

+   1. **Step 1:** Create a new GUITexture to show the key. Create a new GUITexture (`GameObject>Create Other>GUITexture`) and name it `KeyIcon`. Use the texture `Icon-Key` from the 2D Assets folder to define its texture.
+   2. **Step 2:** Place the key in the top-right corner of the screen. Select `KeyIcon` in the Hierarchy and in the Inspector change the Transform X and Y values to 1. Change the Pixel inset values to X = -70, Y = -70, Width = 64, Height = 64 (Figure 16.6).

![](bbox=[0.398, 0.5, 0.867, 0.73])

# Why?

The image is 64x64. With the GUITexture at 1,1,0, the bottom-left corner of the image is at the top-left corner of the screen, meaning that the image is off the screen. By offsetting the pixels by -70 in both X and Y, we slide the image back onto the screen with a 6-pixel buffer above and to the right.

+   3. **Step 3:** Now that you can see what it will look like when visible, move it off the screen. Select `KeyIcon` in the Hierarchy and in the Inspector, change the Transform X = 1, 1.