![](bbox=[0.141, 0.11, 0.854, 0.309])

**Figure 16.28**

Output of Program 16.16 showing blending using the Sugita/Takeshaki RYB color conversion.

# SUPPLEMENTAL NOTES

Even the simple examples given in this chapter require significant computing cycles, and the later ones (Programs 16.13, 16.14, and 16.15) run very slowly. On a standard laptop, the reader can expect them to take several seconds or more to render, especially for large depth of recursion settings. On some machines, the default settings for the graphics card may cause OpenGL to time out, crashing the program before it has a chance to complete. On a Windows machine, the time limit is typically set to 2 seconds, but can be increased by increasing the TdrDelay registry setting. Instructions for doing this are widely available on the Web [A19]. The author set his timeout to 8 seconds. An appropriate value depends on the machine and the application. Be warned that making this change can also make it a bit more difficult to stop a runaway graphics process.

We have tried to write our compute shader code for readability rather than performance; e.g., our heavy use of conditionals (“if” statements) can slow execution. Tricks for removing conditionals can be found elsewhere [H13].

There are a few rather obvious things that we have not implemented in our ray tracer. One is the ability to rotate the sphere. Of course, if the sphere is a solid color or transparent, this is not an issue. However, if it is textured, such as in the examples utilizing the earth texture, it would be desirable to be able to rotate it to different orientations. Such a rotation can be incorporated in the same manner as was done for the box and the plane.