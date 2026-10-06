
对整个 Qt 类范围内的细微改进进行了增强。Qt 4 的功能集现在已经非常广泛，使得 Qt 超越了 GUI 工具包的范畴，变成了一个完整的应用程序开发框架。Qt 4 也是第一个在其支持的所有平台上都提供商业化和开源开发开发的 Qt 版本。

同样在 2005 年，Trolltech 在北京设立了代表处，为中国及该地区的客户提供 Qt/Embedded Linux 和 Qtopia 的销售服务、培训和技术支持。

长期以来，通过非官方的语言绑定，非 C++ 程序员一直可以使用 Qt，特别是针对 Python 程序员的 PyQt。2007 年，为 C# 程序员发布了京都非官方绑定。同样在 2007 年，Trolltech 推出了 Qt Jambi，这是一个官方支持的 Java 版本 Qt API。附录 C 提供了对 Qt Jambi 的介绍。

自 Trolltech 诞生以来，Qt 的人气增长不减，并一直持续今天。这种成功既反映了 Qt 的质量，也反映了它的易用性。在过去的十年里，Qt 已从极少数“圈内人士”使用的产品转变为全球数千名客户和数万名开源开发者每天使用的工具。

## 第一部分：Qt基础

## 1. 入门

![](img/5a524abdf0b0d58fa99d30abb4463611_19_0.png)

- Hello Qt
- 建立连接
- 布局部件
- 使用参考文档

本章展示了如何将基础 C++ 与 Qt 提供的功能相结合，创建几个图形用户界面（GUI）应用程序。本章介绍了两个核心概念：“信号与槽”（signals and slots）和布局。在第 2 章中，我们将进行深入探讨，在第 3 章中，我们将开始构建一个更真实的应用程序。

如果你已经熟悉 Java 或 C# 但对 C++ 经验有限，可能想从阅读附录 D 中的 C++ 介绍开始。

## Hello Qt

让我们从一个简单的 Qt 程序开始。我们将首先逐行研究它，然后查看如何编译和运行它。

```cpp
#include <QApplication>
#include <QLabel>

int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    QLabel *label = new QLabel("Hello Qt!");
    label->show();
    return app.exec();
}
```

1 和 2 包含了 `QApplication` 和 `QLabel` 类的定义。类名与包含它的类相同（大小写相同）。

5 创建了一个 `QApplication` 对象来管理应用程序级的资源。`QApplication` 构造函数需要 argc argv，因为 Qt 支持一些自己的命令行参数。

6 创建了一个显示“Hello Qt!”的 `QLabel` 部件。在 Qt 和 Unix 术语中，widget 是用户界面中的视觉元素。该词源于“window gadget”，等同于 Windows 术语中的“控件”（control）和“容器”（container）。按钮、菜单、滚动条和其他部件都是部件的示例；例如，应用程序窗口通常是一个包含 `QMenuBar`、几个 `ToolBar`、一个 `StatusBar` 以及其他部件的部件。大多数应用程序使用 `QWidget` 或 `QDialog` 作为应用程序窗口，但 Qt 非常灵活，任何部件都可以窗口。在本例中，`QLabel` 部件就是应用程序窗口。

7 使标签可见。部件总是隐藏创建的，以便我们可以在显示它们之前对其进行自定义，从而避免闪烁。

8 将应用程序的控制权交给 Qt。此时，程序进入事件循环。这是一种待机模式，程序等待用户操作（如鼠标点击和按键）。用户操作会产生事件（也称为“消息”），程序可以通过执行一个或多个函数来响应这些事件。例如，当用户点击一个部件时，会产生一个“鼠标按下”和一个“鼠标释放”事件。在这方面，GUI 与传统的批处理程序有很大区别，后者通常处理输入、产生结果并在没有人工干预的情况下终止。

为了简单起见，我们没有特意在 `main()` 函数结束时调用 `delete QLabel`。在这种小型程序中，这种内存泄漏是无害的，因为内会在程序终止时由操作系统回收。

现在可以在你自己的机器上尝试运行该程序了。它看起来应该像图 1.1 所示。首先，你需要安装 Qt 4.3.2（或更新的 Qt 4 版本），目前我们假设你已经正确安装了 Qt 4，并且其 `bin` 目录已你的 `PATH` 环境变量中。（在 Windows 上，这由安装程序自动完成。）你还需要将程序代码保存到名为 `hello.cpp` 的文件中。你可以手动输入 `hello.cpp`，也可以从随书附带的示例复制，路径为 `examples/chap01/hello/hello.cpp`。（所有示例均可在书籍网站获取：http://www.informit.com/title/013235410）。

## 图 1.1 Linux 上的 Hello

从命令行提示符开始，切换到 hello 目录并输入：

```
qmake -project
```

创建一个平台无关的项目文件（hello.pro），然后输入：

```
qmake hello.pro
```

从项目文件创建特定平台的 Makefile。（qmake 工具在附录 B 中有详细介绍。）输入 `make` 构建程序。在 Windows 上输入 `hello` 运行，在 Unix 上输入 `../hello`，在 Mac OS 上打开 `hello.app`。要终止程序，点击窗口标题栏上的关闭按钮。

如果你使用 Windows 并安装了 Qt 开源版和 MinGW 编译器，你有一个 MS-DOS Prompt 窗口快捷方式，其中已为 Qt 正确设置了环境变量。如果你启动此窗口，可以使用上述方法通过 qmake 和 make 在其中编译 Qt 应用程序。可执行文件产生在应用程序的调试/发布文件夹中（例如：C:\examples\chap01\hello\release\hello.exe）。

如果你在带有商业版 Windows 上使用 Microsoft Visual C++，你需要使用 `nmake` 和 `make`。或者，你可以通过输入命令从 hello.pro 创建 Visual Studio 项目文件：

```
qmake -tp vc hello.pro
```

然后在 Visual Studio 中构建程序。如果你在 Mac OS 上使用 Xcode，可以使用以下命令生成 Xcode 项目：

```
qmake -spec macx-xcode hello.pro
```

在进入下一个示例之前，让我们玩点有趣的：替换这一行：

```cpp
QLabel *label = new QLabel("Hello Qt!");
```
