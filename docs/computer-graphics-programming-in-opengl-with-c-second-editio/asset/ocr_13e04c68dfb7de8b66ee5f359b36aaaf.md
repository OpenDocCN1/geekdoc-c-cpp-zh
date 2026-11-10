Mipmapping works by a clever mechanism for storing a series of successively lower-resolution copies of the same image in a texture image one-third larger than the original image. This is achieved by storing the R, G, and B components of the image separately in three-quarters of the texture image space, then repeating the process in the remaining one-quarter of the image space for the same image at one-quarter the original resolution. This subdividing repeats until the remaining quadrant is too small to contain any useful image data. An example image and a visualization of the resulting mipmap is shown in Figure 5.10.

![](bbox=[0.141, 0.296, 0.857, 0.638])

**Figure 5.10**  
Mipmapping an image.

This method of stuffing several images into a small space (well, just a bit bigger than the space needed to store the original image) is how mipmapping got its name. MIP stands for *Multum In Parvo* [Wl83], which is Latin for “much in a small space.”

When actually texturing an object, the mipmap can be sampled in several ways. In OpenGL, the manner in which the mipmap is sampled can be chosen by setting the GL_TEXTURE_MIN_FILTER parameter to the desired *minification* technique, which is one of the following:

+   - **GL_NEAREST_MIPMAP_NEAREST** chooses the mipmap with the resolution most similar to that of the region of pixels being textured. It then obtains the nearest texel to the desired texture coordinates.