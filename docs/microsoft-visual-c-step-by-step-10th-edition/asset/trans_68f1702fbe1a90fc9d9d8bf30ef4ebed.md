
5.向下滚动代码并找到 `showFloatValue` 方法，它看起来如下：

点击此处查看代码图像

```csharp
private void showFloatValue()
{
    float floatVar;
    floatVar = 0.42F;
    value.Text = floatVar.ToString();
}
```

该方法的体包含三个语句。

- 第一条语句声明了一个名为 `floatVar` 的类型为 `float` 的变量。
- 第二条语句为 `floatVar` 赋值值 `0.42F`。

> 请记住，F 类型后缀表示 0.42 应被视为 float 值。如果你忘记了 F，则值 0.42 将被视为 double 类型，你的程序将无法编译，因为在不编写额外代码的情况下，你无法将一种类型的值赋值给不同类型的变量。C# 在这方面非常严格。

- 第三个语句在表单的文本框中显示该变量的值。这条语句需要你注意。如第 1 章所示，在框中显示项目的方法是设置其 `Text` 属性（在第 1 章中是通过使用 XAML 实现的）。你也可以通过编程方式执行此任务，这正是这里正在发生的。注意，你通过使用运行方法时看到的点符号语法来访问对象的属性。（还记得第 1 章的 `Console.WriteLine` 吗？）此外，你放入属性中的数据必须是字符串而不是数字。如果你尝试将数字赋值给 `Text` 属性，你的程序将无法编译。幸运的是，.NET 库通过 `ToString` 方法提供了一些帮助。

.NET 库中的每种数据类型都有 `ToString` 方法。`ToString` 的目的是将对象转换为其字符串表示。`showFloatValue` 方法使用 float 变量 `floatVar` 的 `ToString` 方法生成该变量值的字符串版本。你可以安全地将此字符串赋值给 `value`框的 `Text` 属性。当你创建自己的数据类型和类时，你可以定义 `ToString` 方法的自己的实现，以指定你的类如何表示为字符串。你将在第 7 章“创建和管理类与对象”中学习更多内容。

6. 在代码和文本编辑器窗口中，找到 `showIntValue` 方法：

点击此处查看代码图像

```csharp
private void showIntValue()
{
    value.Text = "to do";
}
```

当你在列表框中选择 `int` 类型时，会调用 `showIntValue` 方法。

7. 在 `showIntValue` 方法的开头，即大括号之后的新行，添加以下**加粗**的两个语句：

点击此处查看代码图像

```csharp
private void showIntValue()
{
    int intVar;
    intVar = 42;
    value.Text = "to do";
}
```

第一条语句创建了一个名为 `intVar` 的变量，它可以保存一个 `int` 值。第二条语句为该变量赋值值 42。

8. 在该方法的原始语句中，将字符串 "to do" 更改为 `intVar.ToString()`。

该方法现在看起来应该完全如下：

点击此处查看代码图像

```csharp
private void showIntValue()
{
    int intVar;
    intVar = 42;
    value.Text = intVar.ToString();
}
```

9. 在“调试”菜单上，选择“启动调试”。
表单再次出现。

10. 在“选择数据类型”列表中，选择 `int`。确认值 42 显示在“示例值”框中。

11. 返回 Visual Studio，然后在“调试”菜单上，选择“停止调试”。

12. 在代码和文本编辑器 窗口中，找到 `showDoubleValue` 方法。

13. 完全按照下方代码中**加粗**字体所示的内容编辑 `showDoubleValue` 方法：

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_124_0.png)

```csharp
private void showDoubleValue()
{
    double doubleVar;
    doubleVar = 0.42;
    value.Text = doubleVar.ToString();
}
```

这段代码与 `show` 方法类似，不同在于它创建名为 `doubleVar` 的变量，保存 double 值并被赋值为 0.42。

14. 在代码和文本编辑器窗口中，找到 `showBoolValue` 方法。

15. 完全按照如下所示编辑 `showBoolValue` 方法：

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_124_1.png)

```csharp
private void showBoolValue()
{
    bool boolVar;
    boolVar = false;
    value.Text = boolVar.ToString();
}
```

同样，这段代码与之前的示例相似，但 `boolVar` 只保存一个布尔值（true 或 false）。在这种情况下，赋值的值是 false。

点击此处查看代码图像

```csharp
//编译时错误
Console.WriteLine("Gillingham" - "Forest Green Rovers");
```

然而，你可以使用 `+` 运算符拼接字符串值。你需要小心，因为这可能会导致意外的结果。例如，以下语句向控制台写入 431（而不是 44）：

点击此处查看代码图像

```csharp
Console.WriteLine("43" + "1");
```
（注：OCR 文本在结尾处截断了，但根据上下文“431 (not 44)”，代码可能是 "43" + "1"）
