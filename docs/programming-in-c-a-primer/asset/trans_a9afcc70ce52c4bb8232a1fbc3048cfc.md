
- 17. 从列表中选择 True，使 Label 控件中显示的文本变为粗体。
- 18. 从工具箱中将一个 RadioButton 控件拖到 FirstForm 窗体上，以添加该 RadioButton 控件。
- 19. 同样，在 FirstForm 窗体上再添加一个 RadioButton 控件。
- 20. 在“属性”窗口中，将已添加的第一个 RadioButton 控件的 Text 属性值更改为 Check factorial。
- 21. 在“属性”窗口中展开 Font 节点，以显示 Bold 选项。
- 22. 单击 Bold 选项旁边的可编辑文本框，以显示一个箭头。
- 23. 单击该箭头，显示包含 True 和 False 值的列表。
- 24. 从列表中选择 True，使 RadioButton 控件中显示的文本变为粗体。
- 25. 同样，在“属性”窗口中将第二个 RadioButton 控件的 Text 属性值更改为 Check Prime Number。
- 26. 使用“属性”窗口中的 Font 节点，将第二个 RadioButton 控件显示的文本 Check Prime Number 设为粗体。
- 27. 从工具箱中将一个 Button 控件拖到 FirstForm 窗体上，以将该控件添加到窗体中。
- 28. 在“属性”窗口中将 Button 控件的 Text 属性值更改为 Start。
- 29. 在“属性”窗口中展开 Font 节点，以显示 Bold 选项。
- 30. 单击 Bold 选项旁边的可编辑文本框，以显示一个箭头。
- 31. 单击该箭头，显示包含 True 和 False 值的列表。
- 32. 从列表中选择 True，使 Button 控件中显示的文本变为粗体。
- 33. 从工具箱中将另一个 Button 控件添加到 FirstForm 窗体。
- 34. 在“属性”窗口中将该 Button 控件的 Text 属性值更改为 Exit。
- 35. 根据要求，使用“属性”窗口更改所添加的两个 Button 控件的 BackColor 属性。
- 36. 选择添加到 FirstForm 窗体中的第一个 Button 控件，以在“属性”窗口中显示 ForeColor 选项，如图 20.18 所示。
- 37. 单击 ForeColor 选项旁边的可编辑文本框中出现的箭头，以显示颜色调色板。
- 38. 从调色板中选择一种颜色，以更改第一个 Button 控件中显示文本的颜色。
- 39. 以更改第一个 Button 控件中文本颜色的相同方式，更改第二个 Button 控件中显示文本的颜色。这样就完成了创建 FirstForm 窗体的任务。图 20.19 显示了带有已添加控件的 FirstForm 窗体：

![](img/bae4ee2c7c29c052feb3b9a9c5659998_411_0.png)

![](img/bae4ee2c7c29c052feb3b9a9c5659998_412_0.png)

图 20.19 设计视图中的 FirstForm 窗体

## 向 FirstForm 窗体添加代码

在 FirstForm 窗体中，我们需要添加代码来指定用于导航到阶乘窗体或 PrimeNo 窗体的功能。要向 FirstForm 窗体添加代码：

- 1. 双击带有 Start 文本的 Button 控件，显示 Code Editor，其中 FirstForm.cs 文件与 FirstForm 窗体关联，如图 20.20 所示。
- 2. 将以下代码添加到 Code Editor 中出现的 button1_Click 事件处理程序，以指定用于显示窗体以计算阶乘和检查素数的功能。

### 程序 20.8 显示窗体

```csharp
if (radioButton1.Checked == true)
{
    factorial f1 = new factorial();
    f1.Show();
}
else if (radioButton2.Checked == true)
{
    PrimeNo f2 = new PrimeNo();
    f2.Show();
}
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_413_0.png)

图 20.20 FirstForm 窗体的代码编辑器窗口

- 3. 单击 Code Editor 顶部出现的由叉号表示的 Close 按钮以关闭编辑器。此时出现 FirstForm 窗体的 FirstForm.cs [Design] 视图。
- 4. 双击带有 Exit 文本的 Button 控件，打开带有 FirstForm.cs 文件和 button2_Click 事件处理程序的 Code Editor。
- 5. 在 button2_Click 事件处理程序中添加以下代码，以指定用于关闭 FirstForm 窗体的功能：

```csharp
this.Close();
```

这样就完成了向 FirstForm 窗体添加代码的过程。

## 创建 Factorial 窗体

我们需要创建一个阶乘窗体，以便输入一个数字并计算其阶乘。要创建 Factorial 窗体：

添加新项 - SampleWinApp2

模板

Visual Studio 已安装的模板

- 类
- Windows 窗体
- 继承的窗体
- 组件类
- XML 文件
- HTML 页
- 位图文件
- Crystal 报表
- 安装程序类
- Windows 脚本宿主
- 资源文件
- 关于框
- 接口
- 用户控件
- 继承的用户控件
- Web 自定义控件
- 数据集
- XSLT 文件
- 文本文件
- 报表
- Windows 服务
- VBScript 文件
- 应用程序配置文件
- MDI 父窗体
- 类图

一个空的类定义

名称：Class1.cs

添加

取消

图 20.21 “添加新项”对话框

- 14. 使用“属性”窗口更改 Button 控件的 BackColor 属性。
- 15. 选择第一个 Button 控件，在“属性”窗口中将其 Text 属性值更改为 Calculate Factorial。
- 16. 同样，将第二个 Button 控件的 Text 属性值更改为 Back to FirstForm。
- 17. 使用“属性”窗口中的 Font 节点，将 Button 控件中显示的文本设为粗体。
- 18. 更改 Button 控件的 ForeColor 属性，以修改控件中显示文本的颜色。
- 19. 向阶乘窗体添加一个 Label 控件和一个 TextBox 控件。
- 20. 在“属性”窗口中将 Label 控件的 Text 属性值更改为 The Factorial is。
- 21. 使用“属性”窗口中出现的 Font 节点，将 Label 控件中显示的文本设为粗体。
- 22. 使用“属性”窗口更改 Label 和 TextBox 控件的 BackColor 属性。这样就完成了创建阶乘窗体的过程。图 20.22 显示了带有已添加控件的阶乘窗体。

![](img/bae4ee2c7c29c052feb3b9a9c5659998_415_0.png)

图 20.22 设计视图中的阶乘窗体

## 向 Factorial 窗体添加代码

我们需要向阶乘窗体添加代码，以指定用于计算一个数字的阶乘以及关闭阶乘窗体的功能。要向阶乘窗体添加代码：

- 1. 双击带有 Calculate 文本的 Button 控件，显示 Code Editor，其中包含 factorial.cs 文件以及该 Button 控件的 button1_Click 事件处理程序。
- 2. 在 button1_Click 事件处理程序中添加以下代码，以指定用于计算阶乘的功能：

### 程序 20.9 | 计算阶乘

```csharp
int num;
long fact;
if (textBox1.Text.Length > 2)
{
MessageBox.Show("Numbers upto 25 are allowed.");
}
num = Int32.Parse(textBox1.Text);
fact = 1;
while (num >= 1 && num <= 25)
{
fact *= num;
num--;
}
textBox2.Text = fact + "";
```

- 3. 单击 Code Editor 顶部出现的由叉号表示的 Close 按钮以关闭编辑器。此时出现阶乘窗体的 factorial.cs [Design] 视图。
- 4. 双击带有 Back to FirstForm 文本的 Button 控件，打开带有 factorial.cs 文件和 button2_Click 事件处理程序的 Code Editor。
- 5. 在 button2_Click 事件处理程序中添加以下代码，以指定用于关闭阶乘窗体的功能：

```csharp
this.Close();
```

这样就完成了向阶乘窗体添加代码的过程。

## 创建 PrimeNoForm

我们需要创建 PrimeNo 窗体，以便输入一个数字并检查该数字是否为素数。要创建 PrimeNo 窗体：

- 1. 使用解决方案资源管理器向 SampleWinApp 应用程序添加一个名为 PrimeNo 的新窗体。
- 2. 使用“属性”窗口将 PrimeNo 窗体的 Text 属性值更改为 Prime Number Form。
- 3. 使用“属性”窗口更改 PrimeNo 窗体的 BackColor 属性。
- 4. 使用工具箱向 PrimeNo 窗体添加一个 Label 控件和一个 TextBox 控件。
- 5. 使用“属性”窗口更改 Label 控件的 BackColor 属性。
- 6. 使用“属性”窗口将 Label 控件的 Text 属性值更改为 Enter a number:。

