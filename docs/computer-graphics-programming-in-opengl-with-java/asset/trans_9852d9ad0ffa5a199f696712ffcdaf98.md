
例如，考虑程序4.1。如果我们重新组织代码，将透视矩阵的计算从 display() 中移除，那么 init()、display() 和 reshape() 函数的修订版本将如下所示：

```java
public void init(GLAutoDrawable drawable)
{
    // same as earlier, plus the following two lines:
    aspect = (float) myCanvas.getWidth() / (float) myCanvas.getHeight();
    pMat.setPerspective((float) Math.toRadians(60.0f), aspect, 0.1f, 1000.0f);
}

public void display(GLAutoDrawable drawable)
{
    // same as earlier, except with the following lines removed:
    // build perspective matrix
    // aspect = (float) myCanvas.getWidth() / (float) myCanvas.getHeight();
    // pMat.setPerspective((float) Math.toRadians(60.0f), aspect, 0.1f, 1000.0f);
    // the rest of the function is unchanged
}

public void reshape(GLAutoDrawable drawable, int x, int y, int width, int height)
{
    GL4 gl = (GL4) GLContext.getCurrentGL();
    aspect = (float) width / (float) height;    // new window width & height are provided by the callback
    gl.glViewport(0, 0, width, height);         // sets region of screen associated with the frame buffer
    pMat.setPerspective((float) Math.toRadians(60.0f), aspect, 0.1f, 1000.0f);
}
```

### 4.11.3 背面剔除

提高渲染效率的另一种方法是利用 OpenGL 执行*背面剔除*的能力。当一个 3D 模型完全“封闭”时，即其内部永远不可见（例如立方体和棱锥），那么结果表明，外表面中那些背向观察者成角度的部分总是会被同一模型的某个其他部分遮挡。也就是说，那些背向观察者的三角形不可能被看到（无论如何它们都会被隐藏面消除覆盖掉），因此没有理由对它们进行光栅化或渲染。

我们可以通过命令 glEnable(GL_CULL_FACE) 要求 OpenGL 识别并“剔除”（不渲染）背面朝向的三角形。我们也可以使用 glDisable(GL_CULL_FACE) 禁用面剔除。默认情况下，面剔除是禁用的，因此如果你希望 OpenGL 剔除背面朝向的三角形，就必须启用它。

启用面剔除后，默认情况下只渲染*正面朝向*的三角形。同样默认情况下，如果从 OpenGL 相机观察时，一个三角形的三个顶点按*逆时针*方向排列（基于它们在缓冲区中定义的顺序），则该三角形被视为正面朝向。顶点按顺时针方向排列的三角形（从 OpenGL 相机观察）是*背面朝向*的，不会被渲染。这种将“正面朝向”定义为逆时针的做法有时称为*环绕顺序*，并且可以通过函数调用 glFrontFace(GL_CCW) 显式设置为逆时针（默认），或通过 glFrontFace(GL_CW) 设置为顺时针。类似地，也可以显式设置渲染的是正面朝向还是背面朝向的三角形。实际上，为此我们指定哪些三角形*不*渲染——也就是哪些被“剔除”。我们可以通过调用 glCullFace(GL_BACK) 指定剔除背面朝向的三角形（尽管这没有必要，因为这是默认行为）。或者，我们可以通过分别将参数 GL_BACK 替换为 GL_FRONT 或 GL_FRONT_AND_BACK，来指定改为剔除正面朝向的三角形，甚至剔除所有三角形。

正如我们将在第6章看到的，3D 模型通常被设计为其外表面由具有相同环绕顺序的三角形构成——最常见的是逆时针——因此如果启用了剔除，默认情况下会渲染模型外表面中面向相机的部分。由于 OpenGL 默认假定环绕顺序为逆时针，如果某个模型被设计为以*顺时针*环绕顺序显示，那么在启用背面剔除时，程序员需要调用 glFrontFace(GL_CW) 来处理这种情况。

注意，对于 GL_TRIANGLE_STRIP 的情况，每个三角形的环绕顺序会交替变化。OpenGL 通过如下方式在构建每个后续三角形时“翻转”顶点序列来补偿这一点：0-1-2，然后是 2-1-3、2-3-4、4-3-5、4-5-6，依此类推。

背面剔除通过确保 OpenGL 不会花时间光栅化和渲染那些永远不打算被看到的表面来提高性能。我们在本章中看到的大多数示例都非常小，因此几乎没有启用面剔除的动力（一个例外是图4.9所示的示例，其中有 100,000 个实例化动画立方体，这可能在某些系统上带来性能挑战）。在实践中，大多数 3D 模型通常是“封闭”的，因此习惯上会常规启用背面剔除。例如，我们可以通过如下修改 display() 函数，将背面剔除添加到程序4.3中：

```java
public void display(GLAutoDrawable drawable)
{
  . . .
  gl.glEnable(GL_CULL_FACE);

  // draw the cube

  gl.glEnable(GL_DEPTH_TEST);
  gl.glDepthFunc(GL_LEQUAL);
  gl.glFrontFace(GL_CW);         // the cube vertices have clockwise winding order
  gl.glDrawArrays(GL_TRIANGLES, 0, 36);

  // draw the pyramid

  . . .
  gl.glEnable(GL_DEPTH_TEST);
  gl.glDepthFunc(GL_LEQUAL);
  gl.glFrontFace(GL_CCW);        // the pyramid vertices have counter-clockwise winding order
  gl.glDrawArrays(GL_TRIANGLES, 0, 18);
}
```

使用背面剔除时，正确设置环绕顺序很重要。错误的设置（例如本应为 GL_CCW 时却设为 GL_CW）可能导致渲染对象的内部而不是外部，进而产生类似于错误透视矩阵所造成的失真。

效率并不是进行面剔除的唯一原因。在后续章节中，我们将看到其他用途，例如当我们想看到 3D 模型的*内部*时，或在使用透明度时。

## 补充说明

JOML 拥有种类繁多的函数，用于执行平移、旋转和缩放。例如，JOML 的函数“translate()”和“translation()”略有不同。前者将平移连接到现有矩阵上，而后者构建一个平移矩阵。我们在示例中已经使用了这两个函数，还有许多其他函数可供选择。读者应仔细复核所使用的 JOML 函数确实执行了期望的操作。

正如本章所提到的，在使用 Java 缓冲区时，建议确保只使用直接缓冲区。例如，很容易想用 Java 的 FloatBuffer.wrap() 函数将存储在数组中的顶点数据放入缓冲区。然而，wrap() 生成的是*非直接*缓冲区，其中得到的缓冲区只是对仍存储在数组中的数据的包装。⁶ 将数据复制到*直接*缓冲区的一种方法是：分配一个直接 ByteBuffer，使用 ByteBuffer.asFloatBuffer() 将其视为 FloatBuffer，然后使用带 put() 命令的循环逐个复制数据。如前所述，JOGL 的 com.jogamp.common.nio.Buffers 类提供了便捷方法，可将数组数据加载到多种缓冲区类型中，从而更容易填充直接缓冲区：

- `newDirectByteBuffer(byte[ ])`
- `newDirectCharBuffer(char[ ])`
- `newDirectDoubleBuffer(double[ ])`
- `newDirectFloatBuffer(float[ ])`
- `newDirectIntBuffer(int[ ])`
- `newDirectLongBuffer(long[ ])`
- `newDirectShortBuffer(short[ ])`

使用上述 JOGL 方法用顶点数据（即打算供 JOGL 应用程序使用的数据）填充缓冲区，还能确保正确的本机字节序。它还能确保正确的容量分配，并且无需进行显式分配。

在 OpenGL/JOGL/GLSL 中，还有大量其他功能和结构可用于管理和利用数据，而本章只是触及了表面。例如，我们还没有介绍*统一块*，这是一种用于组织统一变量的机制，类似于 C 语言中的*结构体*。统一块甚至可以设置为从缓冲区接收数据。另一种强大的机制是*着色器存储块*，它本质上是一个着色器可以写入的缓冲区。

关于管理数据的众多选项，一个很好的参考资料是 *OpenGL 超级宝典* [SW15]，特别是其中题为“数据”的一章（第七版第5章）。它还描述了许多细节和选项

⁶ 在 JOGL 中实际上允许使用非直接缓冲区。但是，当把非直接缓冲区传递给 JOGL 方法时，JOGL 会将其转换为直接缓冲区，而这种转换会带来性能损失。
