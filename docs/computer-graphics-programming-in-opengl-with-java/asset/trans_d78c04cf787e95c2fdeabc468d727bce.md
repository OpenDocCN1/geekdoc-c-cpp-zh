
![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_26_0.png)

**图 2.1**  
基于 JOGL 的图形应用程序概述。

我们将编写的一些代码将使用 Java 并包含 JOGL 调用，另一些将使用 GLSL 编写。我们的 Java/JOGL 应用程序将与 GLSL 模块和硬件协同工作，以生成 3D 图形输出。应用程序完成后，最终用户将与 Java 应用程序交互。

GLSL 是*着色器语言*的一个例子。着色器语言旨在图形管线的上下文中在 GPU 上运行。还有其他着色器语言，例如 HLSL，它与微软的 3D 框架 *DirectX* 配合使用。GLSL 是与 OpenGL 兼容的特定着色器语言，因此除了 Java/JOGL 应用程序代码外，我们还将使用 GLSL 编写着色器代码。

在本章剩余部分，我们将简要“游览”OpenGL 管线。并不要求读者彻底理解每一个细节，只需体会各个阶段如何协同工作。

## 2.1 OPENGL 管线

现代 3D 图形编程利用*管线*，其中将 3D 场景转换为 2D 图像的过程被分解为一系列步骤。OpenGL 和 DirectX 都使用类似的管线。

OpenGL 图形管线的简化概述如图 2.2 所示（并未显示每个阶段，只显示我们将要研究的主要阶段）。Java/JOGL 应用程序将图形数据发送到顶点着色器，处理过程沿管线推进，最终像素输出到显示器上显示。

蓝色阴影阶段（顶点、细分、几何和片段）在 GLSL 中是*可编程*的。Java/JOGL 应用程序的职责之一是将 GLSL 程序加载到这些着色器阶段，如下所示：

- 1. 它使用 Java 获取 GLSL 着色器代码，可以从文本文件中获取，也可以硬编码为字符串。

(1,0,0,1)，对应红色颜色的 RGB 值，外加一个表示不透明度分量的“1”。然后我们使用 OpenGL 调用 glClear(GL_COLOR_BUFFER_BIT) 实际用该颜色填充颜色缓冲区。

### 程序 2.1 第一个 Java/JOGL 应用程序

```java
import javax.swing.*;
import static com.jogamp.opengl.GL4.*;
import com.jogamp.opengl.*;
import com.jogamp.opengl.awt.GLCanvas;

public class Code extends JFrame implements GLEventListener
{  private GLCanvas myCanvas;

   public Code()
   {  setTitle("Chapter2 - program1");
      setSize(600, 400);
      setLocation(200, 200);
      myCanvas = new GLCanvas();
      myCanvas.addGLEventListener(this);
      this.add(myCanvas);
      this.setVisible(true);
   }

   public void display(GLAutoDrawable drawable)
   {  GL4 gl = (GL4) GLContext.getCurrentGL();
      gl.glClearColor(1.0f, 0.0f, 0.0f, 1.0f);
      gl.glClear(GL_COLOR_BUFFER_BIT);
   }

   public static void main(String[] args)
   {  new Code();
   }

   public void init(GLAutoDrawable drawable) { }
   public void reshape(GLAutoDrawable drawable, int x, int y, int width, int height) { }
   public void dispose(GLAutoDrawable drawable) { }
}
```

在 Microsoft Windows 机器上运行 Java/JOGL 应用程序（例如程序 2.1）时，建议添加命令行选项以禁用 Direct3D 加速并禁用 UI 缩放，如下所示：

```bash
java -Dsun.java2d.d3d=false -Dsun.java2d.uiScale=1 Code
```

这些函数的部署机制如下：当 GLCanvas 被设为“可见”时（通过我们对包含它的 JFrame 调用“setVisible(true)”），它会初始化 OpenGL，而 OpenGL 又会创建一个“GL4”对象，我们的应用程序可以使用该对象进行 OpenGL 函数调用。然后 OpenGL 执行“回调”，调用 init()，并向它传递一个“可绘制”对象（在本例中，可绘制对象就是 GLCanvas，尽管从代码中并不明显）。在这个特定示例中，init() 不执行任何操作——在大多数应用程序中，我们会在这里读入 GLSL 代码、加载 3D 模型等。接下来，OpenGL（实际上是 JOGL）调用 display()，同样向它发送可绘制对象。通常的做法是立即获取 GL4 对象并将其放入名为“gl”的变量中（实际上，GL4 是一个接口——在实践中，我们不需要知道实际的 GL 对象类）。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_29_0.png)

**图 2.3**  
程序 2.1 的输出。

稍后我们会看到，如果我们希望场景具有动画效果，Java/JOGL 应用程序将需要告诉 JOGL 额外调用 display()。

现在是仔细查看程序 2.1 中 JOGL 调用的合适时机。考虑下面这个调用：

```java
gl.glClear(GL_COLOR_BUFFER_BIT);
```

由于 JOGL 是 OpenGL 的 Java 绑定，这意味着对 JOGL 的调用会转而生成对 OpenGL 的 C 函数库的调用。在本例中，被调用的 C 函数如 OpenGL 参考文档（可在 https://www.khronos.org/registry/OpenGL-Refpages/gl4/ 查阅）所述，是：

```c
void glClear(GLbitfield mask);
```

首先要注意的是，JOGL 函数的名称与原始 OpenGL C 函数相同，只是前面加上了“gl”——这是 GL4 对象的名称。“gl”后面的句点“.”很重要，因为“gl”是我们调用 OpenGL 函数所依托的对象。

重申一下，GL4 是 OpenGL 函数的 Java 接口。我们可以通过两种方式之一获得它：(a) 调用 drawable.getGL()，利用当 OpenGL 调用（回调）各种 GLEventListener 函数时自动提供的“GLAutoDrawable”对象；或者 (b) 像程序 2.1 中那样调用 GLContext.getCurrentGL()。获取当前 GL4 对象很重要，因为一般来说，OpenGL 文档中描述的任何 OpenGL 函数都可以通过在其前面加上相应 GL4 对象的名称（例如这里的“gl.”）来从 JOGL 中调用。

该参数引用一个名为“GL_COLOR_BUFFER_BIT”的“GLbitfield”；OpenGL 有许多预定义常量（其中一些称为枚举），而这个常量引用的是包含渲染时像素的颜色缓冲区。OpenGL 有多个颜色缓冲区，此命令会清除所有这些缓冲区——也就是说，它用称为“清除色”的预定义颜色填充它们。请注意，此上下文中的“清除”并不意味着“一种透明的颜色”；相反，它指的是重置（清除）颜色缓冲区时应用的颜色。

紧接在调用 glClear() 之前的是对 glClearColor() 的调用。同样，这指定了颜色缓冲区被清除时放入其元素中的值。这里我们指定了 (1.0, 0.0, 0.0, 1.0)，它对应 RGBA 颜色红色。如果未指定“清除色”，默认值为黑色。

最后，除了 display() 和 init() 之外，我们还必须实现 reshape() 和 dispose()。当 GLCanvas 调整大小时会调用 reshape() 函数，应用程序退出时会调用 dispose()。在程序 2.1 中，我们将它们都留空了。

### 2.1.2 顶点着色器和片段着色器

我们的第一个 JOGL 程序实际上没有绘制任何东西——它只是用一种颜色填充了颜色缓冲区。要实际绘制一些东西，我们需要包含一个*顶点着色器*和一个*片段着色器*。

你可能会惊讶地发现，OpenGL 只能绘制少数几种非常简单的东西，例如*点*、*线*或*三角形*。这些简单的东西称为*图元*，因此，大多数 3D 模型由许许多多*图元*组成，通常是三角形。

*图元*由*顶点*组成——例如，一个三角形由三个*顶点*组成。*顶点*可以来自多种来源——它们可以从文件中读取，然后由 Java/JOGL 应用程序加载到缓冲区中，也可以硬编码在 Java 代码甚至 GLSL 代码中。

在这一切发生之前，Java/JOGL 应用程序必须编译并链接适当的 GLSL 顶点着色器和片段着色器程序，然后将它们加载到管线中。我们很快就会看到执行此操作的命令。

应用程序还负责告诉 OpenGL 构造三角形。我们通过使用 JOGL 调用以下 OpenGL 函数来完成此操作：

```c
glDrawArrays(GLenum mode, GLint first, GLsizei count);
```

mode 是图元类型——对于三角形，我们使用 GL_TRIANGLES。参数“first”指示从哪个顶点开始（通常是编号为 0 的顶点，即第一个顶点），而 count 指定要绘制的顶点总数。

调用 glDrawArrays() 时，管线中的 GLSL 代码开始执行。现在让我们向该管线添加一些 GLSL 代码。

无论顶点来自何处，所有顶点都会经过顶点着色器。它们*逐个*经过；也就是说，着色器*每个顶点执行一次*。对于具有大量顶点的大型复杂模型，顶点着色器可能会执行数百次、数千次甚至数百万次，而且常常是并行执行。

让我们编写一个简单程序，其中只有一个顶点，并硬编码在顶点着色器中。这不足以绘制一个三角形，但足以绘制一个点。为了让它显示出来，我们还需要提供一个*片段着色器*。为简单起见，我们将把这两个着色器程序声明为字符串数组。

### 程序 2.2 着色器，绘制一个点

```java
(...imports as before)
public class Code extends JFrame implements GLEventListener
{
    private int renderingProgram;
    private int vao[] = new int[1];   // new declarations

    public Code() { (.....constructor as before) }
    public void display(GLAutoDrawable drawable)
    {   GL4 gl = (GL4) GLContext.getCurrentGL();
        gl.glUseProgram(renderingProgram);
        gl.glDrawArrays(GL_POINTS, 0, 1);
    }

    public void init(GLAutoDrawable drawable)
    {   GL4 gl = (GL4) GLContext.getCurrentGL();
        renderingProgram = createShaderProgram();
```
