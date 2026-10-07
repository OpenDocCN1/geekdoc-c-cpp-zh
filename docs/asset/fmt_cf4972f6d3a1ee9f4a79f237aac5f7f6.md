
1. Save the project. Then, press the `F5` key on the keyboard or click the `Start Debugging` button (▷) on the toolbar to compile and run the application.

> Note: If you typed the statements correctly inside the event handlers, the application should run. If you did not type the statements correctly inside the event handlers, a window will appear reporting build errors. If that happens, click the `No` button in the window and then correct the code so it appears exactly as previously shown.

Figure 2-60 shows the application's form when it starts running and after you have clicked each of the Button controls. After you have tested each button, close the application's form.

**Figure 2-60** The Language Translator application running

### Checkpoint

**2.29** In which group of the Toolbox can you find the Label control tool?

**2.30** Once you have placed a Label control on a form, which property do you use to set the text that you want to display?

**2.31** What property can you use to change the appearance of a Label control's text?

**2.32** What is the default value of a label's `BorderStyle` property?

**2.33** How do you change the `BorderStyle` property of a control in the Properties window?

**2.34** What property determines whether a label can be resized?

**2.35** What property determines the way text is aligned in a Label control?

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_226_0.png)

2.36 How can you use a Label control to display output while a program is running?

2.37 What happens if you assign an empty string to a control's `Text` property in code?

## 2.6 Making Sense of IntelliSense

> Concept

As you type code in the Visual Studio editor, IntelliSense boxes pop up to assist you. You can use the IntelliSense boxes to automatically complete some programming statements after typing only the few characters.

IntelliSense is a feature of Visual Studio that provides automatic code completion as you write programming statements. Once you learn how to use IntelliSense, it helps you write code faster. If you've worked through the previous tutorials in this chapter, you've already encountered IntelliSense. For example, in Step 3 of Tutorial 2-3, you were instructed to write the following statement in the `italianButton_Click` event handler:

```csharp
translationLabel.Text = "Buongiorno";
```

Did you notice that as soon as you started typing the statement, a box popped up on the screen? This is known as an IntelliSense list box. The contents of the list box changes as you type. Figure 2-61 shows the IntelliSense list box after you have typed the characters `tra`.

Figure 2-61 IntelliSense list box displayed

```csharp
private void italianButton_Click(object sender, EventArgs e)
{
    var ToolStripRenderEventArgs
    var ToolStripSeparatorRenderEventArgs
    var TraceR
    var translationRenderer
    var translationLabel
    var translationLabel
```

*(注：由于原文代码块存在异常重复，此处翻译已按样保留)*

IntelliSense 列表框的内容随着你的输入而改变。图 2-61 显示了在你输入字符 `tra` 之后的 IntelliSense 列表框。

图 2-61 显示的 IntelliSense 列表框

```csharp
private void italianButton_Click(object sender, EventArgs e)
{
    var ToolStripRenderEventArgs
    var ToolStripSeparatorRenderEventArgs
    var TraceR
    var translationRenderer
    var translationLabel
```

*(注：原文代码块存在异常重复，此处翻译已按样保留)*

### 2.6 理解 IntelliSense

> 概念

当你在 Visual Studio 编辑中输入代码时，IntelliSense 框会弹出以协助你。你只需要输入几个字符，就可以使用 IntelliSense 框来自动补全某些编程语句。

IntelliSense 是 Visual Studio 的一项功能，它在你编写编程语句时提供自动代码补全。一旦你学会了如何使用 IntelliSense，它就能帮助你更快地编写代码。如果你已经完成了本章之前的几个教程，你已经遇到过 IntelliSense 了。例如，在教程 2-3 的第 3 步中，你被指示在 `italianButton_Click` 事件处理程序中编写以下语句：

```csharp
translationLabel.Text = "Buongiorno";
```

你是否注意到一旦你开始输入该语句，屏幕上就会弹出一个框？这被称为 IntelliSense 列表框。列表框的内容随着你的输入而改变。图 2-61 显示了在你输入字符 `tra` 之后的 IntelliSense 列表框。

图 2-61 显示的 IntelliSense 列表框

```csharp
private void italianButton_Click(object sender, EventArgs e)
{
    var ToolStripRenderEventArgs
    var ToolStripSeparatorRenderEventArgs
    var TraceR
    var translationRenderer
    var translationLabel
```

*(注：原文代码块存在异常重复，此处翻译已按样保留)*

### 2.7 PictureBox 控件

> 概念

`PictureBox` 控件在表单上显示图形。`PictureBox` 控件具有控制图像显示方式的属性。可以使用 `PictureBox` 控件显示位图、GIF 或元文件格式的图像。

图 2-63 空的 `PictureBox`

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_231)

一旦创建了 `PictureBox` 控件，使用其 `Image` 属性来指定要显示的图像。遵循以下步骤：

**第 1 步：** 点击属性窗口中的 `Image` 属性。将出现省略按钮，如图 2-64 所示。

图 2-64 属性窗口中的 `Image`

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_232)

**第 2 步：** 点击省略按钮将弹出资源窗口。

**第 3 步：** 在资源窗口中点击 `Import` 按钮。将弹出打开对话框，用于定位和选择要显示的图像文件。

**第 4 步：** 选择图像文件后，你将在资源窗口中看到它的内容。这表示图像已导入。

图 2-65 被选中并导入的图像

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_233)

**第 5 步：** 点击资源窗口中的 `OK` 按钮，选中的图像将出现在 `PictureBox` 控件中。根据图像的大小，你可能看到它的部分。图 2-66 就是这种情况，因为图像大于 `PictureBox` 控件。

图 2-66 显示在 `PictureBox` 控件中的图像

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_233)

### SizeMode 属性

`PictureBox` 的 `SizeMode` 属性指定控件图像的显示方式。它可以设置为以下值之一：

- NORMAL（常规）：Normal 是默认值。图像将位于 `PictureBox` 控件的左上角。如果图像太大无法放入 `PictureBox` 控件，则会被裁剪。
- STRETCHIMAGE（拉伸）：Stretch 同时在水平和垂直方向上缩放图像以适应 `PictureBox` 控件。如果图像在一种方向上的缩放大于另一个方向，它看起来会被拉伸。
- AUTOSIZE（自动调整大小）：使用 AutoSize，`PictureBox` 控件将自动调整大小以适应图像的大小。
- CENTERIMAGE（居中）：CenterImage 在不缩放图像的情况下将其位于 `PictureBox` 控件中。
- ZOOM（缩放）：Zoom 均匀缩放图像以适应 `PictureBox` 且不丢失原始宽高比例。（宽高比例是图像的宽度与高度的比值。）这导致图像被缩放而不会被拉伸。

图 2-67 设置 `SizeMode` 为 Zoom 后缩放的图像

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_235_0.png)

### 注意

`PictureBox` 控件也有一个 `BorderStyle` 属性，其作用与 `Label` 控件的 `BorderStyle` 属性相同。

### 创建可点击的图像

按钮并不是唯一可以响应 `Click` 事件的控件。`PictureBox` 控件也可以。这意味着应用程序可以显示图像，并在用户点击图像时执行某些操作。

要创建一个可点击的图像，你只需要为显示图像的 `PictureBox` 控件创建一个 `Click` 事件处理器。为 `PictureBox` 控件创建 `Click` 事件处理程序的方法与为 `Button` 控件创建 `Click` 事件处理程序的方法相同：

- 在设计器（Designer）中双击 `PictureBox` 控件。这会在表单源代码文件中创建一个空的 `Click` 事件处理器。
- 在代码编辑器中，你在事件处理程序内部编写你希望在点击图像时执行的语句。

作为一个示例，请查看本教科书附带的学生示例程序中 `Chap02` 文件夹下的 `Cat` 项目。图 2-68 显示了应用程序的表单。`PictureBox` 控件的名称为 `catPictureBox`。它的图像是 `Cat.jpg` 文件，该文件也位于学生示例程序的 `Chap02` 文件夹中。`SizeMode` 属性设置为 `Zoom`，`BorderStyle` 属性设置为 `FixedSingle`。

### 图 2-68 Cat 表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_236_0.png)

在代码编辑器中打开 `Form1.cs` 文件，你会发现我们已经为 `catPictureBox` 控件创建了一个 Cat 事件处理器，如图 2-69 所示。如果你运行应用程序并点击 `PictureBox`，将会弹出一个消息框并显示字符串 `Meow`。

# 图 2-69 Cat 项目 Form1.cs 文件代码

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
```

```csharp
namespace Cat
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
    }

    private void catPictureBox_Click(object sender, EventArgs e)
    {
        MessageBox.Show("Meow");
    }
}
```

教程 2-4 提供了一个练习使用 `PictureBox` 控件的机会。在教程中，你将创建一个包含三个可点击 `PictureBox` 控件的应用程序，显示随书学生示例程序文件中提供的图像。

### 教程 2-4：创建 Flags 应用程序

在本教程中，你将创建一个在 `PictureBox` 控件中显示芬兰、法国和德国国旗的应用程序。当用户点击这些 `PictureBoxes` 之一时，国家的名称将出现在 `Label` 控件中。

- **第 1 步：**启动 Visual Studio 并创建一个名为 `Flags` 的新 Windows Forms 项目。
- **第 2 步：**按照图 2-70 所示设置应用程序表单。注意表单的 `Text` 属性设置为 `Flags`。控件的名称如图所示。每个相关的属性设置请参考表 2-4。

图 2-70 Flags 表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_238_0.png)

表 2-4 控件属性设置

| 控件名称 | 控件类型 | 属性设置 |
|---|---|---|
| `instructionLabel` | Label | **Text:** 点击旗查看国家名称。 |
| `finlandPictureBox` | PictureBox | **Image:** 从学生示例程序的 *Chap02* 文件夹中选择并导入 `Finland.bmp` 文件。**BorderStyle:** FixedSingle **SizeMode:** AutoSize |
| `francePictureBox` | PictureBox | **Image:** 从学生示例程序的 *Chap02* 文件夹中选择并导入 `France.bmp` 文件。**BorderStyle:** FixedSingle **SizeMode:** AutoSize |
| `germanyPictureBox` | PictureBox | **Image:** 从学生示例程序的 `Chap02` 文件夹中选择并导入 `Germany.bmp` 文件。**BorderStyle:** FixedSingle **SizeMode:** AutoSize |
| `countryLabel` | Label | **AutoSize:** False **BorderStyle:** FixedSingle **Font:** Microsoft Sans Serif (Style: Bold, Size: 10 point) **Text:** (Text 属性的内容已被擦除。) **TextAlign:** MiddleCenter |

**第 3 步：** 一旦设置好表单及其控件，你就可以为 `PictureBox` 控件创建 `Click` 事件处理器了。在设计器（*Designer*）中，双击 `finlandPictureBox` 控件。这将打开代码编辑器，你会看到一个名为 `finlandPictureBox_Click` 的空处理器。在事件处理器内部编写以下语句：

```csharp
countryLabel.Text = "Finland";
```
