derived from a generic graphics application (`GApp`) class: The `App` contains a reference to an indexed-face-set model and a single directional light (specified by its direction and radiance), values for the diffuse color of the surface and the diffuse reflection coefficient, and a reference to a shader object.

When the `run()` method on a `GApp` is invoked, it first invokes `GInit`, and then repeatedly invokes `onGraphics()`, whose job is to describe what should be rendered.

As you can see, the initialization of the application instance is fairly straightforward: In lines 20 and 21, we assign a diffuse reflectance and color to be used for a surface, and create a representation of a directional light (a direction and radiance value).

During initialization, `G3D`'s `Shader` class is used to read the vertex and pixel shaders (as text) from their text files (line 25), and we load a model of an icosahedron from a file (line 26), and set the camera's position and view (lines 28 and 29).

At each frame, the `onGraphics` method is called (see Listing 33.2). The `setProjectionAndCameraMatrix` method (line 2) invokes several GL operations to establish values for predefined variables like `gl_ModelViewProjectionMatrix`. The next two lines clear the image on the GPU to a constant color.

# Listing 33.2: The graphics-drawing procedure and `main`.

```
```cpp
1 void App::onGraphics(RenderDevice* rd, Array<SurfaceRef>& posed3D) {
2     rd->setProjectionAndCameraMatrix(defaultCamera);
3     rd->setColorClearValue(Color3(0.1f, 0.2f, 0.4f));
4     rd->clear(true, true, true);
5     rd->pushState(); {
6         SurfaceRef surface = model->pose(G3D::CoordinateFrame());
7
8         // Enable the shader
9         configureShaderArgs(light);
10        rd->setShader(myShader);
11
12        // Send model geometry to the graphics card
13        rd->setObjectToWorldMatrix(surface->coordinateFrame());
14        surface->sendGeometry(rd);
15    } rd->popState();
16 }
17
18 void App::configureShaderArgs() {
19    myShader->args.set("wsLight", light.position.xyz().direction());
20    myShader->args.set("lightColor", light.color);
21    myShader->args.set("wsEyePosition",
22        defaultCamera.coordinateFrame().translation);
23
24    myShader->args.set("diffuseColor", diffuseColor);
25    myShader->args.set("diffuse", diffuse);
26 }
27
28 G3D_START_AT_MAIN();
29
30 int main(int argc, char** argv) {
31    return App().run();
32 }
```
```