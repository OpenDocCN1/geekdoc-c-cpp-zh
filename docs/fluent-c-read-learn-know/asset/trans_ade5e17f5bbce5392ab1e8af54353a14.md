

## 你做得怎么样？

无论你为高度和宽度分配了什么实际值，只要基本结构正确即可。

```xml
<Grid>
<Grid.RowDefinitions>
<RowDefinition Height="40" />
<RowDefinition Height="*" />
<RowDefinition Height="40" />
<RowDefinition Height="40" />
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="40" />
<ColumnDefinition />
</Grid.ColumnDefinitions>

<Rectangle Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"/>
<Rectangle Grid.Row="1" Grid.Column="0" Grid.RowSpan="3" />
<Rectangle Grid.Row="2" Grid.Column="1" />
<Rectangle Grid.Row="3" Grid.Column="1" />
</Grid>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_556_1.png)

## 网格分割器 1-2-3

像 Microsoft Excel 这样的电子表格显然是网格，但即使是 Windows Explorer 这样的东西也有可识别的网格组件。这些窗口中的大多数都允许你通过单击和拖动来更改窗格的相对大小。WPF 中用于添加该功能的工具是 GridSplitter。关于 GridSplitter 的大多数讨论，包括 MSDN 上的讨论，都让它听起来比实际使用要困难得多，因为它们设置了一大堆对于最常见情况来说大多无关的属性。因此，以下是我使用 GridSplitter 控件使网格的行或列可调整大小的三步流程。

- **创建一个行或列定义来容纳网格分割器**

  将行或列的 Width 属性设置为分割器的宽度。你可以将其设置为任何你想要的值，但 5 通常是一个不错的起点。你可以将控件放在与其他元素同一行或同一列中，但要确保 GridSplitter 正确显示可能会变得棘手。为什么要给自己找麻烦呢？

- **将网格分割器添加到网格中**

  你将使用与任何其他元素相同的语法，设置 Row、RowSpan、Column 和 ColumnSpan 属性，以便 GridSplitter 位于你想要的位置。务必显式设置 Width 属性。默认情况下，GridSplitter 的 Width 为零，这使得无法用鼠标抓取它。

- **设置 ResizeBehavior 属性**

  你几乎总是希望将 ResizeBehavior 设置为 "PreviousAndNext"，这告诉 GridSplitter 调整其两侧的行或列的大小。

  MSDN 会告诉你设置 HorizontalAlignment 或 VerticalAlignment 来控制 GridSplitter 的行为，但这有点晦涩。如果你显式设置 ResizeBehavior，代码就变得自解释，这总是比“这个属性比你想象的要多，你只有在有人告诉你时才知道”要好。

### 戴上你的思考帽

如果你还没有这样做，请在 Visual Studio 中创建上一页的 Grid。（你可能希望为 Rectangle 元素添加一个 Stroke，以便你可以看到它们。）然后添加一个 GridSplitter，它从第 1 行到第 3 行分隔第一列和第二列。（保留第一行跨越整个窗口。）

## 你做得怎么样？

```xml
<Grid>
<Grid.RowDefinitions>
<RowDefinition Height="40" />
<RowDefinition Height="*" />
<RowDefinition Height="40" />
<RowDefinition Height="40" />
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="40" />
<ColumnDefinition Width="5" />
<ColumnDefinition />
</Grid.ColumnDefinitions>
<Rectangle Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2" />
<Rectangle Grid.Row="1" Grid.Column="0" Grid.RowSpan="3" />
<Rectangle Grid.Row="2" Grid.Column="2" />
<Rectangle Grid.Row="3" Grid.Column="2" />
<GridSplitter Grid.Row="1" Grid.Column="1" Grid.RowSpan="3"
Width="5" ResizeBehavior="PreviousAndNext" />
</Grid>
```

## 显微镜下

GridSplitter 的另一个有用属性是 ShowsPreview。ShowsPreview 决定 GridSplitter 控制的行或列在用户拖动时是否实际更改，或者仅在用户释放鼠标之前显示更改的预览。

ShowsPreview 默认为 False，这对于大多数情况来说没问题，但如果更新显示时有明显的延迟，你可能希望将其更改为 True。

## 嵌套面板

你已经看到 WPF 面板控件负责显示子元素集合。但你是否意识到这些子元素本身也可以是面板？看下面的窗口。它是 Recipe 系统可能的样子的原型，它有面板套面板套控件……这在现实世界中构建窗口时非常典型。

在 Grid 的这个单元格中，有一个嵌套了 StackPanel 的 ScrollViewer。

DockPanel 的最后一个子元素是一个具有 4 行和 3 列的 Grid。

StackPanel 只是将其子元素堆叠起来。

布局根是一个 DockPanel，Menu、ToolBar、StatusBar 和 TreeView 都停靠在它的边缘。

这是一个停靠在窗口左侧的 TreeView。

这实际上是一个嵌套在 ScrollViewer 中的 Grid，该 ScrollViewer 嵌套在另一个 Grid 中，而该 Grid 嵌套在 DockPanel 中。哎呀！

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_559_0.png)

这个 Label 跨越两列。

如果内容不适合，ScrollViewer 会显示滚动条。

> **休息一下**
>
> 第一部分到此结束。正如你从这个例子中所见，面板可能会变得复杂，但它们真的很容易使用，随着我们继续阅读本书的其余部分，你会有大量的练习。现在，在完成复习并继续学习 WPF 控件类之前，为什么不休息一下呢？

## 复习

每种标准面板控件如何控制其子元素的相对位置？
Grid：
DockPanel：
Canvas：

使用控制该空间的属性标记此图中的每个箭头。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_560_0.png)

Windows Explorer 的布局是许多应用程序中常用的结构。
你会使用哪些 WPF 面板来构建它？不用担心内容，只关注你用来创建窗格的面板控件。（提示：其中一个面板是我们没有讨论过的标准面板，但在第 537 页有示意图。）

## 控件类

第 535 页有一张核心 WPF 类的路线图。在深入探讨从 Control 派生的类的细节之前，让我们先快速看看 Control 本身及其祖先类。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_561_0.png)

Visual 公开控制显示的属性和方法。

FrameworkElement 公开支持布局系统的方法和属性，以及 Initialized 和 Loaded 等生存期事件。

UIElement 公开允许 WPF 元素通过键盘、鼠标、样式或触摸屏与用户交互的所有方法和属性。这里显示的远不止这些——这只是一个示例。

你将用来构建应用程序界面的大多数小部件直接或间接地从 Control 派生，包括我们将在本章余下部分讨论的那些。Control 类添加格式和布局属性，还支持样式和模板，我们将在第 20 章和第 21 章中讨论。

## 控件家族

还记得我说过你将用来构建应用程序的大多数小部件都将从 Control 派生吗？这是一个（部分）层次结构。它们可真多，不是吗？但情况并没有听起来那么糟糕，因为层次结构的工作方式。继续阅读…

- Control
  - Calendar
  - DatePicker
  - FlowDocumentReader
  - PasswordBox
  - StickyNoteControl
  - Separator
  - Decorator
  - ViewBase
  - GridView
  - Primitives.TextBoxBase
    - TextBox
    - RichTextBox
  - Primitives.RangeBase
    - Primitives.ScrollBar
    - ProgressBar
    - Slider
  - ContentControl
    - Window
      - ExpressionTextBox
      - Frame
      - Label
      - ListBoxItem
      - FlowDocumentViewer
      - ToolTip
      - UserControl
    - HeaderedContentControl
      - Expander
      - GroupBox
      - TabItem
    - Primitives.ButtonBase
      - Button
      - ToggleButton
      - CheckBox
      - RepeatButton
  - ItemsControl
    - Primitives.Selector
      - ComboBox
      - TabControl
      - MultiSelector
        - DataGrid
        - ListBox
        - ListView
    - TreeView
    - HeaderedItemsControl
      - MenuItem
      - Toolbar
      - TreeViewItem

