![](bbox=[0.174, 0.103, 0.466, 0.416])

**FIGURE 6.25** Smoke puff used as basis of steam (Smoke0170 (Texture: #43653) at (G)Textures).

![](bbox=[0.606, 0.104, 0.907, 0.329])

**FIGURE 6.26** Cropping to create square image.

![](bbox=[0.165, 0.473, 0.455, 0.702])

**FIGURE 6.27** Cloning in soft edges everywhere.

![](bbox=[0.6, 0.473, 0.895, 0.699])

**FIGURE 6.28** Softened image due to Gaussian blur.

Step 12: Resize the image to 512×512. Do this with Image>Image Size.

# **Why?**

512×512 is of course a power of two size and thus a quick renderer.

Step 13: Save the file to the Incursion–Unity project's Assets folder as WaterSteam_Color.

Step 14: Adjust the import settings to include alpha. Back in Unity, the WaterSteam_Color image should now appear in the Project panel. Select it and in the Inspector panel click the Generate Alpha from Grayscale checkbox. Click Apply.