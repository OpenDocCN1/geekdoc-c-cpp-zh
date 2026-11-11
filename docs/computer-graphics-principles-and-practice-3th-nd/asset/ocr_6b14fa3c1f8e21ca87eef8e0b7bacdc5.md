Listing 15.31 shows how this code is used to model the triangle-and-ground-plane scene. In it, the process of uploading the geometry to the graphics device is entirely abstracted within the `Mesh` class.

*Listing 15.31: Host code to create indexed triangle meshes for the triangle-plus-ground scene.*

```
```cpp
void makeTrianglePlusGroundScene(MeshScene& s) {
    std::vector<Vector3> vertex, normal;
    std::vector<int> index;

    // Green triangle geometry
    vertex.push_back(Point3(0, 1, -2)); vertex.push_back(Point3(-1.9f, -1, -2));
        vertex.push_back(Point3(1.6f, -0.5f, -2));
    normal.push_back(Vector3(0, 0.6f, 1).direction()); normal.
        push_back(Vector3(-0.4f, -0.4f, 1.0f).direction()); normal.
        push_back(Vector3(0.4f, -0.4f, 1.0f).direction());
    index.push_back(0); index.push_back(1); index.push_back(2);
    index.push_back(0); index.push_back(2); index.push_back(1);
    shared_ptr<BSDF> greenBSDF(new PhongBSDF(Color3::green() * 0.8f,
        Color3::white() * 0.2f, 100));

    s.meshArray.push_back(Mesh(vertex, normal, index, greenBSDF));
    vertex.clear(); normal.clear(); index.clear();

    ///////////////////////////////////////////////////////////////
    // Ground plane geometry
    const float groundY = -1.0f;
    vertex.push_back(Point3(-10, groundY, -10)); vertex.push_back(Point3(-10,
        groundY, -0.01f));
    vertex.push_back(Point3(10, groundY, -0.01f)); vertex.push_back(Point3(10,
        groundY, -10));

    normal.push_back(Vector3::unitY()); normal.push_back(Vector3::unitY());
    normal.push_back(Vector3::unitY()); normal.push_back(Vector3::unitY());

    index.push_back(0); index.push_back(1); index.push_back(2);
    index.push_back(0); index.push_back(2); index.push_back(3);

    const Color3 groundColor = Color3::white() * 0.8f;
    s.meshArray.push_back(Mesh(vertex, normal, index, groundColor));

    ///////////////////////////////////////////////////////////////
    // Light source
    s.lightArray.resize(1);
    s.lightArray[0].position = Vector3(1, 3, 1);
    s.lightArray[0].power = Color3::white() * 31.0f;
}
```
```

# ### 15.7.2.3 Creating Shaders

The vertex shader must transform the input vertex in global coordinates to a homogeneous point on the image plane. Listing 15.32 implements this transformation. We chose to use the OpenGL Shading Language (GLSL). GLSL is representative of other contemporary shading languages like HLSL, Cg, and RenderMan. All of these are similar to C++. However, there are some minor syntactic differences between GLSL and C++ that we call out here to aid your reading of this example. In GLSL,