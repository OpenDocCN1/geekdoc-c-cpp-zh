# Beast Settings

There are a couple of important settings I'd like to point out in the Bake tab. Now, each project will inevitably require a different setup, but I often find myself mainly adjusting the Quality, Bounce, Interpolation, and Resolution settings to get the detail and quality needed in the bake as shown in Fig. 8.21.

**Real-Time Lighting**
Back in Chapter 2, in the section "Using Lights," we discussed that real-time lighting can possibly reduce performance. Although it can be best to use real-time lighting sparingly, that doesn't mean you can't use it. Your game type will dictate what can and can't be done in terms of performance. Remember to always test and profile your game and make decisions accordingly.

![](bbox=[0.33, 0.243, 0.95, 0.666])

**FIG 8.21** These Are the Settings I Mainly Check to Adjust Quality.

The Quality setting is pretty self-explanatory as it simply adjusts the quality of the lightmap. A good tip when testing the bake is to lower the Resolution to a low value and setting the Quality to Low. This will speed up the bake and allow you to quickly see the map applied to the geometry.

The Quality will also adjust the Final Gather rays that are sent into the scene. The more the rays are shot out into the scene, the higher the quality of the indirect lighting will be. You can use the Quality presets or manually adjust the ray count. The Contrast Threshold and Interpolation also affect the Final Gather solution. The Contrast Threshold controls new rays from being created based of a color contrast threshold. Higher contrast values will produce smoother but less detailed lightmaps. If you are using a lower number of Final Gather rays, then you may need to increase the Contrast Threshold to be sure that extra rays are not created. The Interpolation controls the smoothing