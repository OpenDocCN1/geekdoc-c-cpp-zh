![](bbox=[0.14, 0.12, 0.55, 0.32])

Aliasing is evident near the top of the image, where the under-sampling of the checkerboard has produced a “striped” effect. Although we can't show it here in a still image, if this were an animated scene, the patterns would likely undulate between various incorrect patterns such as this one.

**Figure 5.8**
'Sparkling' in a texture map.

Another example appears in Figure 5.8, in which the cube has been textured with an image of the surface of the moon [HT12].

At first glance, this image appears sharp and full of detail. However, some of the detail at the upper right of the image is false and causes “sparkling” as the cube object (or the camera) moves. (Unfortunately, we can't show the sparkling effect clearly in a still image.)

These and similar sampling error artifacts can be largely corrected by a technique called *mipmapping*, in which different versions of the texture image are created at various resolutions. OpenGL then uses the texture image that most closely matches the resolution at the point being textured. Even better, colors can be averaged between the images closest in resolution to that of the region being textured. Results of applying mipmapping to the images in Figure 5.7 and Figure 5.8 are shown in Figure 5.9.

![](bbox=[0.14, 0.59, 0.86, 0.85])

**Figure 5.9**
Mipmapped results.