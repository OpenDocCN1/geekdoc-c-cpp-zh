
以及 4. 当我们到达以红色高亮的顶点（即 vertex[i*n+j]）时，这样定义的两个三角形由以下六个顶点构成——其中一个三角形的索引项标记为 1、2、3，分别引用顶点 vertex[i*n+j]、vertex[i*n+j+1] 和 vertex[(i+1)*n+j]；另一个三角形的索引项标记为 4、5、6，引用顶点 vertex[i*n+j+1]、vertex[(i+1)*n+j+1] 和 vertex[(i+1)*n+j]。

程序6.1 展示了如何将我们的球体模型实现为名为 Sphere 的类。生成的球体中心位于原点。同时展示了使用 Sphere 的代码。注意，每个顶点都存储在包含 GLM 类 vec2 和 vec3 实例的 C++ vector 中（这与之前的示例不同，之前的示例中顶点存储在 float 数组中）。vec2 和 vec3 包含用于以 float 值形式获取所需 x、y、z 分量的方法，这些值随后像之前一样放入 float 缓冲区中。我们将这些值存储在变长的 C++ vector 中，因为其大小取决于运行时指定的切片数量。

注意 Sphere 类中三角形索引的计算，如前文图6.8所述。变量“prec”指的是“精度”（precision），在本例中它同时用于表示球体切片区域的数量和每个切片所需的点的数量。由于纹理映射完全环绕球体，我们需要在纹理映射的左右边缘相交的每个点处额外增加一个重合顶点。因此，顶点总数为 (prec+1)*(prec+1)。由于每个顶点会生成六个三角形索引，因此索引总数为 prec*prec*6。

## 程序6.1 程序化生成的球体

*Sphere 类（Sphere.cpp）*

```cpp
#include <cmath>
#include <vector>
#include <iostream>
#include <glm/glm.hpp>
#include "Sphere.h"
using namespace std;

Sphere::Sphere() {
    init(48);
}

Sphere::Sphere(int prec) {  // prec is precision, or number of slices
    init(prec);
}

float Sphere::toRadians(float degrees) { return (degrees * 2.0f * 3.14159f) / 360.0f; }

void Sphere::init(int prec) {
    numVertices = (prec + 1) * (prec + 1);
    numIndices = prec * prec * 6;
    for (int i = 0; i < numVertices; i++) { vertices.push_back(glm::vec3()); }    // std::vector::push_back()
    for (int i = 0; i < numVertices; i++) { texCoords.push_back(glm::vec2()); }   // inserts new element at
    for (int i = 0; i < numVertices; i++) { normals.push_back(glm::vec3()); }     // the end of a vector and
    for (int i = 0; i < numIndices; i++) { indices.push_back(0); }                // increases the vector size by 1

    // calculate triangle vertices
    for (int i = 0; i <= prec; i++) {
        for (int j = 0; j <= prec; j++) {
            float y = (float)cos(toRadians(180.0f - i * 180.0f / prec));
            float x = -(float)cos(toRadians(360.0f / prec) * (float)j) * (float)abs(cos(asin(y)));
            float z = (float)sin(toRadians(360.0f / prec) * (float)j) * (float)abs(cos(asin(y)));
            vertices[i*(prec + 1) + j] = glm::vec3(x, y, z);
            texCoords[i*(prec + 1) + j] = glm::vec2((float)j / prec, (float)i / prec);
            normals[i*(prec + 1) + j] = glm::vec3(x,y,z);
        }
    }

    // calculate triangle indices
    for (int i = 0; i < prec; i++) {
        for (int j = 0; j < prec; j++) {
            indices[6 * (i*prec + j) + 0] = i*(prec + 1) + j;
            indices[6 * (i*prec + j) + 1] = i*(prec + 1) + j + 1;
            indices[6 * (i*prec + j) + 2] = (i + 1)*(prec + 1) + j;
            indices[6 * (i*prec + j) + 3] = i*(prec + 1) + j + 1;
            indices[6 * (i*prec + j) + 4] = (i + 1)*(prec + 1) + j + 1;
            indices[6 * (i*prec + j) + 5] = (i + 1)*(prec + 1) + j;
        }
    }
}

// accessors
int Sphere::getNumVertices() { return numVertices; }
int Sphere::getNumIndices() { return numIndices; }
std::vector<int> Sphere::getIndices() { return indices; }
std::vector<glm::vec3> Sphere::getVertices() { return vertices; }
std::vector<glm::vec2> Sphere::getTexCoords() { return texCoords; }
std::vector<glm::vec3> Sphere::getNormals() { return normals; }
```

### Sphere 头文件（Sphere.h）

```cpp
#include <cmath>
#include <vector>
#include <glm/glm.hpp>

class Sphere
{
private:
    int numVertices;
    int numIndices;
    std::vector<int> indices;
    std::vector<glm::vec3> vertices;
    std::vector<glm::vec2> texCoords;
    std::vector<glm::vec3> normals;
    void init(int);
    float toRadians(float degrees);

public:
    Sphere(int prec);
    int getNumVertices();
    int getNumIndices();
    std::vector<int> getIndices();
    std::vector<glm::vec3> getVertices();
    std::vector<glm::vec2> getTexCoords();
    std::vector<glm::vec3> getNormals();
};
```

### 使用 Sphere 类

```cpp
...
#include "Sphere.h"
...
Sphere mySphere(48);
...

void setupVertices(void) {
    std::vector<int> ind = mySphere.getIndices();
    std::vector<glm::vec3> vert = mySphere.getVertices();
    std::vector<glm::vec2> tex = mySphere.getTexCoords();
    std::vector<glm::vec3> norm = mySphere.getNormals();

    std::vector<float> pvalues;     // vertex positions
    std::vector<float> tvalues;     // texture coordinates
    std::vector<float> nvalues;     // normal vectors

    int numIndices = mySphere.getNumIndices();
    for (int i = 0; i < numIndices; i++) {
        pvalues.push_back((vert[ind[i]]).x);
        pvalues.push_back((vert[ind[i]]).y);
        pvalues.push_back((vert[ind[i]]).z);

        tvalues.push_back((tex[ind[i]]).s);
        tvalues.push_back((tex[ind[i]]).t);

        nvalues.push_back((norm[ind[i]]).x);
        nvalues.push_back((norm[ind[i]]).y);
        nvalues.push_back((norm[ind[i]]).z);
    }
    glGenVertexArrays(1, vao);
    glBindVertexArray(vao[0]);
    glGenBuffers(3, vbo);

    // put the vertices into buffer #0
    glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
    glBufferData(GL_ARRAY_BUFFER, pvalues.size()*4, &pvalues[0], GL_STATIC_DRAW);

    // put the texture coordinates into buffer #1
    glBindBuffer(GL_ARRAY_BUFFER, vbo[1]);
    glBufferData(GL_ARRAY_BUFFER, tvalues.size()*4, &tvalues[0], GL_STATIC_DRAW);

    // put the normals into buffer #2
    glBindBuffer(GL_ARRAY_BUFFER, vbo[2]);
    glBufferData(GL_ARRAY_BUFFER, nvalues.size()*4, &nvalues[0], GL_STATIC_DRAW);
}

void display()
{
    glDrawArrays(GL_TRIANGLES, 0, mySphere.getNumIndices());
    ...
}
```

使用 Sphere 类时，每个顶点位置和每个法向量需要三个值，而每个纹理坐标只需要两个值。这一点体现在 Sphere.h 头文件中的向量声明（vertices、texCoords 和 normals）中，数据随后将从这些向量加载到缓冲区。

需要特别注意的是，虽然在构建球体的过程中使用了索引，但最终存储在 VBO 中的球体顶点数据并不使用索引。相反，setupVertices() 在遍历球体索引时，会为每个索引条目在 VBO 中生成单独的（通常是冗余的）顶点条目。OpenGL 确实具备顶点数据索引机制；为了简洁，本示例中我们没有使用它，但在下一个示例中我们将使用 OpenGL 的索引。

![](img/1695de1bc7486362f86c143285f3fb40_158_0.png)

**图6.9**  
纹理球体模型。

图6.9显示了程序6.1的输出，精度为48。为了清晰起见，视图略微旋转。来自图6.5的纹理已按第5章所述加载。

许多其他模型也可以通过程序化方式创建，从几何形状到现实世界的物体。其中最著名的一个是“犹他茶壶”[CH20]，它由 Martin Newell 于1975年使用各种 Bézier 曲线和曲面开发。*OpenGL 实用工具包*（或“*GLUT*”）[GL20] 甚至包含绘制茶壶的程序（！）（见图6.10）。本书不涉及 GLUT，但 Bézier 曲面将在第11章中介绍。

![](img/1695de1bc7486362f86c143285f3fb40_158_1.png)

**图6.10**  
OpenGL GLUT 茶壶。

## 6.2 OpenGL 索引——构建圆环

### 6.2.1 圆环

生成*圆环*的算法可以在多个网站上找到。Paul Baker 在他的 OpenGL 凹凸贴图教程 [PP07] 中，逐步描述了如何定义一个圆形切片，然后将该切片绕圆旋转以形成一个甜甜圈。图6.11显示了两个视图，分别为侧视图和俯视图。

圆环顶点位置的生成方式与球体的构建方式截然不同。对于圆环，算法先将一个顶点放置在原点右侧，然后通过绕 Z 轴旋转，使该顶点在 XY 平面上沿圆周运动，形成一个“环”。随后，将这个环向外移动“内半径”的距离。纹理坐标和法向量将针对
