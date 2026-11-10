![](bbox=[0.163, 0.11, 0.837, 0.4])

**Figure 17.10**  
Side-by-side output of Program 17.3 using Google Cardboard

Hardware for testing anaglyph examples, such as the one in Program 17.1, is considerably simpler. We use an inexpensive set of cardboard red/cyan glasses, which can be purchased online.

# SUPPLEMENTAL NOTES

The stereoscopic techniques described in this chapter constitute only a very basic introduction. Professional systems for movie theaters and VR games and applications typically utilize more sophisticated models and are more carefully tuned for the hardware being used. We have also ignored important related topics, such as retinal blur for depth of field rendering, which would be incorporated in a fully professional deployment. That said, it is fun to use the simple methods shown here to experience the various examples throughout the textbook with full 3D depth perception.

In just a few cases, there are some stumbling blocks. Some of the examples in the textbook utilize user-defined framebuffers for various purposes or render to textures, such as for building shadows, generating water effects, or doing ray tracing. In those cases, the C++ code would need to be further modified to manage the buffers. This is especially tricky in the water examples from Chapter 15, where the