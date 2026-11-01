
```
return factorial;
}
set
{
    n = value;
}
}
}
```

代码 12.31（续）

13. 构建并运行项目。程序窗口将如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_320_0.png)

图 12.20. 程序窗口

程序按预期计算了阶乘：

![](img/41d82527c4e41cdb7e56259564306ddc_320_1.png)

图 12.21. 阶乘计算结果

我们可以根据需要使用任意多个属性。当需要在类中处理大量变量时，它们非常方便。

## 第13章

![](img/41d82527c4e41cdb7e56259564306ddc_322_0.png)

## C# 中常用类

自本书开始以来，我们一直在项目中使用与事件、变量和操作相关的各种方法。我们还在前几章学习了创建自定义方法和类。在本章中，我们将研究 C# 应用程序开发中非常有用的流行内置类的常用方法，以缩短编程时间。

### 13.1. String 类

如前所述，字符串是由 Unicode 字符组成的集合。基本上，有两个类可以让我们操作字符串：String 类和 StringBuilder 类。

我们将用于操作字符串对象的第一个类是 String 类。String 类位于 .NET 框架的 System 命名空间下，因此在创建新的 C# 项目时即可在代码中使用。换句话说，我们不需要添加新的命名空间即可使用 String 类提供的方法。String 类的常用方法总结在表 13.1 中：

| 方法 | 模板 | 说明 |
|---|---|---|
| Copy() | new_string=String.Copy(string_to_be_copied) | 复制字符串到另一个字符串 |
| Empty() | string_to_be_cleared.Empty() | 清空字符串的内容 |
| Join() | string_to_be_populated =String.Join(separator, array) | 使用指定的分隔符字符将数组的元素复制到字符串中 |
| Split() | string_to_be_split.Split(separator) | 根据分隔符字符拆分字符串 |
| IndexOf() | string_name.IndexOf(searched_character) | 返回字符串中搜索字符的索引 |
| SubString() | string_name.Substring(start, length) | 返回由起始索引和长度指定的子字符串 |
| ToString() | variable.ToString() | 将变量转换为字符串 |
| Concat() | String.Concat(string1, string2) | 合并 string1 和 string2 |

表 13.1. String 类的常用方法（续）

我们现在将在示例项目中使用这些方法。

- 1. 在窗体上添加三个 TextBoxes 和五个 Buttons。
- 2. 将 TextBoxes 的 Name 设置为 string1、string2 和 output。
- 3. 将 Buttons 的 Name 设置为 copyButton、concatButton、substringButton、splitButton 和 emptyButton。
- 4. 分别将 Buttons 的 Text 属性设置为 Copy、Concatenate、Substring、Split 和 Empty。窗体将如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_323_0.png)

图 13.1. 窗体布局

```csharp
private void splitButton_Click(object sender, EventArgs e)
{
    string[] outputString = input1.Text.Split('-');
    foreach (string item in outputString)
    {
        MessageBox.Show(item);
    }
}
```

代码 13.4

请注意，Split() 方法的结果是一个拆分字符串的数组，因此分配给字符串数组。然后，在 foreach 循环中，message box 会逐个显示该数组的元素。

- 10. 最后，将实现 **Empty Button** 的事件处理程序。

我们将清空从 input1 TextBox 获取的字符串，然后将其显示在 output TextBox 中。

```csharp
private void clearButton_Click(object sender, EventArgs e)
{
    string inputString = input1.Text;
    input1String = String.Empty;
}
```

代码 13.5

- 11. 我们已实现所有 Buttons 的方法，并准备构建和运行项目。以下程序窗口将出现：

![](img/41d82527c4e41cdb7e56259564306ddc_325_0.png)

图 13.2. 程序窗口

让我们在输入 TextBoxes 中输入两个字符串并单击 Copy Button。input1 TextBox 的字符串将被复制到一个新字符串中，然后该字符串将显示在 output TextBox 中：

![](img/41d82527c4e41cdb7e56259564306ddc_326_0.png)

图 13.3. 输出 TextBox 中显示的已复制字符串

当我们单击 Concatenate Button 时，两个输入字符串将被连接并显示在输出中：

![](img/41d82527c4e41cdb7e56259564306ddc_326_1.png)

图 13.4. 输出处的连接字符串

然后，单击 Substring Button 以在输出中查看由 input1 的前三个字符组成的子字符串：

![](img/41d82527c4e41cdb7e56259564306ddc_327_0.png)

图 13.5. 输出中显示的子字符串

为了测试 Split Button，我们需要在 input1 TextBox 中有一个带连字符的字符串。因此我将其修改为 Simon-Peter，然后单击 Split Button。字符串将以连字符作为分隔符进行拆分，拆分后的部分将在消息框中显示：

![](img/41d82527c4e41cdb7e56259564306ddc_327_1.png)

图 13.6. 拆分字符串的第一部分

![](img/41d82527c4e41cdb7e56259564306ddc_328_0.png)

图 13.7. 拆分字符串的第二部分

最后，当我们单击 Empty Button 时，字符串将被清除并分配给 output TextBox。由于字符串为空，output TextBox 也将为空：

![](img/41d82527c4e41cdb7e56259564306ddc_328_1.png)

图 13.8. 分配给输出的已清空字符串

### 13.2. StringBuilder 类

StringBuilder 类也有各种操作字符串的方法。然而，与通常的 String 类相比，对于大量字符串元素，它可以更快地执行这些操作。我们需要添加

![](img/41d82527c4e41cdb7e56259564306ddc_330_0.png)

图 13.9. 窗体的布局

请注意，我们需要在 Form1.cs 文件中包含代码行 `using System.Text;` 才能使用 StringBuilder 类。

在处理程序方法正上方的代码行中，创建了一个名为 sbobject 的 StringBuilder 对象。请注意，此代码行位于全局区域，以便可以在代码中的任何位置访问 sbobject。它是通过 StringBuilder() 构造函数方法创建的，这意味着在声明时该对象将为空（即不包含任何字符串）。

在下一行代码中，我们将一个字符串（"John"）追加（添加）到此 StringBuilder 对象。

在最后一行，使用 ToString() 方法将 sbobject 的内容转换为常规字符串以在 output TextBox 中显示。

8. Clear Button 的事件处理程序方法的内容将利用 Clear() 方法清除 sbobject 的内容：

```
private void clearButton_Click(object sender, EventArgs e)
{
    sbObject.Clear();
    displayTextBox.Text = sbObject.ToString();
}
```

代码 13.7

在此事件处理程序方法中，sbobject 的内容被清空，然后显示在 output TextBox 中。

9. 我们将在 Insert Button 的事件处理程序方法中在 sbobject 的指定索引处插入一个字符串。我们将为此目的使用 Insert() 方法：

```csharp
private void insertButton_Click(object sender, EventArgs e)
{
    sbObject.Insert(4, "+");
    displayTextBox.Text = sbObject.ToString();
}
```

代码 13.8

我们在 sbobject 的索引 4 处添加 "+" 字符串，然后在 output TextBox 中显示其内容。

10. 最后，我们将填充 Remove Button 的事件处理程序。我们将按如下方式使用 Remove() 方法：

```csharp
private void removeButton_Click(object sender, EventArgs e)
{
    sbObject.Remove(1, 1);
    displayTextBox.Text = sbObject.ToString();
}
```

代码 13.9

11. 构建并运行项目。程序将如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_331_0.png)

图 13.10. 程序窗口
