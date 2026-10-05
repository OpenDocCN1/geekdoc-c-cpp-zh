

`openFileClick` 方法中的最后两个语句非常重要。它们看起来如下：

点击查看代码图像

```
TextReader reader = new
StreamReader(inputStream.AsStreamForRead());
displayData(reader);
```

第一条语句声明了一个名为 `reader` 的 `TextReader` 变量。`TextReader` 是 .NET 库提供的一个类。你可以用它从文件等源读取字符流。它位于 `System.IO` 命名空间。该语句使用户在 `FilePicker` 对象指定的文件的数据对 `TextReader` 对象可用，然后就可以读取文件数据。

最后一条语句调用了名为 `displayData` 的方法，并将 `reader` 作为参数传递给该方法。`displayData` 方法使用 `reader` 对象读取数据显示在屏幕上（一旦你编写了完成此任务的代码它就会执行）。

- 8. 检查 `displayData` 方法。它目前看起来如下：

点击查看代码图像

```
private void displayData(TextReader reader)
{
  // TODO: add while loop here
}
```

你可以看到，除了注释之外，该方法目前是空的。你需要在这里添加代码来获取并显示数据。

- 9. 将 `// TODO: add while loop here` 注释替换为以下语句：

```
source.Text = "";
```

`source` 变量引用表单上的大框。将它的 `Text` 属性设置为空字符串 (`""`) 可以清除此框中当前显示的任何文本。

- 10. 在你添加到 `displayData` 方法的上一行之后，添加以下语句：

```
string line = reader.ReadLine();
```

该语句声明了一个名为 `line` 的字符串变量，并调用 `reader.ReadLine` 方法从文件中读取第一行并存入该变量。该方法返回文件的下一行文本，或者在没有更多行可读时返回一个名为 `null` 的特殊值。

- 11. 在你刚刚输入的代码之后，向 `displayData` 方法添加以下语句：

点击查看代码图像

```
while (line is not null)
{
    source.Text += line + '\n';
    line = reader.ReadLine();
}
```

这是一个 `while` 循环，它每次迭代一次文件，直到没有更多可用行为止。

`while` 循环开头的布尔表达式检查 `line` 变量的值。如果它不是 `null`，循环体会将当前行文本追加到 `source` 框的 `Text` 属性中，并带有换行符 (`'\n'`)。（`TextReader` 的 `ReadLine` 方法在读取每行时会去掉换行符，因此代码需要将其添加回去。）然后 `while` 循环在执行下一次迭代之前读取下一行文本。当文件中没有更多文本读且 `ReadLine` 方法返回 `null` 值时，`while` 循环结束。

> 注意
> 你也可以使用 `!= null` 来测试空值。然而，`is not null` 表达式更具可读性。

- 12. 在 `while` 循环结束的大括号之后输入以下语句：

```
reader.Dispose();
```

该语句释放与文件相关的资源并关闭它。这是一个良好的习惯，因为它使得其他应用程序可以使用该文件，并释放了访问文件时使用的任何内存和其他资源。

- 13. 在调试（Debug）菜单上，选择启动调试（Start Debugging）。

- 14. 当表单出现时，选择打开文件（Open File）。

- 15. 在打开对话框中，移动到文档文件夹中的 `\Microsoft\VCSBS\Chapter 5\WhileStatement\WhileStatement` 文件夹，选择 `MainPage.xamlcs` 文件，然后选择打开。

> 注意
> 不要尝试打开不包含文本的文件。如果你尝试打开可执行程序或图形文件，例如应用程序将仅显示文件中二进制信息的文本表示。如果文件很大，可能会挂起应用程序，需要你强制终止它。

这一次，所选文件的内容出现在框中；你应该能识别出你一直在编辑的代码。下面的图像显示了应用程序的运行情况：

滚动框中的文本并找到 `displayData` 方法。验证该方法包含你刚刚添加的代码。

- 17. 返回 Visual Studio 并停止调试。

# 编写 for 语句

在 C# 中，大多数 `while` 语句具有以下通用结构：

```
initialization
while (Boolean expression)
{
    statement
    update control variable
}
```

C# 中的 `for` 语句通过组合初始化、布尔表达式和更新控制变量的代码，为这种结构提供了一个更正式的版本。你会发现 `for` 语句非常有用，因为在 `for` 语句中，很难意外遗漏初始化或更新控制变量的代码，所以你不可能写出无限循环的代码。以下是 `for` 语句的语法：

点击查看代码图像

```
for (initialization; Boolean expression; update control variable)
statement
```

构成 `for` 结构主体的语句可以是单行代码，也可以是花括号括的块。

你可以将早之前显示 0 到 9 整数的 `while` 循环重写为如下 `for` 循环：

```
for (int i = 0; i < 10; i++)
{
  Console.WriteLine(i);
}
```

初始化只发生一次，位于循环的最开始。然后，如果布尔表达式为 `true`，则执行语句。发生控制变量更新，然后重新评估布尔表达式。如果条件仍然为 `true`，则再次执行语句，更新控制变量，再次重新评估布尔表达式，依此类推。

注意初始化只发生一次，循环体语句始终在更新之前执行，且更新发生在布尔表达式重新评估之前。

> 提示
> 与 `while` 语句一样，即使 `for` 循环体只包含单个语句，始终使用代码块也被认为是一种良好的习惯。如果你以后在循环体中添加更多语句，这种方法将确保你的代码每次迭代时都执行。

你可以省略 `for` 语句的三个部分之一。如果你省略了布尔表达式，它默认为 `true`，因此下面的 `for` 语句将无限运行：

点击查看代码图像

```
for (int i = 0; i++)
{
    somebody stop
}
```

如果你省略了初始化和更新部分，你就有了一个写法奇怪的 `while` 循环：

```
int i = 0;
for (; i < 10; )
{
    i++;
    }
```

> 注意
> `for` 语句的初始化、布尔表达式和更新控制变量部分必须始终用分号分隔，即使它们被省略了。

你还可以在 `for` 循环中提供多个初始化和更新（尽管只能有一个布尔表达式）。要实现这一点，用逗号分隔各种初始化和更新，如下所示：

点击查看代码图像

```
for (int i = 0, j = 10; i <= j; i++, j--)
{
    ...
}
```

作为最后一个示例，是将前面的练习中的 `while` 循环重写为 `for` 循环：

点击查看代码图像

```
for (string line = reader.ReadLine(); line is not null; line =
    reader.ReadLine())
{
    source.Text += line + '\n';
}
```

# 理解语句范围

你可能注意到可以在 `for` 语句的初始化部分声明变量。变量的作用域是 `for` 语句体并在 `for` 语句结束时消失。此规则有两个重要的后果。首先，在 `for` 语句结束后你无法使用该变量，因为它不再在作用范围内。这是一个示例：

点击查看代码图像

```
for (int i = 0; i < 10; i++)
{
    ...
}
Console.WriteLine(i); // 编译错误
```

其次，你可以编写两个或多个使用相同变量名的 `for` 语句，因为每个变量都在不同的作用域内，如下代码所示：

点击查看代码图像

```
for (int i = 0; i < 10; i++) { ... } for (int i = 0; i < 20; i += 2) // OK { ... }
```

