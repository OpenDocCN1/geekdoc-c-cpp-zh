

- *Project 2010 加载项*: 为 Microsoft Project 创建加载项。
- *Visio 2010 加载项*: 为 Microsoft Visio 创建加载项。
- *Word 2010 加载项*: 为 Microsoft Word 创建加载项。
- *Excel 2010 加载项*: 为 Microsoft Excel 创建加载项。
- *Outlook 2010 加载项*: 为 Microsoft Outlook 创建加载项。
- *Word 2010 文档*: 输出为 Microsoft Word 2007 文档。
- *Excel 2010 模板*: 输出为 Microsoft Excel 2007 模板（一个 .xlt 文件）。
- *InfoPath 2010 加载项*: 为 Microsoft InfoPath 创建加载项。
- *PowerPoint 2010 加载项*: 为 Microsoft PowerPoint 创建加载项。

### Communication Foundation Projects
Windows Communication Foundation 是 Microsoft 提供的一种使程序之间能够相互通信的机制：

- *Syndication Service Library*: 创建一个聚合提要服务（RSS），可使用 ATOM 或 RSS 通信。
- *WCF Service Library*: 用于通信基础的类库。
- *Declarative Flowchart Service Library*: 创建一组使用流程图样式工作流来提供服务的服务。
- *Declarative Sequential Service Library*: 创建一组使用顺序样式工作流来提供服务的服务。

### Workflow Projects
Workflow Foundation 是在 Microsoft 程序中创建工作流的标准库。你可以设置标准审批、文档流转等：

- *Activity Designer Library*: 该项目帮助你创建用于创建活动的用户界面。
- *Activity Library*: 如果你不想创建用于创建活动的用户界面，你可以直接创建活动。
- *Flowchart Workflow Console Application*: 该项目和顺序项目提供了一种在安全环境中测试 WF 工作流的方法。
- *Sequential Workflow Console Application*: 这与流程图 WF 项目类似，但适用于顺序工作流。

### Special Projects
指不符合前述条目的任何内容：

## Chapter 2: Using the Interface

### In This Chapter
- 使用设计器
- 探索解决方案资源管理器
- 使用代码视图进行编码
- 使用“工具”菜单

集成开发环境（IDEs）是程序员工具箱中的瑞士军刀。IDEs 提供了存储程序代码、组织和构建代码以及通过设计编辑器查看成品的机制。IDEs 让事情得以实现，同时还能节省数小时的工作时间。

Visual Studio 正被真正全球公认为 IDE 中的佼佼者，甚至连 Microsoft 的批评者也如此认为。我认识一些 Python 程序员，他们整天在 Linux 机器上冲浪时痛骂 Windows，然后切换到 Windows 分区使用 Visual Studio 用 IRONPython 进行编码。

Visual Studio 令人印象深刻；它非常庞大。世纪之交时（呵！）我与 David Deloveh 合著了一本书，试图涵盖所有 Visual Studio 功能。那本书有 600 页。读者的主要抱怨是：太短了。涵盖不够。现在的 Visual Studio 大了两倍。它太庞大，无法用一章来概括。

因此，与其试图涵盖一切，我让你有机会体验我每天使用的 Visual Studio 功能。我不想隐瞒任何东西，希望你继续探索 IDE 并发现新事物——不要只停留在我告诉你的内容上。这只是对该工具中一些惊人功能的简要概述。

## Designing in the Designer

集成开发环境中集成的一项功能是图形化编辑文件的方式，有时称为图形开发环境或设计器。Visual Studio 允许你图形化编辑五种不同类型的代码库，并提供进一步管理这些代码库的辅助工具。

简而言之，设计器是 Visual Studio 世界中的拖放元素。它不总是开发程序的最佳方式，但有时确实能帮上忙。

Visual Studio 维护的每种主要项目类型都有一个设计器。设计器处理体验中的所见即所得部分，通常还处理幕后的标记代码。

问题在于，由于软件开发世界的需要，不同的设计器各有不同。例如，HTML 和 XAML 之间存在显著差异，因此网页设计器和 WPF 设计器的外观和行为并不相同。

Visual Studio 为你提供了多个视觉设计器来帮助开发应用程序，包括以下这些：

- Class Designer
- Data View
- Web Forms
- Windows Forms
- Windows Presentation Foundation (WPF)

![](img/80ff26f06fc9ab951e1cd4257b867366_543_0.png)

目前 Windows Store 应用使用 Blend 作为其设计表面。我想随着时间的推移这种情况会发生变化，就像 WPF 一样，但目前就是这样，这使它有点超出本迷你书的范围。我建议阅读 Windows 8 Programming with HTML5 For Dummies 以了解有关 Windows Store 应用设计的更多信息。

## Windows Presentation Foundation (WPF)

Windows Presentation Foundation 在第 V 书中有深入介绍，但现在你应该知道它代表了 Microsoft Windows 开发体验的未来。第 V 书全面讲述了 WPF，你可以在那里阅读更多内容。

用户界面设计体验的核心是一种名为 XAML 的语言，它（毫不奇怪）是一种源自 XML 的领域特定标记语言，用于创建用户界面。在图 2-1 所示的设计器中，设计位于上部框架，底层代码位于下部框架。

你可以在设计器中点击设计并移动元素，如果你愿意，也可以利用设计器选择元素并在属性面板中编辑属性（我在即将到来的“Paneling the Studio”部分中介绍）。此外，如果你在代码区域更改了某些内容，你会在设计中看到更改。这是一个不错的系统。

![](img/80ff26f06fc9ab951e1cd4257b867366_544_0.png)

Figure 2-1: The WPF Designer.

WPF 设计器中有一些虽小但重要的功能值得指出。你可以在图 2-1 中看到它们全部。

靠近左上角有一个缩放条。你可以点击其底部进行“缩放以适应”，或移动滑块。这对于处理比屏幕更大的应用程序，或适度调整大小非常宝贵。

在设计与 XAML 框架之间的分隔线左侧有一个小双箭头图标。点击此图标会将底部框架中的内容切换到顶部框架，反之亦然。

在同一分隔线的右侧有三个按钮，用于确定拆分方式——垂直拆分、水平拆分（默认）或不拆分。

设计器本身内置了一些很酷的点选调整工具。这里只举一个例子：在设计器窗口中表格的红色区域点击。将鼠标放在“146”尺寸标识正上方。

看到出现的那个小浮动框了吗？里面有一个星号、一个井号和单词 Auto？这只是 WPF 设计器中众多小助手之一。井号将列宽设置为固定数值（默认即如此）。星号将其设置为表格的百分比——便于调整大小。单词 Auto 根据内容调整列宽。

这些小功能仅对设计器下方框架中的 XAML 进行更改。如果你点击浮动表格设计器中的单词 Auto，你将把这行代码：

```
<ColumnDefinition Width="146" />
```

改为 XAML 框架中的这行代码：

```
<ColumnDefinition Width="Auto" />
```

有些人喜欢代码。有些人喜欢设计器。有些人（像我一样）更喜欢两者之间的一种奇怪混合。你决定如何使用这些工具。

## Windows Forms

Windows Forms 设计器与 WPF 设计器之间的主要区别在于 Windows Forms 缺少代码面板。虽然 Windows Forms 背后有（某种）代码，但你无法编辑它。就这样。

本书不涉及 Windows Forms 主题。虽然它仍然是一个活跃的开发平台，但我不得不做出艰难决定，转而介绍 WPF。它执行与 Windows Forms 相同的编程任务，但技术更新。图 2-2 显示了 Windows Forms 设计器。

![](img/80ff26f06fc9ab951e1cd4257b867366_545_0.png)

**Figure 2-2:** The Windows Forms designer

