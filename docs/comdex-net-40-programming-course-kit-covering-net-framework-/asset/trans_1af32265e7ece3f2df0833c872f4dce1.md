
- 12. *双击* **Form1** 中的 **显示文本** 按钮，并将清单 2.2 中突出显示的代码行 *添加* 到代码编辑器：

### 清单 2.2：从一个窗体显示另一个窗体

```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
    Form2.Show()
End Sub
```

清单 2.2 中突出显示的代码行调用 **Form2** 的 **Show** 方法。在运行时单击 **显示文本** 按钮时，将调用 Form2 的 Show 方法，进而显示 Form2。

- 13. *在设计器中双击 Form2*，并将清单 2.3 中突出显示的代码行 *添加* 到代码编辑器：

### 清单 2.3：从一个窗体读取在另一个窗体中输入的文本

```vb
Private Sub Form2_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
    TextBox1.Text = Form1.TextBox1.Text
End Sub
```

清单 2.3 中突出显示的代码行将 **Form1** 的文本框中的文本添加到 **Form2** 的文本框中。

- 14. *按* 键盘上的 **F5** 键运行应用程序。结果，将显示 **Form1**（图 VB-2.28）。

- 15. 在 **Form1** 的文本框中 *输入* 一些文本（图 VB-2.28）。在本例中，我们输入了 **欢迎使用 Visual Basic 2010**。

- 16. *单击* **显示文本** 按钮（图 VB-2.28）。你在 **Form1** 中输入的文本将显示在 **Form2** 的文本框中，如图 VB-2.29 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_98_0.png)

现在我们来学习如何设置启动窗体。

## 设置启动窗体

启动窗体是包含两个或更多窗体的应用程序加载时显示的第一个窗体。默认情况下，**Form1** 是启动窗体。如果你希望某个窗体成为应用程序执行时显示的第一个窗体，可以将其设为启动窗体。

执行以下步骤将某个窗体设置为启动窗体：

- 1. *打开* **MULTIPLEFORMS** 应用程序。

  默认情况下，**Form1** 是该应用程序的启动窗体。若要将 **Form2** 设为启动窗体，需要打开项目设计器。

- 2. 从菜单栏 *选择* **项目→MULTIPLEFORMS 属性**，打开 MULTIPLEFORMS 属性窗口（图 VB-2.30）。

  MULTIPLEFORMS 属性窗口出现（图 VB-2.31）。

- 3. 从 **启动窗体** 选项下的组合框中 *选择 Form2*（图 VB-2.31）。

![](img/9862a98a1a2d3bb14334137965a1ec60_99_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_99_1.png)

- 4. *按* 键盘上的 **F5** 键运行此应用程序。结果，作为启动窗体的 **Form2** 出现，如图 VB-2.32 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_99_2.png)

图 VB-2.32

## 创建始终置顶的窗体

始终置顶的窗体是运行应用程序时保持在所有其他窗体顶部的窗体。可以通过使用 **属性** 窗口将窗体的 **TopMost** 属性设置为 **True** 来创建始终置顶的窗体。

执行以下步骤创建始终置顶的窗体：

- 1. *启动* Visual Studio 2010。

- 2. 从菜单栏 *选择* **文件→新建→项目**。将打开“新建项目”对话框。

- 3. 在“新建项目”对话框左窗格的 **已安装的模板** 部分中 *选择* **Visual Basic→Windows**。

- 4. 在中间窗格中 *选择* **Windows 窗体应用程序**，以创建 Windows 窗体应用程序。

- 5. 在 **名称** 文本框中输入应用程序名称 **ALWAYSONTOP**（也可在 CD 上获取），并在 **位置** 组合框中输入应用程序的合适位置。

- 6. *单击* **确定** 按钮关闭 **新建项目** 对话框。**ALWAYSONTOP** 应用程序即创建完成，仅显示一个窗体 Form1（图 VB-2.33）。

- 7. 向应用程序中的当前项目再 *添加* 一个窗体 **Form2**（图 VB-2.34）。

- 8. 从工具箱向 **Form1** *添加* 一个 **Button** 控件，并使用 **属性** 窗口将其 **Text** 属性设置为 **显示 Form2**（图 VB-2.34）。

![](img/9862a98a1a2d3bb14334137965a1ec60_100_0.png)

图 VB-2.33

![](img/9862a98a1a2d3bb14334137965a1ec60_100_1.png)

图 VB-2.34

- 9. 在设计器中 *选择* **Form1**，并在 **属性** 窗口中将它的 **TopMost** 属性设置为 **True**，如图 VB-2.35 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_100_2.png)

图 VB-2.35

- 10. *双击* **Form1** 中的 **显示 Form2** 按钮，并将清单 2.4 中突出显示的代码行添加到代码编辑器：

### 清单 2.4：从 Form1 显示 Form2

```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As _
    System.EventArgs) Handles Button1.Click
    Form2.Show()
End Sub
```

清单 2.4 中突出显示的代码行调用 Form2 的 Show 方法，进而显示 Form2。

- 11. *按* 键盘上的 **F5** 键运行应用程序。结果，将显示 **Form1**（图 VB-2.36）。

- 12. *单击* **Form1** 上的 **显示 Form2** 按钮（图 VB-2.36）。结果，**Form2** 将显示在 **Form1** 后面，如图 VB-2.37 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_100_3.png)

图 VB-2.36

![](img/9862a98a1a2d3bb14334137965a1ec60_100_4.png)

图 VB-2.37

## 显示和隐藏窗体与控件

可以通过设置窗体或控件的 **Visible** 属性，使其在运行时可见或不可见。该属性的默认值为 True。如果要隐藏窗体或控件，可以将该窗体或控件的 Visible 属性值设置为 False。

执行以下步骤显示或隐藏窗体或控件：

- 1. *启动* Visual Studio 2010。

- 2. 从菜单栏 *选择* **文件→新建→项目**。将打开“新建项目”对话框。

- 3. 在 **新建项目** 对话框左窗格的“已安装的模板”部分中 *选择* **Visual Basic→Windows**。

- 4. 在中间窗格中 *选择* **Windows 窗体应用程序**，以创建 Windows 窗体应用程序。

- 5. 在 **名称** 文本框中输入应用程序名称 **SHOWHIDE**（也可在 CD 上获取），并在 **位置** 组合框中输入应用程序的合适位置。

- 6. *单击* **确定** 按钮关闭 **新建项目** 对话框。**SHOWHIDE** 应用程序即创建完成，仅显示一个窗体 **Form1**（图 VB-2.38）。

- 7. 向此应用程序中的当前项目再 *添加* 一个窗体 **Form2**。

- 8. 向 **Form1** *添加* 两个 Button 控件，**Button1** 和 **Button2**，如图 VB-2.39 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_101_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_101_1.png)

图 VB-2.38

图 VB-2.39

- 9. 在 **Form1** 中 *选择* **Button2** 按钮，并在 **属性** 窗口中将它的 **Visible** 属性设置为 **False**，如图 VB-2.40 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_101_2.png)

图 VB-2.40

- 10. *双击* **Form1** 中的 **Button1** 按钮，并将以下突出显示的代码片段添加到代码编辑器：

```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
        Button1.Visible = False
        Button2.Visible = True
End Sub
```

- 11. *双击* **Form1** 中的 **Button2** 按钮，并 *添加* 以下突出显示的代码片段到代码编辑器：

```vb
Private Sub Button2_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button2.Click
    Form2.Show()
End Sub
```

- 12. 向 **Form2** *添加* 一个 Button 控件 **Button1**，如图 VB-2.41 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_102_0.png)

图 VB-2.41

- 13. *双击* **Form2** 上的 **Button1** 按钮，并 *添加* 以下突出显示的代码片段到代码编辑器：

```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
    Me.Hide()
End Sub
```

- 14. *按* 键盘上的 **F5** 键运行应用程序。结果，将显示输出（图 VB-2.42）。

  在图 VB-2.42 中，可以看到 **Button1** 按钮可见，而 **Button2** 按钮不可见。这是因为通过将 **Button2** 按钮的 **Visible** 属性设置为 False 将其隐藏了。

- 15. *单击* **Form1** 上的 **Button1** 按钮（图 VB-2.42）。结果，**Button1** 消失，**Button2** 出现在 **Form1** 上（图 VB-2.43）。

- 16. *单击* **Form1** 上的 **Button2** 按钮（图 VB-2.43）。

  结果，将显示 **Form2**（图 VB-2.44）。

- 17. *单击* **Form2** 上的 **Button1** 按钮，如图 VB-2.44 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_102_1.png)

图 VB-2.42

![](img/9862a98a1a2d3bb14334137965a1ec60_102_2.png)

图 VB-2.43

![](img/9862a98a1a2d3bb14334137965a1ec60_102_3.png)

图 VB-2.44

结果，**Form2** 消失。通过这种方式，可以在应用程序中显示和隐藏控件与窗体。

## 在运行时调整和移动窗体与控件

可以分别使用窗体或控件的 **Size** 或 **Location** 属性来调整其大小或移动它们。也可以通过调用窗体或控件的 **SetBounds** 方法来调整其大小并移动它们。

