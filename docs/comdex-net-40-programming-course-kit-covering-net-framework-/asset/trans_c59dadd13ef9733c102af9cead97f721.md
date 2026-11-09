

![](img/9862a98a1a2d3bb14334137965a1ec60_116_0.png)

图 VB-2.78

结果，**TextBox** 控件的事件显示在**属性**窗口中（图 VB-2.79）。

- 10. 选择 **KeyUp** 事件，然后双击该事件前面的组合框内部，如图 VB-2.79 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_116_1.png)

图 VB-2.79

结果，代码编辑器打开，并带有 **KeyUp** 事件的事件处理程序 **TextBox1_KeyUp**。

- 11. 在代码编辑器的 **TextBox1_KeyUp** 事件处理程序中添加以下突出显示的代码片段：

```
Private Sub TextBox1_KeyUp(ByVal sender As System.Object,
    ByVal e As System.Windows.Forms.KeyEventArgs) Handles TextBox1.KeyUp
    If (e.KeyCode > 47 And e.KeyCode < 58) Then
        MsgBox("Numbers are not allowed!")
        TextBox1.Text = ""
    End If
End Sub
```

- 12. 双击窗体中的 Click Me 按钮。代码编辑器中会创建 **Button1_Click** 事件处理程序，如下面的代码片段所示：

```
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
End Sub
```

- 13. 在 **Button1_Click** 事件处理程序中添加以下突出显示的代码片段：

```
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
        MsgBox("Welcome " & TextBox1.Text & "!")
End Sub
```

- 14. 按键盘上的 F5 键运行应用程序。将显示 **Form1**（图 VB-2.80）。

- 15. 在 **Form1** 上的文本框中输入 **5**。会出现一个消息框，消息为 **不允许输入数字！**（图 VB-2.80）。

- 16. 单击**确定**按钮关闭消息框（图 VB-2.80）。

- 17. 在 **Form1** 上的文本框中输入文本 **James**（图 VB-2.81）。

- 18. 单击 Click Me 按钮（图 VB-2.81）。会出现一个消息框，消息为 **欢迎 James！**（图 VB-2.82）。

- 19. 单击**确定**按钮关闭消息框，如图 VB-2.82 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_117_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_117_1.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_117_2.png)

您已经学习了如何在 Visual Basic 2010 中处理事件。下一节将学习如何向 Visual Basic 2010 中的代码添加注释。

## 向代码添加注释

注释是仅为了使程序代码更易于读者理解而添加到程序代码中的附加文本。注释既不会被编译也不会被执行；它们会被语言编译器忽略。Visual Basic 2010 中的注释以单引号 (') 开头。要注释多行，需要在每一行前添加单引号 (')。您还可以通过选择一行或多行代码，然后分别单击文本编辑器工具栏中的注释按钮或取消注释按钮来添加或移除注释。

执行以下步骤向代码添加注释：

- 1. *启动* Visual Studio 2010。
- 2. *打开* **MOUSEANDKEYBOARDEVENTS** 应用程序。
- 3. 打开 **Form1.vb** 文件的代码编辑器，并在 **Button1_Click** 事件处理程序中添加一些文本（图 VB-2.83）。
- 4. 选择该文本，然后单击文本编辑器工具栏中的注释按钮（图 VB-2.83）。
  结果，在代码编辑器中选中的每一行前都会添加一个单引号 (')，将其标记为已注释（图 VB-2.84）。
- 5. *选择*代码编辑器中已注释的行，然后单击文本编辑器工具栏中的取消注释按钮，以取消注释选中的行，如图 VB-2.84 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_117_3.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_117_4.png)

结果，已注释的行变为未注释。

## 小结

本章中，您首先了解了 Form 类，它是所有 Windows 窗体的基类。接着，您学习了在窗体上执行不同操作，例如设置窗体标题、向窗体添加控件、设置控件的 Tab 键顺序，以及在运行时显示和隐藏窗体与控件。您还学习了如何在 Visual Basic 2010 中创建消息框、输入框和对话框。此外，您学习了在 Visual Basic 2010 中处理鼠标和键盘事件。最后，您学习了如何向 Visual Basic 2010 中的代码添加注释。

下一章中，您将学习各种 Windows 控件，例如 **Label**、**TextBox**、**Button** 和 **RadioButton**。

## Windows 窗体控件 - I

### 第 3 章

### 本章内容

- 介绍 Control 类
- 使用 Label 控件
- 使用 TextBox 控件
- 使用 Button 控件
- 使用 RadioButton 控件
- 使用 CheckBox 控件
- 使用 ComboBox 控件
- 使用 ListBox 控件
- 使用 GroupBox 控件
- 使用 Panel 控件
- 使用 PictureBox 控件
- 使用 Timer 控件
- 使用 ProgressBar 控件

Windows 窗体控件是添加到 Windows 窗体应用程序中的控件。您可以使用这些控件接收用户输入或向用户显示某些信息。换句话说，控件用于促进用户与应用程序之间的交互。控件与某些属性、方法和事件相关联，这些属性、方法和事件使控件适合执行特定操作。Visual Basic 2010 提供了许多控件，使您能够接受用户输入或向用户显示输出。这些控件可在 Visual Studio 2010 集成开发环境 (IDE) 的工具箱中找到。通过定位、设计和排列 Windows 窗体上的控件，可以为用户提供良好的可视化界面。

本章首先讨论 **Control** 类。您还将学习使用一些常用的 Windows 窗体控件，包括 **Label、TextBox、Button、RadioButton、CheckBox、ComboBox、ListBox、GroupBox、Panel、PictureBox、Timer** 和 **ProgressBar** 控件。

让我们从讨论 Control 类开始。

## 介绍 Control 类

Control 类是所有 Windows 窗体控件的基类，它属于 **System.Windows.Forms** 命名空间。Control 类的继承层次结构如下：

```
System.Object
    System.MarshalByRefObject
        System.ComponentModel.Component
            System.Windows.Forms.Control
```

在上述继承层次结构中，您可以注意到 **Object** 类是 .NET Framework 类库中所有类的基类。Control 类派生自 Component 类，而 Component 类继承自 **MarshalByRefObject** 类。

所有 Windows 窗体控件都继承 **Control** 类的公共属性、方法和事件。表 3.1 列出了 Control 类的重要属性：

**表 3.1：Control 类的重要属性**

| 属性 | 描述 |
|---|---|
| Anchor | 获取或设置子控件绑定到的父控件的边缘，并确定控件相对于其父控件大小如何调整 |
| BackColor | 获取或设置控件的背景色 |
| BackgroundImage | 获取或设置控件的背景图像 |
| CausesValidation | 获取或设置一个值，该值指定控件在获得焦点时是否验证任何需要验证的控件 |
| Controls | 获取或设置控件中包含的控件集合 |
| Dock | 获取或设置一个值，以指示哪些控件边框停靠到其父控件，并确定控件相对于其父控件大小如何调整 |
| Enabled | 获取或设置一个值，以指示控件是否可以响应用户交互 |
| Font | 获取或设置控件中显示文本的字体 |
| ForeColor | 获取或设置控件的前景色 |
| HasChildren | 返回一个值，指定控件是否包含子控件 |
| Height | 获取或设置控件的高度（以像素为单位） |
| Name | 获取或设置控件的名称 |
| Size | 获取或设置控件的高度和宽度（以像素为单位） |
| TabIndex | 获取或设置控件在其容器（如 Form）中的 Tab 键顺序 |

