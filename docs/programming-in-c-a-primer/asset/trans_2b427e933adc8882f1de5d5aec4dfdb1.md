

# WindowForms 和基于 Web 的 .NET 421 应用程序开发

注意：当我们打开 Default.aspx 页面的设计视图时，包含 Button 和 Label 等控件的工具箱会自动出现。

- 6. 从工具箱拖动一个 Label 控件到 Default.aspx 页面以将控件添加到页面。
- 7. 使用属性窗口将 Label 控件的 Text 属性值更改为 Using Controls in ASP.NET and C#。
- 8. 使用属性窗口按需更改 Label 控件的 BackColor 属性。
- 9. 同样，在 Default.aspx 页面添加另外四个 Label 控件。
- 10. 使用属性对话框将你添加的第一个 Label 控件的 Text 属性更改为 Name。
- 11. 使用属性对话框将你添加的第二个 Label 控件的 Text 属性更改为 Address。
- 12. 使用属性对话框将你添加的第三个 Label 控件的 Text 属性更改为 City。
- 13. 使用属性对话框将你添加的第一个 Label 控件的 Text 属性更改为 Gender。
- 14. 从工具箱拖动一个 TextBox 控件到 Default.aspx 页面以将控件添加到页面。
- 15. 同样在 Default.aspx 页面添加另一个 TextBox 控件。
- 16. 拖动一个 DropDownList 控件到 Default.aspx 页面以将控件添加到页面。
- 17. 在属性窗口中单击 Items 属性以显示椭圆按钮，如图 20.32 所示。

![](img/bae4ee2c7c29c052feb3b9a9c5659998_422_0.png)

18. 单击椭圆按钮以显示 ListItem Collection Editor，如图 20.33 所示。

![](img/bae4ee2c7c29c052feb3b9a9c5659998_423_0.png)

## 图 20.33 ListItem Collection Editor

单击 Add 按钮以向 DropDownList 控件添加一个项目。图 20.34 显示了为 DropDownList 控件添加项目后的列表集合编辑器。

![](img/bae4ee2c7c29c052feb3b9a9c5659998_423_1.png)

## 图 20.34 添加项目后的 Listitem Collection Editor

在 Text 属性旁边的可编辑文本框中输入诸如 Select 之类的文本以指定新项目的文本。

- 21. 同样向 DropDownList 控件添加诸如 Bangalore、Delhi、Calcutta 和 Chennai 之类的项目。
- 22. 单击 OK 按钮关闭 ListItem Collection Editor。
- 23. 从工具箱拖动一个 RadioButton 控件到 Default.aspx 页面以将控件添加到页面。
- 24. 同样，在 Default.aspx 页面添加另一个 RadioButton 控件。
- 25. 将你添加的第一个 RadioButton 控件的 Text 属性值更改为 Male。
- 26. 将你添加的第二个 RadioButton 控件的 Text 属性值更改为 Female。
- 27. 拖动一个 Hyperlink 控件，该控件在工具箱中可用到 Default.aspx 页面以将控件添加到页面。
- 28. 使用属性窗口将 Hyperlink 控件的 Text 属性值更改为 Terms & Conditions。
- 29. 从工具箱拖动一个 CheckBox 控件到 Default.aspx 页面以将控件添加到页面。
- 30. 将 CheckBox 控件的 Text 属性值更改为 Read Terms。
- 31. 从工具箱拖动一个 Button 控件到 Default.aspx 页面以将控件添加到页面。
- 32. 使用属性窗口将 Button 控件的 Text 属性值更改为 Submit Form。
- 33. 使用属性窗口更改 Button 控件的 BackColor 属性。
- 34. 向 Default.aspx 页面添加一个 Label 控件并使用属性窗口按要求更改其 ForeColor 属性。这完成了创建 Default.aspx 页面的任务。图 20.35 显示了添加控件后的 Default.aspx 页面：

![](img/bae4ee2c7c29c052feb3b9a9c5659998_424_0.png)

## 424 C# 编程

注意：当我们创建 ASP.NET 网站时，HyperLink 控件在 Microsoft Visual Studio 2005 中可用。此控件允许我们在基于 Web 的应用程序中创建超链接以在应用程序中包含的页面之间导航。

## 向 Default.aspx 页面添加代码

我们需要向 Default.aspx 页面添加代码以指定诸如隐藏标签和初始化添加到 Default.aspx 页面的控件的值之类的功能。要向 Default.aspx 页面添加代码：

- 1. 右键单击在解决方案资源管理器中出现的 Default.aspx 节点以显示快捷菜单。
- 2. 选择 View Code 选项以显示代码编辑器，其中包含 Default.aspx.cs 文件，其中包含 Page_Load 事件处理程序，如图 20.36 所示。

![](img/bae4ee2c7c29c052feb3b9a9c5659998_425_0.png)

- 3. 在 Page_Load 事件处理程序中输入以下代码以指定隐藏 Default.aspx 页面末尾出现的标签的功能并初始化 TextBox 和 DropDownList 控件。
  
  ```csharp
  Label5.Visible = false;
  if (!IsPostBack)
  {
  	TextBox1.Text = "";
  	TextBox2.Text = "";
  	DropDownList1.SelectedValue = "Select";
  }
  ```

- 4. 单击代码编辑器顶部出现的 Close 按钮关闭代码编辑器。Default.aspx 页面在设计视图中出现。

注意：如果关闭代码编辑器后 Default.aspx 页面出现在源视图中，则我们可以单击 Design 选项卡以显示 Default.aspx 页面的设计视图。

5. 双击文本为 Submit Form 的 Button 控件以显示代码编辑器，其中包含 Default.aspx.cs 文件，其中包含 Button_Click 事件处理程序，如图 20.37 所示。

![](img/bae4ee2c7c29c052feb3b9a9c5659998_426_0.png)

图 20.37 带有 Button_Click 处理程序的代码编辑器

6. 在 Button_Click 事件处理程序中输入以下代码以指定显示末尾出现的标签的功能并检查 RadioButton 和 TextBox 等控件的值以确定它们是否为空。

## 程序 20.11 BUTTON-CLICK 处理程序的代码

```
Label5.Visible = true;
if (TextBox1.Text == "" || TextBox2.Text == "" || DropDownList1.SelectedValue == "Select" ||
(RadioButton1.Checked == false && RadioButton2.Checked == false) || CheckBox1.Checked == false)
{
Label5.Text = "All values are required";
}
else
{
if (RadioButton1.Checked==true)
Response.Redirect("show.aspx?Name=" + TextBox1.Text+ "&Address=" + TextBox2.Text +
"&City=" + DropDownList1.SelectedValue + "&Gender=" + RadioButton1.Text);
else
Response.Redirect("show.aspx?Name=" + TextBox1.Text + "&Address=" + TextBox2.Text +
"&City=" + DropDownList1.SelectedValue + "&Gender=" + RadioButton2.Text);
}
```

这完成了向 Default.aspx 页面添加代码的过程。

## 创建 terms.aspx 页面

terms.aspx 页面允许你查看与作为基于 Web 的应用程序创建的 ASP.NET 网站相关的条款和条件。要创建 terms.aspx 页面：

- 1. 向 Website1 基于 Web 的应用程序添加一个名为 terms.aspx 的新页面。terms.aspx 页面的源视图出现。
- 2. 将在源视图中出现的 title HTML 元素的值更改为 Terms and Conditions Page。
- 3. 在 div HTML 元素下方添加以下代码以在 terms.aspx 页面中显示文本字符串：

```
<font color="blue" face="Verdana"><strong>The terms and conditions of the company is described here.</strong></font>
```

这完成了创建 terms.aspx 页面的过程。图 20.40 显示了添加代码后的 terms.aspx 页面的源视图。

![](img/bae4ee2c7c29c052feb3b9a9c5659998_429_0.png)

图 20.40 添加了 terms.aspx 页面代码的源视图

## 运行 Website1 基于 Web 的应用程序

创建 Website1 基于 Web 的应用程序后，你需要运行该应用程序以测试它是否生成所需的输出。要运行 Website1 基于 Web 的应用程序：

- 1. 按 Ctrl+F5 启动运行 Website1 基于 Web 的应用程序的过程。Default.aspx 页面出现，如图 20.41 所示。
- 2. 在 Name 文本框中输入诸如 Nikita 之类的名称，并在 Address 文本框中输入地址，例如 23, Anjali Apts. Gandhi Colony。

注意：当用户未在 Website1 基于 Web 的应用程序的 Default.aspx 页面中输入任何值时，底部会出现错误消息。

