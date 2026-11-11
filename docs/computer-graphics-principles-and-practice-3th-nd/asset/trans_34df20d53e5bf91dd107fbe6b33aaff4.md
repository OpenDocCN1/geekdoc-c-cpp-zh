
曲线，或至少分组成自身按行主序排列的小块（即“块线性”），以避免垂直迭代的缓存惩罚。缓冲区的起始位置可能不同，并且通常需要额外填充，以确保各行具有特定的内存对齐，用于宽向量操作和减小指针大小。

内存传输的另一个复杂因素是，人们常常希望将计算与内存操作重叠，以避免主机或设备停顿。异步传输通常通过将设备内存语义映射到主机地址空间来实现。之后就可以像二者共享同一内存空间一样执行常规主机内存操作。在这种情况下，程序员必须手动同步主机程序和设备程序，以确保数据不会在一方写入时被另一方读取。映射内存通常不经过缓存，并且往往有对齐方面的考虑，因此程序员还必须小心控制访问模式。

注意，内存传输面向大数据。对于小值，例如标量、4 × 4 矩阵甚至短数组，显式分配、复制和释放这些值会很繁琐。对于一个有二十个左右参数的着色程序，这会带来运行时和软件管理开销。因此，小值通常通过与着色器关联的另一套 API 传递。

### 15.7.2.2 内存实践

清单 15.30 展示了三角形网格类的部分实现。通过渲染调用将单个三角形从主机传输到图形设备会很低效。因此，API 迫使我们在创建场景时一次性将大量几何体加载到设备，并尽可能高效地编码该几何体。

很少有程序员直接针对硬件图形 API 编写代码。这些 API 反映了它们由委员会设计并在供应商之间协商的事实。它们提供了必要的功能，但通过笨拙的接口来实现，从而掩盖了调用代码的底层功能。使用起来容易出错，因为代码直接操作指针并使用手动管理的内存。

例如，在 OpenGL 中，分配设备数组并将其绑定到着色器输入的代码大致如清单 15.29 所示。大多数程序员会将这些直接的主机调用抽象为与供应商无关、更易使用的接口。

清单 15.29：将顶点数组传输到设备并绑定到着色器输入的主机代码。

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

大多数程序员用自己的层来包装底层硬件 API，这一层更易使用，并提供类型安全和内存管理。这还具有将渲染器从特定硬件 API 中抽象出来的优势。大多数主机、操作系统和移动设备供应商有意使用等价但不兼容的硬件渲染 API。将特定硬件 API 抽象为通用 API，使单一代码库更容易支持多个平台，尽管代价是增加一层函数调用。

对于清单 15.30，我们针对这样一种平台抽象编写代码，而不是直接针对硬件 API 编写。在这段代码中，VertexBuffer 类是设备 RAM 中的托管内存数组，而 AttributeArray 和 IndexArray 是 VertexBuffer 的子集。名称中的“vertex”表示这些类存储逐顶点数据。这并不意味着它们只存储顶点位置——例如，m_normal 数组存储在 AttributeArray 中。这种命名约定有点令人困惑，但它继承自 OpenGL 和 DirectX。你可以将这段代码转换为你选择的硬件 API，自己实现 VertexBuffer 和 AttributeArray 类，或使用提供这些抽象的 G3D 等更高级 API。

清单 15.30：索引三角形网格（等价于共享一个 BSDF 的一组三角形实例）的主机代码。

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

清单 15.31 展示了如何使用这段代码来建模三角形和地平面场景。其中，将几何体上传到图形设备的过程完全抽象在 `Mesh` 类中。

清单 15.31：为三角形加地面场景创建索引三角形网格的主机代码。

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

### 15.7.2.3 创建着色器

顶点着色器必须将全局坐标中的输入顶点变换为图像平面上的齐次点。清单 15.32 实现了这一变换。我们选择使用 OpenGL 着色语言（GLSL）。GLSL 代表了 HLSL、Cg 和 RenderMan 等其他当代着色语言。所有这些语言都类似于 C++。然而，GLSL 和 C++ 之间存在一些细微的语法差异，我们在此指出这些差异，以帮助你阅读本示例。在 GLSL 中，
