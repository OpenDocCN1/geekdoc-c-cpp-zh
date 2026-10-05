

4. 在“添加新项”ParamsArray对话框中，在中间面板中，选择“类模板”。在“名称”框中输入 `Utils.cs`，然后点击“添加”。

创建并向项目添加 `Utils.cs` 文件。它包含一个位于 `ParamsArray` 命名空间下的空类 `Utils`。

5. 为 `Utils` 类添加一个公共静态方法 `Sum`。该方法返回一个 `int` 并接受一个名为 `paramList` 的 `int` 值参数数组。它应该像这样：

点击此处查看代码

```csharp
public static int Sum(params int[] paramList)
{
}
```

实现 `Sum` 方法的第一步是检查 `paramList` 参数。该参数可以包含一组有效的整数，可以为 `null`，也可以是一个长度为 0 的数组。在后两种情况下，很难计算和，因此最佳选择是抛出一个 `ArgumentException` 异常。（你可能会认为整数的和为 0，但在本例中，我们将这种情况视为异常。）

6. 在 `Sum` 方法中添加以下加粗所示的代码。如果 `paramList` 为 `null`，此代码将抛出 `ArgumentException` 异常。`Sum` 方法现在应该如下：

点击此处查看代码

```csharp
public static int Sum(params int[] paramList)
{
    if (paramList == null)
    {
        throw new ArgumentException("Utils.Sum: null parameter list");
    }
}
```

7. 在 `Sum` 方法中添加代码，如果参数列表数组的长度为 0，则抛出 `ArgumentException` 异常，如下粗所示：

点击此处查看代码

```csharp
public static int Sum(params int[] paramList)
{
    if (paramList == null)
    {
        throw new ArgumentException("Utils.Sum: null parameter list");
    }

    if (paramList.Length == 0)
    {
        throw new ArgumentException("Utils.Sum: empty parameter list");
    }
}
```

如果数组通过了两个测试，下一步是让数组中所有元素相加。你可以使用 `foreach` 语句来执行此操作，你需要一个局部变量来保存运行总和。

- 8. 在上一步代码之后，声明一个名为 `sumTotal` 的整数变量并将其初始化为 0。

点击此处查看代码

```csharp
public static int Sum(params int[] paramList)
{
    ...
    if (paramList.Length == 0)
    {
        throw new ArgumentException("Utils.Sum: empty parameter list");
    }

    int sumTotal = 0;
}
```

- 9. 在 `Sum` 方法中添加 `foreach` 语句以遍历 `paramList` 数组。该 `foreach` 循环的主体应该将数组中的每个元素加到 `sumTotal`。在方法末尾，使用 `return` 语句返回 `sumTotal` 的值，如下加粗所示：

点击此处查看代码

```csharp
public static int Sum(params int[] paramList)
{
    int sumTotal = 0;
    foreach (int i in paramList)
    {
        sumTotal += i;
    }
    return sumTotal;
}
```

- 10. 在“生成”菜单上，选择“生成解决方案”，然后确认你的解决方案在没有任何错误的情况下完成生成。

# 测试 Utils.Sum 方法

- 1. 在“代码和文本编辑器”窗口中显示 `Program.cs` 文件。

- 2. 在“代码和文本编辑器”窗口中，删除 `// TODO:` 注释并在 `doWork` 方法中添加以下语句：

点击此处查看图像

```assembly
Console.WriteLine(Utils.Sum(null));
```

- 3. 在“调试”菜单上，选择“转到调试启动”。
程序生成并运行，向控制台写入以下消息：

点击此处查看图像

Exception: Utils.Sum: null parameter list

这确认了第一个检查。

