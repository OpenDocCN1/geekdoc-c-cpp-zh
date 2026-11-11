These are followed by a call to send the framebuffer to the display, which is often called a **buffer swap.** An abstracted implementation of this process might look like Listing 15.35. This is called from a main rendering loop, such as Listing 15.36.

*Listing 15.35: Host code to set fixed-function state and shader arguments, and to launch a draw call under an abstracted hardware API.*

```
~~~cpp
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
~~~
```

*Listing 15.36: Host code to set up the main hardware rendering loop.*

```
~~~cpp
OSWindow::Settings osWindowSettings;
RenderDevice* gpu = new RenderDevice();
gpu->init(osWindowSettings);

// Load the vertex and pixel programs
shader = Shader::fromFiles("project.vrt", "shade.pix");

shadowMap = Texture::createEmpty("Shadow map", 1024, 1024,
    ImageFormat::DEPT24(), Texture::DIM_2D_NPOT, Texture::Settings::shadow());
makeTrianglePlusGroundScene(scene);
~~~
```