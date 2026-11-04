
```csharp
// Fig. 14.20: LabelTextBoxButtonTestForm.cs
// Using a TextBox, Label and Button to display
// the hidden text in a password TextBox.
using System;
using System.Windows.Forms;

namespace LabelTextBoxButtonTest
{
    // Form that creates a password TextBox and
    // a Label to display TextBox contents
    public partial class LabelTextBoxButtonTestForm : Form
    {
        // default constructor
        public LabelTextBoxButtonTestForm()
        {
            InitializeComponent();
        }

        // display user input in Label
        private void displayPasswordButton_Click(object sender, EventArgs e)
        {
            // display the text that the user typed
            displayPasswordLabel.Text = inputPasswordTextBox.Text;
        }
    }
}
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_447_0.png)

Fig. 14.20 | 用于在密码框中显示隐藏文本的程序。

首先，通过将控件（一个 TextBox、一个 Button 和一个 Label）拖放到 Form 上来创建 GUI。控件定位后，将其名称在属性窗口中从默认值---textBox1、button1 和 label1---更改为更具描述性的 displayPasswordLabel、displayPasswordButton 和 inputPasswordTextBox。属性窗口中的 (Name) 属性使我们能够更改控件的变量名。Visual Studio 创建必要的代码并将其放置在文件 LabelTextBoxButtonTestForm.Designer.cs 中部分类的 InitializeComponent 方法中。

我们将 displayPasswordButton 的 Text 属性设置为 "Show Me"，并清空 displayPasswordLabel 的 Text，使其在程序开始执行时为空。displayPasswordLabel 的 BorderStyle 属性设置为 Fixed3D，使我们的 Label 具有三维外观。我们还将其 TextAlign 属性更改为 MiddleLeft，以便 Label 的文本在其顶部和底部之间居中显示。当将 UseSystemPasswordChar 设置为 true 时，inputPasswordTextBox 的密码字符由用户系统设置决定。

我们通过在设计模式下双击此控件为 displayPasswordButton 创建事件处理程序。我们在事件处理程序的主体中添加了第 23 行。当用户在正在执行的应用程序中单击 Show Me 按钮时，第 23 行获取用户在 inputPasswordTextBox 中输入的文本并将其显示在 displayPasswordLabel 中。

## 14.6 组框和面板

GroupBoxes 和 Panels 用于在 GUI 上排列控件。GroupBoxes 和 Panels 通常用于对功能相似的多个控件或在 GUI 中相关的多个控件进行分组。当 GroupBox 或 Panel 被移动时，其中的所有控件一起移动。此外，GroupBoxes 和 Panels 还可用于同时显示或隐藏一组控件。当您修改容器的 Visible 属性时，它会切换其中所有控件的可见性。

这两个控件的主要区别在于，GroupBoxes 可以显示标题（即文本）且不包含滚动条，而 Panels 可以包含滚动条且不包含标题。GroupBoxes 默认具有细边框；Panels 可以通过更改其 BorderStyle 属性来设置边框。图 14.21–14.22 分别列出了 GroupBoxes 和 Panels 的常见属性。

> **外观与感觉观察 14.2**
> Panels 和 GroupBoxes 可以包含其他 Panels 和 GroupBoxes 以实现更复杂的布局。

> **外观与感觉观察 14.3**
> 您可以通过在 GroupBox 或 Panel 内锚定和停靠控件来组织 GUI。然后可以将 GroupBox 或 Panel 锚定或停靠在 Form 内。这将控件划分为可轻松排列的功能“组”。

| GroupBox 属性 | 描述 |
|---|---|
| Controls | GroupBox 包含的控件集合。 |
| Text | 指定显示在 GroupBox 顶部的标题文本。 |

Fig. 14.21 | GroupBox 属性。

| Panel 属性 | 描述 |
|---|---|
| AutoScroll | 指示当 Panel 太小而无法显示其所有控件时是否出现滚动条。默认值是 false。 |
| BorderStyle | 设置 Panel 的边框。默认值是 None；其他选项是 Fixed3D 和 FixedSingle。 |
| Controls | Panel 包含的控件集合。 |

Fig. 14.22 | Panel 属性。

要创建 GroupBox，请从 Toolbox 将其图标拖到 Form 上。然后，从 Toolbox 将新控件拖入 GroupBox。这些控件被添加到 GroupBox 的 Controls 属性中并成为 GroupBox 的一部分。GroupBox 的 Text 属性指定 GroupBox 顶部的标题。

要创建 Panel，请从 Toolbox 将其图标拖到 Form 上。然后，您可以通过从 Toolbox 将它们拖到 Panel 上直接向 Panel 添加控件。要启用滚动条，请将 Panel 的 AutoScroll 属性设置为 true。如果 Panel 被调整大小且无法显示其所有控件，则会出现滚动条（图 14.23）。滚动条可用于在设计时和执行时查看 Panel 中的所有控件。在图 14.23 中，我们将 Panel 的 BorderStyle 属性设置为 FixedSingle，以便您可以在 Form 中看到 Panel。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_449_0.png)

Fig. 14.23 | 创建带有滚动条的 Panel。

图 14.24 中的程序使用 GroupBox 和 Panel 来排列 Buttons。当单击这些 Buttons 时，它们的事件处理程序会更改 Label 上的文本。

```csharp
// Fig. 14.24: GroupBoxPanelExampleForm.cs
// Using GroupBoxes and Panels to arrange Buttons.
using System;
using System.Windows.Forms;

namespace GroupBoxPanelExample
{
    // Form that displays a GroupBox and a Panel
    public partial class GroupBoxPanelExampleForm : Form
    {
        // default constructor
        public GroupBoxPanelExampleForm()
        {
            InitializeComponent();
        }
    }
```

Fig. 14.24 | 使用 GroupBoxes 和 Panels 安排 Buttons。（第 1 部分，共 2 部分。）

```csharp
16    // event handler for Hi Button
17    private void hiButton_Click(object sender, EventArgs e)
18    {
19        messageLabel.Text = "Hi pressed";  // change text in label
20    }
21
22    // event handler for Bye Button
23    private void byeButton_Click(object sender, EventArgs e)
24    {
25        messageLabel.Text = "Bye pressed";  // change text in label
26    }
27
28    // event handler for Far Left Button
29    private void leftButton_Click(object sender, EventArgs e)
30    {
31        messageLabel.Text = "Far Left pressed";  // change text in label
32    }
33
34    // event handler for Far Right Button
35    private void rightButton_Click(object sender, EventArgs e)
36    {
37        messageLabel.Text = "Far Right pressed";  // change text in label
38    }
39
40    }
41  }
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_450_0.png)

**Fig. 14.24** | 使用 GroupBoxes 和 Panels 安排 Buttons。（第 2 部分，共 2 部分。）

mainGroupBox 有两个 Buttons——hiButton（显示文本 Hi）和 byeButton（显示文本 Bye）。Panel（名为 mainPanel）也有两个 Buttons，leftButton（显示文本 Far Left）和 rightButton（显示文本 Far Right）。mainPanel 的 AutoScroll 属性设置为 true，允许在 Panel 的内容需要比 Panel 可视区域更多的空间时出现滚动条。Label（名为 messageLabel）最初为空。要向 mainGroupBox 或 mainPanel 添加控件，Visual Studio 会调用每个容器 Controls 属性的 Add 方法。此代码放置在文件 GroupBoxPanelExampleForm.Designer.cs 中部分类中。

四个 Buttons 的事件处理程序位于第 18–39 行。第 20、26、32 和 38 行更改 messageLabel 的文本以指示用户按下了哪个 Button。

## 14.7 CheckBoxes 和 RadioButtons

C# 有两种状态按钮，可以处于开/关或真/假状态——CheckBoxes 和 RadioButtons。与类 Button 类似，类 CheckBox 和 RadioButton 都派生自类 ButtonBase。

### 14.7.1 CheckBoxes

CheckBox 是一个小方块，要么为空白，要么包含复选标记。当用户单击 CheckBox 以选择它时，方块中会出现复选标记。如果用户再次单击 CheckBox 以取消选择它，则会删除复选标记。您还可以通过将 ThreeState 属性设置为 true 来配置 CheckBox 在三种状态（已选中、未选中和不确定）之间切换。一次可以选中任意数量的 CheckBoxes。图 14.25 中列出了常见的 CheckBox 属性和一个常见事件。

| CheckBox 属性和事件 | 描述 |
| --- | --- |
| **常见属性** | |
| Appearance | 默认情况下，此属性设置为 Normal，CheckBox 显示为传统的复选框。如果设置为 Button，CheckBox 会显示为按钮，当 CheckBox 被选中时看起来像是被按下。 |
| Checked | 指示 CheckBox 是否被选中（包含复选标记）或未选中（空白）。此属性返回一个 bool 值。默认值是 false（未选中）。 |
| CheckState | 使用 CheckState 枚举的值指示 CheckBox 是已选中还是未选中（Checked、Unchecked 或 Indeterminate）。当不确定状态应为 Checked 还是 Unchecked 时使用 Indeterminate。当 CheckState 设置为 Indeterminate 时，CheckBox 通常会被着色。 |
| Text | 指定 CheckBox 右侧显示的文本。 |
| ThreeState | 当此属性为 true 时，CheckBox 有三种状态——已选中、未选中和不确定。默认情况下，此属性为 false，CheckBox 只有两种状态——已选中和未选中。当为 true 时，Checked 对已选中和不确定状态都返回 true。 |
| **常见事件** | |
| CheckedChanged | 每当 Checked 或 CheckState 属性更改时都会生成。此事件是 CheckBox 的默认事件。当用户在设计视图中双击 CheckBox 控件时，会为此事件生成一个空事件处理程序。 |

Fig. 14.25 | CheckBox 属性和事件。

图 14.26 中的程序允许用户选择 CheckBoxes 来更改 Label 的字体样式。一个 CheckBox 的事件处理程序应用粗体，另一个的事件处理程序应用斜体。如果两个 CheckBoxes 都被选中，则字体样式设置为粗体和斜体。最初，没有任何 CheckBox 被选中。
