

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_161_0.png)

图 C#5.18

3 按 F5 键运行 SampleApplication 应用程序。输出出现，如图 C#5.19 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_161_1.png)

图 C#5.19

在图 C#5.19 中，button1 Button 控件显示为禁用状态。

## 指定控件的 Tab 顺序

通过设置控件的 TabIndex 属性，可以按适当的顺序访问窗体上的控件。此属性允许你通过按 Tab 键以逻辑方式在全部控件之间导航。

让我们执行以下步骤来指定控件的 Tab 顺序：

1. 重复本章“更改窗体标题”一节的步骤 1 到 3。
2. 在 Name 文本框中输入 TabOrder，并在 Location 组合框中指定适当位置。
3. 单击 OK 按钮。将使用指定的名称和位置创建 TabOrder 应用程序。
4. 从工具箱中拖动两个 Button 控件和两个 TextBox 控件，并将这些控件放到 Form1 窗体上（图 C#5.20）。
5. 将 button1 的 Text 属性设置为 Add Name，将 button2 的 Text 属性设置为 Add Age，如图 C#5.20 所示：

   ![](img/2db4b8b2cb67e7ccc52477a61fe289ab_162_0.png)

   图 C#5.20

6. 选择 button1，并将其 TabIndex 属性设置为 0（零），如图 C#5.21 所示：

   ![](img/2db4b8b2cb67e7ccc52477a61fe289ab_162_1.png)

   图 C#5.21

7. 对 Form1 窗体中的所有其他控件重复步骤 6，为每个控件分配的 TabIndex 属性值比前一个控件大 1。

### 注意

> 设置控件的 Tab 顺序时，请确保其 TabStop 属性设置为 True。如果此属性为 False，用户无法使用 Tab 键到达该控件。

8. 按 F5 键运行 TabOrder 应用程序。焦点位于 Add Name 按钮上，如图 C#5.22 所示。

   ![](img/2db4b8b2cb67e7ccc52477a61fe289ab_163_0.png)

   图 C#5.22

9. 按 Tab 键。输出出现，如图 C#5.23 所示：

   ![](img/2db4b8b2cb67e7ccc52477a61fe289ab_163_1.png)

   图 C#5.23

在图 C#5.23 中，焦点设置到第二个控件，即 TabIndex 值为 1 的控件。在我们的示例中，它是 textbox1。

## 处理 Windows Forms 应用程序的常见事件

C# 是一种事件驱动的语言，在这种语言中，程序流由用户操作控制，例如按键或单击控件。你可以在代码设计器中编写代码来处理事件。

事件主要有两种类型：

- 鼠标事件：指通过鼠标提供输入所生成的事件
- 键盘事件：指通过键盘提供输入所生成的事件

让我们先学习处理鼠标事件。

### 处理鼠标事件

在 C# 中，与控件关联的最常见鼠标事件是 Click 事件。

让我们执行以下步骤，学习处理 Button 控件的 Click 事件：

1. 重复本章“更改窗体标题”一节的步骤 1 到 3。
2. 在 Name 文本框中输入 MouseEvent，并在 Location 组合框中指定适当位置。
3. 单击 OK 按钮。将使用指定的名称和位置创建 MouseEvent 应用程序。
4. 从工具箱中拖动一个 Button 控件和一个 TextBox 控件，并将这些控件放到 Form1 窗体上（图 C#5.24）。
5. 在“属性”窗口中将 button1 的 Text 属性设置为 Click，如图 C#5.24 所示：

   ![](img/2db4b8b2cb67e7ccc52477a61fe289ab_164_0.png)

6. 双击 Button 控件，并在代码编辑器中添加代码清单 5.3 中突出显示的代码，以处理 Button 控件的 Click 事件：

   代码清单 5.3：显示处理 Button 控件 Click 事件的代码

```
private void button1_Click(object sender, EventArgs e)
{
    textBox1.Text = "Welcome to C# 2010";
}
```

7. 按 F5 键运行 MouseEvent 应用程序。单击 Click 按钮后的输出如图 C#5.25 所示：

   ![](img/2db4b8b2cb67e7ccc52477a61fe289ab_164_1.png)

在图 C#5.25 中，文本框显示文本 Welcome to C# 2010。

现在，让我们学习处理键盘事件。

### 处理键盘事件

在 C# 中，除了鼠标事件外，还可以生成键盘事件。Windows Forms 应用程序中的不同键盘事件包括 KeyDown、KeyPress 和 KeyUp。

让我们执行以下步骤，学习处理 TextBox 控件的 KeyPress 事件：

1. 重复本章“更改窗体标题”一节的步骤 1-3。
2. 在 Name 文本框中输入 KeyboardEvent，并在 Location 组合框中指定适当位置。
3. 单击 OK 按钮。将使用指定的名称和位置创建 KeyboardEvent 应用程序。
4. 从工具箱中拖动一个 TextBox 控件，并将其放到 Form1 窗体上（图 C#5.26）。
5. 选择刚刚添加的文本框控件，并打开“属性”窗口以处理 TextBox 控件的 KeyPress 事件（图 C#5.26）。
6. 单击“属性”窗口中的“事件”按钮，与文本框相关的所有事件都会显示在“属性”窗口中（图 C#5.26）。
7. 双击 KeyPress 事件旁边的位置，生成 textBox1_KeyPress 事件处理程序，如图 C#5.26 所示：

   ![](img/2db4b8b2cb67e7ccc52477a61fe289ab_165_0.png)

   图 C#5.26

8. 在代码编辑器中添加代码清单 5.4 中突出显示的代码：

   代码清单 5.4：显示处理 TextBox 控件 KeyPress 事件的代码

```
private void textBox1_KeyPress(object sender, KeyPressEventArgs e)
{
    textBox1.BackColor = Color.Red;
    textBox1.ForeColor = Color.White;
}
```

9. 按 F5 键运行 KeyboardEvent 应用程序。
   当你在 TextBox 控件中键入一些文本时，TextBox 控件的背景色变为红色，文本颜色变为白色，如图 C#5.27 所示：

   ![](img/2db4b8b2cb67e7ccc52477a61fe289ab_165_1.png)

   图 C#5.27

在本节中，你学习了如何处理 Windows Forms 应用程序的常见事件。现在，让我们学习如何向窗体添加控件并对其执行某些操作。

## 使用 Windows Forms 控件

控件是可以放置在窗体上的组件，用于显示某些信息、接受某些用户输入以及执行文本编辑。此外，Windows 控件是用于在 C# 2010 中创建应用程序的基本控件。控件增强了用户与 Windows Forms 应用程序的交互。这些控件是 C# 2010 工具箱中可用的常见控件。Windows Forms 应用程序中的常见控件如下：

- Button 控件
- Label 控件
- TextBox 控件
- RichTextBox 控件
- RadioButton 控件
- CheckBox 控件
- ListBox 控件
- ComboBox 控件
- ListView 控件
- PictureBox 控件
- ProgressBar 控件
- TabControl 控件
- GroupBox 控件
- Timer 控件

现在，让我们学习使用 Button 控件。

### 使用 Button 控件

Button 控件是最基本的 Windows Forms 控件之一。每个 Windows Forms 应用程序至少有一个与之关联的 Button 控件。Button 控件允许你生成 Click 事件。用户可以通过处理 Button 控件的 Click 事件在运行时执行某些操作。

让我们执行以下步骤，在 Windows Forms 应用程序中使用 Button 控件：

1. 重复本章“更改窗体标题”一节的步骤 1 到 3。
2. 在 Name 文本框中输入 WindowsControls，并在 Location 组合框中指定适当位置。
3. 单击 OK 按钮。将使用指定的名称和位置创建 WindowsControls 应用程序。
4. 从工具箱中拖动一个 Button 控件，并将其放到 Form1 窗体上。
5. 在“属性”窗口中将 Button 控件的 Text 属性设置为 Click，如图 C#5.28 所示：

   ![](img/2db4b8b2cb67e7ccc52477a61fe289ab_166_0.png)

   图 C#5.28

在图 C#5.28 中，Button 控件的文本变为 Click。

### 使用 Label 控件

Label 控件是用于显示文本的控件。你可以使用它显示不希望用户编辑的静态文本。它还可用于显示动态文本（即在发生……之后变化的文本

