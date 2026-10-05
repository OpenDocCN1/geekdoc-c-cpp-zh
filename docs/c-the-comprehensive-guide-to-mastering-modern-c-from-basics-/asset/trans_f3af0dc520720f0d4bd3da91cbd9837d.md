
遵循安装程序的建议并重启 Windows 是一个好主意。

接下来，安装 C/C++ 插件：

-   按下 Ctrl + Shift + X 或点击左侧栏中的四方块图标可打开扩展视图。
-   在搜索框中输入 "C++"，列表中会出现原始的 Microsoft C++ 扩展。你可以选择纯扩展或扩展包。我个人选择了后者。它包含了的 C++ 扩展、CMake 扩展以及 C++ 主题。

![](img/290cf954dfcaad53865de6b98cca8e6f_78_0.png)

**图 2.5** 欢迎界面。

现在我们仍然需要一个 C++ 编译器。微软建议你检查是否已经安装了。我们假设你尚未安装。你可以在 MinGW g++ 或 MSVC 编译器之间进行选择。

![](img/290cf954dfcaad53865de6b98cca8e6f_79_0.png)

**图 2.6** VS Code 通过插件支持多种编程语言。

我们在这里使用 MSVC 编译器。最好先关闭 VS Code。然后从 https://visualstudio.microsoft.com/downloads/ 下载 **Build Tools for Visual Studio 2022** 并安装它们。在出现的界面界面，选择左侧的 **Desktop Development with C++**（使用 C++ 的桌面开发），右侧至少选择 MSVC 和 C++-CMake。

![](img/290cf954dfcaad53865de6b98cca8e6f_80_0.png)

**图 2.7** 分别安装的编译器和其他工具。

许多软件包安装完成后，点击安装界面上的 **Start**（开始），你将进入 **VS 2022 开发者命令提示符**（Devconsole）。你可以关闭安装程序。你可以通过在开始栏中输入“Developer Command”并选择 **Devconsole.** 来再次打开 Devconsole。

![](img/290cf954dfcaad53865de6b98cca8e6f_80_1.png)

**图 2.8** 在 Devconsole 中可以使用 cl 编译器。

要使用已安装的编译器启动 VS Code，请在 Devconsole 中输入“code”。

![](img/290cf954dfcaad53865de6b98cca8e6f_81_0.png)

**图 2.9** 支持 C++ 的完整安装的 IDE。

你会看到 C++ 插件用一个新按钮欢迎你。点击它。几秒钟后，你可以点击标记为 **Select My Default Compiler**（选择我的默认编译器）的按钮。那里那里有一个蓝色的完成标记，但你可以轻松地检查该设置。

![](img/290cf954dfcaad53865de6b98cca8e6f_82_0.png)

**图 2.10** 已找到编译器。

![](img/290cf954dfcaad53865de6b98cca8e6f_82_1.png)

**图 2.11** 设置默认编译器。

然后选择 **cl.exe**。这就是你已经在 Devconsole 中尝试过的编译器。如果你愿意，可以自己完成 **Get Started with C++ Development**（开始 C++ 开发）的后续步骤。不过，我也可以向你展示另一种或额外的方法来演示 C++ 程序。

在 VS Code 中通过 `Ctrl+`O` 打开终端。你应该会在你的主目录下得到一个命令提示符。在那里，连续输入 `mkdir modern101` 和 `cd modern101` 以切换到新目录。

![](img/290cf954dfcaad53865de6b98cca8e6f_83_0.png)

**图 2.12** 在新目录启动项目。

然后选择 VS Code 中清晰的 **Open Folder**（打开文件夹）按钮，并选择你刚刚创建的 **modern101** 文件夹。将打开一个新的项目窗口，你必须首先同意 **Yes, I trust the authors of this folder**（是的，我信任此文件夹的作者——也就是你自己）。

![](img/290cf954dfcaad53865de6b98cca8e6f_83_1.png)

**图 2.13** 打开了带有新项目的 VS Code。

你现在会在左侧看到项目区域。在那里，你可以将鼠标指针悬停在 MODERN101 上以显示创建新文件的按钮。你也可以在 Start（开始）下的欢迎区域选择 New File...（新文件...）；会会弹出一个对话框。文件名应该是 modern101.cpp。右侧区域会打开一个文本编辑器，你可以在其中输入源代码。在这里编写你的第一个 C++ 程序吧！

![](img/290cf954dfcaad53865de6b98cca8e6f_84_0.png)

**图 2.14** 在右上角的三角形中输入 C++ 源代码。

现在你只需要点击右上角的三角形即可运行你的程序。输出将在这里显示。
