
假设我们向法语翻译了 19 个字符串并点击了其中 17 个的 `Done` 标记，`lrelease` 会产生以下输出：

更新 '`spreadsheet_de.qm`'（0 已完成，0 未完成）

忽略了 98 个未翻译源文本

更新 '`spreadsheet_fr.qm`'

生成了 19 条翻译（17 已完成，2 未完成）

忽略了 79 个未翻译源文本

运行应用程序时，未翻译的字符串将以原始语言显示。发布版会忽略 `Done` 标记；它可以供翻译人员识别哪些翻译已完成，哪些需要重新审视。

当我们修改应用程序源代码时，翻译文件可能会过期。解决方案是再次运行更新，为新字符串提供翻译并重新生成 `.qm` 文件。有些开发团队发现频繁运行更新很有用，而另一些团队则倾向于等到应用程序几乎准备发布。

更新和 `Qt Linguist` 工具非常智能。不再使用的翻译将保留在 `.ts` 文件中，以备后续发布之用。

关于 `Qt Linguist`、更新和发布的更多信息，请参阅 `http://doc.trolltech.com/4.3/linguist-manual.html` 中的 `Qt Linguist` 手册。该手册包含了对 `Qt Linguist` 用户界面的完整解释以及为程序员提供的分步教程。

## 19. 外观与外观定制

![](img/5a524abdf0b0d58fa99d30abb4463611_707_0.png)

- 使用 `Qt` 样式表
- 自定义 `QStyle`

在某些情况下，我们可能想要更改 `Qt` 内置控件的外观和外观。我们可能只想进行一些微定制以稍微调整审美，或者我们希望实现一种完全全新的样式，为我们的应用程序或系列应用程序提供独特的视觉。无论何种情况，重新定义 `Qt` 内置控件外观都有三种主要方法：

- 我们可以对单个控件类进行子类，并重新实现它们的绘制和鼠标事件处理器。这提供了完全控制，但涉及大量工作。这意味着我们必须遍历所有的代码和 `Qt Designer` 表单，将所有 `Qt` 控件类的出现更改为我们的子类。
- 我们可以自定义 `QStyle` 或预定义的样式（如 `QStyle`）。这种方法非常强大；`Qt` 本身使用它来在其支持的不同平台上提供原生的视觉效果。
- 从 `Qt 4.2` 开始，我们可以使用 `Qt` 样式表，这是一种灵感来自 `HTML CSS`（级联样式表）的机制。由于样式表是在运行时解释的纯文本文件，因此使用它们不需要编程知识。

我们可以通过样式表文件、使用 `Qt Designer` 的样式表编辑器 `qss-line` 选项或在开发期间在应用程序中嵌入 `QText` 来使用样式表。

我们已经涵盖了第一种方法所需的技巧（第 5 章和第 7 章），尽管我们的重点在创建自定义控件上。在本章中，我们将回顾最后两种方法。我们将展示两种自定义样式：指定为样式表的 `Candy` 样式，以及实现为 `QStyle` 子类的 `Bronze` 样式（见图 19.1）。为了保持示例的大小在可控范围内，这两种样式都专注于 `Qt` 控件的一个仔细选择的子集。

### 图 19.1. 本章介绍的自定义样式

[查看全尺寸图像]

## 使用 Qt 样式表

`Qt` 样式表深受 `CSS` 启发，但针对控件进行了调整。一个样式表由影响控件渲染的样式规则组成。这些规则以纯文本指定。由于样式表是在运行时解析的，我们可以通过以下方式为 `Qt` 应用程序指定样式表以尝试不同的设计：使用样式表文件、使用 `Qt Designer` 的样式表编辑器（`qss-line` 选项），或者在开发期间在应用程序中嵌入 `QText`。

样式表应用在当前激活的 `QStyle`（例如 `QWindowsVistaStyle` 或 `QPlastiqueStyle`）之上。因为创建样式表不涉及任何子类化，它们是对比现有控件进行微定制的理想选择。例如，我们希望使用黄色作为应用程序中所有 `QLineEdit` 的背景颜色。可以使用以下样式来实现：

> `Qt 4.3` 中的 `QMacStyle` 不支持样式表。预计这将在未来的发布中得到解决。

```
QLineEdit {
  background-color: yellow;
}
```

在 `CSS` 术语中，`QLineEdit` 被称为选择器，`background-color` 是属性，而 `yellow` 是值。

对于这种定制，使用样式表产生的结果比折腾控件的调色板（`palette`）更可靠。这是因为 `QPalette` 的条目（`Base`、`Button`、`Highlight` 等）被不同样式使用的方式也不同。例如，`QWindowsStyle` 使用 `Base` 调色板条目来填充只读组合框的背景，而 `QPlastiqueStyle` 则出于此目的使用 `Button`。此外，某些样式使用硬编码图像来渲染某些元素，而不是完全使用调色板，通过如下：

![](img/5a524abdf0b0d58fa99d30abb4463611_708_0.png)

![](img/5a524abdf0b0d58fa99d30abb4463611_708_1.png)

相比之下，样式表保证了无论激活何种 `Style`，指定的颜色都将是被使用的。

`QApplication::setStyleSheet()` 为整个应用程序设置样式表：

```
qApp->setStyleSheet("QLineEdit { background-color: yellow;");
```

我们也可以使用 `QWidget::setStyleSheet()` 在控件及其子控件上使用样式表。例如：

```
dialog->setSheet("QLineEdit { background-color: yellow;");
```

如果我们直接在 `QLineEdit` 上使用样式表，可以省略 `QLineEdit` 选择器和括号：

```
lineEdit->setSheet("background-color: yellow;");
```

到目前为止，我们只在一个单个控件类上设置了单个属性。在实践中，样式规则通常会组合在一起。例如，以下规则设置了六个控件类及其子类的前景颜色和背景颜色：

```
QCheckBox, QComboBox, QLineEdit, QListView, QRadioButton, QSpinBox { color: #050505;
background-color: yellow;
}
```

颜色可以通过名称、通过 `#RRGGBB` 格式的 `HTML` 风格字符串，或通过 `RGB` 或 `RGBA` 值指定：

```
QLineEdit {
color: rgb(0, 88, 152);
background-color: rgba(97%, 80%, 9%, 50%);
}
```

使用颜色名称时，可以使用任何被 `Color::setNamedColor()` 函数识别的名称。对于 `RGB`，我们必须指定红色、绿色和蓝色分量，每个分量的范围为 0 到 255。`RGBA` 允许我们指定第四个分量作为 `alpha` 值，这对应于颜色的透明度。而不是均匀颜色，我们还可以指定

```
QLineEdit {
  color: palette(Base);
  background-color: qlineargradient(x1: 0, y1: 0, x2: 1, y2: 1,
  stop: 0 white, stop: 0.4 gray,
  stop: 1 green;
}
```

在第 8 章（第 184 页）中描述的三种梯度类型可用 `qlineargradient()`, `radialgradient()` 和 `conicalgradient()`。其语法在样式表图像引用文档中解释。

使用 `background-image` 属性，我们可以为背景指定图像：

```
QLineEdit {
  color: rgb(0, 88, 152);
  background-image: url(:/images/yellow-bg.png);
}
```

默认情况下，背景图像位于控件的左上角（不包括使用 `margin` 指定间距），并水平垂直重复以填充整个控件。可以通过 `background-position` 和 `background-repeat` 属性进行配置。例如：

```
QLineEdit {
  background-image: url(:/images/yellow-bg.png);
  background-position: top right;
  background-repeat: repeat;
}
```

如果我们同时指定背景图像和背景颜色，背景颜色将透过图像的半透明区域。

到目前，我们使用的所有选择器都是类名。还有其他几种可以使用的选择器；它们列在图 19.2 中。例如，如果我们想为 `OK` 和取消按钮使用前景颜色，我们可以写道

### 图 19.2. 样式表选择器

| 选择器 | 示例 | 匹配的控件 |
| --- | --- | --- |
| 通用 | * | 任何控件 |
| 类型 | QDial |  |
| --- | --- |  |
|  |  | 给定类的实例，包括子类 |
| 类 | .QDial | 给定类的实例，不包括子类 |
| ID | QDial#ageDial | 具有给定对象名称的控件 |
| Qt 属性 | QDial[y="0"] | 某些属性设置为特定值的控件 |
| 子控件 | QFrame > QDial | 作为控件直接子节点的控件 |
| 后代 | QFrame QDial | 作为给定控件后代的控件 |

```
QPushButton[text="OK"] {
  color: green;
}
```

```
QPushButton[text="Cancel"] {
  color: red;
}
```

这种选择器语法适用于任何 `Qt` 属性，尽管我们必须记住，当属性在样式不知的情况下发生变化时，样式是察觉到的。选择器可以以多种方式组合；例如，要选择所有名为 "`okButton`" 且 `x` 和 `y` 属性为 0，同时又是名为 "`frame`" 的 `QFrame` 直接子节点的 `QPushButton`，我们可以这样写：

```
QFrame#frame > QPushButton[x="0"][y="0"]#okButton {
  ..
```

在显示包含大量行编辑器和组合框的大表单应用程序中（例如各种政府机构使用的程序），使用黄色背景色作为必填字段是很常见的。假设我们想这种惯应用到应用程序中。首先，我们将从这个样式表开始：

```
*[mandatory="true"] {
  background-color: yellow;
}
```

尽管 `Qt` 中任何地方都没有定义 `mandatoryField` 属性，但我们可以通过调用 `QObject::setProperty()` 轻松地创建一个。从 `Qt 4.2` 开始，动态设置不存在属性的值会创建该属性。例如：

```
nameLineEdit->setProperty("mandatoryField", true);
genderComboBox->setProperty("mandatoryField", true);
ageSpinBox->setProperty("mandatoryField", true);
```

样式表不仅对控制颜色有用，它们还允许我们对控件元素的大小和位置进行各种调整。例如，可以使用以下规则将复选框和单选按钮指示器的大小增大 20 x 20 像素，并确保指示器与关联文本之间留有 8 像素：

```
QCheckBox::indicator, QRadioButton::indicator {
  width: 20px;
  height: 20px;
}
QCheckBox, QRadioButton {
  spacing: 8px;
```

注意第一个规则的选择器语法。如果我们只写 `QCheckBox` 而不是 `QCheckBox::indicator`，那么我们指定的将整个控件的尺寸，而不是指示器的尺寸。第一个规则如图 19.3 所示。

### 图 19.3. 设置 QCheckBox 的指示器大小

![](img/5a524abdf0b0d58fa99d30abb4463611_712_0.png)

如 `::indicator` 等子控件可以使用与控件相同的方式设置样式。

### 图 19.4. 最常见的自定义子控件

| 子控件 | 描述 |
| --- | --- |
| ::indicator | 复选框、单选按钮、可更改的菜单项或可更改的组框的指示器 |
| ::menu-indicator | 按钮的菜单指示器 |
| ::item | 菜单、菜单栏或状态栏项 |
| ::up-button | 计数器或滚动条的向上按钮 |
| ::down-button | 计数器或滚动条的向下按钮 |
| ::up-arrow | 计数器、滚动条或头部视图的箭头 |
| ::downarrow | 计数器、滚动条、头部视图或组合框的向下箭头 |
| ::drop-down | 组合框的下拉箭头 |
| ::title | 组框的标题 |

除了子控件外，样式表还可以引用特定的控件状态。例如，我们可能希望通过指定 `:hover` 状态，当鼠标悬停在复选框上时将其文本渲染为白色：

```
QCheckBox:hover {
  color: white;
}
```

状态通过使用单冒号 `: ` 表示；而子控件通过使用双冒号 `::` 表示。我们可以连续列出多个状态，每个状态之间用冒号隔开。在这种情况下，该规则仅在控件处于所有指定状态时生效。例如，以下规则仅在鼠标悬停在已选中的复选框上时应用：

```
QCheckBox:checked:hover {
  color: white;
}
```

如果我们希望规则在任何一个状态为真时应用，可以使用多个选择器，并用逗号分隔它们：

```
QCheckBox:hover, QCheckBox:checked {
  color: white;
}
```

使用感叹号 `!` 可以实现逻辑取反：

```
QCheckBox::!checked {
  color: blue;
}
```

状态可以与子控件结合：

```
QComboBox::drop-down:hover {
  image: url(:images/downarrow_bright.png);
}
```

图 19.5 列出了所有可用的样式表。

> 图 19.5. 样式表可访问的一些控件状态

| 状态 | 描述 |
| --- | --- |
| :disabled | 控件被停用 |
| :enabled | 控件已启用 |
| :focus | 控件具有输入焦点 |
| :hover | 鼠标悬停在控件上 |
| :pressed | 正在使用鼠标按下控件 |
| :checked | 按钮被选中 |
| :unchecked | 按钮未被选中 |
| :indeterminate | 按钮部分选中 |
| :open | 控件处于打开或展开状态 |
| :closed | 控件处于关闭或收起状态 |
| :on | 控件处于“开启”状态 |
| :off | 控件处于“关闭”状态 |

样式表还可以与其他技术结合使用，以执行更复杂的自定义。例如，假设我们想在 `QLineEdit` 内部放置一个微小的“删除”按钮，位于 `Qt` 文本的右侧。这涉及创建一个 `EraseButton` 类，并将其放置在 `QLineEdit` 之上（例如使用布局），但也要为按钮留出一些空间，以便输入的文本不会与删除按钮碰撞。通过子类化 `QStyle` 将是不方便的，因为我们必须为 `Qt` 中可能被使用的每种样式创建子类（`QWindowsStyle`、`QPlastiqueStyle` 等）。使用样式表，以下规则就能解决问题：

```
QLineEdit {
padding: 15px;
}
```

`padding` 属性允许我们指定顶部、右侧、底部和左侧的内距。例如，以下规则显示了 `QLineEdit` 的内边距：

```
QLineEdit {
  padding: 0px;
}
```

与大多数控件可以通过样式表自定义一样，图 19.6 所示的模型显示：

1. 内容矩形是最内层的矩形。
2. 内边距矩形包含内容。
3. 边框矩形围绕内边距。
4. 外边距矩形是最外层的矩形。

### 图 19.6. CSS 模型

![](img/5a524abdf0b0d58fa99d30abb4463611_716_0.png)

我们现在展示一个名为 `Candy` 的样式表。图 19.7 显示了样式化的控件。整个样式表作为随书附的 `qss/candy.qss` 提供。

### 图 19.7. Candy 中的控件

![](img/5a524abdf0b0d58fa99d30abb4463611_716_1.png)

对话框本身通过以下规则设置背景图像：

```
Dialog {
    background-image: url(:images/background.png);
}
```

以下规则设置了 `QLabel` 的颜色和字体属性：

```
QLabel {
    font: 9pt;
}
```

下一个规则定义了对话框的 `QLineEdit` 和其 `ListView` 的外观：

```
QLineEdit,
QListView {
  color: rgb(0, 0, 63);
  background-color: rgb(255, 255, 241);
  selection-color: white;
  selection-background-color: rgb(191, 31, 127);
  border: 2px groove gray;
  border-radius: 10px;
  padding: 2px 4px;
}
```
