With the world transform and view-projection matrices added to the shader, you now can see the individual sprite components in the world at arbitrary positions, scales, and rotations, as in Figure 5.7. Of course, all the rectangles are just a solid color for now because `Basic.frag` just outputs blue. This is the last thing to fix to achieve feature parity with the SDL 2D rendering from the previous chapters.

![](bbox=[0.17, 0.39, 0.72, 0.72])

**Figure 5.7** Drawing sprite components with different world transform matrices

# TEXTURE MAPPING

**Texture mapping** is a technique for rendering a