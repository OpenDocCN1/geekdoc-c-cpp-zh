# ## 20.1 The Problem

There are several things that a good decal system should solve:

+   1. The system should integrate well with lighting. Decals should not only change the color, but also change the normal, specular factors, and any other surface parameters such that they become indistinguishable from all other geometry.

+   2. Decals should work convincingly on all surfaces, static and dynamic.

+   3. Decals need to clip properly to geometry boundaries, and possibly even wrap around corners.

+   4. The system needs to work with geometry that might be very different from the geometry used for collision detection.

Item 1 in this list is easily solvable when the graphics engine includes deferred rendering capabilities [2]. For forward renderers, the system in this gem can still be used, but some modifications will be necessary. For a thorough explanation of deferred shading, please refer to [3,4,5,6].

Item 2 can be solved if we can get our hands on a free 8-bit channel in the G-buffer. If not, we can at least make it work on static geometry. This is discussed in Section 20.5.

Item 3 is where the real problems begin. The decal needs to follow the surface to which it is applied, even if that surface is highly tessellated. Some existing decal rendering techniques generate a triangle representation for a decal on such a surface [1], but this can be computationally expensive. Furthermore, the raw mesh is often not available at all on the CPU since the mesh data is loaded into a vertex buffer accessible only by the GPU at a reasonable speed.