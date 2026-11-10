
```java
import static com.jogamp.opengl.GL4.*;
import com.jogamp.opengl.*;
import com.jogamp.opengl.awt.GLCanvas;
import com.jogamp.common.nio.Buffers;
import com.jogamp.opengl.GLContext;
import org.joml.*;

public class Code extends JFrame implements GLEventListener
{
    private GLCanvas myCanvas;

    private int renderingProgram;
    private int vao[] = new int[1];
    private int vbo[] = new int[2];
    private float cameraX, cameraY, cameraZ;
    private float cubeLocX, cubeLocY, cubeLocZ;

    // allocate variables used in display() function, so that they won’t need to be allocated during rendering
    private FloatBuffer vals = Buffers.newDirectFloatBuffer(16);  // utility buffer for transferring matrices
    private Matrix4f pMat = new Matrix4f();            // perspective matrix
    private Matrix4f vMat = new Matrix4f();            // view matrix
    private Matrix4f mMat = new Matrix4f();            // model matrix
    private Matrix4f mvMat = new Matrix4f();           // model-view matrix
    private int mLoc, pLoc;
    private float aspect;

    public Code()
    {
        setTitle("Chapter4 - program1a");
        setSize(600, 600);
        myCanvas = new GLCanvas();
        myCanvas.addGLEventListener(this);
        this.add(myCanvas);
        this.setVisible(true);
    }

    public void init(GLAutoDrawable drawable)
    {
        GL4 gl = (GL4) GLContext.getCurrentGL();
        renderingProgram = Utils.createShaderProgram("vertShader.glsl", "fragShader.glsl");
        setupVertices();
        cameraX = 0.0f; cameraY = 0.0f; cameraZ = 8.0f;
        cubeLocX = 0.0f; cubeLocY = -2.0f; cubeLocZ = 0.0f;  // shifted down the Y-axis to reveal perspective
    }

    // main(), reshape(), and dispose() are unchanged
    public static void main(String[] args) { new Code(); }
    public void reshape(GLAutoDrawable drawable, int x, int y, int width, int height) { }
    public void dispose(GLAutoDrawable drawable) { }
}
```

```java
-1.0f, -1.0f, 1.0f, -1.0f, 1.0f, 1.0f, 1.0f, 1.0f, 1.0f,
-1.0f, -1.0f, 1.0f, -1.0f, -1.0f, -1.0f, 1.0f, 1.0f,
-1.0f, -1.0f, -1.0f, -1.0f, 1.0f, -1.0f, -1.0f, -1.0f, 1.0f,
-1.0f, -1.0f, 1.0f, 1.0f, -1.0f, 1.0f, 1.0f, -1.0f, -1.0f,
1.0f, -1.0f, -1.0f, -1.0f, -1.0f, -1.0f, -1.0f, -1.0f, 1.0f,
-1.0f, 1.0f, -1.0f, 1.0f, 1.0f, -1.0f, 1.0f, 1.0f, 1.0f,
1.0f, 1.0f, 1.0f, -1.0f, 1.0f, 1.0f, -1.0f, 1.0f, -1.0f
};
gl.glGenVertexArrays(vao.length, vao, 0);
gl.glBindVertexArray(vao[0]);
gl.glGenBuffers(vbo.length, vbo, 0);

gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
FloatBuffer vertBuf = Buffers.newDirectFloatBuffer(vertexPositions);
gl.glBufferData(GL_ARRAY_BUFFER, vertBuf.limit()*4, vertBuf, GL_STATIC_DRAW);
    }
}
```

## 顶点着色器（文件名："vertShader.glsl"）

```glsl
#version 430

layout (location=0) in vec3 position;

uniform mat4 mv_matrix;
uniform mat4 p_matrix;

void main(void)
{
  gl_Position = p_matrix * mv_matrix * vec4(position, 1.0);
}
```

## 片段着色器（文件名："fragShader.glsl"）

```glsl
#version 430

out vec4 color;

uniform mat4 mv_matrix;
uniform mat4 p_matrix;

void main(void)
{
  color = vec4(1.0, 0.0, 0.0, 1.0);
}
```

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_94_0.png)

**图 4.3**
程序 4.1 的输出：位于 (0,-2,0) 的红色立方体，从 (0,0,8) 处观察。

让我们仔细看看程序 4.1 中的代码。重要的是我们要理解*所有*部分如何工作，*以及它们如何协同工作*。

从检查 Java/JOGL 清单接近末尾的函数 `setupVertices()` 开始，它由 `init()` 调用。在该函数的开头，声明了一个名为 `vertexPositions` 的数组，其中包含构成立方体的 36 个顶点。起初你可能会想，为什么这个立方体有 36 个顶点，而逻辑上一个立方体应该只需要八个。答案是，我们需要用三角形来构建立方体，因此立方体的六个面中的每一个都需要由两个三角形构成，总共为 6×2=12 个三角形（见图 4.4）。由于每个三角形由三个顶点指定，因此总共为 36 个顶点。由于每个顶点有三个值（x,y,z），所以数组中共有 36×3=108 个值。确实，每个顶点会参与多个三角形，但我们仍然分别指定每个顶点，因为目前我们是分别把每个三角形的顶点沿管线向下传递。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_95_0.png)

立方体在其自身的坐标系中定义，(0,0,0) 位于其中心，其各个角沿 x、y、z 轴的范围为 -1.0 到 +1.0。`setupVertices()` 函数的其余部分设置 VAO、两个 VBO（尽管只使用了一个），并将立方体顶点加载到第 0 个 VBO 缓冲区中。

请注意，`init()` 函数执行只需要完成一次的任务：读入着色器代码并构建渲染程序，以及通过调用“`setupVertices()`”将立方体顶点加载到缓冲区中。请注意，它还将立方体和相机定位在世界中；稍后我们将为立方体制作动画，并了解如何移动相机，届时我们可能需要移除这种硬编码的定位。

现在让我们看看 `display()` 函数。回想一下，`display()` 可能会被反复调用，其调用速率称为*帧率*。也就是说，动画通过非常快速地不断绘制和重绘场景（或*帧*）来工作。通常有必要在渲染一帧之前清除深度缓冲区，以便正确进行隐藏面消除（有时不清除深度缓冲区会导致所有表面都被移除，从而产生完全黑屏）。默认情况下，OpenGL 中的深度值范围为 0.0 到 1.0。清除深度缓冲区通过调用 `glClear(GL_DEPTH_BUFFER_BIT)` 完成，它用默认值（通常为 1.0）填充深度缓冲区。

接下来，`display()` 通过调用 `glUseProgram()` 启用着色器，将 GLSL 代码安装到 GPU 上。回想一下，这并不会运行着色器程序，但它确实使后续的 OpenGL 调用能够确定着色器的*顶点属性*和*统一变量*位置。`display()` 函数接下来获取统一变量位置；构建透视矩阵、视图矩阵和模型矩阵；^3 将视图矩阵和模型矩阵连接成单个 MV 矩阵；并将透视矩阵和 MV 矩阵分配给它们对应的统一变量。

接下来，`display()` 启用包含立方体顶点的缓冲区，并将其附加到第 0 个顶点属性，以准备将顶点发送到着色器。

`display()` 做的最后一件事是通过调用 `glDrawArrays()` 绘制模型，指定该模型由三角形组成并且总共有 36 个顶点。对 `glDrawArrays()` 的调用之前通常会有额外的命令，用于调整该模型的渲染设置。^4 在这个例子中，有两个这样的命令，它们都与深度测试有关。回想第 2 章，OpenGL 使用深度测试来执行隐藏面消除。这里我们启用深度测试，并指定我们希望 OpenGL 使用的特定深度测试。所示设置与第 2 章中的描述相对应；在本书后面，我们将看到这些命令的其他用途。

最后，考虑着色器。首先，请注意它们都包含相同的统一变量声明块。尽管这并不总是必需的，但在特定渲染程序中的所有着色器中包含相同的统一变量声明块通常是一种好做法。

还要注意，在顶点着色器中，传入的顶点属性 position 上存在布局限定符。由于位置被指定为“0”，`display()` 函数可以简单地通过在 `glVertexAttribPointer()` 函数调用的第一个参数中使用 0，以及在 `glEnableVertexAttribArray()` 函数调用中使用 0 来引用该变量。还要注意，position 顶点属性被声明为 `vec3`，因此需要将其转换为 `vec4`，以便与将要与之相乘的 4×4 矩阵兼容。此转换通过 `vec4(position,1.0)` 完成，它从名为“position”的变量构建一个 `vec4`，并在新添加的第四个位置放入值 1.0。

^3 细心的读者可能会注意到，不应该在每次调用 `display()` 时都构建透视矩阵，因为它的值不会改变。这在一定程度上是正确的——如果用户在程序运行时*调整*窗口大小，透视矩阵*确实*需要重新计算。在 4.11 节中，我们将更高效地处理这种情况，并在此过程中将透视矩阵的计算从 `display()` 移到 `init()` 函数中。

^4 通常，这些调用可以放在 `init()` 中而不是 `display()` 中。然而，当绘制具有不同属性的多个对象时，有必要将其中一个或多个调用放在 `display()` 中。为简单起见，我们总是将它们放在 `display()` 中。

