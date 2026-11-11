the vertex shader?” for instance. That’s the role of GL (or DirectX, or any other graphics API).

The details of the linking process that associates host-program variables with shader variables are messy and complicated, and the design of GL is extremely general. Almost every developer will want to work with a **shader wrapper**—a program that once and for all chooses a particular way to use GL to hook a host program to shaders, and provides features like automatic recompilation of shaders, etc. Graphics card manufacturers typically provide shader-wrapper programs to allow the easy development of programs that fit the most common paradigms. Only those who need the finest level of control (or those developing shader-wrapper programs) should actually work with most of the tools GL provides for linking host programs to shader programs.

We’ll use such a shader wrapper—G3D—in writing our example shaders in this chapter. G3D is an open source graphics system developed by one of the authors [McG12], and provides a convenient interface to GL. But the shaders in this chapter can in fact be used with other shader wrappers as well, with essentially no changes.

Let’s look at a first example: a shader that provides Gouraud shading, computed once per vertex, and linearly interpolated across triangles. The host program in this case loads a model in which each vertex has an associated normal vector, and provides a linear transformation from model coordinates to world coordinates, and a camera specification. Listing 33.1 shows the declaration of an App class

*Listing 33.1: The class definition and initialization of a simple program that uses a shader.*

```
class App : public GApp {
private:
    GLight                  light;
    IFSModel::Ref           model;

    /** Material properties and shader */
    ShaderRef               myShader;
    float                   diffuse;
    Color3                  diffuseColor;

    void configureShaderArgs();

public:
    App();
    virtual void onInit();
    virtual void onGraphics(RenderDevice* rd,
                            Array<SurfaceRef>& posed3D);
};

App::App() : diffuse(0.6f), diffuseColor(Color3::blue()),
    light(GLight::directional(Vector3(2, 1, 1), Radiance3(0.8f), false)) {}

void App::onInit() {
    myShader = Shader::fromFiles("gouraud.vrt", "gouraud.pix");
    model = IFSModel::fromFile("icosa.ifs");

    defaultCamera.setPosition(Point3(1.0f, 1.0f, 1.5f));
    defaultCamera.lookAt(Vector3::zero());

    ... further initializations ...
}
```