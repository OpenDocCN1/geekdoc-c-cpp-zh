What lies between the vertex and fragment shaders is a mini-pipeline of several modules,⁵ shown in Figure 16.5 as a single box. They work together to complete the transformation pipeline to convert to window coordinates, to perform clipping/culling against the view frustum, and to perform rasterization to produce a sequence of output fragments.

The **fragment shader** (whose equivalent in Direct3D is called the “pixel shader”) is called once for each fragment and receives the fragment’s location (in window coordinates) and the already-interpolated varying outputs from the vertex shader. In very simple cases, the fragment shader often does nothing but pass the color unchanged through to the next stage, but the fragment shader is essential for lighting algorithms for which simple linear interpolation between vertices is insufficient, and is also instrumental in special effects such as blurring.

At the end of the pipeline lie the per-fragment operations, similar to those found in the OpenGL FF pipeline.

# 16.3.2  The Nature of the Core API

The OpenGL Core API retains only a fraction of the entry points that were present to support the FF pipeline. The techniques for specifying and transmitting textures and meshes have not changed significantly, and end-of-pipeline activities like blending and double-buffering are similar. However, all other information and operations now lie inside in the uniforms, attributes, and shader code. The leaner OpenGL Core API is mostly concerned with activities of the following types:

+   - Buffer object management—control over all data stored on the GPU, including allocation/deallocation and data transmission
+   - Drawing commands—sending meshes down the pipeline
+   - Shader-program management—downloading, compiling, activating, and setting up uniforms and attributes
+   - Texturing management—installation and management of texture data structures for use by vertex and fragment shaders
+   - Per-fragment operations—control over per-fragment operations at the end of the pipeline, such as blending and dithering
+   - And framebuffer direct access—pixel-level read/write access

# 16.4  Architectures of Graphics Applications

We now discuss the general structure of a typical graphics application, some approaches to speed up certain parts of this structure, and various kinds of software designed to offload that work from the typical designer.

# 16.4.1  The Application Model

A typical 3D application includes an **application model (AM)**—a collection of data, resident in a database or in data structures, whose application-domain

⁵. On some hardware platforms, this part of the pipeline is also programmable, through use of a third type of shader, known as a “geometry shader.”