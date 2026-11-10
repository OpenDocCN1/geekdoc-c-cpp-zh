

![](img/1695de1bc7486362f86c143285f3fb40_159_0.png)

**图 6.11**  
构建圆环。

这些顶点逐一构建。每个顶点还会生成一个与圆环表面相切的附加向量（称为*切向量*）。

构成圆环的其他环的顶点是通过将初始环绕 Y 轴旋转而生成的。每个生成顶点的切向量和法向量同样通过将初始环的切向量和法向量绕 Y 轴旋转来计算。创建顶点后，逐环遍历这些顶点，并为每个顶点生成两个三角形。生成构成这两个三角形的六个索引表条目的方式，与我们为球体所做的方式类似。

我们为其余环选择纹理坐标的策略是：使纹理图像的 S 轴绕圆环水平周长缠绕一半，然后在另一半重复。当我们绕 Y 轴旋转生成这些环时，我们指定一个变量 ring，它从 1 开始，增加到指定的精度（同样称为“prec”）。然后我们将 S 纹理坐标值设置为 ring*2.0/prec，使 S 在 0.0 到 2.0 之间变化，然后按照第 5.10 节所述，将纹理的平铺模式设置为 GL_REPEAT。采用这种方法的动机是避免纹理图像在水平方向上显得过度“拉伸”。如果反过来，我们确实想让纹理完全环绕圆环拉伸，只需从纹理坐标计算中移除“*2.0”乘数即可。

在 C++/OpenGL 中构建 Torus 类的方式与 Sphere 类几乎完全相同。然而，我们可以利用 OpenGL 对顶点索引的支持，来充分利用构建圆环时创建的索引（我们本来也可以对球体这样做，但我们没有）。对于包含数千个顶点的非常大的模型，使用 OpenGL 索引可以提高性能，因此我们接下来将介绍如何做到这一点。

## 6.2.2 OpenGL 中的索引

在球体和圆环模型中，我们都会生成一个整数索引数组，其中的索引指向顶点数组。对于球体，我们使用索引列表构建完整的独立顶点集，并将其加载到 VBO 中，就像我们在前几章的示例中所做的那样。实例化圆环并将其顶点、法向量等加载到缓冲区，可以用与程序 6.1 类似的方式完成，但我们将改用 OpenGL 的索引。

使用 OpenGL 索引时，我们还会将索引本身加载到 VBO 中。我们额外生成一个 VBO 来保存索引。由于每个索引值只是一个整数引用，我们首先将索引数组复制到 C++ 整数向量中，然后使用 glBufferData() 将该向量加载到新增的 VBO 中，并指定该 VBO 的类型为 GL_ELEMENT_ARRAY_BUFFER（这告诉 OpenGL 该 VBO 包含索引）。完成此操作的代码可以添加到 setupVertices() 中：

```cpp
std::vector<int> ind = myTorus.getIndices();  // torus index accessor returns indices as an int vector
. . .
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, vbo[3]);      // vbo #3 is the additional added vbo
glBufferData(GL_ELEMENT_ARRAY_BUFFER, ind.size()*4, &ind[0], GL_STATIC_DRAW);
```

在 display() 方法中，我们将 glDrawArrays() 调用替换为 glDrawElements() 调用，后者告诉 OpenGL 利用索引 VBO 来查找要绘制的顶点。我们还会使用 glBindBuffer() 绑定包含索引的 VBO，并指定哪个 VBO 包含索引以及它是 GL_ELEMENT_ARRAY_BUFFER。代码如下：

```cpp
numTorusIndices = myTorus.getNumIndices();
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, vbo[3]);
glDrawElements(GL_TRIANGLES, numTorusIndices, GL_UNSIGNED_INT, 0);
```

有趣的是，用于绘制球体的着色器无需修改即可继续用于绘制圆环，即使我们在 C++/OpenGL 应用程序中为实现索引而进行了更改。OpenGL 能够识别 GL_ELEMENT_ARRAY_BUFFER 的存在，并利用它来访问顶点属性。

程序 6.2 展示了一个名为 Torus 的类，它基于 Baker 的实现。“inner”和“outer”变量分别对应图 6.11 中的内半径和外半径。prec（“precision”）变量的作用与球体中的类似，顶点数和索引数的计算方式也类似。相比之下，

```cpp
// build the ring by rotating points around the origin, then moving them outward
glm::mat4 rMat = glm::rotate(glm::mat4(1.0f), amt, glm::vec3(0.0f, 0.0f, 1.0f));
glm::vec3 initPos(rMat * glm::vec4(0.0f, outer, 0.0f, 1.0f));
vertices[i] = glm::vec3(initPos + glm::vec3(inner, 0.0f, 0.0f));

// compute texture coordinates for each vertex on the ring
texCoords[i] = glm::vec2(0.0f, ((float)i / (float)prec));

// compute tangents and normals -- first tangent is Y-axis rotated around Z
rMat = glm::rotate(glm::mat4(1.0f), amt+(3.141592f/2.0f), glm::vec3(0.0f, 0.0f, 1.0f));
tTangents[i] = glm::vec3(rMat * glm::vec4(0.0f, -1.0f, 0.0f, 1.0f));
sTangents[i] = glm::vec3(glm::vec3(0.0f, 0.0f, -1.0f));    // second tangent is -Z.
normals[i] = glm::cross(tTangents[i], sTangents[i]);       // their X-product is the normal.
}
// rotate the first ring about Y to get the other rings
for (int ring = 1; ring < prec + 1; ring++) {
    for (int vert = 0; vert < prec + 1; vert++) {
        // rotate the vertex positions of the original ring around the Y axis
        float amt = (float) (toRadians(ring * 360.0f / prec));
        glm::mat4 rMat = glm::rotate(glm::mat4(1.0f), amt, glm::vec3(0.0f, 1.0f, 0.0f));
        vertices[ring * (prec + 1) + vert] = glm::vec3(rMat * glm::vec4(vertices[vert], 1.0f));

        // compute the texture coordinates for the vertices in the new rings
        texCoords[(ring * (prec + 1)) + vert] = glm::vec2((float)ring * 2.0f / (float)prec, texCoords[vert].t);

        // rotate the tangent and bitangent vectors around the Y axis
        rMat = glm::rotate(glm::mat4(1.0f), amt, glm::vec3(0.0f, 1.0f, 0.0f));
        sTangents[ring * (prec + 1) + vert] = glm::vec3(rMat * glm::vec4(sTangents[vert], 1.0f));
        rMat = glm::rotate(glm::mat4(1.0f), amt, glm::vec3(0.0f, 1.0f, 0.0f));
        tTangents[ring * (prec + 1) + vert] = glm::vec3(rMat * glm::vec4(tTangents[vert], 1.0f));

        // rotate the normal vector around the Y axis
        rMat = glm::rotate(glm::mat4(1.0f), amt, glm::vec3(0.0f, 1.0f, 0.0f));
        normals[ring * (prec + 1) + vert] = glm::vec3(rMat * glm::vec4(normals[vert], 1.0f));
    }
}

// calculate triangle indices corresponding to the two triangles built per vertex
for (int ring = 0; ring < prec; ring++) {
    for (int vert = 0; vert < prec; vert++) {
        indices[(ring * prec + vert) * 6 + 0] = ring * (prec + 1) + vert;
        indices[(ring * prec + vert) * 6 + 1] = (ring + 1) * (prec + 1) + vert;
        indices[(ring * prec + vert) * 6 + 2] = ring * (prec + 1) + vert + 1;
        indices[(ring * prec + vert) * 6 + 3] = ring * (prec + 1) + vert + 1;
        indices[(ring * prec + vert) * 6 + 4] = (ring + 1) * (prec + 1) + vert;
        indices[(ring * prec + vert) * 6 + 5] = (ring + 1) * (prec + 1) + vert + 1;
    }
}
}
```

## 使用 Torus 类（采用 OpenGL 索引）

```cpp
…
#include "Torus.h"
…
Torus myTorus(0.5f, 0.2f, 48);
…
void setupVertices(void) {
    std::vector<int> ind = myTorus.getIndices();
    std::vector<glm::vec3> vert = myTorus.getVertices();
    std::vector<glm::vec2> tex = myTorus.getTexCoords();
    std::vector<glm::vec3> norm = myTorus.getNormals();

    std::vector<float> pvalues;
    std::vector<float> tvalues;
    std::vector<float> nvalues;

    int numVertices = myTorus.getNumVertices();
    for (int i = 0; i < numVertices; i++) {
        pvalues.push_back(vert[i].x);
        pvalues.push_back(vert[i].y);
        pvalues.push_back(vert[i].z);

        tvalues.push_back(tex[i].s);
        tvalues.push_back(tex[i].t);

        nvalues.push_back(norm[i].x);
        nvalues.push_back(norm[i].y);
        nvalues.push_back(norm[i].z);
    }
    glGenVertexArrays(1, vao);
    glBindVertexArray(vao[0]);
    glGenBuffers(4, vbo);                    // generate VBOs as before, plus one for indices

    glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);                    // vertex positions
    glBufferData(GL_ARRAY_BUFFER, pvalues.size() * 4, &pvalues[0], GL_STATIC_DRAW);

    glBindBuffer(GL_ARRAY_BUFFER, vbo[1]);                    // texture coordinates
    glBufferData(GL_ARRAY_BUFFER, tvalues.size() * 4, &tvalues[0], GL_STATIC_DRAW);

    glBindBuffer(GL_ARRAY_BUFFER, vbo[2]);                    // normal vectors
    glBufferData(GL_ARRAY_BUFFER, nvalues.size() * 4, &nvalues[0], GL_STATIC_DRAW);

    glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, vbo[3]);            // indices
    glBufferData(GL_ELEMENT_ARRAY_BUFFER, ind.size() * 4, &ind[0], GL_STATIC_DRAW);
}
```

