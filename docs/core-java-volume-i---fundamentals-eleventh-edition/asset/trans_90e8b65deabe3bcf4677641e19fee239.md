
当然，Java 开发环境也有拖放式 GUI 构建器。然而，了解“底层”究竟发生了什么仍然很重要，因为即使是这些工具中最好的，也通常需要手工调整。

### 11.2.1 布局管理器

让我们从回顾清单 10.4 中的程序开始，该程序使用按钮来改变框架的背景颜色。

这些按钮包含在一个 JPanel 对象中，并由 *流式布局管理器* 管理，这是面板的默认布局管理器。图 11.4 显示了当您向面板添加更多按钮时会发生什么。正如您所看到的，当没有更多空间时，就会开始新的一行。

![](img/127bccebb2cfadea3f02579edaad63c3_663_0.png)

**图 11.4** 由流式布局管理的包含六个按钮的面板

此外，即使当用户调整框架大小时，按钮也保持在面板中居中（见图 11.5）。

![](img/127bccebb2cfadea3f02579edaad63c3_663_1.png)

**图 11.5** 改变面板大小会自动重新排列按钮。

一般来说，*组件* 被放置在 *容器* 内部，而 *布局管理器* 决定组件在容器中的位置和大小。

按钮、文本字段和其他用户界面元素扩展自 Component 类。组件可以放置在容器（如面板）中。容器本身可以被放入其他容器中，因此 Container 类扩展了 Component。图 11.6 显示了 Component 的继承层次结构。

![](img/127bccebb2cfadea3f02579edaad63c3_664_0.png)

**图 11.6** Component 类的继承层次结构

> **注意：** 不幸的是，继承层次结构在两个方面有些不整洁。首先，顶级窗口（如 JFrame）是 Container 的子类，因此也是 Component 的子类，但它们不能放置在其他容器中。此外，JComponent 是 Container 的子类，而不是 Component。因此，您可以将其他组件添加到 JButton 中。（但是，这些组件不会被显示。）

每个容器都有一个默认布局管理器，但您始终可以设置自己的布局管理器。例如，语句

```java
panel.setLayout(new GridLayout(4, 4));
```

使用 GridLayout 类将组件布局为四行四列。当您向容器添加组件时，容器的 add 方法会将组件和任何放置指令传递给布局管理器。

| `java.awt.Container` | `1.0` |
|---|---|
| `void setLayout(LayoutManager m)` | 设置此容器的布局管理器。 |
| `Component add(Component c)` | |
| `Component add(Component c, Object constraints)` | `1.1` |
|  | 将组件添加到此容器并返回组件引用。 |

| `java.awt.FlowLayout` | `1.0` |
|---|---|
| `FlowLayout()` | |
| `FlowLayout(int align)` | |
| `FlowLayout(int align, int hgap, int vgap)` | |
|  | 构造一个新的 FlowLayout。align 参数是 `LEFT`、`CENTER` 或 `RIGHT` 之一。 |

### 11.2.2 边框布局

*边框布局管理器* 是每个 `JFrame` 的内容窗格的默认布局管理器。与完全控制每个组件位置的流式布局管理器不同，边框布局管理器允许您选择希望将每个组件放置在哪里。您可以选择将组件放置在内容窗格的中心、北、南、东或西（见图 11.7）。

例如：

```java
frame.add(component, BorderLayout.SOUTH);
```

边缘组件首先布局，剩余可用空间由中心组件占据。当容器调整大小时，边缘组件的尺寸不变，但中心组件会改变大小。通过指定 `BorderLayout` 类的常量 `CENTER`、`NORTH`、`SOUTH`、`EAST` 或 `WEST` 来添加组件。并非所有位置都需要被占据。如果您不提供任何值，则假定为 `CENTER`。

![](img/127bccebb2cfadea3f02579edaad63c3_666_0.png)

**图 11.7** 边框布局

> **注意：** BorderLayout 常量被定义为字符串。例如，`BorderLayout.SOUTH` 被定义为字符串 "South"。这比使用字符串更安全。如果您不小心拼错了字符串，例如 `frame.add(component, "south")`，编译器不会捕获该错误。

与流式布局不同，边框布局会让所有组件扩展以填充可用空间。（流式布局让每个组件保持其首选大小。）当您添加按钮时，这就会成为一个问题：

```java
frame.add(yellowButton, BorderLayout.SOUTH); // 不要这样做
```

图 11.8 显示了使用上述代码片段时会发生什么。按钮会扩展以填充框架的整个南部区域。而且，如果您再向南部区域添加另一个按钮，它只会替换掉第一个按钮。

![](img/127bccebb2cfadea3f02579edaad63c3_666_1.png)

**图 11.8** 由边框布局管理的单个按钮

要解决这个问题，请使用额外的面板。例如，请看图 11.9。屏幕底部的三个按钮都包含在一个面板中。该面板被放入内容窗格的南部区域。

![](img/127bccebb2cfadea3f02579edaad63c3_667_0.png)

**图 11.9** 放置在框架南部区域的面板

要实现这种配置，首先创建一个新的 JPanel 对象，然后将各个按钮添加到面板中。面板的默认布局管理器是 FlowLayout，对于这种情况这是一个不错的选择。使用您之前见过的 add 方法将各个按钮添加到面板中。按钮的位置和大小由 FlowLayout 管理器控制。这意味着按钮在面板中保持居中，并且不会扩展以填充整个面板区域。最后，将面板添加到框架的内容窗格中。

```java
var panel = new JPanel();
panel.add(yellowButton);
panel.add(blueButton);
panel.add(redButton);
frame.add(panel, BorderLayout.SOUTH);
```

边框布局会扩展面板的大小以填充整个南部区域。

| `java.awt.BorderLayout` | `1.0` |
|---|---|
| • `BorderLayout()` | |
| • `BorderLayout(int hgap, int vgap)` | 构造一个新的 BorderLayout。 |

### 11.2.3 网格布局

网格布局像电子表格一样，将所有组件按行和列排列。所有组件都被赋予相同的大小。图 11.10 中的计算器程序使用网格布局来排列计算器按钮。当您调整窗口大小时，按钮会随之增大和缩小，但所有按钮都具有相同的大小。

![](img/127bccebb2cfadea3f02579edaad63c3_668_0.png)

**图 11.10** 一个计算器

在网格布局对象的构造函数中，您需要指定所需的行数和列数。

```java
panel.setLayout(new GridLayout(4, 4));
```

添加组件时，从第一行的第一个条目开始，然后是第一行的第二个条目，依此类推。

```java
panel.add(new JButton("1"));
panel.add(new JButton("2"));
```

当然，很少有应用程序会有像计算器界面那样严格的布局。在实践中，小网格（通常只有一行或一列）可以用于组织窗口的局部区域。例如，如果您想要一行大小相同的按钮，可以将按钮放入由单行网格布局管理的面板中。

| `java.awt.GridLayout` | `1.0` |
|---|---|
| • `GridLayout(int rows, int columns)` | |
| • `GridLayout(int rows, int columns, int hgap, int vgap)` | |
| 构造一个新的 GridLayout。rows 和 columns 中的一个（但不能同时）可以为零，表示每一行或每一列的组件数量任意。 | |

## 11.3 文本输入

我们终于可以开始介绍 Swing 用户界面组件了。我们从允许用户输入和编辑文本的组件开始。您可以使用 JTextField 和 JTextArea 组件进行文本输入。文本字段只能接受一行文本；文本区域可以接受多行文本。JPasswordField 接受一行文本但不会显示内容。

这三个类都继承自一个名为 JTextComponent 的类。您无法自己构造 JTextComponent，因为它是一个抽象类。另一方面，正如 Java 中经常出现的情况，当您查阅 API 文档时，可能会发现您要找的方法实际上位于父类 JTextComponent 中，而不是派生类中。例如，获取或设置文本字段或文本区域中文本的方法实际上位于 JTextComponent 中。

| `javax.swing.text.JTextComponent` | `1.2` |
|---|---|
| `String getText()` | |
| `void setText(String text)` | 获取或设置此文本组件的文本。 |
| `boolean isEditable()` | |
| `void setEditable(boolean b)` | 获取或设置 editable 属性，该属性决定用户是否可以编辑此文本组件的内容。 |

### 11.3.1 文本字段

向窗口添加文本字段的通常方法是将其添加到面板或其他容器中——就像添加按钮一样：

```java
var panel = new JPanel();
var textField = new JTextField("Default input", 20);
panel.add(textField);
```

这段代码添加了一个文本字段，并通过将字符串 "Default input" 放入其中来初始化它。此构造函数的第二个参数设置宽度。在这种情况下，宽度是 20“列”。不幸的是，列是一个相当不精确的度量。一列是您用于文本的字体中一个字符的预期宽度。其想法是，如果您预计输入最多为 n 个字符，则应将 n 指定为列宽。在实践中，这种度量效果不太好，为了安全起见，您应该将最大输入长度加 1 或 2。另外，请记住
