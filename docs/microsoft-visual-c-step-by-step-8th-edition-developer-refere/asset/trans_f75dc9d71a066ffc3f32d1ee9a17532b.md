

```
StreamReader(inputStream.AsStreamForRead());
displayData(reader);
```

第一条语句声明了一个名为 reader 的 TextReader 变量。TextReader 是 Microsoft.NET Framework 提供的类，可用于从文件等来源读取字符流。它位于 System.IO 命名空间中。此语句使用户在 FileOpenPicker 中指定的文件中的数据可供 TextReader 对象使用，然后该对象可用于从文件中读取数据。最后一条语句调用名为 displayData 的方法，将 reader 作为参数传递给该方法。displayData 方法使用 reader 对象读取数据并将其显示到屏幕上（或者在您编写完成此操作的代码后才会这样做）。

8. 检查 displayData 方法。它目前看起来像这样：

Click here to view code image

```
private void displayData(TextReader reader)
{
    // TODO: add while loop here
}
```

您可以看到，除了注释外，此方法目前是空的。这里需要添加获取和显示数据的代码。

9. 用以下语句替换 // TODO: add while loop here 注释：

```
source.Text = "";
```

source 变量指的是表单上的大文本框。将其 Text 属性设置为空字符串（“”）会清除当前显示在此文本框中的任何文本。

10. 在您刚刚添加到 displayData 方法的上一行之后添加以下语句：

Click here to view code image

```
string line = reader.ReadLine();
```

此语句声明一个名为 line 的字符串变量，并调用 reader.ReadLine 方法将文件中的第一行读入此变量。此方法返回文件中的下一行文本，或在没有更多行可读时返回一个名为 null 的特殊值。

11. 在 displayData 方法中，在您刚刚输入的代码之后添加以下语句：

Click here to view code image

```
while (line != null)
{
    source.Text += line + '\n';
    line = reader.ReadLine();
}
```

这是一个 while 循环，它一次一行地遍历文件，直到没有更多行可用。

while 循环开头的布尔表达式检查 line 变量中的值。如果它不是 null，则循环体通过将其附加到 source 文本框的 Text 属性以及一个换行符（'\n'——TextReader 对象的 ReadLine 方法在读取每一行时都会去掉换行符，因此代码需要将其重新添加）来显示当前行文本。while 循环然后在执行下一次迭代之前读取下一行文本。while 循环在文件中没有更多文本可读且 ReadLine 方法返回 null 值时结束。

+   12. 在 while 循环末尾的右大括号之后输入以下语句：

```
reader.Dispose();
```

此语句释放与文件关联的资源并关闭它。这是良好的做法，因为它使其他应用程序能够使用该文件，并释放用于访问文件的任何内存和其他资源。

+   13. 在 Debug 菜单上，单击 Start Debugging。

+   14. 当表单出现时，单击 Open File。

+   15. 在 Open file picker 或 Open 对话框中，移动到您的 Documents 文件夹中的 \Microsoft Press\VCSBS\Chapter 5\WhileStatement\WhileStatement 文件夹，选择文件 MainPage.xaml.cs，然后单击 Open。

# Note

不要尝试打开不包含文本的文件。如果您尝试打开可执行程序或图形文件，例如，应用程序将简单地显示此文件中二进制信息的文本表示。如果文件很大，它可能会使应用程序挂起，需要您强制终止它。

这次，所选文件的内容出现在文本框中——您应该能认出您一直在编辑的代码。以下图像显示了应用程序的运行情况：

16. 滚动文本框中的文本并找到 displayData 方法。验证此方法是否包含您刚刚添加的代码。

17. 返回 Visual Studio 并停止调试。

## Writing for statements

在 C# 中，大多数 while 语句具有以下一般结构：

```
initialization
while (Boolean expression)
{
    statement
    update control variable
}
```

C# 中的 for 语句通过将初始化、布尔表达式和更新控制变量的代码组合在一起，为这种构造提供了一个更正式的版本。您会发现 for 语句很有用，因为在 for 语句中，很难意外地遗漏初始化或更新控制变量的代码，因此您不太可能编写无限循环的代码。以下是 for 语句的语法：

Click here to view code image

![](img/16f6e3fe08f01ddadb2741a92c392b0e_159_0.png)

```
for (initialization; Boolean expression; update control variable)
    statement
```

构成 for 构造体的语句的主体可以是一行代码，也可以是用大括号括起来的代码块。

您可以将前面显示的用于显示 0 到 9 的整数的 while 循环重写为以下 for 循环：

```
for (int i = 0; i < 10; i++)
{
    Console.WriteLine(i);
}
```

初始化只发生一次，在循环开始时。然后，如果布尔表达式计算为 true，则语句运行。控制变量更新发生，然后布尔表达式重新评估。如果条件仍然为 true，则再次执行语句，更新控制变量，再次评估布尔表达式，依此类推。

请注意，初始化只发生一次，循环体中的语句总是在更新之前执行，并且更新在布尔表达式重新评估之前发生。

# Tip

与 while 语句一样，即使 for 循环的主体只包含单个语句，也被认为是一种良好的做法，始终使用代码块。如果您以后向 for 循环的主体添加其他语句，这种方法将有助于确保您的代码始终作为每次迭代的一部分执行。

您可以省略 for 语句的三个部分中的任何一个。如果省略布尔表达式，它默认为 true，因此以下 for 语句会无限运行：

Click here to view code image

```
for (int i = 0; ;i++)
{
    Console.WriteLine("somebody stop me!");
}
```

如果您省略初始化和更新部分，您将得到一个拼写奇怪的 while 循环：

```
int i = 0;
for (; i < 10; )
{
    Console.WriteLine(i);
    i++;
}
```

# Note

for 语句的初始化、布尔表达式和更新控制变量部分必须始终用分号分隔，即使它们被省略。

您也可以在 for 循环中提供多个初始化和多个更新。（只能有一个布尔表达式。）要实现这一点，请用逗号分隔各种初始化和更新，如以下示例所示：

Click here to view code image

```
for (int i = 0, j = 10; i <= j; i++, j--)
{
    ...
}
```

作为最后一个示例，这里是前面练习中的 while 循环重写为 for 循环：

Click here to view code image

```
for (string line = reader.ReadLine(); line != null; line = reader.ReadLine())
{
    source.Text += line + '\n';
}
```

## Understanding for statement scope

您可能已经注意到，您可以在 for 语句的初始化部分声明一个变量。该变量的作用域限定为 for 语句的主体，并在 for 语句结束时消失。此规则有两个重要后果。首先，您不能在 for 语句结束后使用该变量，因为它不再在作用域内。以下是一个示例：

Click here to view code image

```
for (int i = 0; i < 10; i++)
{
    ...
}
Console.WriteLine(i); // compile-time error
```

其次，您可以编写两个或多个 for 语句重用相同的变量名，因为每个变量都在不同的作用域中，如以下代码所示：

Click here to view code image

```
for (int i = 0; i < 10; i++)
```
