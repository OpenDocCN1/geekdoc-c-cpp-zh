using an interpolator. The pixel shader can then use these UV coordinates to look up the post-process volume's z-value in the depth texture, as illustrated in Figure 5.8.3.

![](bbox=[0.27, 0.16, 0.88, 0.45])

These two z-values are compared in the pixel shader, and alpha testing is used to mask which pixels get written to the frame buffer. If the z-value of the scene pixel is greater than the post-process volume's, the alpha of the resulting pixel is set to 1, otherwise, it is set to 0. With an alpha test compare function of greater-than and an alpha reference value of 0, this allows us to kill pixels that are in front of the post-process volume. We could alternatively use the assembly texkill (or HLSL clip() ) intrinsic to perform this conditional pixel killing.

After our rendering pass, what we will have is a rendered scene that is “clipped away” by our post-process volume mesh at the pixel level. The post-process volume mesh used for this clipping operation can be arbitrarily complicated, as shown in Figure 5.8.4.

![](bbox=[0.37, 0.72, 0.77, 0.95])