

通过这样做，可以在很大程度上改进它们。在我们使用的 Scala 实现中，这意味着对 Java GUI 库存在依赖。

Java 最初发布时，只有一个 GUI 库，称为抽象窗口工具包 Abstract Windowing Toolkit，AWT。AWT 库通过直接调用操作系统或窗口环境来构建 GUI 的元素。这使 AWT 在速度方面具有显著优势。然而，它也带来了显著的限制。由于 Java 的跨平台特性，他们只在 AWT 中包含了几乎所有平台上都存在的元素。它们是 GUI 构建的最基本部分，如窗口、按钮、文本框等。这些元素由底层平台绘制，并且始终看起来像底层平台。

外观的限制和组件类型的有限数量导致为 Java 标准创建了第二个 GUI 库。这个第二个库称为 Swing，它是一个“纯”Java 库。这意味着 Swing 中的所有代码都是用 Java 编写的。它使用对 AWT 的调用来实现功能，但不会直接调用 Java 本身之外的任何东西。Swing 库包含大量比 AWT 提供的更强大、更灵活的 GUI 元素。它还包括使 GUI 元素的呈现方式不同而不必看起来像底层系统的能力。最初这种灵活性是以速度为代价的。随着时间的推移，进行了各种优化，现在只要程序员不做任何愚蠢的事情来减慢速度，Swing 运行得非常好。

Scala 有自己的库，它是 Swing 的包装器。它对 Swing 进行调用，我们称之为 Swing，但我们以独特于 Scala 的方式与之交互。这使事情变得更简单，也是本书如此早地包含 GUI 的一个重要原因。

各种 GUI 库层层构建的方式使得我们将使用其中每个库的一点。Scala Swing 库是我们将重点关注的大部分时间。我们使用的类型位于 scala.swing 和 scala.swing.event 包中。每隔一段时间我们可能不得不回到 Java Swing 库，它位于 javax.swing¹ 以及其下的各个包中。偶尔甚至需要降到 AWT。我们将在下一章中使用相当数量的 AWT 类型。它们来自 java.awt 包及其子包。

## 11.2 GUI 组件

GUI 的构建非常模块化。它们是通过组合不同的称为组件的部件构建的。我们使用的特定类型，例如 **Button**，是更通用的 **Component** 类型的子类型。子类型化在第 7.5.3 节中简要讨论，将在第 19 章中更详细地讨论。

### 11.2.1 框架和窗口

要显示 GUI，我们需要首先打开一个窗口。有不止一种类型的窗口。我们将用作应用程序主窗口的类型称为

¹ 你可能会对包名中的 java x 感到好奇。Java 中有几个库以这种方式开头。这些是最初作为非标准库扩展包开始的库。当它们被纳入标准库时，原始名称被保留以免破坏使用它们的现有代码。

![](img/157fcf510c119278e4b1267c62717fa8_284_0.png)

**图 11.1：** 这是一个由简单脚本打开的示例窗口。窗口为 500x500 像素，标题为“First GUI”。关闭窗口时，脚本将退出。

a **MainFrame**。其他选项包括常规 **Frame** 和 **Dialog**。**MainFrame** 的优点是关闭时终止程序。以下是一个可以运行以打开窗口的小脚本。

```
import scala.swing._

val frame=new MainFrame {
	title = "First GUI"
	size = new Dimension(500,500)
}

frame.visible=true
```

运行它时应该会弹出一个看起来像图 11.1 的窗口。这个脚本中有很多值得描述的内容。我们从一个 **import** 语句开始。下划线是一个通配符，告诉 Scala 导入 `scala.swing` 包中的所有内容。我们在这里不需要这样做，但随着我们继续下去会更有用，因为我们将使用这个包中的许多不同类型。

导入之后，我们创建 **Frame** 并将其存储在名为 **frame** 的 **val** 中。这里的语法可以这样读。我们正在创建一个新的 **MainFrame** 对象，花括号括起我们想要放入此对象的内容。在花括号内，我们更改了一些内容，使其不会使用 MainFrame 的默认值。第一个是设置标题。它出现在窗口顶部。之后我们设置大小。大小的类型为 Dimension（技术上是 java.awt.Dimension）。在这个脚本中，我们创建一个新的 Dimension 对象，宽度和高度都设置为 500。

创建 frame 之后，有一行将 frame 中的 visible 值设置为 true。这会导致窗口弹出并可见。²

### 11.2.2 组件

为了使 GUI 执行某些操作，我们需要向其中添加其他组件。scala.swing 包中有许多不同的组件。下面列出了部分内容及其简要描述。

- **Button** - 一个标准的按钮，点击后可执行操作。通过调用 Button(text:String)(action : => Unit) 创建。
- **CheckBox** - 一个可选择或取消选择的带标签框。使用 new CheckBox(label:String) 创建。包含 selected:Boolean，可告诉您框当前是否被选中。
- **ComboBox** - 这是一个下拉框，允许用户从多个选项中选择。使用 new ComboBox(items:Seq[A]) 创建。内部有一个名为 selection 的对象，用于处理当前选择。使用 selection.index 获取当前选择的索引。
- **EditorPane** - 一个复杂的文本元素，显示多行和格式。使用 new EditorPane(contentType:String,text:String) 创建。
- **Label** - 一个简单、非活动的标签。使用 new Label(text:String) 创建。
- **ListView** - 一个可选择的列表信息显示。使用 new ListView(items:Seq[A]) 创建。内部有一个名为 selection 的对象，用于处理列表上的选择。您可以使用集合 selection.indices 与所选的索引值交互。
- **PasswordField** - 一个隐藏输入数据的文本字段。如果没有默认值，使用 new PasswordField 创建；如果想使用默认值，使用 new PasswordField(text:String)。有一个名为 text:String 的成员，可告诉您当前输入的文本。
- **ProgressBar** - 用于显示进度的图形显示。具有名为 min:Int、max:Int 和 value:Int 的字段，用于控制/读取进度显示。
- **RadioButton** - 一个可选择的按钮，可以放入 ButtonGroup 中以便一次只能选择一个。有一个名为 selected:Boolean 的字段，可告诉您当前是否被选中。
- **ScrollBar** - 一个水平或垂直的滚动条。ScrollBar 具有 minimum、maximum 和 value，均为 Ints，可让您设置或检查其位置。很少有应用程序会直接使用 ScrollBar。您通常想要的功能是下一节中描述的 ScrollPane 的一部分。

有一些组件可以容纳多个其他组件并控制布局方式。这些可以嵌套在彼此内部以产生程序员想要的整体效果。

简单的容器组件，仅定位和调整其内容的大小，称为面板。还有更复杂的容器，提供一些用户交互。这些称为窗格。下面列出了 scala.swing 中包含的不同面板和窗格。

- **BorderPanel** - 可在 North、South、East、West 和 Center 位置容纳多达五个不同的组件。组件作为 (Component,Position) 的元组添加到 BorderPanel 的布局中。Positions 属于 BorderPanel.Position（例如，BorderPanel.Position.North）。
- **BoxPanel** - 可容纳可变数量的组件，方向为垂直或水平，每个组件占用其所需空间。创建新的 BoxPanel 时，您会传递一个方向（例如 new BoxPanel(Orientation.Vertical)）。组件可以一次一个地添加到 contents（例如 contents+=Button("text")(action)）。
- **FlowPanel** - 可容纳多个组件，从左到右布局，当变得太长时像文字处理器中的文本一样换行。您可以在构造时传递可变长度的 Components 列表作为参数，或将组件添加到 contents。
- **GridBagPanel** - 一个灵活且强大的容器，将内容保存在可变大小的网格中。组件作为 (Component,GridBagPanel.Constraints) 的元组添加到布局中。此面板很复杂，本章中不会使用。
- **GridPanel** - 包含组件的规则网格。您在创建时指定网格的行数和列数（例如 new GridPanel(3,4) 表示 3 行 4 列）。内部的 Components 添加到面板的 contents。
- **ScrollPane** - 一个容纳单个 Component 的窗格，可作为构造参数传入。如果内容 Component 比此显示的更大，则会自动添加滚动条以便用户滚动。
- **SplitPane** - 一个容纳两个 Components 的容器。它们被一个用户可以按需移动的栏分隔开。在构造时应提供方向和两个子组件（例如 new SplitPane(Orientation.Horizontal,leftComp,rightComp)）。
- **TabbedPane** - 这可以容纳多个不同的 Components。一次只显示一个 Component，但所有它们的标签始终显示。用户可以点击标签将一个带到前面。您可以通过将它们添加到 TabbedPane 内部的 page 对象来添加 Components。添加到其中的是 Page 对象。每个 Page 对象通过为其提供一个用于标签的 String 和应放在该标签下的 Component 来构造（例如 pages += new Page("A Tab",tabComponent)）。

单独的这些都不足以创建复杂的 GUI。相反，通常的做法是将面板和窗格嵌套在彼此内部以创建所需的效果。

为了说明这一点，我们将为本章中将构建的一个小程序布局 GUI。该程序将类似于数字食谱书。该程序应能够存储多个食谱。对于每个食谱，它应允许用户指定配料及其用量，以及烹饪说明的文字描述。

