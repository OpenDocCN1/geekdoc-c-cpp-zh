The problem is that Unity now attempts to automatically resize images to power of two textures. The problem is that 432×163 is not a power of two. This means that the image gets stretched (and thus mushy) so that even when it is defined as the Config Dialog Banner (Figure 18.10), it looks really bad in the final build (Figure 18.11).

![](bbox=[0.03, 0.235, 0.43, 0.492])

![](bbox=[0.48, 0.235, 0.87, 0.492])

The solution to this is simple but surprisingly poorly documented in the Dialog Banner support documents. We just need to make sure that Unity does not resize this particular image to a power of two image. To do this, select the file in the Project panel, and then in the Inspector change the Texture Type to Advanced. Change the nonpower-of-two drop-down menu to None and press the Apply button to reimport the file (Figure 18.12).

![](bbox=[0.24, 0.625, 0.94, 0.94])