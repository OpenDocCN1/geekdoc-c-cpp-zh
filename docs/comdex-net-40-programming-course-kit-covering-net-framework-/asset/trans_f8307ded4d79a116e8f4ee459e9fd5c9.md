
![](img/9862a98a1a2d3bb14334137965a1ec60_126_0.png)

图 VB-3.11

- 11. *双击* **提交** 按钮，并将以下突出显示的代码行添加到 *代码编辑器*：

```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
    MsgBox("The information entered by you has been sent to the server!")
End Sub
```

在前面的代码片段中，**Button1_Click** 是一个事件处理程序，用于处理 **Button** 控件 **Button1** 的 **Click** 事件。这意味着，当用户在运行时单击 **Button1** 时，将执行 **Button1_Click** 事件处理程序中编写的代码。执行时，前面代码片段中突出显示的代码行会打开一个消息框，显示消息 **您输入的信息已发送到服务器！**

> 消息框中提供的消息取决于您的需求。您可以根据应用程序的功能显示任何消息。

- 12. 按键盘上的 **F5** 键运行应用程序。将显示输出（图 VB-3.12）。
- 13. 在 **用户名** 文本框中输入用户名（图 VB-3.12）。
- 14. 在 **密码** 文本框中输入密码（图 VB-3.12）。
- 15. 在 **地址** 文本框中输入地址（图 VB-3.12）。
- 16. 单击 **提交** 按钮，如图 VB-3.12 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_126_1.png)

图 VB-3.12

将打开一个消息框，显示消息 **您输入的信息已发送到服务器！**（图 VB-3.13）。

- 17. 单击 **确定** 按钮关闭消息框，如图 VB-3.13 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_127_0.png)

您已经了解了三个基本的 Windows 窗体控件：**Label**、**TextBox** 和 **Button**。现在让我们继续学习允许我们进行选择的控件，如 **RadioButton**、**CheckBox**、**ComboBox** 和 **ListBox**。

## 使用 RadioButton 控件

**RadioButton** 控件也称为选项按钮，用于从一组选项中选择一个选项。单选按钮总是成组工作，这意味着当您从一组单选按钮中选择一个单选按钮时，该组中的其他单选按钮会自动取消选择。单选按钮可以显示文本、图像或两者。**RadioButton** 类派生自 **System.Windows.Forms** 命名空间，为 **RadioButton** 控件提供功能。**RadioButton** 类的一些重要属性列于表 3.8：

**表 3.8：RadioButton 类的值得注意的属性**

| 属性 | 描述 |
|---|---|
| Appearance | 获取或设置一个值，该值确定 RadioButton 控件的外观 |
| AutoCheck | 获取或设置一个值，该值指示当单选按钮被选中时，Checked 值和控件外观是否自动更改 |
| AutoSize | 获取或设置一个值，该值指定 RadioButton 控件是否自动调整大小以显示其所有内容 |
| Checked | 获取或设置 RadioButton 控件是否被选中 |
| Image | 获取或设置显示在 RadioButton 控件上的图像 |
| TextAlign | 获取或设置 RadioButton 控件上文本的对齐方式 |

表 3.9 列出了 **RadioButton** 类的一个重要方法：

**表 3.9：RadioButton 类的值得注意的方法**

| 方法 | 描述 |
|---|---|
| PerformClick | 为单选按钮生成 Click 事件，类似于用户在 RadioButton 控件上执行的单击 |

执行以下步骤，在 Windows 窗体应用程序中使用 **RadioButton** 控件：

- 1. *启动* Visual Studio 2010。
- 2. *选择*菜单栏中的 **文件→新建→项目**。**新建项目** 对话框打开。
- 3. *选择* **新建项目** 对话框左窗格中 **已安装的模板** 部分的 **Visual Basic→Windows**。
- 4. *选择*中间窗格中的 **Windows 窗体应用程序** 模板，以创建 Windows 窗体应用程序。
- 5. 在 **名称** 文本框中*输入*应用程序名称 **RadioButtonControl**，并在 **位置** 组合框中输入该应用程序的适当位置。
- 6. *单击* **确定** 按钮关闭 **新建项目** 对话框。**RadioButtonControl** 应用程序即创建完成（图 VB-3.14）。
- 7. 从 **工具箱** 中*拖放*一个 **Label** 控件、四个 **RadioButton** 控件和一个 **TextBox** 控件到 Form1 窗体上。

执行以下步骤，在 Windows 窗体应用程序中使用 **CheckBox** 控件：

- 1. *启动* Visual Studio 2010。
- 2. *选择*菜单栏中的 **文件→新建→项目**。**新建项目** 对话框打开。
- 3. *选择* **新建项目** 对话框左窗格中已安装的模板部分的 **Visual Basic→Windows**。
- 4. *选择*中间窗格中的 **Windows 窗体应用程序** 模板，以创建 Windows 窗体应用程序。
- 5. 在名称文本框中*输入*应用程序名称 **CheckBoxControl**（也可在随附 CD 中找到），并在位置组合框中输入该应用程序的适当位置。
- 6. *单击* **确定** 按钮关闭 **新建项目** 对话框。**CheckBoxControl** 应用程序即创建完成（图 VB-3.17）。
- 7. 从工具箱中*拖放*一个 **Label** 控件和四个 **CheckBox** 控件到 Form1 窗体上。
- 8. *设置* **Label** 控件的 **Text** 属性为 **选择您拥有的车辆：**，使用属性窗口。
- 9. *设置*第一个、第二个、第三个和第四个 CheckBox 控件的 Text 属性分别为 **自行车、踏板车、摩托车**和**汽车**，使用属性窗口。设置属性后，窗体显示如图 VB-3.17 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_130_0.png)

图 VB-3.17

- 10. *双击* **自行车** 复选框，并将以下突出显示的代码行*添加*到代码编辑器：

```vb
Private Sub CheckBox1_CheckedChanged(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles CheckBox1.CheckedChanged
        If CheckBox1.Checked = True Then
            MsgBox("You have selected: 'Cycle'.")
        End If
End Sub
```

在前面的代码片段中，**CheckBox1_CheckedChanged** 是一个事件处理程序，用于处理 **CheckBox** 控件 CheckBox1 的 **CheckedChanged** 事件。这意味着，当用户在运行时选中 CheckBox1 时，将执行 CheckBox1_CheckedChanged 事件处理程序中编写的代码。前面代码片段中突出显示的代码行检查 CheckBox1 的 Checked 属性是否设置为 True；如果是，则将 **MsgBox** 中的消息设置为 **您已选择：“自行车”。**

- 11. *双击* **踏板车** 复选框，并将以下突出显示的代码行*添加*到代码编辑器：

```vb
Private Sub CheckBox2_CheckedChanged(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles CheckBox2.CheckedChanged
        If CheckBox2.Checked = True Then
            MsgBox("You have selected: 'Scooter'.")
        End If
End Sub
```

前面代码片段中突出显示的代码行检查 **CheckBox2** 的 **Checked** 属性是否设置为 **True**；如果是，则将 **MsgBox** 中的消息设置为 **您已选择：“踏板车”。**

- 12. *双击* **摩托车** 复选框，并将以下突出显示的代码行*添加*到代码编辑器：

```vb
Private Sub CheckBox3_CheckedChanged(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles CheckBox3.CheckedChanged
    If CheckBox3.Checked = True Then
        MsgBox("You have selected: 'Motorcycle'.")
    End If
End Sub
```

前面代码片段中突出显示的代码行检查 **CheckBox3** 的 **Checked** 属性是否设置为 **True**；如果是，则将 **MsgBox** 中的消息设置为 **您已选择：“摩托车”。**

- 13. *双击* **汽车** 复选框，并将以下突出显示的代码行*添加*到代码编辑器：

```vb
Private Sub CheckBox4_CheckedChanged(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles CheckBox4.CheckedChanged
    If CheckBox4.Checked = True Then
        MsgBox("You have selected: 'Car'.")
    End If
End Sub
```

前面代码片段中突出显示的代码行检查 **CheckBox4** 的 **Checked** 属性是否设置为 **True**；如果是，则将 **MsgBox** 中的消息设置为 **您已选择：“汽车”。**

- 14. 按键盘上的 **F5** 键运行应用程序。输出显示出来（图 VB-3.18）。

- 15. 选择 **踏板车** 复选框。出现一个消息框，显示消息 **您已选择：“踏板车”**（图 VB-3.18）。

- 16. 单击 **确定** 按钮关闭消息框。（图 VB-3.18）。

- 17. 选择 **汽车** 复选框。出现一个消息框，显示消息 **您已选择：“汽车”**（图 VB-3.18）。

- 18. 单击 **确定** 按钮关闭消息框，（图 VB-3.19）。

![](img/9862a98a1a2d3bb14334137965a1ec60_131_0.png)

图 VB-3.18    图 VB-3.19

您已经学习了如何使用 **CheckBox** 控件。现在让我们学习如何使用 **ComboBox** 控件。

## 使用 ComboBox 控件

**ComboBox** 在下拉列表中显示项列表。它是文本框和下拉列表的组合，用户可以在文本框中输入项，也可以从下拉列表中选择项。用户只能从下拉列表中选择一个选项。用户选择某个选项后，**ComboBox** 中包含的下拉列表会自动折叠。您还可以在此下拉列表中添加或移除项。**ComboBox** 控件中的每个项都通过其在下拉列表中的位置（称为索引）来识别。**ComboBox** 类包含在 **System.Windows.Forms** 命名空间中，提供
