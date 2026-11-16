

## 树形视图

树形视图（TreeView，用于显示层次数据）是唯一直接继承自 ItemsControl 的常见控件。（大多数控件是通过 Selector 类间接继承的。）与许多项控件一样，TreeView 将 Items 集合重新定义为特定类型的集合，在此例中为 TreeViewItem，而 TreeViewItem 本身也是一个项控件，通过 HeaderedItemsControl 实现。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_580_0.png)

TreeViewItem 本身也是一个项控件，因此它可以包含子项集合。

### 动动脑筋

使用 XAML 集合语法，你能想出如何指定创建所示 TreeView 的集合吗？（如果你忘了集合语法的工作原理，请查阅第 513 页。提示：你使用 Header 属性来指定 TreeView 显示的文本。）

```
MainWindow
First Top Level Item
  I'm a child
  I'm a child, too
Second Top Level Item
  One
  Two
  Three
  Four
Last Item
  A
  B
    B1
    B2
  C
```

## 你做得怎么样？

这是个难题，还是你觉得轻松搞定？如果有点困难，不要放弃。我保证，熟能生巧，会越来越容易。

我是否让你措手不及了？集合语法也是你指定面板内容的方式。

```
<TreeView FontFamily="Brandywine"
FontSize="24">
<TreeViewItem Header="First Top Level Item">
<TreeViewItem Header="I'm a child" />
<TreeViewItem Header="I'm a child, too" />
</TreeViewItem>
<TreeViewItem>
<TreeViewItem Header="Second Top Level Item">
<TreeViewItem Header="One" />
<TreeViewItem Header="Two" />
<TreeViewItem Header="Three" />
<TreeViewItem Header="Four" />
</TreeViewItem>
<TreeViewItem Header="Last Item">
<TreeViewItem Header="A" />
<TreeViewItem Header="B" />
<TreeViewItem Header="B1" />
<TreeViewItem Header="B2" />
<TreeViewItem Header="C" />
</TreeViewItem>
</TreeView>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_582_1.png)

TreeViewItem 集合可以根据需要嵌套任意深度。

## 列表框和组合框

ListBox 和 ComboBox 控件是两种最常用的项控件。它们都继承自 Selector 类，后者添加了允许用户在控件中选择项的属性。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_583_0.png)

当我们在第 22 章学习 WPF 绑定时，将讨论 SelectedItem（用户实际选择的项）和 SelectedValue（与 SelectedItem 关联的指定属性的值）之间的区别。

因为 ListBoxItem 继承自 ContentControl 而非 ItemsControl，所以你设置的是 Content 属性，而不是 Header。

ListBox 和 ComboBox 还为其项集合定义了不同的类型。如你所见，ComboBoxItem 继承自 ListBoxItem。

### 动动脑筋

本章我们大量使用了 XAML，所以让我们用 C# 来做点什么。你能编写一个应用程序，显示一个包含三四个项的 ListBox，在窗口加载时选中列表中的第二个项，然后在用户选择其他项时在 MessageBox 中显示 SelectedIndex 吗？（提示：你需要添加一个事件处理程序。你还记得如何从属性窗口做到这一点吗？）运行应用程序时，它会显示两次 MessageBox。你知道为什么吗？

## 你做得怎么样？

当你在代码中设置 SelectedIndex 时，应用程序会先显示 MessageBox。我们将在下一章了解如何修复这一点。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_584_0.png)

## XAML

这里没有什么太棘手的，只要你没有过于照搬 TreeView 示例即可——ListBoxItem 是一个内容控件，因此你可以使用属性语法显式设置 Content 属性，也可以像我在这里所做的那样，使用内容语法隐式设置。

```
<Grid>
    <ListBox Name="SampleListBox" Margin="10,10">
        <ListBoxItem>First Item</ListBoxItem>
        <ListBoxItem>Second Item</ListBoxItem>
        <ListBoxItem>Third Item</ListBoxItem>
        <ListBoxItem>Fourth Item</ListBoxItem>
    </ListBox>
</Grid>
```

## 选择第二个项

做这件事的最佳位置是在窗口构造函数中，它应该如下所示：

```
public MainWindow()
{
    InitializeComponent();
    this.SampleListBox.SelectedIndex = 1;
}
```

你记得从零开始计数吗？

## 响应 SELECTIONCHANGED 事件

如果你从属性窗口操作，这个很简单。否则，该方法的语法比较繁琐：

```
private void SampleListBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    MessageBox.Show(this.SampleListBox.SelectedIndex.ToString());
}
```

## 选项卡控件

在用一个综合运用所学知识的练习来结束本章之前，让我们快速了解一下 TabControl，这是另一种管理屏幕空间的有用机制。现代应用程序在很大程度上已用选项卡窗口取代了使用子窗口的旧 MDI 结构。你需要处理的唯一新属性是 TabStripPlacement。使用此控件所需的其他所有内容你都已了解。你印象深刻吗？我是！

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_1.png)

TabItem 中的 TabStripPlacement 属性是只读的。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_2.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_3.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_4.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_5.png)

TabStripPlacement 属性允许你控制选项卡标签出现的位置。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_6.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_7.png)

### 综合运用

我们将通过一个扩展练习来结束本章，该练习运用所学知识来勾勒出一个真实的应用程序组件。它的外观将如下所示：

应用程序首次打开时，将在 TreeView 中显示食谱列表，以及一个只有一个空白选项卡的 TabControl。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_586_0.png)

当用户在 TreeView 中双击一个食谱时，我们将打开一个新选项卡。（目前我们不必担心选项卡的内容，只关心标题。）

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_586_1.png)

### 动动脑筋

在开始编码之前，花些时间思考我们需要做什么。你能回答下面这些问题吗？

主窗口左侧有一个 TreeView，右侧有一个 TabControl。当窗口大小调整时，TreeView 的宽度保持不变。你认为作为布局根，最好使用哪种面板类型？

TabItem 的 Header 中有两个项。你将如何实现？（提示：Header 属性定义为 Object 类型。）

当食谱列表中的某个项被双击时，将打开一个新选项卡。你需要将该代码放在事件处理程序中。你认为应该响应哪个事件？（提示：当 TreeView 被选中时，检查属性窗口中的可用事件。）

你可以使用哪个属性来获取用户双击项的引用？

选项卡标题同时列出了食谱名称和食谱类型（例如，“开胃菜”或“甜点”）。你可以使用哪个属性来获取食谱类型的引用？

我们的食谱层次结构有两个级别。只有当用户双击第二级项（例如，“Mini Crostini”，而不是“开胃菜”）时，你才希望添加新选项卡。你认为如何检查这一点？（提示：记住 GetType() 方法？）

要添加新的 TabItem，你需要先创建它，然后将其添加到 TabControl 的项集合中。你认为将如何操作？

刚添加的选项卡在 TabControl 中被选中会很方便。但这不会自动发生。你将设置 TabItem 的哪个属性来选中它？

### 你做得怎么样？

下面是我解决这个问题的方法。但请记住，编程中很少有绝对的东西。如果你对这些问题的回答不同，你能证明你的答案是正确的吗？

- **你认为作为布局根，最好使用哪种面板类型？**
  *我将使用 DockPanel，但其他面板也可以。*

- **TabItem 的 Header 中有两个项。你将如何实现？**
  *有其他方法，但最简单的可能是将两个标签放在一个面板中。我将使用 StackPanel。*

- **你认为应该响应哪个事件？**
  *我们将使用 MouseDoubleClick 事件。*

- **你可以使用哪个属性来获取用户双击项的引用？**
  *我们可以使用 SelectedItem。*

- **你可以使用哪个属性来获取食谱类型的引用？**
  *所选项的 Parent 属性将为我们提供引用，但我们需要将两个对象都强制转换为 TreeViewItem。*

- **只有当用户双击第二级项时，你才希望添加新选项卡。你认为如何检查这一点？**
  *你可以测试 Parent.GetType().Name == "TreeView"*

- **要添加新的 TabItem，你需要先创建它，然后将其添加到 TabControl 的项集合中。你认为将如何操作？**
  *我们可以调用 Items 集合的 Add() 方法。*

- **你将设置 TabItem 的哪个属性来选中它？**
  *我们只需将 IsSelected 设置为 true。*

