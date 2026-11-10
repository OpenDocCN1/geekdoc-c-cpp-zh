

它在深度缓冲区中。用于构建透视矩阵的近裁剪面和远裁剪面之间的范围越大，两个对象的点（实际深度相似但不相等）就越有可能在深度缓冲区中被表示为相同的数值。因此，程序员需要选择近裁剪面和远裁剪面的值，以最小化两个平面之间的距离，同时确保场景中所有必要的对象都位于视锥体内。

同样重要的是要理解，由于透视变换的效果，改变近裁剪面的值比等效地改变远裁剪面的值，对 Z-fighting 伪影出现可能性的影响更大。因此，建议避免选择离眼睛太近的近裁剪面。

本书前面的示例在调用 perspective() 时，对近、远裁剪面简单地使用了 0.1 和 1000 这两个值。这些值可能需要根据你的场景进行调整。

## 4.10 图元的其他选项

OpenGL 支持多种图元类型——到目前为止，我们已经看到了两种：GL_TRIANGLES 和 GL_POINTS。实际上，还有其他几种。OpenGL 支持的所有可用图元类型都属于三角形、线段、点和补丁（patch）这几类。以下是完整列表：

### 三角形图元

| 图元 | 描述 |
|---|---|
| **GL_TRIANGLES**<br>![GL_TRIANGLES 示意图](gl_triangles.png) | 本书中最常用的图元类型。经过管线的顶点构成独立的三角形：<br>`vertices:` 0 1 2 3 4 5 6 7 8 等。<br>`triangles:` ✓ ✓ ✓ |
| **GL_TRIANGLE_STRIP**<br>![GL_TRIANGLE_STRIP 示意图](gl_triangle_strip.png) | 经过管线的每个顶点会与前面两个顶点高效地构成一个三角形：<br>`vertices:` 0 1 2 3 4 等。<br>`triangles:` ✓ ✓ ✓ |
| GL_TRIANGLE_FAN | [示意图：顶点 0、1、2、3、4 构成三角形扇形] 经过管线的每一对顶点都会与第一个顶点构成一个三角形：<br><br>*vertices:* 0 1 2 3 4 等。<br><br>*triangles:* [三角形示意图] |
| GL_TRIANGLES_ADJACENCY | 仅用于几何着色器。允许着色器访问当前三角形的顶点，以及额外的相邻顶点。 |
| GL_TRIANGLE_STRIP_ADJACENCY | 仅用于几何着色器。与 GL_TRIANGLES_ADJACENCY 类似，不同之处在于三角形顶点像 GL_TRIANGLE_STRIP 一样重叠。 |

### 线段图元

| 图元 | 描述 |
|---|---|
| GL_LINES | [示意图：两组独立线段] 经过管线的顶点构成独立的线段：<br><br>*vertices:* 0 1 2 3 4 5 等。<br><br>*lines:* [线段示意图] |
| GL_LINE_STRIP | [示意图：由连续顶点构成的线段] 经过管线的每个顶点会与前面的顶点高效地构成一条线段：<br><br>*vertices:* 0 1 2 3 等。<br><br>*lines:* [线段示意图] |
| GL_LINE_LOOP | 与 GL_LINE_STRIP 相同，只是在第一个顶点和最后一个顶点之间也会形成一条线段。 |
| GL_LINES_ADJACENCY | 用于几何着色器。允许着色器访问当前线段的顶点，以及额外的相邻顶点。 |
| GL_LINE_STRIP_ADJACENCY | 与 GL_LINES_ADJACENCY 类似，不同之处在于线段顶点像 GL_LINE_STRIP 一样重叠。 |

### 点图元

| 图元 | 描述 |
|---|---|
| GL_POINTS | 经过管线的每个顶点都是一个点。 |

### 补丁图元

| 图元 | 描述 |
|---|---|
| GL_PATCHES | 仅用于曲面细分着色器（tessellation shaders）。它表示一组顶点从顶点着色器传递到曲面细分控制着色器，在那里它们通常用于将细分网格塑造成曲面。 |

## 4.11 性能编码

随着 3D 场景复杂度的增加，我们会越来越关注性能。我们已经看到过一些为了速度而做出编码决策的例子，例如使用实例化（instancing）以及将开销较大的计算移入着色器。

实际上，我们呈现的代码已经包含了一些我们尚未讨论的额外优化，其中部分优化得益于 JOML 数学库。现在我们探讨这些优化以及其他重要技术。

### 4.11.1 尽量减少动态内存分配

在 Java/JOGL 应用程序中，与性能相关的关键模块显然是 display() 函数。这是在任何动画或实时渲染期间被反复调用的函数，因此我们必须在这个函数（或它调用的任何函数）中力求最高效率。

将 display() 函数中的开销保持在最低限度的一个重要方法是避免任何需要内存分配的步骤。因此，需要避免的典型例子包括：

- 实例化对象
- 声明变量
- 分配缓冲区

我们鼓励读者回顾一下到目前为止开发的每个程序，并注意在 display() 函数实际被调用之前，display() 函数中使用的每个变量（除了 GL4 变量 gl）都已声明并分配了空间。另一个例子是 Matrix4fStack，JOML 要求预先分配最大栈大小，这样整个栈就会提前分配完毕，因此在 display() 中执行的“压栈”操作不会动态分配空间。实际上，我们现在尽量减少 display() 中出现的任何类型的声明或实例化。例如，程序 4.1 在其清单的开头包含了以下代码块：

```
    // allocate variables used in display(), so they aren't allocated during rendering
    private FloatBuffer vals = Buffers.newDirectFloatBuffer(16);   // for transferring matrices
    private Matrix4f pMat = new Matrix4f();    // perspective matrix
    private Matrix4f vMat = new Matrix4f();    // view matrix
    private Matrix4f mMat = new Matrix4f();    // model matrix
    private Matrix4f mvMat = new Matrix4f();   // model-view matrix
    private int mvLoc, pLoc;
    private float aspect;
```

请注意，我们特意在代码块顶部添加了一条注释，表明这些变量是为在 display() 函数中稍后使用而预先分配的（尽管我们只是现在才明确指出来）。

还有其他更微妙的例子。例如，将数据从一种类型转换为另一种类型的函数调用，在某些情况下可能会实例化并返回转换后的新数据。因此，理解从 display() 调用的任何库函数的行为非常重要。

幸运的是，我们使用的数学库 JOML 经过精心设计，可以消除（或至少尽量减少）调用其函数所导致的内存分配，同时仍然提供 OpenGL 所需的功能。它的大多数函数直接作用于调用该函数的对象，或作用于其参数之一（而不是构建一个结果并返回它），因此在这两种情况下，都可以预先分配保存结果的空间。

JOML 在以这种方式最大化性能方面的巧妙设计，可以从对 glUniformMatrix4fv() 的调用中看出。让我们仔细看看这样一个调用，它将模型视图矩阵传输到一个 uniform 变量：

```
    gl.glUniformMatrix4fv(mvLoc, 1, false, mvMat.get(vals));
```

回想一下，变量 mvMat 的类型是 Matrix4f，我们希望将该矩阵中的值发送到由 mvLoc 指向的着色器 uniform。不出所料，JOML 库提供了一个 get() 函数来获取矩阵值。我们通常可能会期望这样的“get”函数将那些值返回到一个对象（例如数组）中（就像其他数学库如 glm 或 graphicslib3D 所做的那样）。然而，JOML 却要求在调用 get() 时包含一个参数，然后将该参数用作放置检索到的矩阵值的目的地。巧妙之处在于，JOML 的 get() 函数还会返回一个对用户提供的目的地对象的引用，因此可以直接将对 get() 的调用放入 glUniformMatrix4fv() 的调用中（该调用期望这样的引用）。还要注意，我们已经在 display() 外部的声明块中声明并分配了这个目的地变量“vals”（以及 display() 中使用的所有其他变量）。从某种意义上说，get() 实际上是在做一种“put”，但以这种方式实现时，显然能够满足 OpenGL 环境中“get”函数的需求，而且效率要高得多。

按照 JOML 开发人员的建议，我们使用了期望 FloatBuffer 作为目的地参数形式的 get()。JOGL 允许将缓冲区或数组传输到结构化 uniform 变量（例如 mat4 或 vec4）。但使用缓冲区时性能稍好一些，尤其是在这里，因为 JOML 强制使用直接 NIO 缓冲区，而不是作为 Java 基本类型包装器的缓冲区。

### 4.11.2 预计算透视矩阵

另一个可以减少 display() 函数开销的优化措施，是将透视矩阵的计算移到 init() 函数中。我们之前在 4.5 节中（嗯，在一个脚注中）提到过这种可能性。虽然这当然很容易做到，但有一个小问题。虽然通常不需要重新计算透视矩阵，但如果运行应用的用户*调整*了窗口大小（例如通过拖动窗口角落的调整大小手柄），那么就有*必要*重新计算。

幸运的是，每当窗口大小调整时，JOGL 都会自动调用 reshape()。到目前为止，我们一直将 reshape() 函数留空——现在我们可以利用它了。我们只需将计算透视矩阵的代码移到 init() 中，并同时将其复制到 reshape()。

