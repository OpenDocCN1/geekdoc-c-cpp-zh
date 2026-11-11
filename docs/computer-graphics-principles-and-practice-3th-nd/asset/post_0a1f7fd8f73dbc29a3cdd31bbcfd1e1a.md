
This leaves us with two choices when designing an algorithm with more significant processing, especially at the pixel level. The first choice is to build a hybrid renderer that performs some of the processing on a more general processor, such as the host, or perhaps on a general computation API (e.g., CUDA, DirectCompute, OpenCL, OpenGL Compute). Hybrid renderers typically incur the cost of additional memory operations and the associated synchronization complexity.

The second choice is to frame the algorithm purely in terms of rasterization operations, and make multiple rasterization passes. For example, we can’t conveniently cast shadow rays in most hardware rendering APIs today. But we can sample from a previously rendered shadow map.

Similar methods exist for implementing reflection, refraction, and indirect illumination purely in terms of rasterization. These avoid much of the performance overhead of hybrid rendering and leverage the high performance of hardware rasterization. However, they may not be the most natural way of expressing an algorithm, and that may lead to a net inefficiency and certainly to additional software complexity. Recall that changing the order of iteration from ray casting to rasterization increased the space demands of rendering by requiring a depth buffer to store intermediate results. In general, converting an arbitrary algorithm to a rasterization-based one often has this effect. The space demands might grow larger than is practical in cases where those intermediate results are themselves large.

Shading languages are almost always compiled into executable code at runtime, inside the API. That is because even within products from one vendor the underlying micro-architecture may vary significantly. This creates a tension with the compiler between optimizing the target code and producing the executable quickly. Most implementations err on the side of optimization, since shaders are often loaded once per scene. Beware that if you synthesize or stream shaders throughout the rendering process there may be substantial overhead.

Some languages (e.g., HLSL and CUDA) offer an initial compilation step to an intermediate representation. This eliminates the runtime cost of parsing and some trivial compilation operations while maintaining flexibility to optimize for a specific device. It also allows software developers to distribute their graphics applications without revealing the shading programs to the end-user in a human-readable form on the file system. For closed systems with fixed specifications, such as game consoles, it is possible to compile shading programs down to true machine code. That is because on those systems the exact runtime device is known at host-program compile time. However, doing so would reveal some details of the proprietary micro-architecture, so even in this case vendors do not always choose to have their APIs perform a complete compilation step.

### 15.7.2.4 Executing Draw Calls

To invoke the shaders we issue `draw calls`. These occur on the host side. One typically clears the framebuffer, and then, for each mesh, performs the following operations.

- 1. Set fixed-function state.
- 2. Bind a shader.
- 3. Set shader arguments.
- 4. Issue the draw call.

These are followed by a call to send the framebuffer to the display, which is often called a **buffer swap**. An abstracted implementation of this process might look like Listing 15.35. This is called from a main rendering loop, such as Listing 15.36.

*Listing 15.35: Host code to set fixed-function state and shader arguments, and to launch a draw call under an abstracted hardware API.*

```cpp
void loopBody(RenderDevice* gpu) {
    gpu->setColorClearValue(Color3::cyan() * 0.1f);
    gpu->clear();

    const Light& light = scene.lightArray[0];

    for (unsigned int m = 0; m < scene.meshArray.size(); ++m) {
        Args args;
        const Mesh& mesh = scene.meshArray[m];
        const shared_ptr<BSDF>& bsdf = mesh.bsdf();

        args.setUniform("fieldOfViewX",         camera.fieldOfViewX());
        args.setUniform("zNear",                camera.zNear);
        args.setUniform("zFar",                 camera.zFar);

        args.setUniform("lambertian",           bsdf->lambertian);
        args.setUniform("glossy",               bsdf->glossy);
        args.setUniform("glossySharpness",      bsdf->glossySharpness);

        args.setUniform("lightPosition",        light.position);
        args.setUniform("lightPower",           light.power);

        args.setUniform("shadowMap",            shadowMap);

        args.setUniform("width",                gpu->width());
        args.setUniform("height",               gpu->height());

        gpu->setShader(shader);

        mesh.sendGeometry(gpu, args);
    }
    gpu->swapBuffers();
}
```

*Listing 15.36: Host code to set up the main hardware rendering loop.*

```cpp
OSWindow::Settings osWindowSettings;
RenderDevice* gpu = new RenderDevice();
gpu->init(osWindowSettings);

// Load the vertex and pixel programs
shader = Shader::fromFiles("project.vrt", "shade.pix");

shadowMap = Texture::createEmpty("Shadow map", 1024, 1024,
    ImageFormat::DEPTH24(), Texture::DIM_2D_NPOT, Texture::Settings::shadow());
makeTrianglePlusGroundScene(scene);

12 // The depth test will run directly on the interpolated value in
13 // o.z/o.w, which is going to be smallest at the far plane
gpu->setDepthTest(RenderDevice::DEPTH_GREATER);
gpu->setDepthClearValue(0.0);

while (! done) {
    loopBody(gpu);
    processUserInput();
}

...
```

## 15.8 Performance and Optimization

We’ll now consider several examples of optimization in hardware-based rendering. This is by no means an exhaustive list, but rather a set of model techniques from which you can draw ideas to generate your own optimizations when you need them.

### 15.8.1 Abstraction Considerations

Many performance optimizations will come at the price of significantly complicating the implementation. Weigh the performance advantage of an optimization against the additional cost of debugging and code maintenance. High-level algorithmic optimizations may require significant thought and restructuring of code, but they tend to yield the best tradeoff of performance for code complexity. For example, simply dividing the screen in half and asynchronously rendering each side on a separate processor nearly doubles performance at the cost of perhaps 50 additional lines of code that do not interact with the inner loop of the renderer.

In contrast, consider some low-level optimizations that we intentionally passed over. These include reducing common subexpressions (e.g., mapping all of those repeated divisions to multiplications by an inverse that is computed once) and lifting constants outside loops. Performing those destroys the clarity of the algorithm, but will probably gain only a 50% throughput improvement.

This is not to say that low-level optimizations are not worthwhile. But they are primarily worthwhile when you have completed your high-level optimizations; at that point you are more willing to complicate your code and its maintenance because you are done adding features.

### 15.8.2 Architectural Considerations

🔶 The primary difference between the simple rasterizer and ray caster described in this chapter is that the “for each pixel” and “for each triangle” loops have the opposite nesting. This is a trivial change and the body of the inner loop is largely similar in each case. But the trivial change has profound implications for memory access patterns and how we can algorithmically optimize each.

Scene triangles are typically stored in the heap. They may be in a flat 1D array, or arranged in a more sophisticated data structure. If they are in a simple data structure such as an array, then we can ensure reasonable memory coherence by iterating through them in the same order that they appear in memory. That produces efficient cache behavior. However, that iteration also requires substantial
