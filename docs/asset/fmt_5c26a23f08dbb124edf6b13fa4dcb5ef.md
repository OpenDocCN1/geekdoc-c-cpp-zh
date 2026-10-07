
# C++ 3D 图形技能精通指南

![](img/5f029c1d57776416a7d2524f3734d7cf_0_0.png)

## 使用 C++ 的 OpenGL 图形学编程

使用 C++ 的 OpenGL 图形学编程

使用 C++ 进行 OpenGL 需要配置若干库。此时，根据个人的需求，有大量令人眼花缭乱的选项供选择。在本节中，我们将描述需要哪些库、每个库的某些常用选项，以及我们在整本书中将使用的选项。有关如何为你的特定平台安装和配置这些库的详细信息，请参阅附录。

总而言之，你需要用于以下函数的语言和库：

- C++ 开发环境
- OpenGL / GLSL
- 窗口管理
- 扩展库
- 纹理管理

读者可能需要执行几个准备步骤，以确保这些项中的每一个都已在其系统中正确安装并可以正常访问。在接下来的子节中，我们将简要描述每一个项；有关如何安装和配置它们以便使用的详细信息，请参阅附录。

C++ 是一种通用编程语言，最早于 20 世纪 80 年代中期。它的设计以及通常被编译为原生机器代码的特性，使其成为需要高性能（如 3D 图形计算）系统的优秀选择。C++ 的另一个优势是 OpenGL 调用是基于 C 的。

有许多 C++ 开发环境可用。在本书中，如果使用 PC，我们推荐使用 Visual Studio [`VS17`]，如果使用 Macintosh，则使用 Xcode [`XC18`]。根据你的平台，安装和配置每个环境的描述已列在附录中。

OpenGL 1.0 版本于 1992 年出现，作为计算机图形特定厂商应用程序编程接口（APIs）的“开放”替代方案。

它的规范和开发由 OpenGL 架构评审委员会 (ARB) 管理和控制，当时是一个由行业参与者组成新组建的群体。2006 年，ARB 将 OpenGL 规范的控制权交给了 Khronos Group，这是一个非营利财团，不仅管理 OpenGL 规范，还管理各种其他开放行业标准。被称为“立即渲染模式”。

自诞生以来，OpenGL 定期进行修订和扩展。2004 年，2.0 版本引入了 OpenGL 着色器语言 (`GLSL`)，允许“着色器程序”直接安装并运行在图形流水线阶段中。

2009 年，3.1 版本删除了大量已弃弃的特性，以强制使用着色器着色而非早期方法（称为核心配置模式）。更近的特性是 4.0 版本（2010 年），它在可编程流水线中添加了细分阶段。

OpenGL 假设用户正在使用带有支持至少 4.3 版本 OpenGL 的图形显卡的机器。如果你不确定你的 GPU 支持哪个版本的 OpenGL，网上有很多免费的应用程序可以用来查找。其中一个应用程序是由名为 realtechvr* 公司开发的 `GLView` [`GV16`]。

OpenGL 不直接在计算机屏幕上绘图。相反，它渲染一个帧缓冲区，而将帧缓冲区的内容绘制到屏幕窗口上是单台机器的任务。有各种库支持完成此操作。一种选择是使用操作系统提供的窗口功能，例如 Microsoft Windows API。这通常是不切实际的，并且需要大量的低级编码。`GLUT` 是一个历史上流行的选项；然而，它已经被弃用。一个现代化的扩展是 `freeglut`。其他相关选项是 `CPW`、`GLOW` 和 `GLUI`。

最流行的选项之一，也是本书使用的选项，是 `GLFW`，它具有对 Windows、MacOS、Linux 和其他系统的内置支持 [`GF17`]。它可以从 `www.glfw.org` 下载，并且必须在要使用的机器上进行编译（我们在附录中描述了这些步骤）。

1 尽管如此，许多显卡制造商（特别是 NVIDIA）继续支持已废弃用的功能。

OpenGL 围绕一组基础函数和一种扩展机制组织，以在技术不断进步时支持新功能。OpenGL 的现代版本（例如我们在书中使用的 4+ 版本）需要识别 GPU 上可用的扩展。核心 OpenGL 中内置了用于执行此操作的命令，但它们涉及许多几行相当复杂的代码，并且对于使用的每个现代命令——而且我们在书中经常使用它们——都必须执行这些代码。因此，使用扩展库来处理这些细节，并直接为程序员提供这些命令进行修改已成为标准做法。示例包括 `Glee`、`GLEoader`、`GLEW`，以及最近的 `GLW` 和 `GLAD`。

列出的库中，常用的是 `GLEW`，它代表 OpenGL Extension Wrangler。它适用于包括 Windows、Macintosh 和 Linux 在内的多种操作系统 [7]。`GLEW` 并不是一个完美的选择；例如，它需要额外的 DLL。最近，许多开发者正在选择 `GL3W` 或 `GLAD`。它们的优势是自动更新，但它们也要求安装 Python。出于这些原因，我们在本书中选择使用 `GLEW`。它可以在 `gle.sourceforge.org` 下载。安装和配置 `GLEW` 的完整说明已列在附录中。

3D 图形大量使用向量和矩阵代数。由于由于原因，通过配备函数库或类包来支持常见的数学任务，极大方便了 OpenGL 的使用。常用的 OpenGL 的两种库有 `Eigen` 和 `vmath`，后者是流行的 [15]。

大约最流行的，也是本书使用的，是 OpenGL 数，通常称为 `GLM`。它是一个兼容 Windows、Macintosh 和 Linux 的头文件 C++ 库 [7]。`GLM` 提供了与图形概念相关的基础数学函数，例如向量、矩阵和元数。它还包含了用于创建和使用常用 3D 结构的实用类，如透视和观察矩阵。它于 2005 年首次发布，由 Christophe Riccio 维护 [`17`]。安装 `GLM` 的说明已在附录中。

从第 5 章开始，我们将使用图像文件为对象添加“纹理”。这意味着我们经常需要在 C++/OpenGL 代码中加载此类图像文件。可以从开始编写纹理加载器；然而，考虑到各种图像格式，通常优先是使用纹理加载库。示例包括 `FreeImage`、`Devil`、`OpenGL (GL)` 和 `Giraw`。最常用的加载库是 Simple OpenGL Image Loader (`SOIL`)，尽管它已经有些过时。

本书使用的纹理加载库是 `SOIL2`，它是 `SOIL` 的更新分支。与我们之前选择的库一样，`SOIL2` 兼容多种平台 [`SO17`]，详细的安装配置说明在附录中。

还有许多读者可能希望使用的其他有用库。例如，在书中展示了如何从开始实现一个简单的“OBJ”模型加载器。然而，正如我们所看到的，它并没有处理 OBJ 标准中提供的许多选项。一些更复杂的 OBJ 导入器示例是 `Assimp` 和 `tinyobloader`。对于我们的示例，我们将只使用书中描述和实现的简单模型。

在开发本书的 C++ 版本期间，我们一直在为运行示例程序所需的特定平台配置信息寻求最佳方法。配置一个用于 C++ 使用 OpenGL 的系统比使用 Java 的等效配置要复杂得多，后者可以在几个简短的段落内描述（如在 Java 版书中所示 [`GC18`]）。最终，我们选择将安装和配置信息分离到各个特定平台的附录中。我们希望

这将为每位读者提供一个单一的相关区域，用于查找其特定系统的信息，同时避免因平台特定的细节而拖累正文内容，因为这些细节可能对每位读者都适用。在本版中，我们在附录 A 中提供了 Microsoft Windows 的详细配置说明，在附录 B 中提供了 Apple Macintosh 的说明。

- [`GC18`] V. Gordon and J. Clevenger, Computer Graphics Programming in OpenGL with Java, 2nd ed. (Mercury Learning, 2018).
- [`GE17`] OpenGL Extension Wrangler (GLEW), accessed October 2018, [`http://glew.sourceforge.net/`](http://glew.sourceforge.net/)
- [`GF17`] Graphics Library Framework (GLFW), accessed October 2018, [`http://www.glfw.org/`](http://www.glfw.org/)
- [`GM17`] OpenGL Mathematics (GLM), accessed December 2017, [`http://glm-tru.net/0.9/8/index.html`](http://glm-tru.net/0.9/8/index.html)
- [`GV16`] GLView, realtech-vr, accessed October 2018, [`http://www.realtech-vr.com/`](http://www.realtech-vr.com/)
- [`SO17`] Simple OpenGL Image Library 2 (SOIL2), SpartanJ, accessed October 2018, [`https://bitbucket.org/Spartan/soil2`](https://bitbucket.org/Spartan/soil2)
- [`SW15`] G. Sellers, R. WrightJr., and N. Hamel, OpenGLSuperBible: Comprehensive Tutorial and Reference, 7th ed. (Addison-Wesley, 2015).
- [`VS17`] Microsoft Visual Studio downloads, accessed October 2018, [`https://www.visualstudio.com/downloads`](https://www.visualstudio.com/downloads)
- [`XC18`] Apple Developer site for Xcode, accessed January 2018, [`https://developer.apple.com/xcode`](https://developer.apple.com/xcode)

OpenGL（图形库）是一种多平台的 2D 和 3D 图形 API，它结合了硬件和软件。使用 OpenGL 需要一张支持足够新版本的 OpenGL 的显卡（GPU）（如第 1 章所述）。

在硬件方面，OpenGL 提供了一个多阶段的图形流水线，该流水线可以使用名为 `GLSL`（OpenGL 着色器语言）的语言进行部分编程。

在软件方面，OpenGL 的 API 用 C 和 C++ 编写。对于十多种其他流行语言（Java、Perl、Python、Visual Basic、Delphi、Haskell、Lisp、Ruby），提供了稳定的语言绑定（“封装器”），性能几乎等同。本教程使用 C++，这可能是最流行的语言选择。使用 C++ 时，程序员编写运行在 CPU 上的代码（当然是经过编译的），并包含 OpenGL 调用。我们将包含 OpenGL 调用的 C++ 程序称为 C++/OpenGL 应用。C++/OpenGL 应用程序的一个重要任务是将程序员的 GLSL 代码安装到 GPU 上。

图 2.1 显示了基于 C++ 的图形应用程序的概述，其中软件组件用粉色突出显示。

我们将编写一些 C++ 代码（包含 OpenGL 调用），另一些将用 GLSL 编写。我们的 C++/OpenGL 应用程序将与 GLSL 模块以及硬件协同工作，创建 3D 图形输出。一旦应用程序完成，最终用户将与 C++ 应用程序进行交互。

![](img/5f029c1d57776416a7d2524f3734d7cf_7_0.png)

图 2.1 基于 C++ 的图形应用程序概述。

`GLSL` 是着色器语言的一个示例。着色器语言旨在图形流水线的环境中运行在 GPU 上。还有其他着色器语言，例如 `HLSL`，它与微软的 3D 框架 DirectX 工作；`GLSL` 是兼容 OpenGL 的特定着色器语言，除了 C++/OpenGL 应用代码外，我们用 GLSL 编写着色代码。

在本章的剩余部分，我们将对 OpenGL 流水线进行简单的“之旅”。读者不需要深入理解每一个细节，但应该了解各个阶段是如何协同工作的。

现代 3D 图形利用流水线，其中将 3D 场景转换为 2D 图像的过程分解为一系列步骤。OpenGL 和 DirectX 使用类似的流水线。

图 2.2 显示了 OpenGL 流水线的简化概述（未显示每个阶段，我们将学习主要阶段）。C++/OpenGL 应用程序将数据发送到顶点着色器——通过流水线处理，然后产生像素并显示在显示器上。

在着色器中定义的阶段（顶点、细分、几何和片元）在 `GLSL` 中是可编程的。C++/OpenGL 应用程序的任务之一是将 `GLSL` 程序加载到这些着色器阶段，如下所示：

1. 它使用 C++ 获取 `GLSL` 代码，从文件获取或硬编码为字符串。
2. 然后它创建 OpenGL 对象并加载 `GLSL` 到其中。
3. 最后，它使用 OpenGL 命令编译并链接对象。

在实践中，通常需要为顶点和片元阶段提供 `GLSL` 代码，而细分和几何阶段是可选的。让我们遍历整个过程，看看每个步骤发生了什么。

图形应用程序的大部分用 C++ 编写。根据程序的目的，它可以使用标准 C++ 库与最终用户交互。我们将使用几个额外的库：`GLEW`（扩展封装）、`GLM`（数学）、`SOIL2`（图像加载）和 `GLFW`（图形库）。`GLFW` 库包含一个名为 `GLFWwindow` 的类，我们可以在上面绘制 3D 场景。正如提到的，OpenGL 提供了将 `GLSL` 程序安装到可编程着色器并进行编译的命令。

`init()` 函数是放置应用程序初始化任务的地方。`display()` 方法是放置在 `GLFWwindow` 上进行绘制代码的地方。

img/5f029c1d57776416a7d2524f373d7cf_8_0.png

在此示例中，`glClear()` 命令指定了清除背景时应用的颜色值——在本例中为 (1,0,0,1)，对应红色的 RGB 值（加上透明度部分的“1”）。然后我们使用 OpenGL `glClear(GL_COLOR_BUFFER_BIT)` 填充缓冲区。

```
#include <GL/glew.h>
#include <GLFW/glfw3.h>
#include <iostream>

using namespace std;

    glClear(1.0, 0.0, 0.0, 1.0);
    glClear(GL_COLOR_BUFFER_BIT);
}

int main(void) {
    if (!glfwInit()) return EXIT_FAILURE;
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
    GLFWwindow* window = glfwCreateWindow(600, 600, "Chapter 2 - program 1", NULL, NULL);
    glfwMakeContextCurrent(window);
    if (glewInit() != GLEW_OK) { return EXIT_FAILURE; }
    glfwSwapInterval(1);

    init(window, 0);
        display(window, glfwGetTime());
        glfwSwapBuffers(window);
        glfwPollEvents();
    }

    glfwDestroyWindow(window);
    glfwTerminate();
    return EXIT_SUCCESS;
}
```

程序 2.1 的输出如图 2.3 所示。

这些函数的部署机制如下：

分别使用 `glfwInit()` 和 `glewInit()` 命令初始化 GLFW 和 GLEW 库。使用 `glfwCreateWindow()` 命令创建 GLFW 窗口以及关联的 OpenGL 上下文，并通过选项指定任何预定义的窗口。我们的窗口指定机器必须兼容 OpenGL 4.3 版本（"major=4" 和 "minor=3"）。`glfwCreateWindow` 命令上的参数指定了窗口的宽度和高度（以像素为单位）以及位于窗口顶部的标题。（另外两个参数设置为 `NULL`，我们没有使用它们，但它们允许全屏模式和资源共享。）通过使用 `glfwSwapInterval()` 和 `glfwSwapBuffers()` 命令启用垂直同步（VSync）——GLFW 窗口默认带有缓冲区。注意，GLFW 窗口不会自动将关联的 OpenGL 上下文设置为当前——因此，我们还调用了 `glfwMakeContextCurrent()`。

![](img/5f029c1d57776416a7d2524f3734d7cf_10_0.png)

图 2.3

程序 2.1 的输出。

`main()` 包含一个非常简单的渲染循环，重复调用我们的 `display()` 函数。它还调用了 `glfwSwapBuffers()` 和 `glfwPollEvents()`，后者处理其他与窗口相关的事件（例如按键）。当 GLFW 检测到应该关闭窗口的事件时（例如用户点击右上角的“X”），循环将终止。注意，我们在 `init()` 和 `display()` 调用中包含了一个对 GLFW 窗口对象的引用；这些函数在某些情况下需要访问它。我们还在调用 `display()` 时包含了当前上下文文，这对于确保我们的动画无论使用何种计算机都能以相同的速度运行非常有用。为了实现这一目的，我们使用了 `glfwTime()`，它返回自 GLFW 初始化以来的流逝时间。

- 1 “上下文（**context**）”指的是一个 OpenGL 实例及其状态信息，其中包含颜色缓冲区等项目。
- 2 “双缓冲（**Double buffering**）”意味着有两个颜色缓冲区——一个正在显示，另一个正在渲染。在渲染完整个帧后，两个缓冲区会进行交换。双缓冲被用于减少不理想的视觉伪影。

现在是时候仔细观察程序 2.1 中的 OpenGL 调用了。考虑下面这一个：

```
glClear(GL_COLOR_BUFFER_BIT);
```

在这种情况下，所调用的 OpenGL 函数如 OpenGL 参考文档（可在网站 `https://www.opengl.org/sdk/docs` 获取）描述所示：

```
glClear(GLbitfield mask);
```
