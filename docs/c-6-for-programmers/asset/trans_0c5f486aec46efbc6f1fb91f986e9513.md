
```csharp
// Fig. 14.26: CheckBoxTestForm.cs
// Using CheckBoxes to toggle italic and bold styles.
using System;
using System.Drawing;
using System.Windows.Forms;

namespace CheckBoxTest
{
    // Form contains CheckBoxes to allow the user to modify sample text
    public partial class CheckBoxTestForm : Form
    {
        // default constructor
        public CheckBoxTestForm()
        {
            InitializeComponent();
        }

        // toggle the font style between bold and
        // not bold based on the current setting
        private void boldCheckBox_CheckedChanged(object sender, EventArgs e)
        {
            outputLabel.Font = new Font(outputLabel.Font,
                outputLabel.Font.Style ^ FontStyle.Bold);
        }

        // toggle the font style between italic and
        // not italic based on the current setting
        private void italicCheckBox_CheckedChanged(
            object sender, EventArgs e)
        {
            outputLabel.Font = new Font(outputLabel.Font,
                outputLabel.Font.Style ^ FontStyle.Italic);
        }
    }
}
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_452_0.png)

图 14.26 | 使用 CheckBoxes 切换斜体和粗体样式。

boldCheckBox 的 Text 属性设置为 Bold。italicCheckBox 的 Text 属性设置为 Italic。outputLabel 的 Text 属性设置为 Watch the font style change。创建控件后，我们定义它们的事件处理程序。在设计时双击 CheckBoxes 会创建空的 CheckedChanged 事件处理程序。

要更改 Label 的字体样式，请将其 Font 属性设置为新的 Font 对象（第22-23行和第31-32行）。Font 类位于 System.Drawing 命名空间中。此处使用的 Font 构造函数接受一个 Font 和一个新样式作为参数。参数 outputLabel.Font 使用 outputLabel 原始字体名称和大小。样式通过 FontStyle 枚举的成员指定，该枚举包含 Regular、Bold、Italic、Strikeout 和 Underline。（Strikeout 样式使文本显示一条删除线。）Font 对象的 Style 属性是只读的，因此只能在创建 Font 对象时设置。

## 14.7.2 使用位运算符组合字体样式

样式可以通过位运算符组合——位运算符是对信息位进行操作的运算符。所有数据在计算机中均表示为0和1的组合。每个0或1代表一个位。FontStyle（命名空间 System.Drawing）表示为一组位，其选择方式允许我们使用位运算符组合不同的 FontStyle 元素以创建复合样式。这些样式*并非互斥*，因此我们可以组合不同样式并移除它们，而不影响先前 FontStyle 元素的组合。

我们可以使用*逻辑或*（|）运算符或*逻辑异或*（^）运算符（又称XOR）组合各种字体样式。当*逻辑或*运算符应用于两个位时，如果两个位中至少有一个为1，则结果为1。使用*逻辑或*运算符组合样式的方式如下。假设 FontStyle.Bold 由位01表示，FontStyle.Italic 由位10表示。当我们使用*逻辑或*（|）组合这些样式时，得到位11。

```
01      =       Bold
10      =       Italic
--
11      =       Bold and Italic
```

*逻辑或*运算符有助于创建样式组合。然而，如果我们想*撤销*样式组合，就像我们在图14.26中所做的那样，会发生什么？

*逻辑异或*运算符使我们能够组合样式，并*撤销*现有的样式设置。当*逻辑异或*应用于两个位时，如果两个位值相同，则结果为0；如果两个位值不同，则结果为1。

使用*逻辑异或*组合样式的方式如下。再次假设 FontStyle.Bold 由位01表示，FontStyle.Italic 由位10表示。当我们对两种样式使用*逻辑异或*（^）时，得到位11。

```
01      =       Bold
10      =       Italic
--
11      =       Bold and Italic
```

现在，假设我们想从先前 FontStyle.Bold 和 FontStyle.Italic 的组合中*移除* FontStyle.Bold 样式。最简单的方法是再次对复合样式和 FontStyle.Bold 应用*逻辑异或*（^）运算符。

```
11      =       Bold and Italic
01      =       Bold
--
10      =       Italic
```

这是一个简单的示例。考虑有五个 FontStyle 值（Bold、Italic、Regular、Strikeout 和 Underline），共产生16种 FontStyle 组合时，使用位运算符组合 FontStyle 值的优势就更加明显。使用位运算符组合字体样式大大减少了检查所有可能字体组合所需的代码量。

在图14.26中，我们需要设置 FontStyle，使文本原来不是粗体则显示为粗体，反之亦然。第23行使用*位异或运算符*来实现这一点。如果 outputLabel.Font.Style 是粗体，则结果样式不是粗体。如果文本原本是斜体，则结果样式为粗体斜体，而不仅仅是粗体。第32行对 FontStyle.Italic 的处理相同。

如果我们不使用位运算符来复合 FontStyle 元素，就必须测试当前样式并相应地更改它。在 boldCheckBox_CheckedChanged 中，我们可以测试常规样式并将其设为粗体，测试粗体样式并将其设为常规，测试斜体样式并将其设为粗斜体，测试斜体粗体样式并将其设为斜体。这很繁琐，因为每添加一个新样式，组合数就会翻倍。为下划线添加一个 CheckBox 将需要额外测试8种样式。为删除线添加一个 CheckBox 将需要额外测试16种样式。

## 14.7.3 单选按钮

单选按钮（由类 RadioButton 定义）与 CheckBoxes 相似，也有两种状态——选中和未选中（也称为取消选中）。但是，RadioButtons 通常以组的形式出现，在组中一次只能选择一个 RadioButton。在组中选择一个 RadioButton 会强制取消选择所有其他 RadioButton。因此，RadioButtons 用于表示一组互斥选项（即不能同时选择多个选项的集合）。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_454_0.png)

> **观感观察 14.4**
> 
> *当用户应在一个组中只选择一个选项时，使用 RadioButtons。当用户应能在一个组中选择多个选项时，使用 CheckBoxes。*

添加到一个容器中的所有 RadioButtons 都处于同一组。要将 RadioButtons 分成多个组，必须将它们添加到不同的容器中，例如 GroupBoxes 或 Panels。RadioButton 的常见属性和一个常见事件在图14.27中列出。

| RadioButton 的属性和事件 | 描述 |
|---|---|
| *常见属性* | |
| Checked | 指示 RadioButton 是否被选中。 |
| Text | 指定 RadioButton 的文本。 |
| *常见事件* | |
| CheckedChanged | 每次选中或取消选中 RadioButton 时生成。在设计视图中双击 RadioButton 控件时，会为此事件生成事件处理程序。 |

**图 14.27**  |  RadioButton 的属性和事件。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_455_0.png)

## 软件工程观察 14.1

Form、GroupBox 和 Panel 可以作为 RadioButton 的逻辑组。每组内的 RadioButtons 彼此互斥，但不与不同逻辑组中的 RadioButtons 互斥。

图14.28中的程序使用 RadioButtons 让用户为 MessageBox 选择选项。选择所需属性后，用户按下 Display 按钮以显示 MessageBox。左下角的 Label 显示 MessageBox 的结果（即用户单击了哪个按钮——Yes、No、Cancel 等）。

```csharp
// Fig. 14.28: RadioButtonsTestForm.cs
// Using RadioButtons to set message window options.
using System;
using System.Windows.Forms;

namespace RadioButtonsTest
{
    // Form contains several RadioButtons--user chooses one
    // from each group to create a custom MessageBox
    public partial class RadioButtonsTestForm : Form
    {
        // create variables that store the user's choice of options
        private MessageBoxIcon IconType { get; set; }
        private MessageBoxButtons ButtonType { get; set; }

        // default constructor
        public RadioButtonsTestForm()
        {
            InitializeComponent();
        }

        // change Buttons based on option chosen by sender
        private void buttonType_CheckedChanged(object sender, EventArgs e)
        {
            if (sender == okRadioButton) // display OK Button
            {
                ButtonType = MessageBoxButtons.OK;
            }
            // display OK and Cancel Buttons
            else if (sender == okCancelRadioButton)
            {
                ButtonType = MessageBoxButtons.OKCancel;
            }
            // display Abort, Retry and Ignore Buttons
            else if (sender == abortRetryIgnoreRadioButton)
            {
                ButtonType = MessageBoxButtons.AbortRetryIgnore;
            }
        }
    }
```
