

### 程序 2.5 绘制三角形

**顶点着色器**

```glsl
#version 430
void main(void)
{
    if (gl_VertexID == 0) gl_Position = vec4(0.25, -0.25, 0.0, 1.0);
    else if (gl_VertexID == 1) gl_Position = vec4(-0.25, -0.25, 0.0, 1.0);
    else gl_Position = vec4(0.25, 0.25, 0.0, 1.0);
}
```

**C++/OpenGL 应用程序——在 display() 中**

```cpp
...
glDrawArrays(GL_TRIANGLES, 0, 3);
```

![](img/1695de1bc7486362f86c143285f3fb40_48_0.png)

**图 2.15**  
绘制一个简单三角形。

## 2.5 为场景添加动画

本书中的许多技术都可以*动画化*。这指的是场景中的物体正在移动或变化，并且场景会被反复渲染，以实时反映这些变化。

回顾第 2.1.1 节，我们已将 main() 构造为：先对 init() 进行一次调用，然后反复调用 display()。因此，尽管前面的每个示例看起来可能只是一个固定不变的渲染场景，但实际上 main 中的循环一直在使它被一遍又一遍地绘制。

因此，我们的 main() 已经具备支持动画的结构。我们只需设计 display() 函数，使其随着时间改变所绘制的内容。场景的每次渲染称为一个*帧*，调用 display() 的频率称为*帧率*。应用程序逻辑中运动速率的处理，可以通过自上一帧以来经过的时间来控制（这就是将“currentTime”作为 display() 函数参数的原因）。

程序 2.6 展示了一个示例。我们取用程序 2.5 中的三角形并为其添加动画，使它向右移动，然后向左移动，来回往复。在此示例中，我们没有考虑经过的时间，因此三角形的移动速度可能会因计算机速度不同而快慢不一。在后续示例中，我们将使用经过的时间，以确保动画无论在哪台计算机上运行都以相同速度播放。

在程序 2.6 中，应用程序的 display() 方法维护一个变量“x”，用于偏移三角形的 X 坐标位置。每次调用 display() 时，它的值都会改变（因此每一帧的值都不同），并且每当它达到 1.0 或 -1.0 时就会反向。x 的值会被复制到顶点着色器中名为“offset”的对应变量。执行此复制的机制使用了所谓的 uniform 变量，我们将在第 4 章稍后学习它。目前还不需要理解 uniform 变量的细节。现在只需注意，C++/OpenGL 应用程序首先调用 glGetUniformLocation() 获取指向“offset”变量的指针，然后调用 glProgramUniform1f() 将 x 的值复制到 offset。随后，顶点着色器将 offset 加到正在绘制的三角形的 X 坐标上。还要注意，每次调用 display() 时都会清除背景，以避免三角形移动时留下拖尾。图 2.16 展示了三个时间点上的显示情况（当然，运动无法在静态图中展示）。

### 程序 2.6 简单动画示例

**C++/OpenGL 应用程序：**

```cpp
// same #includes and declarations as before, plus the following:
float x = 0.0f;            // location of triangle on x axis
float inc = 0.01f;         // offset for moving the triangle

void display(GLFWwindow* window, double currentTime) {
    glClear(GL_DEPTH_BUFFER_BIT);
    glClearColor(0.0, 0.0, 0.0, 1.0);      // clear the background to black, each time
    glClear(GL_COLOR_BUFFER_BIT);

    glUseProgram(renderingProgram);

    x += inc;                              // move the triangle along x axis
    if(x > 1.0f) inc = -0.01f;             // switch to moving the triangle to the left
    if (x < -1.0f) inc = 0.01f;                      // switch to moving the triangle to the right
    GLuint offsetLoc = glGetUniformLocation(renderingProgram, "offset");   // get ptr to "offset"
    glProgramUniform1f(renderingProgram, offsetLoc, x);        // send value in "x" to "offset"

    glDrawArrays(GL_TRIANGLES, 0, 3);
}   // remaining functions, same as before
```

**顶点着色器：**

```glsl
#version 430
uniform float offset;
void main(void)
{ if (gl_VertexID == 0) gl_Position = vec4(0.25 + offset, -0.25, 0.0, 1.0);
  else if (gl_VertexID == 1) gl_Position = vec4(-0.25 + offset, -0.25, 0.0, 1.0);
  else gl_Position = vec4(0.25 + offset, 0.25, 0.0, 1.0);
}
```

![](img/1695de1bc7486362f86c143285f3fb40_50_0.png)

**图 2.16**  
一个带动画的移动三角形。

请注意，除了添加用于为三角形制作动画的代码之外，我们还在 `display()` 函数的开头添加了以下行：

```cpp
glClear(GL_DEPTH_BUFFER_BIT);
```

虽然在这个特定示例中并非严格必需，但我们还是在这里添加了它，并且它将继续出现在我们的大多数应用程序中。回顾第 2.1.7 节中的讨论，*隐藏面消除*需要颜色缓冲区和深度缓冲区。随着我们逐步绘制越来越复杂的三维场景，就有必要每帧初始化（清除）深度缓冲区，尤其是对于带动画的场景，以确保深度比较不会受到旧深度数据的影响。从前面的示例应当可以明显看出，清除深度缓冲区的命令与清除颜色缓冲区的命令基本相同。

## 2.6 组织 C++ 代码文件

到目前为止，我们一直将所有 C++/OpenGL 应用程序代码放在一个名为“main.cpp”的文件中，并将 GLSL 着色器放在名为“vertShader.glsl”和“fragShader.glsl”的文件中。虽然我们承认，将大量应用程序代码塞进 main.cpp 并不是最佳实践，但本书采用了这一约定，以便在每个示例中都绝对清楚地表明哪个文件包含与所讨论示例相关的主要 C++/OpenGL 代码块。在整本教材中，它都将始终被称为“main.cpp”。在实践中，应用程序当然应当模块化，以恰当地反映应用程序所执行的任务。

然而，随着内容推进，我们会遇到一些创建模块的情形，这些模块将在许多不同的应用程序中有用。只要合适，我们就会将这些模块移到单独的文件中，以便于复用。例如，稍后我们将定义一个 Sphere 类，它在许多不同示例中都会有用，因此它将被分离到自己的文件（Sphere.cpp 和 Sphere.h）中。

同样，当我们遇到希望复用的函数时，我们会将它们放入名为“Utils.cpp”的文件（以及关联的“Utils.h”）中。我们已经见过几个适合移入“Utils.cpp”的函数：第 2.2 节描述的错误检测模块，以及第 2.3 节描述的用于读取 GLSL 着色器程序的函数。后者特别适合重载，从而可以为给定应用程序中组装的各种可能的管线着色器组合分别定义“createShaderProgram()”函数：

- `GLuint Utils::createShaderProgram(const char *vp, const char *fp)`
- `GLuint Utils::createShaderProgram(const char *vp, const char *gp, const char *fp)`
- `GLuint Utils::createShaderProgram(const char *vp, const char *tCS, const char *tES, const char *fp)`
- `GLuint Utils::createShaderProgram(const char *vp, const char *tCS, const char *tES, const char *gp, const char *fp)`

上一列表中的第一种情况支持仅使用顶点着色器和片段着色器的着色器程序。第二种支持使用顶点、几何和片段着色器的程序。第三种支持使用顶点、细分和片段着色器的程序。第四种支持使用顶点、细分、几何和片段着色器的程序。每种情况接受的参数都是包含着色器代码的 GLSL 文件的路径名。例如，下面的调用使用其中一个重载函数来编译并链接一个包含顶点着色器和片段着色器的着色器管线程序。完成后的程序被放入变量“renderingProgram”中：

```cpp
renderingProgram = Utils::createShaderProgram("vertShader.glsl", "fragShader.glsl");
```

![](img/1695de1bc7486362f86c143285f3fb40_52_0.png)

这些 createShaderProgram() 实现都可以在随附 CD 中找到（在“Utils.cpp”文件中），并且它们都同样集成了第 2.2 节中的错误检测模块。它们并没有什么新内容；只是为了方便而按这种方式组织。随着本书内容的推进，我们还会陆续向 Utils.cpp 中添加其他类似函数。强烈建议读者查看随附 CD 上的 Utils.cpp 文件，甚至根据需要向其中添加内容。其中找到的程序是按照我们在书中学习这些方法的过程构建的，研究它们的组织方式应当有助于加深读者自己的理解。

关于“Utils.cpp”文件中的函数，我们将它们实现为静态方法，因此不必实例化 Utils 类。读者可能更愿意将它们实现为实例方法而不是静态方法，甚至实现为独立函数，这取决于所开发特定系统的架构。

我们所有的着色器都将以“.glsl”扩展名命名。

## 补充说明

本入门章节中，我们没有讨论 OpenGL 管线的许多细节。我们跳过了一些内部阶段，并且完全省略了纹理是如何处理的。我们的目标是尽可能简单地勾勒出我们将编写代码所依托的框架。随着内容推进，我们将继续学习更多细节。

我们还推迟了细分和几何相关代码示例的展示。在后续章节中，我们将构建完整系统，展示如何为每个阶段编写实用的着色器。

