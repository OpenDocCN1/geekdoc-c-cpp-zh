resulting from rigid objects moving in the scene is shown. Both translational and rotational motion are visible in this still image. (Images courtesy of Terathon Software LLC.)

![](bbox=[0.17, 0.17, 0.41, 0.5])

# Figure 17.2: Motion blur resulting from vertex movement on a skinned character model. (Image courtesy of Terathon Software LLC.)

At the end of the rendering process for a single frame, we apply to the entire screen a post-processing shader that generates the motion blur effect using the data stored in the velocity buffer. This shader can usually be combined with other post-processing effects such as glow, distortion, and color matrix application. The shader that generates the motion blur reads the screen-space velocity for each pixel from the velocity buffer and uses it to choose a set of sample points at which the color buffer is then read. These color samples are distributed along the direction of the velocity, and they are spread over a larger distance for higher velocities. After the color samples are collected, they are combined to generate the final color for each pixel.

It is not always the case that we want to use all of the color