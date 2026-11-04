
## 以编程方式使用资源

在此示例中，我们将图像作为资源添加到项目中。这会使 IDE 将图像复制到应用的可执行文件中，并使应用能够通过项目的 Properties 命名空间访问这些图像。这样做后，当你将应用移动到其他位置或计算机时，无需担心需要将图像与应用一起打包。

如果你要创建新项目，请使用以下步骤将图像作为资源添加到项目中：

- 1. 创建项目后，在“解决方案资源管理器”中右键单击项目的 Properties 节点，然后选择“打开”以显示项目属性。
- 2. 在左侧的选项卡中，单击“资源”选项卡。
- 3. 在“资源”选项卡顶部，单击“添加资源”旁边的向下箭头，然后选择“添加现有文件...”，以显示“将现有文件添加到资源”对话框。
- 4. 找到要作为资源添加的图像文件，然后单击“打开”按钮。我们在本章示例的 Images 文件夹中提供了三个示例图像。
- 5. 保存项目。

这些文件现在会出现在“解决方案资源管理器”中名为 Resources 的文件夹中。在今后大多数使用图像的示例中，我们都会使用这种方法。

项目的资源可通过其 Resources 类（属于项目的 Properties 命名空间）供应用访问。Resources 类包含一个 ResourceManager 对象，用于以编程方式与资源交互。要访问图像，可以使用 GetObject 方法，该方法接受资源在“资源”选项卡中显示的名称作为参数（例如 "image0"），并将资源作为 Object 返回。第 27-28 行使用字符串内插表达式的结果调用 GetObject：

```
$"image{ImageNumber}"
```

该表达式通过将下一张图片的索引（ImageNumber，先前在第 23 行获得）放在单词 "image" 的末尾来构造资源名称。必须将此 Object 转换为 Image 类型（System.Drawing 命名空间），才能将其赋给 PictureBox 的 Image 属性（第 26-28 行）。

Resources 类还提供对已定义资源的直接访问，可使用 Resources.resourceName 形式的表达式，其中 resourceName 是创建资源时为资源提供的名称。使用此类表达式时，返回的资源已经具有适当的类型。例如，Properties.Resources.image0 是表示第一张图像的 Image 对象。

## 14.9 工具提示

在第 2 章中，我们演示了工具提示——当鼠标悬停在 GUI 中的某一项上时出现的有帮助的文本。回想一下，Visual Studio（以及大多数带 GUI 的应用）中的工具提示可帮助你熟悉 IDE 的功能，并可作为每个工具栏图标功能的有用提醒。本节演示如何使用 ToolTip 组件向应用添加工具提示。图 14.31 描述了 ToolTip 类的常见属性和一个常见事件。

| ToolTip 属性和一个事件 | 描述 |
|---|---|
| *常见属性* | |
| AutoPopDelay | 鼠标位于控件上时工具提示显示的时间量（以毫秒为单位）。 |
| InitialDelay | 工具提示出现之前，鼠标必须悬停在控件上的时间量（以毫秒为单位）。 |
| ReshowDelay | 两个不同工具提示出现之间的时间量（以毫秒为单位）（当鼠标从一个控件移动到另一个控件时）。 |
| *常见事件* | |
| Draw | 当工具提示即将显示时引发。此事件允许程序员修改工具提示的外观。 |

图 14.31 | ToolTip 属性和一个事件。

从“工具箱”添加 ToolTip 组件时，它会出现在组件栏中——当窗体处于设计模式时，该组件栏位于窗口底部。将 ToolTip 添加到窗体后，窗体的其他控件会在“属性”窗口中显示一个新属性。此属性在“属性”窗口中显示为 ToolTip on，后面是 ToolTip 组件的名称。例如，如果窗体的 ToolTip 命名为 helpfulToolTip，则可以设置控件的 ToolTip on helpfulToolTip 属性值，以指定控件的工具提示文本。图 14.32 演示了 ToolTip 组件。对于此示例，我们创建一个包含两个 Label 的 GUI，以便为每个 Label 演示不同的工具提示文本。由于此示例中没有事件处理代码，因此不展示窗体类的代码。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_462_0.png)

![](img/3f5ef6be1748bb746e5f71a483bba4d0_462_1.png)

图 14.32 | 演示 ToolTip 组件。

在此示例中，IDE 将 ToolTip 组件命名为 toolTip1。图 14.33 显示了组件栏中的 ToolTip。我们将第一个 Label 的工具提示文本设置为 "First Label"，将第二个 Label 的工具提示文本设置为 "Second Label"。图 14.34 演示了为第一个 Label 设置工具提示文本。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_463_0.png)

组件栏中的 ToolTip

图 14.33 | 演示组件栏。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_463_1.png)

用于设置工具提示文本的属性

工具提示文本

图 14.34 | 设置控件的工具提示文本。

## 14.10 NumericUpDown 控件

有时，你会希望将用户的输入选择限制在特定的数值范围内。这正是 NumericUpDown 控件的用途。此控件显示为 TextBox，右侧有两个小 Button——一个带向上箭头，一个带向下箭头。默认情况下，用户可以像在 TextBox 中一样在此控件中键入数值，也可以单击向上和向下箭头来分别增大或减小控件中的值。范围中的最大值和最小值分别由 Maximum 和 Minimum 属性指定（两者均为 decimal 类型）。Increment 属性（也是 decimal 类型）指定当用户单击箭头时当前值变化多少。DecimalPlaces 属性指定控件应显示的小数位数。图 14.35 描述了 NumericUpDown 的常见属性和一个事件。

| NumericUpDown 属性和一个事件 | 描述 |
|---|---|
| *常见属性* | |
| DecimalPlaces | 指定控件中显示的小数位数。 |
| Increment | 指定当用户单击控件的向上和向下箭头时，控件中的当前数字变化多少。 |
| Maximum | 控件范围中的最大值。 |
| Minimum | 控件范围中的最小值。 |
| UpDownAlign | 修改 NumericUpDown 控件上向上和向下 Button 的对齐方式。此属性可用于将这些 Button 显示在控件的左侧或右侧。 |
| Value | 控件中当前显示的数值。 |
| *常见事件* | |
| ValueChanged | 当控件中的值更改时引发此事件。这是 NumericUpDown 控件的默认事件。 |

图 14.35 | NumericUpDown 属性和一个事件。

图 14.36 演示了 GUI 中用于计算利率的 NumericUpDown 控件。此应用中执行的计算与图 6.6 中的计算类似。TextBox 用于输入本金和利率金额，NumericUpDown 控件用于输入我们要计算利息的年数。

```csharp
1 // Fig. 14.36: InterestCalculatorForm.cs
2 // Demonstrating the NumericUpDown control.
3 using System;
4 using System.Windows.Forms;
5 
6 namespace NumericUpDownTest
7 {
8     public partial class InterestCalculatorForm : Form
9     {
10        // default constructor
11        public InterestCalculatorForm()
12        {
13            InitializeComponent();
14        }
15 
16        private void calculateButton_Click(object sender, EventArgs e)
17        {
18            // retrieve user input
19            decimal principal = decimal.Parse(principalTextBox.Text);
20            double rate = double.Parse(interestTextBox.Text);
21            int year = (int) yearUpDown.Value;
22 
23            // set output header
24            string output = "Year\tAmount on Deposit\r\n";
```

图 14.36 | 演示 NumericUpDown 控件。（第 1 部分，共 2 部分。）
