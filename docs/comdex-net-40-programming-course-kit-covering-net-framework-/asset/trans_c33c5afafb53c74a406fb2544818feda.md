
处理异常会消耗大量系统资源和执行时间。因此，应避免对可预测事件处理异常。可以通过以下两种语句来处理异常：

- try-catch-finally 语句
- throw 语句

下面详细讨论这些语句。

## 使用 try-catch-finally 语句

在 .NET Framework 中，异常在运行时引发和处理。.NET Framework 提供了一个称为 **try-catch-finally** 语句的处理程序来处理异常。使用 try-catch-finally 语句时，应用程序被划分为不同的代码块。最可能引发异常的代码放在 try 块中，处理异常的代码放在 catch 块中。如果发生异常，则执行 catch 块，然后将控制权转移到 finally 块。无论是否发生异常，finally 块始终执行。一个 try 块允许多个 catch 块；但是，一个 try 块只能有一个 finally 块。

如果在 try 语句中引发异常，控制权将转移到关联的 catch 语句，然后转移到 finally 语句（如果存在）。如果 try 语句未引发任何异常，控制权将直接转移到 finally 语句（如果存在）。没有 catch 或 finally 语句的 try 语句会导致语法错误。try 语句必须始终伴随 catch 或 finally 语句。try-catch-finally 语句的语法如下：

```csharp
try
{
    // code which can cause exception
}
catch (exception-declaration)
{
    // the block of code that handles the exception
}
finally
{
    // the block of code to be executed whether the exception is raised or not
}
```

下面通过执行以下步骤创建一个应用程序，以了解 **try-catch-finally** 语句的用法：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏中选择 **文件→新建→项目**。**新建项目**对话框打开。
- 3. 在**新建项目**对话框左窗格的**已安装的模板**部分中选择 **Visual C#→Windows**。
- 4. 在右窗格中选择 **Windows 窗体应用程序** 以创建 Windows 窗体应用程序。
- 5. 在**名称**文本框中输入应用程序名 **try_catch_finallyExample**（也可在光盘中找到），并在**位置**框中输入合适的应用程序位置。
- 6. 单击**确定**按钮关闭**新建项目**对话框。**try_catch_finallyExample** 应用程序即创建完成（图 C#-7.19）。
- 7. 选择 Form1 并按 F4 键打开 Form1 的属性窗口（图 C#-7.19）。
- 8. 将 Form1 窗体的 Text 属性设置为 Try Catch Finally，如图 C#-7.19 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_457_0.png)

图 C#-7.19

- 9. *拖放*表 7.2 中列出的控件到窗体上，并设置它们的属性值：

**表 7.2：要添加到 try_catch_finallyExample 应用程序的控件**

| 控件 | Name 属性值 | Text 属性值 |
|---|---|---|
| 标签 | label1 | 第一个数 |
| 标签 | label2 | 第二个数 |
| 文本框 | textBox1 | [空白] |
| 文本框 | textBox2 | [空白] |
| 按钮 | button1 | 相除 |

- 10. *双击* **相除**按钮，并在该按钮的 Click 事件中键入清单 7.7 给出的代码片段：

### 清单 7.7：显示 Click 事件的代码

```csharp
private void Button1_Click(object sender, EventArgs e)
{
    int num1, num2, result;
    try
    {
        num1 = System.Convert.ToInt32(textBox1.Text);
        num2 = System.Convert.ToInt32(textBox2.Text);
        result = num1 / num2;
        MessageBox.Show(result.ToString());
    }
    catch (DivideByZeroException ex)
    {
        MessageBox.Show("Cannot divide by zero." + "This is a logical error" + ex.ToString());
    }
    finally
    {
        MessageBox.Show("finally block");
    }
}
```

在清单 7.7 中，声明了三个整数变量：num1、num2 和 result。用户输入的数字存储在 num1 和 num2 中，它们的除法结果存储在 result 变量中。最后，使用 MessageBox.Show 方法在消息框中显示结果。可能引发异常的语句写在 try 语句中。如果引发 DivideByZeroException 异常，则 catch 语句处理它，并显示一个包含异常详细描述的消息框。最后，finally 语句执行，并显示一个消息为 finally block 的消息框。

- 11. 按 F5 键执行应用程序。输出显示出来（图 C#-7.20）。
- 12. 分别在第一个数和第二个数文本框中输入值。在本例中，我们输入了 600 和 3（图 C#-7.21）。
- 13. 单击相除按钮（图 C#-7.21）。
    
    出现一个消息框，显示两个数字相除的结果（图 C#-7.21）。
- 14. 单击**确定**按钮以显示 finally 块消息（图 C#-7.21）。

![](img/9862a98a1a2d3bb14334137965a1ec60_458_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_458_1.png)

- 15. 单击**确定**按钮关闭消息框，如图 C#-7.22 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_458_2.png)

- 16. 现在，在第二个数文本框中输入 0，并单击相除按钮。出现一个消息框，其中包含异常的详细描述（图 C#-7.23）。
    
    程序引发异常 System.DivideByZeroException，并显示在消息框中。发生该异常是因为我们尝试将一个数除以零。
- 17. 单击**确定**按钮关闭消息框，如图 C#-7.23 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_458_3.png)

出现另一个消息框，显示 finally 块消息（图 C#-7.24）。

- 18. 单击**确定**按钮关闭消息框，如图 C#-7.24 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_459_0.png)

图 C#-7.24

## 使用 throw 语句

可以使用 throw 语句在应用程序中引发异常。引发的异常可以在 try-catch-finally 语句中处理。throw 语句的语法如下：

```csharp
throw [expression]
```

在前面的语法中，expression 指要引发的异常的信息。不带任何表达式的 throw 语句只能在 catch 语句中使用，其中 throw 语句重新引发当前由 catch 语句处理的异常。

下面通过执行以下步骤创建一个应用程序，以了解如何使用 throw 语句：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏中选择 **文件→新建→项目**。**新建项目**对话框打开。
- 3. 在**新建项目**对话框左窗格的**已安装的模板**部分中选择 Visual C#→Windows。
- 4. 在右窗格中选择 **Windows 窗体应用程序** 以创建 Windows 窗体应用程序。
- 5. 在**名称**文本框中输入应用程序名 **throwStatementExample**（也可在光盘中找到），并在**位置**框中输入合适的应用程序位置。
- 6. 单击**确定**按钮关闭**新建项目**对话框。**throwStatementExample** 应用程序即创建完成（图 C#-7.25）。
- 7. 选择 Form1 并按 F4 键打开 Form1 的属性窗口（图 C#-7.25）。
- 8. 将 **Form1** 窗体的 **Text** 属性设置为 **抛出异常示例**，如图 C#-7.25 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_459_1.png)

图 C#-7.25

- 9. *拖放*表 7.3 中列出的控件到 Form1 窗体上，并设置它们的属性值：

| 控件 | Name 属性值 | Text 属性值 |
|---|---|---|
| 标签 | label1 | 输入数字（0-10） |
| 文本框 | textBox1 | [空白] |
| 按钮 | button1 | 提交 |

- 10. *双击* **提交**按钮，并在该按钮的 *Click* 事件中添加清单 7.8 给出的代码片段：

### 清单 7.8：显示使用 throw 语句抛出异常的代码

```csharp
private void button1_Click(object sender, EventArgs e)
{
    int num1 = 0;
    try
    {
        num1 = System.Convert.ToInt32(textBox1.Text);
        if (num1 >= 0 && num1 <= 10)
        {
            MessageBox.Show("You have entered : " + textBox1.Text);
        }
        else
        {
            throw new Exception("Number should be between 0 and 10");
        }
    }
    catch (Exception ex)
    {
        MessageBox.Show("Exception occurred " + ex.ToString());
    }
}
```

在清单 7.8 中，声明了一个整数变量 **num1**，用于存储 TextBox1 中输入的值。使用 if 语句检查 **num1** 变量中输入的值是否在 0 到 10 之间。如果条件为 true，则出现一个消息框，显示用户输入的数字。如果条件为 false，则引发异常，并将控制权传递给 catch 语句。

- 11. *按* **F5** 键执行应用程序。输出显示出来，如图 C#-7.26 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_460_0.png)

图 C#-7.26

- 12. *在* **输入数字（0-10）** 文本框中输入一个值。在本例中，我们输入了值 12（图 C#-7.27）。
- 13. *单击* **提交**按钮，如图 C#-7.27 所示：

