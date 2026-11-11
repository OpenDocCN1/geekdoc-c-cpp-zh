
curves, or at least grouped into small blocks that are themselves row-major (i.e., “block-linear”), to avoid the cache penalty of vertical iteration. The origin of a buffer may differ, and often additional padding is required to ensure that rows have specific memory alignments for wide vector operations and reduced pointer size.

Another complicating factor for memory transfer is that one would often like to overlap computation with memory operations to avoid stalling either the host or device. Asynchronous transfers are typically accomplished by semantically mapping device memory into the host address space. Regular host memory operations can then be performed as if both shared a memory space. In this case the programmer must manually synchronize both host and device programs to ensure that data is never read by one while being written by the other. Mapped memory is typically uncached and often has alignment considerations, so the programmer must furthermore be careful to control access patterns.

Note that memory transfers are intended for large data. For small values, such as scalars, 4 × 4 matrices, and even short arrays, it would be burdensome to explicitly allocate, copy, and free the values. For a shading program with twenty or so arguments, that would incur both runtime and software management overhead. So small values are often passed through a different API associated with shaders.

### 15.7.2.2 Memory Practice

Listing 15.30 shows part of an implementation of a triangle mesh class. Making rendering calls to transfer individual triangles from the host to the graphics device would be inefficient. So, the API forces us to load a large array of the geometry to the device once when the scene is created, and to encode that geometry as efficiently as possible.

Few programmers write directly to hardware graphics APIs. Those APIs reflect the fact that they are designed by committees and negotiated among vendors. They provide the necessary functionality but do so through awkward interfaces that obscure the underlying function of the calling code. Usage is error-prone because the code operates directly on pointers and uses manually managed memory.

For example, in OpenGL, the code to allocate a device array and bind it to a shader input looks something like Listing 15.29. Most programmers abstract these direct host calls into a vendor-independent, easier-to-use interface.

Listing 15.29: Host code for transferring an array of vertices to the device and binding it to a shader input.

```cpp
// Allocate memory:
GLuint vbo;
glGenBuffers(1, &vbo);
glBindBuffer(GL_ARRAY_BUFFER, vbo);
glBufferData(GL_ARRAY_BUFFER, hostVertex.size() * 2 * sizeof(Vector3), NULL, GL_STATIC_DRAW);
GLintptr deviceVertex = 0;
GLintptr deviceNormal = hostVertex.size() * sizeof(Vector3);

// Copy memory:
glBufferSubData(GL_ARRAY_BUFFER, deviceVertex, hostVertex.size() *
    sizeof(Point3), hostVertex[0]);

// Bind the array to a shader input:
int vertexIndex = glGetAttribLocation(shader, "vertex");
glEnableVertexAttribArray(vertexIndex);
glVertexAttribPointer(vertexIndex, 3, GL_FLOAT, GL_FALSE, 0, (GLvoid*)deviceVertex);
```

Most programmers wrap the underlying hardware API with their own layer that is easier to use and provides type safety and memory management. This also has the advantage of abstracting the renderer from the specific hardware API. Most console, OS, and mobile device vendors intentionally use equivalent but incompatible hardware rendering APIs. Abstracting the specific hardware API into a generic one makes it easier for a single code base to support multiple platforms, albeit at the cost of one additional level of function invocation.

For Listing 15.30, we wrote to one such platform abstraction instead of directly to a hardware API. In this code, the VertexBuffer class is a managed memory array in device RAM and AttributeArray and IndexArray are subsets of a VertexBuffer. The “vertex” in the name means that these classes store per-vertex data. It does not mean that they store only vertex positions—for example, the m_normal array is stored in an AttributeArray. This naming convention is a bit confusing, but it is inherited from OpenGL and DirectX. You can either translate this code to the hardware API of your choice, implement the VertexBuffer and AttributeArray classes yourself, or use a higher-level API such as G3D that provides these abstractions.

Listing 15.30: Host code for an indexed triangle mesh (equivalent to a set of triangle instances that share a BSDF).

```cpp
 1 class Mesh {
 2 private:
 3     AttributeArray m_vertex;
 4     AttributeArray m_normal;
 5     IndexStream m_index;
 6
 7     shared_ptr<BSDF> m_bsdf;
 8
 9 public:
10
11     Mesh() {}
12
13     Mesh(const std::vector<Point3>& vertex,
14          const std::vector<Vector3>& normal,
15          const std::vector<int>& index, const shared_ptr<BSDF>& bsdf) : m_bsdf(bsdf) {
16
17         shared_ptr<VertexBuffer> dataBuffer =
18             VertexBuffer::create((vertex.size() + normal.size()) *
19                 sizeof(Vector3) + sizeof(int) * index.size());
20         m_vertex = AttributeArray(vertex[0], vertex.size(), dataBuffer);
21         m_normal = AttributeArray(normal[0], normal.size(), dataBuffer);
22
23         m_index = IndexStream(&index[0], index.size(), dataBuffer);
24     }
25
26     ...
27 };
28
29 /** The rendering API pushes us towards a mesh representation
30     because it would be inefficient to make per-triangle calls. */
31 class MeshScene {
32 public:
33     std::vector<Light>    lightArray;
34     std::vector<Mesh>    meshArray;
35 };
```

Listing 15.31 shows how this code is used to model the triangle-and-ground-plane scene. In it, the process of uploading the geometry to the graphics device is entirely abstracted within the `Mesh` class.

Listing 15.31: Host code to create indexed triangle meshes for the triangle-plus-ground scene.

```cpp
void makeTrianglePlusGroundScene(MeshScene& s) {
    std::vector<Vector3> vertex, normal;
    std::vector<int> index;

    // Green triangle geometry
    vertex.push_back(Point3(0, 1, -2));
    vertex.push_back(Point3(-1.9f, -1, -2));
    vertex.push_back(Point3(1.6f, -0.5f, -2));
    normal.push_back(Vector3(0, 0.6f, 1).direction());
    normal.push_back(Vector3(-0.4f, -0.4f, 1.0f).direction());
    normal.push_back(Vector3(0.4f, -0.4f, 1.0f).direction());
    index.push_back(0);
    index.push_back(1);
    index.push_back(2);
    index.push_back(0);
    index.push_back(2);
    index.push_back(1);
    shared_ptr<BSDF> greenBSDF(new PhongBSDF(Color3::green() * 0.8f,
        Color3::white() * 0.2f, 100));

    s.meshArray.push_back(Mesh(vertex, normal, index, greenBSDF));
    vertex.clear();
    normal.clear();
    index.clear();

    ///////////////////////////////////////////////////////////////
    // Ground plane geometry
    const float groundY = -1.0f;
    vertex.push_back(Point3(-10, groundY, -10));
    vertex.push_back(Point3(-10, groundY, -0.01f));
    vertex.push_back(Point3(10, groundY, -0.01f));
    vertex.push_back(Point3(10, groundY, -10));

    normal.push_back(Vector3::unitY());
    normal.push_back(Vector3::unitY());
    normal.push_back(Vector3::unitY());
    normal.push_back(Vector3::unitY());

    index.push_back(0);
    index.push_back(1);
    index.push_back(2);
    index.push_back(0);
    index.push_back(2);
    index.push_back(3);

    const Color3 groundColor = Color3::white() * 0.8f;
    s.meshArray.push_back(Mesh(vertex, normal, index, groundColor));

    ///////////////////////////////////////////////////////////////
    // Light source
    s.lightArray.resize(1);
    s.lightArray[0].position = Vector3(1, 3, 1);
    s.lightArray[0].power = Color3::white() * 31.0f;
}
```

### 15.7.2.3 Creating Shaders

The vertex shader must transform the input vertex in global coordinates to a homogeneous point on the image plane. Listing 15.32 implements this transformation. We chose to use the OpenGL Shading Language (GLSL). GLSL is representative of other contemporary shading languages like HLSL, Cg, and RenderMan. All of these are similar to C++. However, there are some minor syntactic differences between GLSL and C++ that we call out here to aid your reading of this example. In GLSL,
