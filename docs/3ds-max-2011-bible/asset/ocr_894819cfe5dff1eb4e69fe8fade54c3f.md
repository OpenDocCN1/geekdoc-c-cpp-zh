When the Backface Cull on Object Creation option is enabled, the backside of an object in wireframe mode is not displayed. If disabled, you can see the wireframe lines that make up the backside of the object. The Backface Cull option setting is determined when the object is created, so some objects in your scene may be backface culled and others may not be. Figure 4.23 includes a sphere and a cube on the left that are backface culled and a sphere and cube on the right that are not.

# FIGURE 4.23

Backface culling simplifies objects by hiding their backsides.

![](bbox=[0.04, 0.36, 0.42, 0.61])

# Note

The Object Properties dialog box also contains a Backface Cull option.

The Attenuate Lights option causes objects farther back in a viewport to appear darker. Attenuation is the property that causes lights to diminish over distance.

In the Viewport Configuration dialog box, you can set Safe Regions, which are borders that the renderer includes. The Mask Viewport to Safe Region option causes the objects beyond the Safe Region border to be invisible.

The Update Background While Playing option causes viewport background bitmaps to be updated while an animation sequence plays. Viewport backgrounds can be filtered if the Filter Environment Background option is enabled, but this slows the update time. If this option is disabled, the background image appears aliased and pixelated.

The Display World Axis option displays the axes in the lower-left corner of each viewport. This can be helpful as you learn to navigate in 3D space. The Grid Nudge Distance is the distance that an object moves when Grid Nudge (+ and – on the numeric keypad) keys are used. Objects without scale, such as lights and cameras, appear in the scene according to the Non-Scaling Object Size value. Making this value large makes lights and camera objects very obvious.

# Enabling ghosting

Ghosting is similar to the use of "onion skins" in traditional animation, causing an object's prior position and next position to be displayed. When producing animation, knowing where you're going and where you've come from is helpful.

Max offers several ghosting options. You can set whether a ghost appears before the current frame, after the current frame, or both before and after the current frame. You can set the total number of ghosting frames and how often they should appear. You also can set an option to show the frame numbers.