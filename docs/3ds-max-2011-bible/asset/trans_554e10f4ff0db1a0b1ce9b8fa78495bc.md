

事实上，你已经在不知不觉中使用了 MAXScript。一些按钮和 rollout 使用了 MAXScript 的片段来执行你的命令。而且在你使用 MAXScript 创建了一个新功能后，你可以将其透明地集成到 Max 中，并像使用任何其他 Max 功能一样轻松地使用它。

MAXScript 是一种功能齐全且非常强大的计算机语言，但你不必是计算机程序员，甚至不需要任何之前的编程经验就能从 MAXScript 中受益。在接下来的几个部分中，你将看到使用 MAXScript 的一些简单方法。现在，就把 Max 中的脚本想象成电影或戏剧中的脚本——它告诉将会发生什么，谁来做什么，以及何时发生。以你的场景作为舞台，脚本指导 Max 为你表演。

在你深入之前最后一点说明：MAXScript 如此强大，以至于可以写一整本书来介绍它以及它支持的每一个特性，但这不是这里的目的。本章的组织方式旨在让你入门 MAXScript 的世界，并教授你需要的基本技能，以便从中获得一些收益。这里提供的内容是一个基础，你可以根据自己的兴趣和需求在此基础上构建。

## MAXScript 工具

MAXScript 无处不在，可以在许多不同的地方找到。本节介绍 MAXScript 工具以及不同脚本是如何创建和使用的。

让我们看看在处理 MAXScript 时使用的一些工具。Max 有几个工具，可以使创建和使用脚本尽可能简单。

## MAXScript 菜单

MAXScript 菜单包括你可以用来创建新脚本、打开和运行脚本、打开 MAXScript Listener 窗口（键盘快捷键，F11）或 MAXScript Editor 窗口、启用 Macro Recorder、打开 Visual MAXScript Editor，或访问 Debugger 对话框的命令。

New Script 命令打开一个 MAXScript Editor 窗口，这是一个用于编写 MAXScript 的文本编辑器。有关此编辑器窗口的更多信息，请参阅本章后面的“MAXScript Editor 窗口”部分。Open Script 命令打开一个文件对话框，你可以用它来定位 MAXScript 文件。打开后，脚本文件会在 MAXScript Editor 窗口中打开，如图 49.1 所示。MAXScript 文件具有 .ms 或 .mrc 扩展名。Run Script 命令也会打开一个文件对话框，你可以在其中选择要执行的脚本。

### Note

当你使用 Run Script 时，一些脚本会立即执行，而其他脚本则会作为新工具安装。

MAXScript Listener 命令打开 MAXScript Listener 窗口。你也可以通过按 F11 键盘快捷键打开此窗口。Macro Recorder 命令开始记录 MAXScript 宏。MAXScript Listener 和记录宏将在本章后面介绍。

## MAXScript Utility rollout

你可以通过在 Command Panel 中打开 Utilities 面板并单击 MAXScript 按钮来访问 MAXScript Utility rollout，如图 49.2 所示。这会打开一个 rollout，你可以在其中执行与 MAXScript 菜单相同的许多命令。

MAXScript rollout 还包括一个 Utilities 下拉列表，其中包含任何已安装的脚本化实用程序。每个脚本化实用程序都作为一个新功能供你使用。这些实用程序的参数会显示在 MAXScript rollout 下方出现的新 rollout 中。

## FIGURE 49.1

MAXScript 使用标准语法在简单的文本编辑器窗口中编写。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1224_0.png)

## FIGURE 49.2

Utilities 面板上的 MAXScript rollout 是开始使用 MAXScript 的绝佳位置。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1224_1.png)

## Tutorial: Using the SphereArray script

这是一个让你玩一玩并在过程中获得 MAXScript 经验的机会。在 DVD 的 Chap 49 目录中有一个名为 SphereArray.ms 的简单脚本。它类似于 Tools 菜单中的 Array 命令，只是 SphereArray 创建对象的副本并以球形图案随机放置它们。

要加载和使用 SphereArray 脚本，请按照以下步骤操作：

- 1. 选择 Create↳ Standard Primitives↳ Box，并在 Top 视口中拖动以创建一个长度为 10，宽度和高度值均为 1.0 的 Box 对象。
- 2. 选择该 box 对象，在 Command Panel 中打开 Utilities 面板（图标是一个锤子），并单击 MAXScript 按钮。
- MAXScript rollout 出现。
- 3. 在 MAXScript rollout 中单击 Run Script 按钮以打开 Choose Editor file 对话框，从 DVD 上的 Chap 49 目录中找到 SphereArray.ms 文件，然后单击 Open。
- SphereArray 实用程序安装并出现在 Utilities 下拉列表中。（因为 SphereArray 是一个脚本化实用程序，运行它只会安装它。）
- 4. 从 Utilities 下拉列表中选择 SphereArray。确保 box 对象已选中。
- 5. 在 Sphere Array rollout 中，在 Object Count 字段中输入 50，在 Radius 字段中输入 2.0。现在单击 Go! 按钮运行脚本。
- 脚本在场景中添加了 50 个 box 的副本，并将它们随机放置在距离 box 位置两单位的位置。

图 49.3 显示了 SphereArray MAXScript 实用程序的结果。请注意，SphereArray 脚本看起来与 Max 中的任何其他功能或工具一样。

## FIGURE 49.3

SphereArray MAXScript 实用程序的结果

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1225_0.png)

## MAXScript Listener window

图 49.4 显示了 MAXScript Listener 窗口（键盘快捷键 F11），它让你能够与解释 MAXScript 命令的 Max 部分进行交互。Listener 窗口的顶部窗格（粉色区域）让你输入 MAXScript 命令；结果在底部窗格（白色区域）中报告

Listener 窗口。你也可以在底部窗格中输入 MAXScript 命令，但将它们输入顶部窗格可以使命令与结果分开。如果你拖动两个窗格之间的间隔，你可以根据需要调整两个窗格的大小。

## Chapter 49: Automating with MAXScript

### Note

当你第一次打开 MAXScript Listener 时，顶部窗格不可见，但如果你拖动分隔线，你可以使两个窗格都可见。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1226_0.png)

## FIGURE 49.4

MAXScript Listener 窗口解释你的命令。

当你键入命令到任一窗格并按 Enter 时，MAXScript 解释器会评估该命令并以结果作出响应。例如，如果你键入简单的数学表达式 2+2 并按 Enter，则结果 4 会以蓝色显示在下一行。大多数结果以蓝色显示，但任何发生的错误结果会以红色显示。例如，如果你输入命令 hello there，则会出现红色 Type 错误结果，因为 MAXScript 解释器不理解该命令。

### Caution

MAXScript 解释器非常挑剔。拼写错误会产生错误，但 MAXScript 不区分大小写，这意味着就 Max 而言，大写和小写字母是相同的。因此，你可以键入 sphere、Sphere 或 SPHERE，Max 看不出任何区别。

Listener 窗口具有以下菜单：

- **File:** 你可以使用此菜单关闭窗口（Ctrl+W）、保存你的工作（Ctrl+S）、运行脚本（Ctrl+R）、打开脚本进行编辑（Ctrl+O），或从头创建新脚本（Ctrl+N）。
- **Edit:** 此菜单是你访问所需所有常用编辑功能的地方，例如剪切、粘贴和撤销。
- **Search:** 你使用此菜单在窗口中搜索特定文本（Ctrl+F）、查找下一个实例（Ctrl+G）或替换文本（Ctrl+H）。
- **MacroRecorder:** 此菜单让你为 MAXScript Macro Recorder 设置各种选项。
- **Debugger:** 此菜单提供了一种打开 Debugger 对话框的方法。
- **Help:** 此菜单提供对 MAXScript Reference（F1）的访问。

