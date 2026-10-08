
# 第 12 章 可扩展性

![](img/170b148e5ba8f4b05aa8234f929ebba6_357_0.png)

**图 12.1**
**API 插件**

插件库是一个动态库，它可以与核心 API 独立进行编译，并由 API 按需显式加载。

## 12.1.1 插件模型概述

许多商业软件包示例允许通过使用 C/C++ 插件来扩展其核心功能。例如，Apache Web 服务器支持基于 C 的“模块”，Adobe Photoshop 支持多种插件类型来处理图像，而 Firefly、Chrome 和 Opera 等浏览器支持 Netscape 插件 API (`NPAPI`)，用于创建如 Adobe Flash 或 PDF 阅读器之类的浏览器插件。Qt 工具包也可以通过 `PluginLoader` 类进行扩展（服务端插件 API 有时被称为 Apache 模块接口，称为服务端 API，或 SAPLI）。

在你的 API 中采用插件模型的优点之处如下：

- **更强的通用性。** 你的 API 可以用于解决更广泛的问题，而无需你为所有这些问题都实现解决方案。
- **社区催化剂。** 通过赋予用户在你的 API 框架内解决问题的能力，你可以激发一个由用户为你的基础设计贡献扩展的社区。
- **更小的更新。** 作为插件的功能可以通过放入新版本的插件来独立于应用程序进行易于的更新。这通常比分发整个应用程序的新版本要小得多。
- **面向未来。** 你的 API 可能会达到一个稳定性水平，让你认为不再需要进一步更新。然而，你的 API 功能的进一步进化可以通过开发插件来继续，允许 API 在更长的时间内保持有用性和相关性。例如，`NPAPI` 在近年来已经衰落，但它仍然是许多 Web浏览器编写插件的流行方法。
- **隔离风险。** 插件对内部开发有益，可以让工程师在不破坏系统核心部分稳定性的情况下更改功能。

正如刚才所暗示的，插件系统并不一定仅供你的客户端使用。你也可以将核心 API 实现的部分开发为插件。事实上，这实际上是一种良好的做法，因为它确保了你完全执行了你的插件架构，并且与用户处于同一个世界中（“吃自己的狗粮”）。例如，GNU 图像处理程序 (`GIMP`) 使用其 GIMP Plugin API 将许多内置图像处理函数作为插件发布。

## NETSCAPE 插件

Netscape 插件 API (`NPAPI`) 提供了一个跨平台 API，用于在各种 Web 浏览器中嵌入自定义功能。该接口源于 Adobe Systems 为了将 PDF 查看器集成到早期 Netscape 浏览器中的工作。这种 C 插件 API 至今仍用于在浏览器（如 Mozilla Firefox、Apple Safari 和 Google Chrome）中嵌入原生扩展。例如，Shockwave Flash、Apple QuickTime、Microsoft Silverlight 都是作为插件实现的（尝试在 Firefox 中输入 `"about:plugins"` 来查看已安装插件列表）。

`NPAPI` 在 Web 浏览器内部提供了以下能力：

- 注册 MIME 类型
- 在浏览器窗口的区域内绘制。
- 接收鼠标和键盘事件。
- 通过 HTTP 发送和接收数据。
- 添加链接到新 URL 的超链接或热点。
- 与文档对象模型 (`DOM`) 通信。

20世纪90年代当我在 SRI International 时，我们开发了一个名为 TerraVision 的基于 Web 的3D 地形可视化系统（Leclerc and Lau, 1994）。它最初是一个桌面应用程序，需要 SSI RealityEngine 处理器；然而，随着通用图形硬件的发展，我们最终能够让在标准 PC 的 Netscape Navigator 和 Microsoft Explorer 中作为“地球项目”运行。

![](img/170b148e5ba8f4b05aa8234f929ebba6_358_0.png)

由于 TerraVision 是一个多线程应用程序，为了在非线程安全的环境中运行它，我们必须在单独的进程中运行。然而，我们的 Netscape 插件会为 TerraVision 创建一个新的运行进程，并传递一个用于绘图的窗口句柄。插件与 TerraVision 进程之间的所有通信通过管道 I/O 处理。

## 12.1.2 插件系统设计问题

设计插件系统有许多方法。你当前项目的最佳解决方案可能不是下一个项目的最佳选择。因此，我将首先尝试梳理出你在设计插件系统时应该注意的一些高级问题。

同时，还有许多适用于所有插件系统的通用概念。例如，在支持动态插件库时，你总是需要一种加载动态库并访问该文件中符号的机制。通常，在创建任何插件系统时，你必须设计两个主要特性（见图 12.2）。

![](img/170b148e5ba8f4b05aa8234f929ebba6_359_0.png)

**图 12.2**
**插件管理器存在于核心 API 中。它发现并加载基于插件 API 构建的插件。**

- **插件 API**：这是你的用户在创建插件时必须编译并与之链接的 API。我将它与你的核心 API 区分开来，核心 API 是你添加插件系统的较大代码库。
- **插件管理器 (`Plugin Manager`)**：这是发现并加载基于插件 API 构建的插件的组件。

有了这些通用概念，让我们来看看影响你 API 的决策。

- **版本控制。** 你可能希望处理不同版本的插件。确定什么构成了不兼容的 API 是困难的，这通常留给插件作者。例如，你可以指定一个版本范围。
- **内部外部元数据。** 元数据（如人类可读的名称和版本信息）可以定义在插件代码中，也可以定义在外部文件中。使用外部文件的优点是，你实际上不需要加载所有插件就可以知道可用集合。
- **通用专用型插件管理器。** 实现插件管理器的一种方法是使其非常底层且通用的，也就是说，它加载插件并访问符号。然而，这样做意味着插件管理器不知道你 API 中具体类型的存在。结果是，它可能会将对象返回为 `void*`，你必须将这些类型强制转换为具体类型。
- **安全性。** 你必须决定如何信任用户插件。插件是任意编译的代码，允许它们在你的进程中运行。插件在理论上可以做任何事情，从访问它不应该访问的数据、删除用户硬盘上的文件，到导致整个应用程序崩溃。
- **静态/动态库。** 正如以前所述，将插件定义为静态库是可能的，这意味着它们必须被编译到应用程序中。应用程序更常用的解决方案是动态库。编写静态插件的限制是，你必须确保没有两个插件定义相同的符号，也就是说，每个插件的初始化函数必须是唯一的，例如 `<PluginName>_PluginInit()`。在动态库的情况下，你可以为每个插件使用相同的初始化函数名称，例如 `PluginInit()`。

## 12.1.3 在 C++ 中实现插件

我已经发现支持 C++ 插件可能会困难，因为存在跨平台和跨编译器的 ABI 问题。然而，由于这是一本关于 C++ API 设计的书籍，让我们花些时间介绍一些让你能够稳健（robustly）使用 C++ 插件的解决方案。

首先，如果你要求插件开发者使用与你构建 API 时相同的编译器版本，那么你就不需要担心任何问题。

如果情况并非如此，一种解决方案是为插件使用绑定技术，例如在 Windows 上使用 COM 等 IPC 解决方案，或者为你的 API 创建绑定，并让用户使用 Python 或 Ruby 等跨平台脚本语言编写扩展（这在前章中介绍过）。

如果你为了获得最高性能而绝对需要使用 C++ 插件，或者你觉得创建 COM 或绑定对于你的需求来说过于沉重，你仍然有方法可以在插件中更安全地使用 C++。以下列表提供了最佳实践，其中许多已在位于 `http://www.codeproject.com` 上的开源 DynObj 库中实现。

- *使用抽象类。* 实现抽象基类的方法可以使插件免受 ABI 问题的影响，因为虚方法调用通常表示为类虚函数表（vtable）中的索引。虚表格式在不同编译器之间可能不同，但在实践中这种情况通常不会发生。（不过注意，不同的编译器对虚方法的排序可能不同，因此最好避免这些。）接口中的所有方法都需要是纯虚的，尽管方法也可以足够安全地使用，使得代码将直接嵌入插件中。
- *对自由函数使用链接（linkage）。* 你的插件 API 中的所有全局函数都应使用 C 链接以避免 C++ ABI 问题，即它们应该用 `extern "C"` 声明。同样，插件传递给核心 API 的函数回调也应该使用 C 链接以获得最大的可移植性。
- *避免 STL 和异常。* STL 类（如 `std::string` 和 `std::vector`）的不同实现之间可能不具有 ABI 兼容性。最好在核心 API 和插件 API 之间的任何函数调用中都避免这些容器。同样，由于异常的 ABI 在不同编译器之间是不稳定的，这些应该在你的插件 API 中被避免。
- *不要混合分配器。* 可能会链接到与你的 API 不同的内存分配器。例如，在 Windows 上，调试构建（debug builds）通常比发布构建（release builds）使用不同的分配器。这对你的插件系统设计的影响是：插件必须分配并释放它的所有对象，或者插件应该将控制权交给核心 API 来创建和销毁所有对象。然而，你的核心 API 应该返回由插件分配的释放，反之亦然。

将所有这些信息整合在一起，我现在将开发一个灵活且稳健的跨平台 C++ 插件系统。插件系统将使用新的 C++ 类，通过提供一个或多个工厂方法来向核心 API 注册。我们继续第 3 章中的可扩展示例并对其进行增强。

### 12.1.4 API

插件系统将使用新的 C++ 类，通过提供一个或多个工厂方法向核心 API 注册。我们继续第 3 章中的可扩展示例并对其进行增强。

插件 API 是你提供的供核心 API 调用的接口。核心 API 会加载 `pluginapi.h`。这些定义让我们在 Windows 下指定正确的导出/导入装饰符。`CORE_API` 用于装饰属于核心 API 的函数，`PLUGIN_API` 用于装饰插件中定义的函数。这些宏的定义记录在 `defines.h` 头文件中，看起来如下：

```cpp
// defines.h

#ifdef _WIN32

#ifdef BUILDING_CORE

#define CORE_API __declspec(dllexport)

#define PLUGIN_API __declspec(dllimport)

#else

#define CORE_API __declspec(dllimport)

#define PLUGIN_API __declspec(dllimport)

#endif

#else

#define CORE_API

#define PLUGIN_API

#endif
```

注意，在构建核心 API 时必须设置 `BUILDING_CORE` 定义，这些宏才能正常工作，例如在 Windows 编译命令行中添加 `/BUILDING_CORE`。在编译插件时不需要此定义。

头文件提供了插件的初始化和清理函数：`PLUGIN_INIT()` 和 `PLUGIN_FREE()`。我还提供了 `PLUGIN_FUNC()` 宏来让核心 API 调用。最后，我提供了一个函数 `RegisterRenderer()`，允许插件向核心 API 注册新的 `IRenderer` 类。

这是插件 API 的草稿：

```cpp
// pluginapi.h

#include "defines.h"

#include "renderer.h"

#define CORE_FUNC extern "C" CORE_API

#define PLUG_FUNC extern "C" PLUGIN_API

#define PLUG_INIT() PLUG_FUNC void pluginInit()

#define PLUG_FREE() PLUG_FUNC void pluginFree(IRenderer*)

CORE_FUNC void RegisterRenderer(const char *type,
    RendererInitFunc init_cb,
    RendererFreeFunc free_cb);
```

## 12.1 通过插件扩展 369

```cpp
virtual void SetLookAt(double x, double y, double z) = 0;
virtual void Render() = 0;
```

这与第 3 章中提供的定义基本相同，只是我将 `LoadScene()` 方法更改为接受 `const char*` 参数而不是 `std::string`（为了解决我对比不同编译器之间 STL 类二进制兼容性的顾虑）。

## 12.1.5 示例插件

现在我已经开发了一个初级的的插件 API，让我们来看一下基于此 API 构建的插件可能是什么样的。你需要包含的基础部分有：

- 1. 新的 `IRenderer` 类。
- 2. 用于创建和销毁该类的回调函数。
- 3. 一个插件初始化程序，用于向 Core API 注册我们的创建/销毁回调。

以下是此类插件的代码。该插件使用 `"opengl"` 定义并注册了一个新的渲染器。它定义在一个新的 `OpenGLRenderer` 类中，该类派生自 `IRenderer` 抽象基类。

```cpp
// plugin.cpp

#include "pluginapi.h"

#include <iostream>

class OpenGLRenderer : public IRenderer {

public:

    ~OpenGLRenderer() {}

    bool LoadScene(const char* filename) { return true; }

    void SetViewport(int w, int h) {}

    void SetCameraPosition(double x, double y, double z) {}

    void SetLookAt(double x, double y, double z) {}

    void Render() { std::cout << "OpenGL Render" << std::endl; }

};

PLUGIN_FUNC IRenderer *CreateRenderer() {

    return new OpenGLRenderer();

}

PLUGIN_FUNC void DestroyRenderer(IRenderer *r) {

    delete r;

}

PLUGIN_INIT() {

    RegisterRenderer("opengl", CreateRenderer, DestroyRenderer);

    return 0;

}
```
