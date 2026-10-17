
# 特别章节：构建你自己的虚拟机 421 计算机

从 00 开始顺序执行，除非通过控制转移跳转到程序的其他部分。

使用变量 `accumulator` 来表示累加器寄存器。使用变量 `instructionCounter` 来存储正在执行指令的内存地址数（0 到 99）。使用变量 `operationCode` 来存储当前正在执行的操作（指令字为两位数字）。使用变量 `operand` 来存储指令所操作的内存地址数。因此，如果一条指令是一个操作数，它就是当前正在执行指令的右侧两个数字。不要直接从内存中执行指令。相反，将下一个要执行的指令从内存传输到名为 `instructionRegister` 的变量中。然后“提取”左边的两个数字并“提取”右边的两个数字，将其放入变量 `operationCode` 中。

当 Simpleton 开始时，特殊寄存器的初始化如下：

```
accumulator          +0000
instructionCounter   00
instructionRegister  +0000
operationCode        00
operand              00
```

现在让我们“走一遍”第一条 SML 指令的执行过程，位于内存地址 00 的 +1009。这个过程被称为指令执行周期。

`instructionCounter` 告诉我们下一个要执行指令的位置。我们使用 C 语句 `instructionRegister = memory[instructionCounter];` 从内存获取该地址的内容。

通过以下语句从指令寄存器中提取操作码和操作数：

```
operationCode = instructionRegister / 100;
operand = instructionRegister % 100;
```

现在 Simpleton 必须确定该操作实际上是读（写入值、加载和加法）。使用 `switch` 语句区分 SML 的十二种操作。`switch` 模拟了各种 SML 指令的行为如下（我们将其余部分留给读者）：

```
read:     scanf("%d",&memory[operand]);
load:     accumulator = memory[operand];
add:      accumulator += memory[operand];
```

各种指令：我们稍后会讨论。

此指令打印消息：

*** Simpleton execution terminated ***

然后打印所有 100 个内存位置中每个寄存器的名称和内容。这种打印输出通常被称为计算机“内存转储”（computer dump）。为了帮助你编写 `dump` 函数，下面的输出显示了一个示例转储：

```
REGISTERS:
accumulator +0000
instructionCounter 00
instructionRegister +0000
operationCode 00
operand 04
```

```
MEMORY:
| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 0 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 |
| 10 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 |
| 20 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 |
| 30 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 |
| 40 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 |
| 50 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 |
| 60 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 |
| 70 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 |
| 80 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 |
| 90 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 | +0000 |
```

执行程序后的转储将显示执行结束时时指令和数据的实际值。

## 特别章节：构建你自己的虚拟机

条件跳转“如果累加器为零”指令模拟如下：

```
if (accumulator == 0) {
    instructionCounter = operand;
}
```

# 使用 Webots 仿真器进行机器人开发

为这些机器人开发控制器软件。Webots 使用 Apache 开源许可证。以下来自其许可证网页页的内容：

> “Webots 根据 Apache 2.0 协议的条款发布。Apache 2.0 是一种 [sic] 对行业友好、无污染、许可性的开源许可证，它允许任何人免费地出于任何目的（包括商业应用）使用软件代码。”

Webots 首次于 1996 年在瑞士联邦洛理工学院（EPFL）开发。1998 年，从 EPFL 离出来的派生公司 Cyberbots 成立，接管了 Webots 仿真器的开发。直到 2018 年，Webots 一直以专有许可软件的形式出售。Cyberbots 在 Apache 2.0 许可证下将 Webots 开源。这在入门级编程书中通常不会被讨论，但 Webots 让它变得简单。Webots 附带了数十种当今最流行的真实世界机器人的仿真，这些机器人可以行走、飞行、滚动、行驶和移动。有关当前的附带机器人列表，请参阅：

https://cyberbotics.com/doc/guide/robots

# 自包含开发环境

Webots 是一个自包含的机器人仿真环境，包含了你开始机器人开发和实验所需的所有内容。它包括：

- 一个交互式 3D 仿真区域，用于查看和与仿真交互，
- 一个代码编辑器，你可以在其中查看仿真代码、修改它并编写自己的代码，
- 编译器和解释器，允许你使用 C、C++、Java、Python 和 MATLAB 编写 Webots 代码，

你可以轻松地修改现有的仿真并重新运行它们以查看更改的效果。你也可以开发全新的仿真，就像你在本案例中做的那样。

# 安装 Webots

首先，在以下处检查 Webots 系统要求：

https://cyberbotics.com/doc/guide/system-requirements

你可以从 Cyberbot 官网下载 Windows、macOS 或 Linux 的 Webots 安装程序：

https://cyberbotics.com/

7. “Webots 用户指南 R2020b 版本 2—许可证协议。”访问于 2020 年 12 月 14 日。https://cyberbotics.com/doc/guide/webots-license-agreement。

8. “Cyberbot。”访问于 2020 年 12 月 13 日。https://cyberbotics.com/#cyberbotics。

9. “Webots。”访问于 2020 年 12 月 13 日。https://en.wikipedia.org/wiki/Webots。

# 引导导览

安装完成后，在你的系统上运行 Webets 应用程序。你可以在 Webets 引导导览中快速浏览许多附带的机器人仿真和机器人的能力。要这样做，选择 Help > Webets Guided Tour...（当你第一次打开 Webets 环境时，此引导导览将自动开始）。然后，在出现的窗口（图 7.19）中，勾选 Auto 复选框并点击 Next。这将开始向你展示每个演示的短时间，然后切换到下一个。Guided Tour - Webets 窗口显示每个仿真的简要描述。图 7.19 显示了第三个仿真的描述，该仿真出现在图 7.20 中。

![](img/3f09be2f99b7b6bd5428b767d0b2bfa1_426_0.png)

图 7.19 如图 7.20 所示 ROBOTIS OP3 机器人的简要描述 [本例中的截图版权归 2020 Cybernetics Ltd. 所有，根据 Apache 许可证 2.0 版（“许可证”）获得许可；除非符合许可证，否则你不得使用此文件。你可以在 http://www.apache.org/licenses/LICENSE-2.0 获取许可证副本]

当引导导览概述每个仿真时，你将在 Webots 环境中实时看到它。

# 使用 Webots 仿真器进行机器人开发

为这些机器人开发控制器软件。Webots 使用 Apache 开源许可证。以下来自其许可证网页的内容：

> “Webots 根据 Apache 2.0 协议的条款发布。Apache 2.0 是一种 [sic] 对行业友好、无污染、许可性的开源许可证，它允许任何人免费地出于任何目的（包括商业应用）使用软件代码。”

Webots 首次于 1996 年在瑞士联邦洛理工学院（EPFL）开发。1998 年，从 EPFL 离出来的派生公司 Cyberbots 成立，接管了 Webots 仿真器的开发。直到 2018 年，Webots 一直以专有许可软件的形式出售。Cyberbots 在 Apache 2.0 许可证下将 Webots 开源。这在入门级编程书中通常不会被讨论，但 Webots 让它变得简单。Webots 附带了数十种当今最流行的真实世界机器人的仿真，这些机器人可以行走、飞行、滚动、行驶和移动。有关当前的附带机器人列表，请参阅：

https://cyberbotics.com/doc/guide/robots

# 自包含开发环境

Webots 是一个自包含的机器人仿真环境，包含了你开始机器人开发和实验所需的所有内容。它包括：

- 一个交互式 3D 仿真区域，用于查看和与仿真交互，
- 一个代码编辑器，你可以在其中查看仿真代码、修改它并编写自己的代码，
- 编译器和解释器，允许你使用 C、C++、Java、Python 和 MATLAB 编写 Webots 代码，

你可以轻松地修改现有的仿真并重新运行它们以查看更改的效果。你也可以开发全新的仿真，就像你在本案例中做的那样。

# 安装 Webots

首先，在以下处检查 Webots 系统要求：

https://cyberbotics.com/doc/guide/system-requirements

你可以从 Cyberbot 官网下载 Windows、macOS 或 Linux 的 Webots 安装程序：

https://cyberbotics.com/

7. “Webots 用户指南 R2020b 版本 2—许可证协议。”访问于 2020 年 12 月 14 日。https://cyberbotics.com/doc/guide/webots-license-agreement。

8. “Cyberbot。”访问于 2020 年 12 月 13 日。https://cyberbotics.com/#cyberbotics。

9. “Webots。”访问于 2020 年 12 月 13 日。https://en.wikipedia.org/wiki/Webots。

# 引导导览

安装完成后，在你的系统上运行 Webets 应用程序。你可以在 Webets 引导导览中快速浏览许多附带的机器人仿真和机器人的能力。要这样做，选择 Help > Webets Guided Tour...（当你第一次打开 Webets 环境时，此引导导览将自动开始）。

然后，在出现的窗口（图 7.19）中，勾选 Auto 复选框并点击 Next。这将开始向你展示每个演示的短时间，然后切换到下一个。Guided Tour - Webets 窗口显示每个仿真的简要描述。图 7.19 显示了第三个仿真的描述，该仿真出现在图 7.20 中。

![](img/3f09be2f99b7b6bd5428b767d0b2bfa1_426_0.png)

图 7.19 如图 7.20 所示 ROBOTIS OP3 机器人的简要描述 [本例中的截图版权归 2020 Cybernetics Ltd. 所有，根据 Apache 许可证 2.0 版（“许可证”）获得许可；除非符合许可证，否则你不得使用此文件。你可以在 http://www.apache.org/licenses/LICENSE-2.0 获取许可证副本]

当引导导览概述每个仿真时，你将在 Webots 环境中实时看到它。

# 第 1 步：启动 Websots

在第 1 步中，只需打开 Websots 环境。你将执行下方讨论的后续步骤。

# 第 2 步：创建虚拟世界

世界定义了仿真环境并存储在 `.wbt` 文件中。该文件在内部使用虚拟现实建模语言 `VRML` 来描述世界的元素。每个世界都可以具有某些特性，例如重力，这些特性会影响物体之间的交互。世界指定了机器人可以漫游的区域以及它与之交互的对象。向导菜单中的“创建 Websots 项目目录”向导（图 7.21–7.24）将引导你按照 Websots 要求的文件夹结构设置新世界。

在“创建 Websots 项目目录”向导屏幕（图 7.21）中，只需点击“继续”（Continue）或“下一步”（Next）即可进入下一步。

![](img/3f09be2f99b7b6bd5428b767d0b2bfa1_429_0.png)

图 7.21 创建 Websots 项目目录向导的初始界面。

在向导的“目录选择”步骤（图 7.22）中，将项目的目录名称从 `my_project`（默认）更改为 `my_first_simulation`——此文件夹的默认位置是你用户账户的 Documents 文件夹¹³

在向导的“设置”步骤（图 7.23）中，你将世界文件名从 `empty.wbt`（默认）更改为 `my_first_simulation.wbt`，并确保勾选了四个复选框。这将为你的虚拟世界添加几个 Websots 预定义组件。

向导的“结论”步骤（图 7.24）显示了向导将为你的仿真生成的文件夹和文件。在随后的步骤中，你将添加障碍物机器人，配置各种设置并编写一些控制机器人的 C 代码。

> ¹³. 你可以更改 Websots 项目的存储位置。我们存储在用户账户的 `/Users/paul1/Documents` 文件夹中，你会在几张截图中看到它。

![](img/3f09be2f99b7b6bd5428b767d0b2bfa1_430_0.png)

**图 7.22** 将默认项目目录名称更改为 my_first_simulation。

![](img/3f09be2f99b7b6bd5428b767d0b2bfa1_430_1.png)

**图 7.23** 更改默认文件名并确保勾选了所有复选框。

![](img/3f09be2f99b7b6bd5428b767d0b2bfa1_430_2.png)

**图 7.24** 向导将为你的仿真生成的文件夹和文件摘要。

当你在“创建 Websots 项目目录”向导（图 7.24）中点击 Done（macOS）或 Finish（Windows 和 Linux）时，Websots 3D 视图区域将显示一个带有棋盘地板的空 `RectangleArena`——这是 RectangleArena 的默认设置（图 7.25）。有几种地板样式可可选。你可以在学习如何更改世界中元素的设置后，对这些选项进行实验。在 3D 视图区域中，使用鼠标轮进行缩放，你可以点击并拖动 `RectangleArena` 从不同角度查看并旋转它。

![](img/3f09be2f99b7b6bd5428b767d0b2bfa1_431_0.png)

**图 7.25** 完成“创建 Websots 项目目录”向导后 RectangleArena 的初始视图。

# 第 3 步：修改 RectangleArena

仿真中的每个元素都是世界场景树中的一个节点，你可以在 Websots 环境的左侧看到它。在此步骤中，你将选择场景树中的一个节点，然后更改它的一个设置（字段）。执行此步骤后，环境应该如图 7.26 所示。

RectangleArena 之上的彩色箭头出现在你通过点击物体或点击场景树中看到的任何物体上。你可以拖动这些箭头来移动、旋转和倾斜物体¹⁴ 拖动箭头沿轴移动物体。拖动圆形箭头绕轴旋转物体。保存环境，然后尝试这些箭头，观察它们如何影响 RectangleArena 的位置。你可以重置环境以恢复原始位置。

+ 14. “Webots User Guide R2020b revision 2 — The 3D Window — Moving a Solid.” 2020年12月13日。https://cyberbotics.com/doc/guide/the-3d-window/moving-a-solid.

![](img/3f09be2f99b7b6bd5428b767d0b2bfa1_432_0.png)

**图 7.26** 修改棋盘图案尺寸和高度后的 RectangleArena。

# 第 4 步：添加 WoodenBox 障碍物

Websots 环境带有近800个预定义的物体和机器人——称为 `PROTO` 节点。`PROTO` 节点描述了你可以添加到仿真中的复杂物体或机器人。丰富的 `PROTO` 节点允许你创建真实世界的 3D 仿真。
