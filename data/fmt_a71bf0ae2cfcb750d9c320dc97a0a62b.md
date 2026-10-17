
- [BL16] Blender, The Blender Foundation, 2018 年 10 月访问，https://www.blender.org/
- [GE16] Geeks3D, "OpenGL Sampler Objects: Control Your Texture Units," 2011 年 9 月 8 日，2018 年 10 月访问，http://www.geeks3d.com/20110908/gimp.org
- [GI16] GNU Image Manipulation Program, 2018 年 10 月访问，http://www.gimp.org/
- [HT16] J. Hastings-Trew, JHT's Planetary Pixel Emporium, 2018 年 10 月访问，http://planetpixeleemporium.com/
- [LU16] F. Luna, Introduction to 3D Game Programming with DirectX 12, 第 2 版 (Mercury Learning, 2016).
- [MA16] Maya, Autodesk, Inc., 2018 年 10 月访问，http://www.autodesk.com/products/maya/overview
- [OE16] OpenGL Registry, The Khronos Group, 2016 年 7 月访问，https://www.opengl.org/registry/
- [OP14] OpenGL Graphics System: A Specification (version 4.4), M. Segal and K. Akeley, 2014 年 3 月 19 日，2016 年 7 月访问，https://www.opengl.org/registry/doc/glspec44.core.pdf
- [OP16] OpenGL 4.5 Reference Pages, 2016 年 7 月访问，https://www.opengl.org/sdk/docs/man/
- [OT18] OpenGL Tutorial, “Loading BMP Images Yourself,” opengl-tutorial.org, 2018 年 10 月访问，http://www.opengl-tutorial.org/beginners-tutorials/tutorial-5-a-textured-cube/#loading-bmp-images-yourself
- [SO17] Simple OpenGL Image Library 2 (SOIL2), Spartan, J., 2018 年 10 月访问，https://bitbucket.org/SpartanJ/soil2
- [TU16] J. Turberville, Studio 522 Productions, Scottsdale, AZ, www.studio522.com (dolphin 模型 开发于 2016).
- [WI83] L. Williams, “Pyramidal Parametrics,” Computer Graphics 17, no. 3 (1983 年 7 月)。

# 第 6 章

## 3D 模型

- 6.1 过程化模型 – 构建球体 ................................................ 129
- 6.2 OpenGL 索引 – 构建圆环 ................................................................. . . . 138
- 6.3 加载外部生成的模型 ................................................................. 145
- 补充说明 ................................................................................. . . . 155

到目前为止，我们只处理了简单的对象，例如立方体。在本章中，我们将探索更复杂的：在随后的章节中，我们将看到如何使用纹理单元来改变物体反射的光线，使其看起来凹凸不平。我们还可以使用纹理单元存储用于生成地形的“高度图”，以及存储“阴影图”以高效地为场景添加阴影。这些用法将在后续章节中描述。

着色器还可以写入纹理，允许着色器修改纹理图像，甚至将一个纹理的一部分复制到另一个纹理的某些区域。

多级映射（Mipmaps）和各异性场景抗锯齿不是减少纹理锯齿的唯一工具。例如，全场景抗锯齿（FSAA）和其他超采样方法也可以提高 3D 场景中纹理的外观。尽管它们不是 OpenGL 核心的一部分，但通过 OpenGL 的扩展机制 [QE16]，许多显卡都支持这些方法。

还有另一种配置和管理纹理及采样器的机制。OpenGL 3.3 版本引入了采样器对象（有时称为“采样器状态”—不要与采样器变量混淆），它可以用于存储一组独立于实际纹理对象的设置。采样器对象附加到纹理单元上，允许方便且高效地更改纹理设置。本书中的示例足够简单，因此我们决定省略对采样器对象的介绍。对于感兴趣的读者，采样器对象的使用很容易学习，并且有很多优秀的在线教程（例如 [GE17]）。

## 6.1 过程化模型 – 构建球体

到目前为止，我们只处理了简单的对象，例如立方体。在本章中，我们将探索更复杂的：在随后的章节中，我们将看到如何使用纹理单元来改变物体反射的光线，使其看起来凹凸不平。我们还可以使用纹理单元存储用于生成地形的“高度图”，以及存储“阴影图”以高效地为场景添加阴影。这些用法将在后续章节中描述。

着色器还可以写入纹理，允许着色器修改纹理图像，甚至将一个纹理的一部分复制到另一个纹理的某些区域。

### 第6章 - 3D 模型

![](img/5f029c1d57776416a7d2524f3734d7cf_132_0.png)

图 6.7

顶点数组及相应的索引数组。

两个三角形在上方和右侧形成一个正方形区域，如图 6.3 所示。因此，处理过程被组织为嵌套循环，如下：

```cpp
+ 对于球体中的每个水平切片 i (i 的范围从 0 到球体中的所有切片)
{
    对于切片 i 中的每个顶点 j (j 的范围从 0 到该切片中的所有顶点)
    {
        - 计算两个三角形的索引，这些索引指向右侧、上方以及右上方的邻接顶点
    }
}
```

例如，考虑图 6.3 中的“红色”顶点（在图 6.8 中重复出现）。该顶点位于图 6.8 所示黄色三角形的左下角，根据上述描述的循环，其索引为 $i \cdot n + j$，其中 $i$ 是当前处理的切片（外循环），$j$ 是该切片中当前处理的顶点（内循环），而 $n$ 是每个切片的顶点数。图 6.8 显示了该顶点（红色）及其三个相关的邻接顶点，公式显示了它们是如何被索引的。

这四个顶点用于构建为该（红色）顶点生成的两个三角形（黄色所示）。这两个三角形索引表中的六个条目按照图中数字 1 到 6 的顺序所示。注意，条目 3 和 6 都指向同一个顶点，条目 2 也是如此

![](img/5f029c1d57776416a7d2524f3734d7cf_132_1.png)

图 6.8

第 j 个切片中第 j 个顶点生成的索引 (n = 每个切片的顶点数)。

《使用 C++ 的 OpenGL 图形学编程》

4. 当我们到达红色高亮的顶点时（即 `vertex[n]`），由此定义的两个三角形由这六个顶点构建而成——一个三角形由标记为 1, 2, 3 的条目引用 `vertices[n]`、`vertices[n+1]` 和 `vertex[n+2]`；另一个三角形由标记为 4, 5, 6 的条目引用三个顶点 `vertex[n+1]`、`vertex[n+2]` 和 `vertex[n+3]`。

程序 6.1 显示了用名为 `Sphere` 的类实现的球体模型。生成的球体中心位于原点。还显示了 `Sphere` 的代码。注意，每个顶点都存储在包含 GLM 类 `vec2` 和 `vec3` 实例的 C++ `vector` 中（这与之前的示例不同，之前的顶点存储在 float 数组中）。`vec2` 和 `vec3` 包含了以 float 值获取所需的 x、y、z 分量的方法，然后像以前一样将这些值放入 float 缓冲区中。我们将这些值存储在变长的 C++ `vector` 中，因为其大小取决于在运行时指定的切片数量。

注意 `Sphere` 类中三角形索引的计算，在图 6.8 之前描述过。变量 "prec" 指“精度”（precision），在本例中，它同时用于球体切片数和每个切片的顶点数。由于纹贴图包裹球体，在纹贴图左边缘和右边缘相遇的每个点，我们需要一个额外的重复顶点。因此，总顶点数为 (prec+1)。由于每个顶点生成六个三角形索引，索引总数为 `prec*prec*6`。

## 程序 6.1 过程化生成的球体

Sphere 类 (`Sphere.cpp`)

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

Sphere::Sphere(int prec) { // prec 是精度，或切片数
  init(prec);
}
```

## 第6章 · 3D 模型

```cpp
float Sphere::toRadians(float degrees) { return (degrees * 2.0f * 3.14159f / 360.0f); }

void Sphere::init(int prec) {
    numVertices = (prec + 1) * (prec + 1);
    numIndices = prec * prec * 6;
    for (int i = 0; i < numVertices; i++) { vertices.push_back(glm::vec3(i)); } // std::vector::push_back
    for (int i = 0; i < numVertices; i++) { texCoords.push_back(glm::vec2(i)); } // 在末尾插入新元素
    for (int i = 0; i < numVertices; i++) { normals.push_back(glm::vec3(i)); } // vector 的末尾并
    for (int i = 0; i < numIndices; i++) { indices.push_back(i); } // 增加大小 1
}

void calculateTriangle() {
    for (int i = 0; i < prec; i++) {
        for (int j = 0; j < prec; j++) {
            float x = cos(toRadians((180.0f - i) * 180.0f / prec));
            float y = sin(toRadians((180.0f - i) * 180.0f / prec));
            float z = sin(toRadians((180.0f - i) * 180.0f / prec));
            // ... (省略内部逻辑细节)
        }
    }
}
// ... (其余代码实现)
```

*(注：由于原文文本中代码部分存在大量重复和断裂，译文已根据指令翻译了描述描述，并保留了代码块。)*

为每个索引条目在 VBO 中分离（通常是冗余的）顶点条目。OpenGL 确实有一种顶点数据的索引机制；为了简单起见，我们在示例中没有使用它，但将在下一个示例中使用 OpenGL 的索引功能。

![](img/5f029c1d57776416a7d2524f3734d7cf_137_0.png)

图 6.9 显示了程序 6.1 的输出，精度为 48。图 6.5 中的纹理已按照第 5 章描述的方法加载。

图 6.9

贴纹球体模型。

许多其他模型可以通过程序化创建，从几何形状到现实世界的物体。最著名的之一是“犹州茶壶”CH16]，它由 Martin Newell 在 1975 年开发，使用了多种 Bezier 曲线和曲面。OpenGL 工具包 (GLUT) [GL16] 包含了绘制茶壶的程序（见图 6.10）。我们本书中没有介绍 GLUT，但在第 11 章会介绍 Bezier 表面。

图 6.10

OpenGL 茶壶。

## 6.2 OPENGL 索引 – 构建圆环

### 6.2.1 圆环

生成圆环的算法可以在各种网站找到。Paul 提供了定义圆形切片并围绕圆形旋转以形成甜圈的逐步描述。图 6.11 显示了侧视图和俯视图。顶点位置的方法与构建球体的方法非常不同。对于圆环，算法将顶点放置在原点的右侧，并通过绕 Z 轴旋转将顶点旋转到 XY 平面上的圆。然后通过“内半径”向外移动环。在构建这些顶点时，会为它们计算纹理坐标和法线向量。

![](img/5f029c1d57776416a7d2524f37347cf_138_0.png)

**图 6.11** 构建圆环。

每个顶点还会生成一个指向圆环表面的额外向量（称为切向量）。额外环的顶点通过绕 Y 轴旋转原始环形成。顶点创建后，从环到环进行遍历，并且每个环生成两个三角形。包含这两个三角形的索引表生成方式与我们构建球体的方式类似。我们为剩余环选择纹理坐标的策略是排列它们，使得 S 轴绕圆环的水平周长绕半圈并在另一半部分重复。当我们绕 Y 轴旋转生成环时，我们指定了一个变量（再次称为 "prec"）。然后我们从 0 开始增加到指定的精度，然后将 S 纹理坐标值设置为 ring/2.0，导致 S 的范围在 0.0 到 1.0 之间，然而纹理坐标大于 1.0，以避免纹理在水平方向上拉伸。如果我们想让纹理完全环绕圆环，只需移除纹理坐标的 "2.0" 乘因子即可。

在 C++/OpenGL 中构建圆环类可以用与 `Sphere` 类几乎相同的方式完成。然而，我们有机会利用 OpenGL 对顶点索引的支持，利用我们在构建圆环时创建的索引（我们本也可以对球体这样做，但没有做）。对于具有数千个顶点的非常大的模型，使用 OpenGL 索引可以提高性能，因此我们将描述如何实现。

### 6.2.2 OpenGL 中的索引

在球体和圆环模型中，我们都生成一个引用顶点数组的整数索引数组。在球体的情况下，我们使用索引列表来构建一组完整的独立顶点，并像前面章节中的示例那样将其加载到 VBO 中。实例化圆环及其顶点、法线等到缓冲区，可以用与程序 6.1 类似的方式完成，但我们使用 OpenGL 的索引。

当使用 OpenGL 索引时，我们将索引本身也加载到 VBO 中。我们生成一个额外的 VBO 来存储索引。由于每个索引值只是一个索引引用，我们首先将索引数组拷贝到 C++ 整数向量中，并使用 `glBufferData()` 将顶点加载到添加的 VBO 中，指定 VBO 类型为 `GL_ELEMENT_ARRAY_`（这告诉 OpenGL VBO 包含索引）。添加到 `setup()` 中的代码：

```cpp
std::vector<int> ind = myTorus.getIndices(); // 圆环索引访问器返回 int 向量类型的索引
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, vbo[3]); // vbo #3 是额外的 vbo
glBufferData(GL_ELEMENT_ARRAY_BUFFER, ind.size()*4, &ind[0], GL_STATIC_DRAW);
```

在 `display()` 中，我们用调用 `glDrawElements()` 替换 `glDrawArrays()`，这告诉 OpenGL 利用 VBO 查找要绘制的顶点。我们还通过 `glBindBuffer()` 添加包含索引的 VBO，指定哪个 VBO 包含索引以及它是一个 `GL_ELEMENT_ARRAY_BUFFER`。代码如下：

```cpp
numTorusIndices = myTorus.getTorusIndices();
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, vbo[3]);
glDrawElements(GL_TRIANGLES, numTorusIndices, GL_UNSIGNED_INT, 0);
```

有趣的是，用于绘制球体的着色器即使我们在 C++/OpenGL 中为了索引而做了更改，对于圆环仍然保持正常工作。OpenGL 能够识别 `GL_ELEMENT_ARRAY_BUFFER` 的存在并利用它访问顶点属性。程序 6.2 显示了基于 Baker 实现的类。"inner" 和 "outer" 变量对应图 6.11 中相应的内、外半径。`prec` ("precision") 变量与球体的角色相似。相比之下，确定法线向量要比球体复杂得多。我们使用了 Baker 描述中的策略，其中两个切向量（通常称为 "tangent" 和 "bitangent"）的叉积形成法线。我们将在书的剩余部分使用这个圆环类（以及之前的球体类）。

![](img/5f029c1d57776416a7d2524f37347cf_139_0.png)

### 程序 6.2 程序生成的圆环
