
To understand why a high texel density causes texels to appear to be missing, we need to look more closely at how texture sampling works in general. Recall that textures use UV coordinates (also called texture coordinates) in the range of (0, 0) for the top-left corner and (1, 1) for the bottom-right corner.

Suppose you have a texture that’s a 4×4 square of texels. In this case, the UV coordinate for the center of the top-left texel is (0.125, 0.125). Similarly, the exact center of the texture corresponds to the UV coordinate (0.5, 0.5), as in Figure 13.2(a).

Now suppose you have a texel density of 1:2, and you draw the region of the texture from (0, 0) to (0.5, 0.5). This means that the top one-fourth of the texture appears at two times the size onscreen. When drawing this in the fragment shader, each fragment (pixel) gets a UV coordinate corresponding to the center of the pixel. For example, the top-left pixel in Figure 13.2(b) is sampling from the texture with a UV coordinate of (0.0625, 0.0625). However, in the original image, no texel’s center directly corresponds to this coordinate. This is where a filtering algorithm comes in: It helps select what color to draw for these in-between UV coordinates.

In nearest-neighbor filtering, you simply select the texel whose center is the closest to that UV coordinate. So, because the top-left coordinate of (0.0625, 0.0625) is closest to the white texel at (0.125, 0.125), nearest-neighbor filtering selects white for that pixel. The result of this is that every texel is resized proportionally to the texel density, as in Figure 13.2(b). More plainly, in nearest-neighbor filtering, increasing the size of the texture onscreen increases the perceived size of each texel, making the image look pixelated.

In **bilinear filtering**, you find the four texel centers closest to a UV coordinate, and the sampled color at a UV coordinate is the weighted average between these four nearest texels. This yields a smoother transition as the image magnifies, though the image will appear blurry if magnified too much. Figure 13.2(c) illustrates bilinear filtering. Notice that there are fewer neighboring pixels with the same color, but instead the colors blend together.

![](img/e9afcec1487716b0ef80d7e7c09869c8_840_0.png)

Figure 13.2 (a) Original texture; texture at 2x magnification with (b) nearest-neighbor filtering and (c) bilinear filtering

To understand how to calculate the weighted average in bilinear filtering, remember that you can treat a color as a 3D value and interpolate between colors the same way you interpolate other values. You then decompose the bilinear interpolation into the two separate axes' interpolations. Consider a point P that's nearest the four texels A, B, C, and D, as in Figure 13.3. First, you compute the interpolation between the colors at A and B in the u direction and, similarly, the interpolation between C and D in the u direction. This yields colors at the two points R and S, shown in Figure 13.3. Finally, you interpolate the colors at R and S in the v direction, which yields the final color at P.

![](img/e9afcec1487716b0ef80d7e7c09869c8_841_0.png)

**Figure 13.3** Bilinear interpolation of P relative to texels A, B, C, and D

Given the texture coordinates for A, B, C, D, and P, you can calculate this bilinear interpolation with the following set of equations:

```
uFactor = 1 - (P.u - A.u) / (B.u - A.u)
R_color = uFactor * A_color + (1 - uFactor) * B_color
S_color = uFactor * C_color + (1 - uFactor) * D_color
vFactor = 1 - (P.v - A.v) / (C.v - A.v)
P_color = vFactor * R_color + (1 - vFactor) * S_color
```

In these equations, uFactor determines the weighting in the u component direction, and vFactor determines the weighting in the v component direction. You then use these weightings to first calculate the colors at R and S and then, finally, the color at P.

These bilinear filtering calculations automatically occur on the graphics card if the texture has bilinear filtering enabled. And although this sounds like a lot of calculations to do for every fragment that samples the texture, modern graphics hardware can rapidly perform millions of such calculations per second.

As you've seen, magnifying the texture too much causes the image to appear either pixelated or blurry, depending on the technique used. The issue with reducing the size of the texture is that there aren't enough texture samples to maintain all the information stored in the texture. Returning to the example texture, if you reduce the size of the image by a factor of two, the filtering loses details from the texture, as in Figure 13.4(b). You no longer see the border, as in the original image. This example is especially dramatic because you have only four pixels left after the size reduction.

![](img/e9afcec1487716b0ef80d7e7c09869c8_843_0.png)

Figure 13.4: (a) Original texture; (b) texture bilinear filtered to half size

## Mipmapping

In mipmapping, rather than having a single source texture, you generate a series of additional textures, called mipmaps, that are at lower resolutions than the source texture. For example, if the source texture has a resolution of 256x256, you may generate mipmaps of 128x128, 64x64, and 32x32. Then, when it's time to draw the texture onscreen, the graphics hardware can select the mipmap texture that yields a texel density closest to 1:1. While mipmapping doesn't improve texture quality when you're magnifying a texture to a resolution higher than the original resolution, it greatly improves the quality when you're reducing the size of a texture.

The main reason for the quality improvement is that you generate the mipmap textures only once—at the time the texture is loaded. This means that you can use more expensive algorithms that generate high-quality mipmaps (such as using a box filter). Thus, sampling from these high-quality mipmaps with a texel density close to 1:1 will look much better than sampling from the original texture with some higher texel density, such as 4:1.

Figure 13.5 illustrates sample mipmaps for the star texture. The highest-resolution texture is the original texture at 256×256, and the remaining textures are auto-generated mipmaps. Note how even the smallest mipmap maintains the border of the texture, which was missing previously when you directly sampled from the 256×256 texture at a low texel density.

![](img/e9afcec1487716b0ef80d7e7c09869c8_845_0.png)

Figure 13.5 Star texture with three mipmap textures

Much as texture sampling can use nearest-neighbor filtering or bilinear filtering, there are two different approaches to applying mipmaps. In **nearest-neighbor mipmapping**, you simply select the mipmap that gives the texel density closest to 1:1. Although this works well in many cases, in some instances (such as with a floor texture), it may cause banding at the borders where the mipmap texture (or **mip level**) changes. In **trilinear filtering**, you sample the two mip levels closest to a 1:1 texel density separately (with bilinear filtering), and the final color is a blend between these two samples. This is “trilinear” because it blends now in three dimensions— the UV coordinates of the texture samples as well as the mip-level blend.

Enabling mipmapping for a texture in OpenGL is straightforward. After loading a texture with the code from Chapter 5, you simply add a call to glGenerateMipmap:

Click here to view code image

```
glGenerateMipmap(GL_TEXTURE_2D);
```

This automatically generates appropriate mip levels, using a high-quality filtering algorithm.

When setting texture parameters, you can set both the minimization filter (what happens when the texture becomes smaller onscreen) and the magnification filter (what happens when the texture becomes larger onscreen). This is what the GL_TEXTURE_MIN_FILTER and GL_TEXTURE_MAG_FILTER parameters reference.

After you’ve generated the mipmaps, you then change the texture parameter for the min filter to use mipmapping. To do trilinear filtering, you use these texture parameters:

Click here to view code image

```
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER,
GL_LINEAR_MIPMAP_LINEAR);
```
