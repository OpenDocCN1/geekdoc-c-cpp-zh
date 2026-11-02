
## 研究生学位论文答辩
## 基于深度学习的污水处理过程软测量建模方法研究
答辩人：李伟
指导教师：张敏教授
答辩时间：2024年5月20日
答辩地点：环境工程学院 301 会议室
## 汇报提纲
- 1. 研究背景与意义
- 2. 国内外研究现状
- 3. 主要研究内容与方法
- 4. 实验设计与结果分析
- 5. 结论与展望

![](img/f938eba5f15e231d828a6255e7ec5523_415_0.png)

> 调用 `setVisible(true)` 会使框架出现在你的屏幕上。如果你忘记调用 `setVisible(true)`（我经常犯这个错），当你运行《清单 20-1》中的代码时，你的屏幕上将看不到任何东西。直到你弄清楚自己做错了什么，这总是让人非常不安。

## 构造函数调用
在《清单 17-3》（第 17 章）中，我使用以下行创建了 Purchase 类的一个实例

```
Purchase onePurchase = new Purchase();
```

《清单 20-1》中的代码做了同样的事情。在《清单 20-1》中，我使用以下行创建了 JFrame 类的一个实例：

```
JFrame frame = new JFrame();
```

将第 17 章中的图 17-4 与本章的图 20-4 进行比较。

![](img/f938eba5f15e231d828a6255e7ec5523_415_1.png)

当你输入 `MyFrame extends JFrame` 时，你声明你的新 `MyFrame` 类具有 Java 自身 `JFrame` 类内置的所有方法和其它内容，甚至更多。例如，`JFrame` 实例具有 `setDefaultCloseOperation`、`pack` 和 `setVisible` 方法，因此每个新的 `MyFrame` 实例也具有 `setDefaultCloseOperation`、`pack` 和 `setVisible` 方法（参见图 20-6）。

![](img/f938eba5f15e231d828a6255e7ec5523_419_0.png)

**图 20-6：** `MyFrame` 实例具有许多方法。

当你在代码中加入 `extends JFrame` 这一词时，你就可以免费获得所有 `JFrame` 方法。`MyFrame` 类的代码不需要对诸如 `setDefaultCloseOperation`、`pack` 和 `setVisible` 之类的方法进行声明。这些声明已经存在于 Java API 中的 `JFrame` 类里。`MyFrame` 类代码中唯一的声明是针对全新事物——特定于你新声明的 `MyFrame` 类的事物。就好像《清单 20-2》包含以下信息：

```java
public class MyFrame is a kind of JFrame {

    And in addition what's in JFrame, MyFrame also has
    a brand new constructor:
    public MyFrame() {
        // Etc.
    }
}
```

在 Mac 上，你会得到一个 .dmg 文件。根据 Mac 网页浏览器的设置，浏览器可能会或可能不会自动展开 .dmg 文件。如果没有，请双击 .dmg 文件开始安装。

- 5. **按照安装程序的说明进行操作。**

在 Windows 计算机上，你接受一堆默认值。

在 Mac 上，你将 Scene Builder 的图标拖到 Applications 文件夹中。

就这样！你已经安装了 Scene Builder。

## 安装 e(fx)clipse
Eclipse 拥有自己的复杂设施用于集成新功能。Eclipse 工具称为 *Eclipse 插件*。初次安装 Eclipse 时，你会默认获得许多插件。然后，为了增强 Eclipse 的功能，你可以安装许多额外的插件。

Eclipse 的 e(fx)clipse 插件促进了 JavaFX 应用程序的创建。你可以将插件添加到现有的 Eclipse 安装中，但下载一个全新的 Eclipse 副本（已预装 e(fx)clipse 的副本）要简单得多。以下是获取新 Eclipse 副本的方法：

- 1. 访问 `efxclipse.bestsolution.at`。
- 2. 查找包含 All-in-One 下载的页面。
- 3. 在 All-in-One 下载页面上，查找下载适用于你操作系统的 Eclipse 副本的方式。

你的 Eclipse 下载的位数（32 位或 64 位）必须与你的 Java 版本的位数匹配。有关 32 位和 64 位位数的完整说明，请参阅第 2 章。

- 4. **按照适当的链接或点击适当的按钮开始下载。**
- 5. **按照第 2 章中的说明在你的计算机上安装这个新副本的 Eclipse。**

![](img/f938eba5f15e231d828a6255e7ec5523_424_0.png)

将 Eclipse 的新副本放在一个全新的文件夹中。这样你就不必卸载旧的 Eclipse 副本（事实上，在你的计算机上拥有两个独立的 Eclipse 安装是有帮助的）。在我的 Windows 计算机上，我有 `c:\eclipse` 文件夹和一个 `c:\eclipsefx` 文件夹。两个文件夹都有各自名为 `configuration`、`features` 和 `plugins` 的子文件夹。两个文件夹都有各自的 eclipse.exe 文件。同样，我的 Mac 在 Applications 文件夹内同时拥有 eclipse 和 e(fx)clipse 文件夹。

![](img/f938eba5f15e231d828a6255e7ec5523_425_0.png)

当你打开任何一个 `eclipse` 副本时，程序会提示你在硬盘上为 Eclipse 工作区（你的 Eclipse 项目集合）选择一个位置。此时，你有以下选择：

- **你可以为两个不同的工作区使用两个不同的文件夹——一个工作区用于你的原始 Eclipse 副本，另一个工作区用于你的新 Eclipse 副本。**

这样做可以使你的原始工作（前几章的工作）与本章的工作分开。此外，使用两个不同的工作区，你可以同时运行两个 Eclipse 副本。

- **或者，你可以将两个版本的 Eclipse 都指向同一个文件夹（从而使用同一个工作区）。**

这样做可以使所有工作都集中在一个地方。你不必更改工作区即可在原始工作和本章工作之间切换。缺点是，你不能同时使用同一个工作区运行两个 Eclipse 副本。

![](img/f938eba5f15e231d828a6255e7ec5523_425_1.png)

不要为你对 Eclipse 工作区的决定而烦恼。在任何 Eclipse 副本中，你都可以从一个工作区切换到另一个工作区。你可以在每次启动 Eclipse 时决定使用特定的工作区。你也可以通过在 Eclipse 主菜单中选择 File>Switch Workspace 来在工作区之间切换。

![](img/f938eba5f15e231d828a6255e7ec5523_425_2.png)

你需要至少 JDK 7u7 才能运行 `e(fx)clipse`。

## 创建一个简易的 JavaFX 项目
有一句古老的格言：“一图胜千言。”如果把诸如 `javafx.application.Application` 对象之类的东西，以及关联视为三个独立的词，那么同一张图片就值 70 个词。在本节中，你将创建一个图片，Eclipse 将据此构建一个 70 词的 Java 程序。

- 1. **按照前几节（“安装 Scene Builder”和“安装 e(fx)clipse”部分）的说明进行操作。**
- 2. **启动你的新 Eclipse 副本并点击欢迎屏幕上的 Workbench 图标。**
- 3. **从 Eclipse 的菜单栏中选择 File>New>Project。**
  新建项目对话框出现。
- 4. **在对话框的列表中，展开 JavaFX 分支。在该分支中，选择 JavaFX project 然后点击 Next。**
  新建 Java 项目对话框出现。

- 5. 在新建 Java 项目对话框中，为你的项目输入一个名称。

如果你严格按照我的说明操作，请将项目命名为 MyFirstJavaFXProject。

- 6. 在新建 Java 项目对话框中，选择 JavaSE-1.7 或 JavaSE-1.8。

你可以用更早版本的 Java 运行 JavaFX 程序，但使用 Java 7 更新 7（JDK 7u7）或更高版本会更轻松。

- 7. 点击 Finish 关闭新建 Java 项目对话框。

点击 Finish 后，你可能会或可能不会看到一个对话框，警告你 Mercurial（无论那是什么）未正确配置。如果看到此对话框，请查找对话框中的 Restore Defaults 按钮。点击该按钮，然后点击 OK。

你会看到 Eclipse 工作台，其中在 Eclipse 的 Package Explorer 中显示了你新建的项目。

![](img/f938eba5f15e231d828a6255e7ec5523_426_0.png)

## 运行你的简易 JavaFX 项目
在上一节中，你使用 e(fx)clipse 创建了一个全新的 JavaFX 项目。当你运行新项目的代码时，你会看到图 20-8 中的内容。你会看到一个里面什么都没有的窗口。

![](img/f938eba5f15e231d828a6255e7ec5523_426_1.png)

图 20-8：
一个空窗口。

