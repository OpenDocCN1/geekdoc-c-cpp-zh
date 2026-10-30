

## 2.1.2 项目结构

> 注意：启动 IDE 时，你可以选择 Eclipse 将创建新文件夹并查找现有项目文件的 workspace。你可以随时通过 IDE 主菜单选择 File | Switch Workspace 在 workspaces 之间切换。

在你的 workspace 中，你会看到一个名为 BuddyFix 的文件夹（或你为新项目选择的名称）。在其中你会看到一些子文件夹（见图 2.3）。如表 2.1 所总结的那样，文件夹结构如下：

- /inc 和 /src 文件夹是保存项目生成的 C++ 代码文件的位置；/inc 中的 .h 文件和 /src 中的 .cpp 文件。
- /Home 文件夹是应用读写任何数据文件或文件夹的文件系统根目录。
- /Icons 文件夹是你应该存储应用使用的图标的位置，也是向导复制默认应用图标的位置——当然，当你创建真正的项目时，你应该为自己的 artwork 更改它。
- /Res 文件夹是你的应用程序保存其使用的资源文件的位置。我们将在创建 BuddyFix UI 时看到资源的使用方式。

![](img/a257d5fd53a79a244a20e587cd2f08f6_46_0.png)

图 2.3 BuddyFix 文件夹和子文件夹。

这些是元数据文件，对你的项目至关重要。它们声明用于创建最终应用包的应用信息——应用名称和版本、厂商名称等——以及关于你的应用使用的 API 的关键信息和任何安全权限，即 bada 中称为 *privileges* 的权限，使用它们是必需的。权限是 bada 安全模型的一部分，我们将在第 4 章详细讨论它们。

当你开始一个真正的项目时，你需要使用通过 bada 开发者门户上的账户可用的工具创建清单的自定义版本（见第 2.7 节）。但起初我们完全不必担心这些细节；Application Wizard 生成的默认元数据文件足以开始使用。

**application.xml**  
*由应用打包工具用于创建可安装的包。声明应用名称、描述、厂商和版本；标识应用图标文件。*

**manifest.xml**  
*由认证过程用于权限检查。声明应用属性包括密钥和 ID；所需设备功能，例如 CPU 类型、最小堆大小、屏幕尺寸、使用的传感器；以及所需的权限。*

> **注意：** 如果你做过任何 widget 开发，那么 `application.xml` 会看起来很熟悉；它是定义 W3C 风格¹ widget 包的 `config.xml` 文件的等价物；如果你为 Android 开发过，`manifest.xml` 与 Android 清单文件的工作类似。

¹参见 www.w3.org.

## 2.1.4 构建和运行

虽然我们除了运行向导之外什么也没做，但我们已经有足够的代码来构建和启动我们应用的第一个骨架版本。

让我们验证代码是否可以构建。

在 IDE 中，通过 Project Explorer 按名称选择你的项目。从菜单栏选择 **Project | Build Project**，你的项目应该编译并链接（见图 2.4）。

![](img/a257d5fd53a79a244a20e587cd2f08f6_49_0.png)

图 2.4 构建项目。

当你的项目成功构建后，Project Explorer 中会显示一个 Binaries 文件夹，它映射到 Windows 文件系统中的 Simulator-Debug 目录，其中存储项目二进制文件和对象文件。

要启动你的应用，通过 Project Explorer 按名称选择你的项目。从菜单栏选择 Run | Run As | 1 bada Simulator Application 从弹出菜单中。

bada Simulator 将运行。我们在创建项目时选择了 Wave 作为手机型号，所以我们看到的是在 PC 屏幕上运行的 Wave 的良好近似。

Simulator 启动并初始化，短暂显示手机主屏幕，然后启动我们的应用（见图 2.5）。

> 注意：Application Wizard 将使用 Form Based Application 选项生成的任何应用的应用标题栏设置为“Hello bada！”，并在应用运行时以 OK 按钮启动。这有点令人困惑，因为不明显的是正在运行的是我们的应用。但请相信我们——确实是！

![](img/a257d5fd53a79a244a20e587cd2f08f6_50_0.png)

**图 2.5** 我们的应用在 Simulator 中运行。

要关闭应用，选择 Simulator 上手机的 **Power/End** 键。你的应用将关闭，你将被返回到主屏幕。选择 **Menu** 键进入 Application Manager。你将在图标菜单列表中看到你的应用，使用默认应用图标（见图 2.6）。

> **注意：** 当 BuddyFix 启动时，你可能注意到在应用程序显示之前短暂显示了一个启动画面，基于 `/Icons` 文件夹中的默认文件 `splash.png`。你可以通过更改此文件来更改显示的图像。启动画面是你的 bada 项目的可自定义属性——它以与设置应用图标相同的方式设置。
> 
> 顺便说一下，启动画面是为了填补应用启动时的任何延迟而显示的。延迟可能由于多种原因发生，具体取决于手机在任何时间点的负载。启动画面 *不是* 由应用本身显示以隐藏应用初始化时的延迟。而且，事实上，你应该设计你的应用以推迟可能导致显示其主屏幕时出现明显延迟的任何初始化。你可以通过使用多线程技术在后台执行此类初始化，或在应用启动后推迟此更深层次的初始化，或两者兼而有之来实现这一点。
> 
> 一个提示：为了通过认证过程，bada 应用必须拥有自己的启动画面和应用图标。

![](img/a257d5fd53a79a244a20e587cd2f08f6_51_0.png)

图 2.6 BuddyFix 显示在主菜单中。

## 2.1.5 标准输出

Eclipse IDE 中的一个有用视图是 Output 面板。当你在 Simulator 中启动应用时，系统会记录“Application started”消息，当你关闭应用时，系统会记录“Application finished”消息：

```
0010.200, INFO, P26, T-01, A-01, OspMain (24) > Application started.
0014.030, INFO, P26, T-01, A93, OspMain (39) > Application finished.
```

在这两个日志点之间，你可以使用 bada 的日志宏 AppLog()、AppLogDebug() 和 AppLogException() 输出类似 printf 的日志语句，以在运行时跟踪你的应用行为。例如，要输出一条简单的日志消息，添加以下行：

```
AppLog("This message will display in the output view");
```

日志文件可以导出为带有 .log 后缀的简单文本文件。在 Output 面板中，一旦你的应用程序正在运行，选择左侧的第二个图标（如图 2.7 所示）；将调用一个对话框，允许将输出保存到开发机器上的日志文件。

![](img/a257d5fd53a79a244a20e587cd2f08f6_52_0.png)

**图 2.7** bada IDE 的 Output 面板。

日志消息也由断言宏 AppAssert() 和 AppAssertIf() 写入，它们测试条件为真（或分别为假），以及我们将在第 4 章详细讨论的异常处理宏。

调试宏在 SDK Help 中有描述，在 IDE 中选择 Help | Help Contents | bada Developer Guide。

## 2.2 应用 UI

我们说过 bada 应用程序可以被认为是一个做某事的 GUI，其中 GUI 是你的应用向用户展示的公共面孔。在深入实际操作并向你展示如何构建简单的 GUI 之前，让我们先填补一些背景。

根据其复杂程度，一个应用程序可能只需要一个屏幕——例如计算器应用的简单计算器布局。或者它可能需要多个屏幕，例如地址簿应用，它可能会将主屏幕组织为姓名和地址条目的滚动列表，并提供一个详细信息屏幕来显示单个完整条目的详细信息，以及编辑屏幕以启用条目详细信息、标签等的编辑。

让你的 GUI 设计正确是作为应用开发者你将面临的最重要任务之一。关于良好 UI 设计的艺术有很多文章，关于良好移动 UI 设计的特殊情况也有很多文章。两个最突出的特征是：对细节的狂热关注和无情的简化。

同样重要的是，要理解你的应用 GUI 在平台外观和感觉的上下文中。记住 bada 的设计是将智能手机体验从高端推向中端。这影响了 bada 触摸 UI 的设计，进而应影响你的 GUI 设计。

2 Scott Jensen 的《The Simplicity Shift》（剑桥大学出版社，2002 年）是对工程主导设计习惯的极好纠正。Christian Lindholm 等人的《Mobile Usability: How Nokia Changed the Face of the Mobile Phone》（麦格劳-希尔，2003 年）提供了第一代和第二代移动电话 UI 演变的迷人案例研究。Barbara Ballard 的《Designing the Mobile User Experience》（Wiley，2007 年）是一本很好的概览文本。而没有 Bill Moggridge 的《Designing Interactions》（MIT Press，2007 年）的应用开发者是不完整的。网络上也有大量关于移动 UI 设计一般原则的资料，包括为你可能熟悉的其他移动平台发布的优秀文档，与所有移动应用开发相关，无论平台如何。

