

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_75_0.png)

**图 3.15**  
透视视景体或视锥体。

透视矩阵用于将 3D 空间中的点变换到它们在近裁剪平面上的适当位置，其构建过程是首先计算 q、A、B 和 C 的值，然后使用这些值构造矩阵，如图 3.16 所示（并在 [WB15] 中推导）。

$$
q = \frac{1}{\tan\left(\frac{\text{FieldOfView}}{2}\right)}
$$

$$
A = \frac{q}{\text{aspectRatio}}
$$

$$
B = \frac{Z_{\text{near}} + Z_{\text{far}}}{Z_{\text{near}} - Z_{\text{far}}}
$$

$$
C = \frac{2 \cdot (Z_{\text{near}} \cdot Z_{\text{far}})}{Z_{\text{near}} - Z_{\text{far}}}
$$

$$
\begin{bmatrix}
A & 0 & 0 & 0 \\
0 & q & 0 & 0 \\
0 & 0 & B & C \\
0 & 0 & -1 & 0
\end{bmatrix}
$$

**图 3.16**  
构建透视矩阵。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_78_0.png)

我们可以将其编码为一个简单的 Java/JOGL 工具函数，该函数在给定相机位置、目标位置和初始“上”向量 Ŷ 的指定值的情况下构建一个观察矩阵。由于 JOML 包含了用于构建观察矩阵的函数 Mat4f.setLookAt()，我们只需使用它。该函数在本教材后面会很有用，尤其是在第 8 章生成阴影时。

### 3.10 用于构建矩阵变换的 GLSL 函数

尽管 JOML 包含了用于执行本章所述许多 3D 变换（例如平移、旋转和缩放）的预定义函数，但 GLSL 只包含基本的矩阵运算，例如加法、串联等。因此，当我们需要在着色器中执行某些 3D 计算时，有时必须编写自己的 GLSL 工具函数来构建 3D 变换矩阵。在 GLSL 中，保存此类矩阵的合适数据类型是 mat4。

在 GLSL 中初始化 mat4 矩阵的语法是按列加载值的。前四个值放入第一列，接下来四个值放入下一列，依此类推，如下例所示：

```glsl
mat4 translationMatrix =
    mat4( 1.0, 0.0, 0.0, 0.0,    // note this is the leftmost column, not the top row
           0.0, 1.0, 0.0, 0.0,
           0.0, 0.0, 1.0, 0.0,
           tx, ty, tz, 1.0 );
```

该代码构建了前面图 3.3 中描述的平移矩阵。

程序 3.1 包含五个 GLSL 函数，用于构建 4x4 平移、旋转和缩放矩阵，每个函数分别对应本章前面给出的公式。我们将在本书后面使用其中一些函数。

### 程序 3.1 在 GLSL 中构建变换矩阵

```glsl
// builds and returns a translation matrix
mat4 buildTranslate(float x, float y, float z)
{
    mat4 trans = mat4(1.0, 0.0, 0.0, 0.0,
                      0.0, 1.0, 0.0, 0.0,
                      0.0, 0.0, 1.0, 0.0,
                      x, y, z, 1.0 );
    return trans;
}

// builds and returns a matrix that performs a rotation around the X axis
mat4 buildRotateX(float rad)
{
    mat4 xrot = mat4(1.0, 0.0, 0.0, 0.0,
                     0.0, cos(rad), -sin(rad), 0.0,
                     0.0, sin(rad), cos(rad), 0.0,
                     0.0, 0.0, 0.0, 1.0 );
    return xrot;
}

// builds and returns a matrix that performs a rotation around the Y axis
mat4 buildRotateY(float rad)
{
    mat4 yrot = mat4(cos(rad), 0.0, sin(rad), 0.0,
                     0.0, 1.0, 0.0, 0.0,
                     -sin(rad), 0.0, cos(rad), 0.0,
                     0.0, 0.0, 0.0, 1.0 );
    return yrot;
}

// builds and returns a matrix that performs a rotation around the Z axis
mat4 buildRotateZ(float rad)
{
    mat4 zrot = mat4(cos(rad), -sin(rad), 0.0, 0.0,
                     sin(rad), cos(rad), 0.0, 0.0,
                     0.0, 0.0, 1.0, 0.0,
                     0.0, 0.0, 0.0, 1.0 );
    return zrot;
}

// builds and returns a scale matrix
mat4 buildScale(float x, float y, float z)
{ mat4 scale = mat4(x, 0.0, 0.0, 0.0,
                    0.0, y, 0.0, 0.0,
                    0.0, 0.0, z, 0.0,
                    0.0, 0.0, 0.0, 1.0 );
  return scale;
}
```

## 补充说明

在本章中，我们已经看到了将矩阵变换应用于点的示例。稍后，我们还需要将这些相同的变换应用于向量。为了实现对向量 V 的变换，使其等价于对点应用某个矩阵变换 M，在一般情况下需要计算 M 的*逆转置*，记为 (M⁻¹)ᵀ，并将 V 与该矩阵相乘。在某些情况下，M=(M⁻¹)ᵀ，此时可以直接使用 M。例如，本章中看到的基本旋转矩阵就等于其自身的逆转置，因此也等于（对点的变换）。因此，本书中的示例在将变换应用于向量时有时会使用 (M⁻¹)ᵀ，有时则直接使用 M。

本节描述的许多 JOML 函数会修改指定的矩阵，并且（有点违反直觉地）返回对同一矩阵的引用，而不是构建并返回一个新矩阵。这是出于性能原因，将在第 4 章中更详细地讨论。

本章尚未讨论的一个问题是让摄像机在空间中平滑移动的技术。这些技术非常有用，尤其是在游戏和 CGI 电影中，而且在可视化、虚拟现实和 3D 建模中也很重要。实现这一功能的代码被称为*摄像机控制器*，关于这一主题有许多在线资源 [TR15]。

我们没有为所介绍的所有矩阵变换提供完整的推导过程（可以在其他资料中找到，例如 [FV95]）。我们力求简明扼要地总结进行基本 3D 图形编程所必需的点、向量和矩阵运算。随着本书内容的推进，我们将遇到所介绍方法的许多实际用途。

## 练习

- 3.1 修改程序 2.5，使顶点着色器包含程序 3.1 中的一个 buildRotate() 函数，并将其应用于构成三角形的各点。这将使三角形从其原始方向旋转。你不需要让旋转动画化。

- 3.2 *（研究）* 在 3.4 节末尾，我们指出欧拉角在某些情况下会导致不良的伪影。最常见的一种称为“万向节锁”。请描述万向节锁，给出一个示例，并解释为什么万向节锁会引发问题。

- 3.3 *（研究）* 避免使用欧拉角时可能出现伪影的一种方法是使用*四元数*。我们没有学习四元数；不过，JOML 包含一个 Quaternionf 类。请对四元数进行一些独立研究，并熟悉相关的 JOML Quaternionf 类。

## 参考文献

- [CR86] C. Crivelli，*天使报喜与圣埃米迪乌斯*（1486 年），藏于英国伦敦国家美术馆，访问于 2020 年 7 月，https://www.nationalgallery.org.uk/paintings/carlo-crivelli-the-annunciation-with-saint-emidius

- [EU76] L. Euler，*Formulae generales pro translatione quacunque corporum rigidorum*（任意刚体平移的一般公式），Novi Commentarii academiae scientiarum Petropolitanae 20，1776 年。

- [FV95] J. Foley、A. van Dam、S. Feiner 和 J. Hughes，*计算机图形学——原理与实践*，第 2 版（Addison-Wesley，1995 年）。

- [KU98] J. B. Kuipers，*四元数与旋转序列*（普林斯顿大学出版社，1998 年）。

- [TR15] T. Reed，OpenGL 第 3B 部分：摄像机控制（博客）。访问于 2021 年 3 月，https://www.trentreed.net/blog/qt5-opengl-part-3b-camera-control

- [WB15] W. Brown，LearnWebGL（2015），第 8.2 章（正交投影），访问于 2021 年 3 月，http://learnwebgl.brown37.net/08_projections/projections_ortho.html

OpenGL 中的一个相关结构称为*顶点数组对象*，或 *VAO*。VAO 是在 OpenGL 3.0 版本中引入的，提供了一种组织缓冲区并在复杂场景中简化缓冲操作的方式。OpenGL 要求至少创建一个 VAO，就我们的目的而言，一个就足够了。

例如，假设我们希望显示两个对象。在 Java/JOGL 端，我们可以通过声明一个 VAO 和一组关联的两个 VBO（每个对象一个）来实现，如下所示：

```java
private int vao[] = new int[1];    // OpenGL requires these values be specified in arrays
private int vbo[] = new int[2];
...
gl.glGenVertexArrays(1, vao, 0);
gl.glBindVertexArray(vao[0]);
gl.glGenBuffers(2, vbo, 0);
```

这两个 OpenGL 命令 glGenVertexArrays() 和 glGenBuffers() 分别创建 VAO 和 VBO，并为这些项目生成整数 ID，这些 ID 存储在数组 vao 和 vbo 中。glBindVertexArray() 的目的是使指定的 VAO 处于“活动”状态，以便生成的缓冲区¹与该 VAO 关联。

缓冲区需要在顶点着色器中声明一个对应的*顶点属性*变量。顶点属性通常是着色器中声明的第一批变量。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_85_0.png)

¹ 在整个示例中，声明了两个缓冲区，以强调*通常*我们会使用多个缓冲区。稍后，我们将使用额外的缓冲区来存储与顶点相关联的其他信息，例如颜色。在当前情况下，我们只使用已声明缓冲区中的一个，因此只需声明一个 VBO 就足够了。

