+   - **GL_LINEAR_MIPMAP_NEAREST** chooses the mipmap with the resolution most similar to that of the region of pixels being textured. It then interpolates the four texels nearest to the texture coordinates. This is called “linear filtering.”
+   - **GL_NEAREST_MIPMAP_LINEAR** chooses the two mipmaps with resolutions nearest to that of the region of pixels being textured. It then obtains the nearest texel to the texture coordinates from each mipmap and interpolates them. This is called “bilinear filtering.”
+   - **GL_LINEAR_MIPMAP_LINEAR** chooses the two mipmaps with resolutions nearest to that of the region of pixels being textured. It then interpolates the four nearest texels in each mipmap and interpolates those two results. This is called “trilinear filtering” and is illustrated in Figure 5.11.

![](bbox=[0.287, 0.424, 0.701, 0.666])

![](bbox=[0.141, 0.704, 0.479, 0.921])

Trilinear filtering is usually preferable, as lower levels of blending often produce artifacts, such as visible separations between mipmap levels. Figure 5.12 shows a close-up of the checkerboard using mipmapping with only linear filtering enabled. Note the circled artifacts where the vertical lines suddenly change from thick to thin at a mipmap boundary. By contrast, the example in Figure 5.9 used trilinear filtering.