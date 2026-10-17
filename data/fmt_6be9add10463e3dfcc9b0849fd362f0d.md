
```csharp
using System.Windows.Forms;

namespace Card_Flip
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

    private void showBackButton_Click(object sender, EventArgs e)
    {
        cardBackPictureBox.Visible = true;
        cardFacePictureBox.Visible = false;
    }

    private void showFaceButton_Click(object sender, EventArgs e)
    {
        cardBackPictureBox.Visible = false;
        cardFacePictureBox.Visible = true;
    }
}
```

**步骤 6:** 保存项目。然后，按键盘上的 `F5` 键，或点击工具栏上的启动调试按钮（ )）来编译并运行应用程序。

通过点击按钮来测试应用程序。当你点击*Show the Card Face*按钮时，你将看到卡片的正面（卡片背面应该是隐藏的）。当你点击*Show the Back*按钮时，你将看到卡片的背面（卡片正面应该是隐藏的）。完成后，关闭应用程序。

![](img/8a88e1d8c69a687988c05f162ce32cac_119_0.png)

> 注意：如果你在事件处理程序内部正确输入了语句，应用程序应该可以运行。如果你没有正确输入事件处理程序中的语句，将出现一个窗口报告错误。如果发生这种情况，点击窗口中的 No 按钮，然后修正代码使其如之前所示。

> 注意：除了 `PictureBox` 之外，许多类型的控件都有 `Visible` 属性。例如，你可以通过设置其属性来使 `Label` 控件可见或隐藏。

### 语句的顺序执行

在教程 2-5 中，事件处理程序包含多个语句。例如，这里是 `showBackButton_Click`：

```csharp
private void showBackButton_Click(object sender, EventArgs e)
{
    cardBackPictureBox.Visible = true;
    cardFacePictureBox.Visible = false;
}
```

## 第 2 章 C# 简介

此方法有两个赋值语句。当方法执行时，语句按照从方法开始到结束的顺序执行。此语句执行：

```
cardBackPictureBox.Visible = true;
```

然后执行此语句：

```
cardFacePictureBox.Visible = false;
```

在应用程序运行时，通过点击 `showBackButton` 控件，你无法判断语句是按此顺序执行的，因为应用程序执行非常快。然而，重要的是你要理解语句是按照它们出现的顺序逐个执行的。在这个特定方法中，哪个赋值语句在前并不重要。如果我们反转语句的顺序，我们在屏幕上看不到区别，因为应用程序执行非常快。在大多数应用程序中，你会开始编写执行多个步骤的处理器，大多数情况下必须按特定顺序执行这些步骤，否则程序不会产生正确的结果。

## 检查点

- 38 `PictureBox` 用于什么？
- 39 `PictureBox` 位于工具箱的何处？
- 40 如何在 `PictureBox` 中显示图像？
- 41 `PictureBox` 控件的 `SizeMode` 属性默认值是什么？
- 42 将 `SizeMode` 属性设置为 `Zoom` 如何影响在 `PictureBox` 中显示的图像？
- 43 如何创建图像？
- 44 控件的 `Visible` 属性值如何改变运行时外观？

## 注释、空行和缩进

> 概念 注释是放置在源代码中的简短说明，用于解释程序部分的功能。程序员通常在代码中使用空行和缩进来组织代码并使其阅读。

### 注释

注释是放置在程序不同部分的简短说明，解释这些部分的功能。注释不是给编译器看的，而是给阅读代码并试图理解其作用的人看的。在 C# 中有三种注释：行注释、块注释和文档注释。行注释出现在程序中。用双斜杠（`//`）开始行注释。斜杠之后到行尾的内容会被编译器忽略。行注释可以出现在任何地方。下面的代码示例显示了我们在教程 2-5 的 `showButtonClick` 事件处理程序中使用注释。每个注释解释了下一行代码的作用：

```csharp
private void showButtonClick_Click(object sender, EventArgs e)
    // 使卡片的背面可见。
    cardFacePictureBox.Visible = true;
    // 使卡片的正面隐藏。
    cardFacePictureBox.Visible = false;
```

行注释不占据整行。符号 `//` 之后到行尾的内容会被忽略。因此，注释可以出现在执行语句之后。下面的代码示例显示：

```csharp
private void showButtonClick_Click(object sender, EventArgs e)
    cardFacePictureBox.Visible = true; // 显示卡片背面。
    cardFacePictureBox.Visible = false; // 隐藏正面。
```

块注释可以占据块中的多个连续行。块注释以 `/*`（斜杠加星号）开始，以 `*/` 结束。标记之间的所有内容都会忽略。下面的代码示例显示了如何使用块注释：

```csharp
/*
showButtonClick 控件的事件处理程序。
此方法使卡片的背面可见，并使卡片的正面隐藏。
*/
```

```csharp
private void showButtonClick_Click(object sender, EventArgs e)
    cardFacePictureBox.Visible = true; // 显示卡片背面。
    cardFacePictureBox.Visible = false; // 隐藏正面。
```

此代码示例的前五行是块注释，解释了 `showbutton_click` 方法的作用。注释让编写说明变得更容易，你不需要用注释符号标记每一行。

使用注释时请记住以下点：

- 注意不要将起始符号 (`/*`) 与结束符号 (`*/`) 颠倒。
- 不要忘记结束符号。

这些错误中的每一个都容易追踪，并会阻止程序编译。

第三种注释被称为文档注释。专业程序员使用文档注释在程序源代码中嵌入详细的文档。Visual Studio 可以从注释中提取信息并生成外部文档文件。单行文档注释以双斜杠（`//`）开始。块文档注释以 `/**` 开始并以 `/` 结束。虽然文档注释对程序员有用，但我们在这书中不使用它们。

作为一名初级程序员，你可能会抵制在程序中编写大量注释的想法。毕竟，编写真正能做事情的代码要有趣得多。然而，花额外时间编写注释是至关重要的我们

# 第 2 章 Visual C# 简介

当你将来需要修改或调试程序时，这几乎肯定可以节省时间。即使是大型且复杂的程序，如果有适当的注释，也可以变得易于阅读和理解。

# 使用空行和缩进让你的代码更易读

程序员通常在代码中使用空行和缩进来创建视觉上的组织感。这与作者在书籍页面上安排文本的方式类似。他们不是将每一章都写成一长串句子，而是将其分成在页面上视觉上隔开的段落。这并没有改变书中的信息，但让它变得更易阅读。

例如，在下面的代码示例中，我们在方法内部插入了一个空行，以便在视觉上将代码分为两组语句。空行不是必须的，但它让代码更便于人类阅读。

```sharp
private void showBackButton_Click(object sender, EventArgs e) {
    // 让卡片背面的图像可见。
    cardBackPictureBox.Visible = true;
    // 让卡片面的图像不可见。
    cardFacePictureBox.Visible = false;
}
```

程序员还使用缩进来组织你的代码。你可能已经注意到代码编辑器中，所有在大括号 (`{}`) 内部的语句都缩进了。例如，命名空间内部的所有语句都缩进了，类内部的所有语句都缩进了，方法内部的所有语句都缩进了。事实上，通常不需要 Visual Studio，但就可以对你以这种方式编写的代码进行自动缩进。

虽然缩进不是必须的，但它让你的代码变得易读得多。通过对方法内部的语句进行缩进，你在视觉上将它们区分开来。因此，你可以一眼看出哪些语句是在方法内部。类和命名空间也是如此。这种缩进的做法是几乎所有程序员都遵循的惯例。

## 检查点

- 2.45 注释的作用是什么？
- 2.46 单行注释和块注释有什么区别？
- 2.47 在记住块注释的开始和结束符号时，你应该注意什么？
- 2.48 为什么程序员要在代码中插入空行和缩进？

# 编写关闭应用程序表单的代码

> 概念：要在代码中关闭应用程序的表单，你需要使用 `this.Close();` 语句。

你在本教程中创建的所有应用程序都需要用户点击标准的 Windows 关闭按钮 (`X`) 来关闭应用程序。标准的 Windows 关闭按钮出现在几乎每个窗口的右上角。然而，在许多应用程序中，你可能想给用户提供一种关闭应用程序的替代方案。例如，你可能想创建一个退出按钮，在它被点击时关闭应用程序。

要关闭应用程序的表单，你执行执行以下语句：

```csharp
this.Close();
```

让我们来看这个语句如何使用的示例。图 2-75 显示了名为“Exit Button Demo”的项目中的表单和代码。你在表单上看到的按钮控件名为 `exitButton`。在表单代码中，你可以看到我们为该按钮创建了一个点击处理程序（Click handler）。当用户点击按钮时，它会关闭表单，从而关闭应用程序。

# 图 2-75 带有退出按钮的表单

![](img/8a88e1d8c69a687988c05f162ce32cac_123_0.png)

# 2.10 处理语法错误

**概念：** 当你输入代码时，Visual Studio 代码编辑器会检查每个语句并报告发现的语法错误。这允许你快速纠错。

编写代码需要大量的精确性。即使是微小的错误，例如在应该使用小写字母的地方使用了大写字母，或者忘记用分号结束语句，会导致应用程序代码无法编译和执行。回想第 1 章，这类错误被称为语法错误。

Visual Studio 代码编辑器在你输入错误后不久报告错误方面做得很好。当你向编辑器中输入一个语句时，Visual Studio 会对其进行分析，如果发现语法错误，它会用波浪线标出。图 2-76 显示了一个示例。如果你将光标悬停在波浪线上，错误描述将在工具提示窗口中弹出。该描述通常会提供足够的信息，让你确定错误的原因以及如何修复它。

# 图 2-76 错误下划

```csharp
private void messageButton_Click(object sender, EventArgs e)
{
    MessageBox.Show("Hello world");
}

// 这条波浪线表示错误。
```

如果项目代码中存在语法错误，并且你尝试编译并执行它（通过按键盘上的 `F5` 键，或点击工具栏上的启动调试 (`▶`) 按钮），你将看到图 2-77 所示的窗口，报告错误。点击“否”按钮关闭窗口，你将看到图 2-78 所示的错误列表（Error List）。

# 图 2-77 报告生成错误的窗口

![](img/8a88e1d8c69a687988c05f162ce32cac_124_0.png)

# 图 2-78 错误列表窗口

![](img/8a88e1d8c69a687988c05f162ce32cac_124_1.png)

注意，错误列表窗口显示了错误描述、包含错误的源代码、行号以及错误所在的列。

## 检查点

- 2.49 使用什么语句可以关闭应用程序的表单？
- 2.50 Visual Studio 是如何报告语法错误的？
- 2.51 如果将光标悬停在波浪线上，会发生什么？
- 2.52 为什么程序员要在代码中插入空行和缩进？

## 术语

- 字母顺序
- 赋值运算符
- 赋值语句
- 自动大小属性
- 块注释
- 布尔值
- 边界样式
- 括号
- 驼峰命名法
- 分类
- 点击事件
- 设计时间
- 对话框
- 文档注释
- 事件处理程序
- 字体属性
- 标识符
- 字面量
- 可

## 复习题

### 单选题

- 1. (____) 是设计器中的虚线。
  a. 选择
  b. 标记
  c. 边界
  d. 框
- 2. (____) 是新项目中创建表单名称。
  a. Form1
  b. Main
  c. New1
  d. Blank
- 3. (____) 属性显示在按钮上的文本。
  a. Name
  b. Text
  c. Tag
  d. Face
- 4. 包含程序代码的文件被称为 (____)。
  a. 目标文件
  b. 可执行文件
  c. 语言文件
  d. 源代码文件
- 5. 命名空间是包含 (____) 的容器。
  a. 方法
  b. 名称
  c. 空间
  d. 类
- 6. (____) 是在应用程序运行时发生特定事件时执行的方法。
  a. 动作过程
  b. 事件处理程序
  c. 运行时过程
  d. 事件方法
- 7. `MessageBox.Show("Hello World");` 语句是 (____) 的示例。
  a. 方法调用
  b. 命名空间
  c. 点击事件
  d. 事件处理程序
- 8. 在编程中，string 指 (____)。
  a. 许多行代码
  b. 并行内存位置
  c. 字符序列
  d. 几乎任何内容
- 9. C# 中的 (____) 标记编程语句的结束。
  a. 分号
  b. 句号
  c. 连字符
  d. 下划线
- 10. 写入程序代码中的数据是 (____)。
  a. 标识符
  b. 指定符
  c. 关键字
  d. 字面量
- 11. 你构建 GUI 并编写应用程序代码的时间被称为 (____)。
  a. 运行时
  b. 设计时间
  c. 代码时间
  d. 规划时间
- 12. 应用程序执行的时间被称为 (____)。
  a. 运行时间
  b. 设计时间
  c. 执行
  d. 运行时
- 13. 当你想在表单上显示文本时，你使用 (____) 控件。
  a. 按钮
  b. 图片框
  c. 标签
  d. 框
- c. Label（标签）
d. TextBox（文本框）
- 15. ________ 属性允许你设置控件文本的字体、字体样式和大小。
  a. Style（样式）
  b. AutoSize（自动大小）
  c. Text（文本）
  d. Font（字体）
- 16. ________ 属性可以设置为两个可能值之一：True 或 False。
  a. Boolean（布尔型）
  b. Logical（逻辑）
  c. Binary（二进制）
  d. Dual（双重）
- 17. Label 控件有一个 ________ 属性，用于控制调整大小的方式。
  a. Stretch（拉伸）
  b. AutoSize（自动大小）
  c. Dimension（尺寸）
  d. Fixed（固定）
- 18. ________ 属性可以更改标签中文本的对齐方式。
  a. TextPosition（文本位置）
  b. AutoAlign（自动对齐）
  c. TextCenter（文本中）
  d. TextAlign（文本对齐）
- 19. 在代码中，使用 ________ 在控件的属性中存储值。
  a. Click event（点击事件）
  b. method call（方法调用）
  c. assignment statement（赋值语句）
  d. Boolean value（布尔值）
- 20. 等号 (=) 被称为 ________。
  a. equality symbol（相等符号）
  b. assignment operator（赋值运算符）
  c. equality operator（等值运算符）
  d. property position（属性位置）
- 21. 代码中引用控件属性的标准表示法是 ________。
  a. ControlName.PropertyName（控件名.属性名）
  b. ControlName=PropertyName（控件名=属性名）
  c. PropertyName.ControlName（属性名.控件名）
  d. PropertyName=ControlName（属性名=控件名）
- 22. ________ 是 Visual Studio 的一项功能在你编写编程语句时提供自动代码补全。
  a. AutoCode（自动代码）
  b. AutoComplete（自动完成）
  c. IntelliSense（智能感知）
  d. IntelliCode（智能代码）
- 23. 你可以使用 ________ 控件在表单上显示图形图像。
  a. Graphics（图形）
  b. PictureBox（图片框）
## 第 2 章 Visual C# 简介
- c. Drawing（绘制）
d. ImageBox（图像框）
- 24. 一旦创建了 PictureBox 控件，你就使用它的属性来指定它将显示的图像。
  a. Image（图像）
  b. Source（源）
  c. DrawSource（绘制源）
  d. ImageList（图像列表）
- 25. PictureBox 控件的属性指定控件图像显示的方式。
  a. RenderMode（渲染模式）
  b. DrawMode（绘制模式）
