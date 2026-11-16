# # Volumetric Post-Processing

To apply our volumetric post-process, we will define the concept of a post-process volume. The post-process volume is a 3D object that will affect any scene pixels that are behind it. Figure 5.8.2 shows an example of a post-process volume.

![](bbox=[0.35, 0.2, 0.76, 0.4])

FIGURE 5.8.2 The post-process volume.

Unlike standard post-processes, we are using a 3D shape, not a 2D image-space rectangle, as our post-process region. The post-process volume defines a region—it is not meant to be rendered directly. The post-process volume could be a simple cube as shown in Figure 5.8.2 or it could be defined by a more arbitrary shape as discussed in [Oat04]. Naturally, some scene objects may penetrate the post-process volume, causing only a portion of the object to be distorted.

# ## Depth Awareness

With our post-process volume defined, we can classify our scene in two sets: regions that are behind the front of the volume and regions that are in front of it. We could simply sort the objects in our scene to try and figure out the spatial relationship with the post-process volume; however, this would not work for objects intersecting the volume and would not be robust in general for arbitrary scenes.

+   In effect, we need to:
+   * Render only objects that are behind or contained by our post-process volume to an offscreen render target.
+   * Apply the post-process effect (i.e., a warp to simulate refraction due to heat) to the render target.
+   * Render objects that are in front of the post-process volume.

The first problem is how to render only objects that are behind the post-process volume in image space. We would like to compare the z-values of the pixels of the scene