

```
addValues; // compile-time error, no parentheses
addValues(); // compile-time error, not enough arguments
addValues(39); // compile-time error, not enough arguments
addValues("39", "3"); // compile-time error, wrong types for arguments
```

addValues 方法返回一个 `int` 类型的值。你可以在任何可以使用 `int` 值的地方使用此值。考虑以下示例：

点击此处查看代码图片

```
int result = addValues(39, 39); // 在赋值语句的右侧
showResult(addValues(39, 39)); // 作为另一个方法调用的参数
```

下面的练习将继续“方法（Methods）”的应用。这次，你将检查一些方法调用。

## 检查方法调用

- 1. 返回 Methods 项目。（如果你是从上一个练习继续操作，Visual Studio 2022 已经打开了该项目。如果不是，请从文档文件夹中的 `\Microsoft Press\VCSBS\Chapter 3\Methods` 文件夹打开它。）

- 2. 在代码和文本编辑器窗口中显示 `MainPage.xaml.cs` 的代码。

- 3. 找到 `calculateClick` 方法。然后查看该方法中 `try` 语句和左大括号之后的前两个语句。（你将在第 6 章“管理错误和异常”中学习 try 语句。）

这些语句如下：

点击此处查看代码图片

```
int leftHandSide = System.Int32.Parse(lhsOperand.Text);
int rightHandSide = System.Int32.Parse(rhsOperand.Text);
```

这两个语句声明了两个 `int` 变量：`leftHandSide` 和 `rightHandSide`。注意变量是如何初始化的。在这两种情况下都调用了 `System.Int32` 结构体的 `Parse` 方法。（`System` 是命名空间，`Int32` 是该命名空间中结构体的名称。你将在第 9 章“使用枚举和结构创建值类型”中学习结构体。）你见过这个方法；它接受一个字符串参数并将其转换为 `int` 值。这两行代码获取用户在表单的 `lhsOperand` 和 `rhsOperand` 框中输入的内容并将其转换为 `int` 值。

- 4. 查看 `calculateClick` 方法中的第四条语句（在 `if` 语句和另一个左括号之后）：

点击此处查看代码图片

```
calculatedValue = addValues(leftHandSide, rightHandSide);
```

该语句调用了 `addValues` 方法，将 `leftHandSide` 和 `rightHandSide` 变量的值作为参数传递。`addValues` 方法的返回值存储在 `calculatedValue` 变量中。

- 5. 查看下一条：

```
showResult(calculatedValue);
```

该语句调用了 `showResult` 方法，将 `calculatedValue` 变量中的值作为参数传递。`showResult` 方法没有返回值。

- 6. 在代码和文本编辑器窗口中，找到你之前过的 `showResult` 方法。

该方法的唯一语句是这个：

点击此处查看代码图片

```
result.Text = answer.toString();
```

注意，`toString` 方法调用使用了括号，即使没有参数。

> 提示
> 你可以通过在方法名前面加上对象的名称来调用属于其他对象的方法。在先前的示例中，表达式 `answer.toString()` 调用了属于名为 `answer` 的对象的名为 `toString` 的方法。

## 从方法返回多个值

在某些情况下，你可能想从方法返回多个值。例如，在 Methods 项目中，你可能希望将 `divideValues` 和 `remainderValues` 操作的效果合并到一个方法中，返回操作数相除的结果以及余数。你可以通过返回元组（tuple）来实现这一点。

元组是一个较小的值集合（严格来说，元组包含两个值，但 C# 元组可以包含此更大的集合）。你通过在方法定义中指定类型列表来指示方法返回一个元组——每个返回的值对应一个类型。方法中的 `return` 语句返回一个值列表，如下例所示：

点击此处查看代码图片

```
(int, int) returnMultipleValues(...)
{
    int val1;
    int val2;
    // 计算 val1 和 val2 的值
    return (val1, val2);
}
```

当你调用该方法时，你需要提供变量。如果你只对其中一个值感兴趣，可以使用丢弃（discard）。丢弃是在 C# 7.0 中引入的。以下代码显示了如何创建和调用返回元组的方法。

- 1. 返回 Methods 项目，并在代码和文本编辑器中显示 `MainPage.xaml.cs` 的代码。

- 2. 找到 `divideValues` 和 `remainderValues` 方法并删除它们。

- 3. 在方法体中添加以下代码：

点击此处查看代码图片

```csharp
private (int, int) divide(int leftHandSide, int rightHandSide)
{
    int division = leftHandSide / rightHandSide;
    int remainder = leftHandSide % rightHandSide;
    return (division, remainder);
}
```

- 4. 向上到 `calculateClick` 方法，并在方法末尾找到以下语句：

点击此处查看代码图片

```csharp
else if (division.Checked.Value)
{
    calculatedValue = divideValues(leftHandSide);
}
```

- 5. 删除这段代码。`divideValues` 余数方法不再存在，它们已被单一的 `divide` 方法取代。

- 6. 在被删除的代码处添加以下语句：

点击此处查看代码图片

```csharp
if (division.Checked.Value)
{
    int division, remainder;
    (division, remainder) = divide(leftHandSide, rightHandSide);
    result.Text = $"{division} remainder {remainder}";
}
```

此代码调用了 `divide` 方法。返回值显示在 Result 块中。

- 7. 在解决方案管理器中，双击 `MainPage.xaml` 文件在设计视图窗口显示表单。

- 8. 选择  按钮。然后按 Delete 将从表单中删除。不再需要此选项。

- 9. 在调试菜单上，选择启动调试以编译并运行应用程序。

- 10. 在 Left Operand 框中输入 59；在 Right Operand 框中输入 13；选择 Division，然后 Calculate。

- 11. 验证 Result 框包含“4 remainder 7”。

- 12. 返回 Visual Studio。在调试菜单上，选择停止调试。

## 范围

你创建变量来存储值。你可以在应用程序的各个点创建变量。例如，Methods 项目中的 `calculateClick` 方法创建一个名为 `calculatedValue` 的 `int` 变量并赋值为初始值 0，如下所示：

点击此处查看代码图片

```csharp
private void calculateClick(object sender, RoutedEventArgs e)
{
    int calculatedValue = 0;
    ...
```

该变量在定义处开始存在，`calculateClick` 方法中的后续语句可以使用它。这是一个重要的点：变量只有在被创建后才能被使用。当方法执行结束时，该变量就会消失且无法在其他地方使用。

