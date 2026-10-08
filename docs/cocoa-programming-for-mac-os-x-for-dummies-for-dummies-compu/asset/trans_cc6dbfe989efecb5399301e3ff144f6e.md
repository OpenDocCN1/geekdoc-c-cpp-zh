

## 图 3-15：单击项目窗口工具栏中的“Build”按钮以运行您的项目。

![](img/ea40cad434a338535474e82c1a6ace20_80_0.png)

## 第 4 章 Interface Builder（界面构建器）

**本章内容**

- 熟悉 Interface Builder 的操作界面
- 在界面上添加控件
- 编辑控件的属性
- 编辑和创建新菜单
- 实现用于操作界面的代码

Cocoa 开发中第二重要的组件（第一个是 Xcode；参见第 3 章）就是与其同名的 Interface Builder 应用程序，它允许您为 Cocoa 项目构建界面。Interface Builder 让您能够轻松地通过拖放功能为您的软件构建美观的界面——无需编写任何代码。更重要的是，您在 Interface Builder 中创建的界面遵循 Apple 严格的“人机界面指南”（Human Interface Guidelines），因此您有很大机会制作出 Mac 用户（他们可能比较挑剔）既喜欢查看又愿意使用的应用程序。

在本章中，您将参观 Interface Builder，并在过程中检查其功能。为了帮助您适应 Interface Builder，我们将改进您在第 3 章中创建的计算器应用程序。到本章结束时，您的计算器将拥有一个新的菜单、额外的界面元素以及增加的功能。

![](img/ea40cad434a338535474e82c1a6ace20_82_0.png)

您可以在 *For Dummies* 网站上找到本章的项目文件，网址为 www.dummies.com/go/cocoafd。

### 参观 Interface Builder

要开始使用 Interface Builder，请复制第 3 章已完成的项目文件夹。请始终确保您的 Cocoa 项目及相关文件存放在可写介质上，这通常是您的硬盘。

将代码复制到硬盘后，请按照以下步骤开始在 Interface Builder 中处理该项目：

1.  打开 `My First Project.xcodeproj` 文件。
    Xcode 启动，项目打开。
2.  在 Xcode 中展开项目的 Resources（资源）文件夹，以显示 `MainMenu.xib` 文件。
3.  在 Xcode 中，双击 `MainMenu.xib` 文件在 Interface Builder 中打开它。

`MainMenu.xib` 是您的计算器项目的界面文件。图 4-1 展示了 `MainMenu.xib` 文件在 Xcode 中的位置。

尽管 Xcode 和 Interface Builder 是两个不同的应用程序，但它们协同工作，为您提供集成的 Cocoa 体验。

**图 4-1：MainMenu.xib 包含您项目的界面外观。**

![](img/ea40cad434a338535474e82c1a6ace20_83_0.png)

顺带一提，`MainMenu.xib` 中的 XIB 文件扩展名表明这是一种较新的 Interface Builder 项目文件格式，在 Xcode 3 中引入。此前，该文件使用 NIB 扩展名，它是 Next Interface Builder（Next 界面构建器）的缩写。为什么是 NeXT？NeXT 是史蒂夫·乔布斯（Steve Jobs）在回归 Apple 之前担任首长的公司名称。Apple 生产了 Next 操作系统，该系统成为 Mac OS X 的核心。XIB 文件就是那个时代的遗留产物。Cocoa 极客们仍然在使用这些 NIB 文件——旧习难改。您曾尝试过发音 "NeXT" 吗？此外，Cocoa 中类名开头的 AS 代表 NextStep，这是 Cocoa 中源自 NeXT 的另一个历史细节。

当您首次启动 Interface Builder 时，可能会看到多达五个窗口。图 4-2 显示了 Interface Builder 中出现的各种窗口。虽然它不是五个主要窗口之一，但“字符串”（Strings）窗口也可能出现。字符串窗口存在的可能性比其他窗口小，但如果您使用它，请随意选择。本章中您将不使用它。

![](img/ea40cad434a338535474e82c1a6ace20_84_0.png)

**图 4-2：Interface Builder 有五个主要窗口。**

设计窗口

表 4-1 描述了为什么需要每个窗口，以及如果当前未显示该窗口时如何显示它。

| 表 4-1 Interface Builder 的主要窗口 |
| :--- | :--- | :--- |
| **窗口** | **显示方法** | **用途** |
| 项目窗口 | 在 Xcode 中双击 XIB 文件 | 存储界面文件的组件。 |
| 设计窗口 | 在 XIB 项目窗口中双击 Window（窗口）图标 | 将窗口用作应用程序界面的一部分。 |
| 检查器窗口 | 选择 工具 > 检查器 | 查看和编辑项目中的界面及其他类的属性。 |
| 库 | 选择 工具 > 库 | 将控件从库窗口拖放到设计窗口以创建界面。 |
| 菜单编辑器 | 在 XIB 项目窗口中双击 MainMenu（主菜单）图标 | 创建、删除或编辑应用程序的菜单。 |

使用这五个窗口构成了 Interface Builder 的主要工具。结合使用这些工具，您可以为 Cocoa 应用程序构建完整的界面。但这并非 Interface Builder 能做的全部。您还可以：

- 在项目中创建类。
- 通过单击和拖放将类连接到界面元素。这些连接充当界面与 Xcode 项目之间的桥梁。
- 允许 Interface Builder 处理编写界面部分代码的脏活。只需单击一次，它就能在 Xcode 中生成必要的接口和实现文件，供您稍后添加代码。

### Interface Builder 项目窗口

NIB 项目窗口是您项目界面的核心。这是存储项目界面组件的地方。NIB 项目窗口具有三种不同的视图，类似于 Finder（访达）：

- **图标：** 将 XIB 文件中的对象显示为大型图标网格。图 4-3 展示了 Interface Builder 项目窗口的图标视图格式。

**图 4-3：使用图标视图快速查看 XIB 文档中的项目。**

![](img/ea40cad434a338535474e82c1a6ace20_86_0.png)

- **列表：** 将 XIB 文件中的对象显示为垂直层次结构。列表视图对于定位窗口中的控件非常有用。当您需要选择嵌入在其他控件中的控件时，它会派上用场（参见图 4-4）。当您想将嵌入的控件移动或复制到另一个对象或控件时，或者想查看上下文中的嵌入控件时，它也很有用。

**图 4-4：使用列表视图查看 XIB 项目的类层次结构。**

![](img/ea40cad434a338535474e82c1a6ace20_86_1.png)

- **列：** 将 XIB 文件中的对象显示为水平层次结构（参见图 4-5）。列视图类似于列表视图，只是它以水平方式显示项目项的层次安排。

**图 4-5：列视图水平显示层次信息。**

![](img/ea40cad434a338535474e82c1a6ace20_87_0.png)

Xcode 为您作为新项目一部分创建的每个新 NIB 文件默认都有六个项目：

- File's Owner（文件所有者）
- First Responder（第一响应者）
- Font Manager（字体管理器）
- Application（应用程序）
- MainMenu（主菜单）
- Window（窗口）

MainMenu 和 Window 是现阶段您需要关注的内容。正如您可能猜到的那样，MainMenu 是编辑界面菜单的地方。Window 是一个窗口对象，您可以将其用于界面中。

### 设计窗口

设计窗口代表您界面中的一个窗口，也是您添加控件的地方。然后，您的用户使用这些控件来操作您的应用程序。要查看设计窗口：

1.  在 NIB 项目窗口中，双击 Window。
    窗口对象的内容将显示出来，如图 4-6 所示。
2.  窗口打开后，选择一个控件。
    例如，选择 Calculate（计算）按钮。

**图 4-6：设计窗口是布局界面控件的地方。**

![](img/ea40cad434a338535474e82c1a6ace20_88_0.png)

3.  按住 Option 键，并在窗口内移动光标。
    当经过一个控件时，Interface Builder 会显示指南线和数字，告知您所选控件与光标下方控件之间的距离。图 4-7 说明了按钮和答案字段之间的距离。

**图 4-7：选择一个控件并按住 Option 键以显示指南线。**

![](img/ea40cad434a338535474e82c1a6ace20_88_1.png)

4.  保持按钮选中状态，按住 Option 键并将光标移动到窗口中没有控件的区域。
    您会看到定义所选按钮位置的指南线。图 4-8 显示了按钮在计算器界面中的位置。

![](img/ea40cad434a338535474e82c1a6ace20_88_2.png)

您可以通过用鼠标拖动来移动设计窗口中的控件。您也可以选择一个控件并使用方向键移动它。当您在窗口中移动控件时，Interface Builder 会显示指南以帮助您准确放置控件。

