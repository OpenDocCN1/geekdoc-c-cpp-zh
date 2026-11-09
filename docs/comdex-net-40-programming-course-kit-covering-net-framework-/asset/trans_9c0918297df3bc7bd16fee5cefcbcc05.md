
一旦将 ImageButton 控件放置到 Web 窗体上，以下代码片段就会被添加到该网页的源代码中：

```aspx
<asp:ImageButton ID="ImageButton1" runat="server" />
```

它是一个 ImageButton 控件，因此你可以通过设置该 ImageButton 控件的 ImageUrl 属性来在其上添加图像。

现在，按照以下步骤从计算机向应用程序添加图像：

- 9. 在**解决方案资源管理器**窗口中右击项目名称，然后从上下文菜单中选择“添加现有项”选项，如图ASP-2.13所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_490_0.png)

“添加现有项”对话框将打开（图ASP-2.14）。

- 10. 从“文件名”组合框右侧的下拉列表中选择“所有文件”选项，如图ASP-2.14所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_490_1.png)

- 11. 导航到计算机上保存要添加到应用程序的图像的位置。在本例中，我们导航到 C:\Users\Public\Pictures\Sample Pictures 文件夹（图ASP-2.15）。

- 12. 选择要添加到应用程序的图像。在本例中，我们从 Sample Pictures 文件夹中选择了 Tulips 图像（图ASP-2.15）。

- 13. 单击“添加”按钮将图像添加到应用程序，如图ASP-2.15所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_491_0.png)

图ASP-2.15

所选图像将添加到应用程序文件夹中。你可以在**解决方案资源管理器**窗口中查看它（图ASP-2.16）。

- 14. 打开**ImageButton1**控件的**属性**窗口（图ASP-2.17）。

- 15. 单击**ImageUrl**属性的省略号按钮，如图ASP-2.17所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_491_1.png)

图ASP-2.16

![](img/9862a98a1a2d3bb14334137965a1ec60_491_2.png)

图ASP-2.17

**选择图像**对话框将打开（图ASP-2.18）。

- 16. 从**文件夹内容**窗格中选择图像，然后单击**确定**按钮（图ASP-2.18）。

它会在**ImageButton**控件中显示图像，如图ASP-2.19所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_491_3.png)

图ASP-2.18

![](img/9862a98a1a2d3bb14334137965a1ec60_491_4.png)

图ASP-2.19

- 17. *双击* Default.aspx 网页上的**ImageButton1**控件，并将以下代码片段添加到**Default.aspx.cs**文件中，如清单2.2所示：

**清单2.2：** 演示处理 ImageButton1 控件 Click 事件的代码

```csharp
protected void ImageButton1_Click(object Sender, ImageClickEventArgs e) {
    Response.Write("This is an Image Button Control Example");
}
```

前面的代码片段在单击 ImageButton1 控件时会在浏览器上显示一条消息 **This is an Image Button Control Example**。Response.Write 方法用于在运行时将消息打印到页面上。

- 18. *按* F5 键以在 Web 浏览器中查看输出（图ASP-2.20）。

- 19. *单击* 该图像（图ASP-2.20）。

将显示一条消息 **This is an Image Button Control Example**，如图ASP-2.21所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_492_0.png)

图ASP-2.20

![](img/9862a98a1a2d3bb14334137965a1ec60_492_1.png)

图ASP-2.21

## 使用 ListBox 控件

ListBox 控件是一种标准 Web 服务器控件，用于显示项列表。它允许你从网页上的项列表中选择一个或多个项。默认情况下，你一次只能从 ListBox 控件中选择一个项；但是，你可以通过将 SelectionMode 属性设置为 Multiple 来更改 ListBox 控件的行为。ListBox 类位于 System.Web.UI.WebControls 命名空间中。

ListBox 控件的重要属性列在表2.10中：

| 属性 | 描述 |
|---|---|
| `BorderColor` | 获取或设置控件的边框颜色 |
| `BorderStyle` | 获取或设置控件的边框样式 |
| `BorderWidth` | 获取或设置控件的边框宽度 |
| `Rows` | 获取或设置 ListBox 控件中显示的行数 |
| `SelectionMode` | 获取或设置 ListBox 控件的选择模式 |
| `Items` | 获取或设置 ListBox 控件的项 |

**ListBox**控件有一个名为**Items**的属性，用于将项添加到 ListBox 控件中。你可以向该集合中添加项以及从中移除项。

执行以下步骤来使用**ListBox**控件：

- 1. *打开* Visual Studio 2010。

- 2. 从菜单栏中*选择* **文件 → 新建 → 网站**。将打开**新建网站**对话框。

- 3. 从**新建网站**对话框的**已安装模板**窗格中*选择* **Visual C#**。

- 4. 在**新建网站**对话框的右窗格中*选择* **ASP.NET 网站**。

- 5. 在**Web 位置**组合框中*指定*应用程序的位置和名称。在本例中，我们提供的名称为 **ListBoxExample**。

- 6. *单击* **确定**按钮以保存所有设置。将创建 **ListBoxExample** 应用程序（也随附在 CD 中）（图ASP-2.22）。

- 7. *单击* **设计**选项卡以查看 **Default.aspx** 页面的设计（图ASP-2.22）。

- 8. 从**工具箱**中*添加*一个**ListBox**控件到 Web 窗体上，如图ASP-2.22所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_493_0.png)

一旦将 **ListBox1** 控件放置到 Web 窗体上，以下代码片段就会被添加到该网页的源代码中：

```aspx
<asp:ListBox ID="ListBox1" runat="server"></asp:ListBox>
```

- 9. 从**工具箱**中*添加*一个**Label**、两个**Button**、一个**TextBox**控件。

- 10. 将 **Label**、**Button1** 和 **Button2** 的 **Text** 属性分别*设置*为 **Enter a Fruit Name**、**Add** 和 **Remove**。

- 11. *单击* **ListBox1** 控件的 **Items** 属性上显示的省略号按钮。它将打开 **ListItem 集合编辑器**对话框（图ASP-2.23）。

- 12. *单击* **添加**按钮，在**成员**窗格中添加一个项，并在**成员**窗格下添加该项（图ASP-2.23）。

- 13. 在**ListItem 属性**窗格下的**Text**属性中*键入* **Apple**，然后按 **ENTER** 键。**ListItem** 数组的文本将更改为 **Apple**，如图ASP-2.24所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_493_1.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_493_2.png)

- 14. 在**成员**窗格下再添加两个项，并将它们的文本设置为 **Mango** 和 **Banana**（图ASP-2.25）。

- 15. *单击* **确定**按钮以关闭对话框，如图ASP-2.25所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_494_0.png)

图ASP-2.25

**Default.aspx** 网页上的 **ListBox** 控件显示了我们在该控件的 **Items** 集合中刚刚添加的项，如图ASP-2.26所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_494_1.png)

图ASP-2.26

- 16. *双击* **Default.aspx** 网页上的**添加**按钮，并在**添加**按钮控件的 **Click** 事件中*添加*清单2.3中给出的代码：

**清单2.3：** 演示处理 Button1 控件 Click 事件的代码

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    ListBox1.Items.Add(TextBox1.Text);
    TextBox1.Text = " ";
}
```

前面的代码片段将 **TextBox1** 控件的文本添加到 **ListBox1** 控件中。

- 17. *双击* **Default.aspx** 网页上的**移除**按钮，并在**移除**按钮控件的 **Click** 事件中添加清单2.4中给出的代码：

**清单2.4：** 演示处理 Button2 控件 Click 事件的代码

```csharp
protected void Button2_Click(object sender, EventArgs e)
{
    ListBox1.Items.Remove(ListBox1.SelectedItem);
}
```

当你单击**移除**按钮时，前面的代码片段会从 **ListBox1** 控件中移除所选项。

- 18. 按 F5 键运行应用程序（图ASP-2.27）。

- 19. 在“输入水果名称”文本框中键入 Orange，然后单击“添加”按钮（图ASP-2.27）。

水果名称 Orange 将添加到 ListBox 控件中，如图ASP-2.28所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_495_0.png)

图ASP-2.27

![](img/9862a98a1a2d3bb14334137965a1ec60_495_1.png)

图ASP-2.28

你也可以从 ListBox 控件中移除项。在本例中，我们要移除项 **Banana**。

- 20. 选择要移除的项，例如 **Banana**，然后单击**移除**按钮。列表项（**Banana**）将从 ListBox 控件中移除（图ASP-2.29）。

列表项 Banana 已从 ListBox1 中移除，如图ASP-2.30所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_495_2.png)

图ASP-2.29

![](img/9862a98a1a2d3bb14334137965a1ec60_495_3.png)

图ASP-2.30

让我们讨论 **RadioButton** 控件。

## 使用 RadioButton 控件

**RadioButton** 控件是一种 ASP.NET Web 服务器控件，用于接受用户输入。**RadioButton** 类用于从网页上显示的一组选项中做出单一选择。为了一次只选择一个选项，你需要通过设置 **GroupName** 属性来对 **RadioButton** 控件进行分组。**RadioButton** 类包含在 **System.Web.UI.WebControls** 命名空间中。RadioButton 控件的重要属性列在表2.11中：
