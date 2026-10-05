

```csharp
bool inWord;
...
if (inWord == true) // 正确，但不常用
...
if (inWord) // 更常见且被认为更好的写法
```

# 使用代码块分组语句

注意前面显示的 `if` 语句语法规定，`if ( 布尔表达式 )` 之后只能跟一个语句，`else` 关键字之后也只跟一个语句。然而从语义上来说，当布尔表达式为真时，你可能需要执行多条语句。

你可以将语句组合在一个新方法中然后调用该新方法，更简单的解决方案是将语句组合在一个块（block）中。块简单来说就是一组在左大括号和右大括号之间的语句序列。

在接下来的示例中，将 `seconds` 变量重置为 0 和将 `minutes` 变量加 1 的两个语句组合在一个块中，如果 `seconds` 的值等于 59，则执行整个块：

```csharp
int seconds = 0;
int minutes = 0;
...
if (seconds == 59)
{
    seconds = 0;
    minutes++;
}
else
{
    minutes++;
}
```

> **重要**
> 如果省略了大括号，C# 编译器会将第一条语句（`seconds = 0;`）与 `if` 语句关联。在编译程序时，后续语句（`minutes++`）不会被编译器识别为 `if` 语句的一部分。此外，当编译器遇到 `else` 关键字时，它不会将其与之前的 `if` 语句关联；而是会报告语法错误。因此，良好的做法是始终在块中为 `if` 语句的每个分支定义语句，即使该块只包含单条语句。如果你以后想添加更多代码，这可能会避免你后续很多麻烦。

块还会开启一个作用域。你可以在块内部定义变量，这些变量会在块结束时消失。以下代码片段阐明了这一点：

点击此处查看代码图片

```csharp
if (...)
{
    int myVar = 0;
    // 在此处可以使用 myVar
} // myVar 在此处消失
else
{
    // 在此处无法使用 myVar
}
myVar 在此处无法使用
```

# 级联 if 语句

你可以将 `if` 语句嵌套在其他 `if` 语句内部。通过这种，你可以链联一系列布尔表达式，按顺序进行测试，直到其中一个结果为真。

在接下来的示例中，`day` 的值为 0，第一个表达式为真，`dayName` 被赋值字符串 "Sunday"。如果 `day` 的值不为0，第一个测试失败，控制权传递到 `else` 子句，该句执行第二个 `if` 语句并将 `day` 的值与 1 进行比较。第二个 `if` 语句只有在第一个语句为假时才执行。同样，第三个 `if` 语句只有在第一个和第二个测试均为假时才执行，依此类推。

```csharp
if (day == 0)
{
    dayName = "Sunday";
}
 if (day == 1)
{
  dayName = "Monday";
}
else if (day == 2) {
  dayName = "Tuesday";
}else if (day == 3) {
  dayName = "Wednesday";
}else if (day == 4) {
  dayName = "Thursday";
}else if (day == 5) {
  dayName = "Friday";
}else if (day == 6) {
  dayName = "Saturday";
}else {
  dayName = "unknown";
}
```

在接下来的练习中，你将编写一个使用级联 if 语句来比较两个日期的方法。

# 编写 if 语句

- 1. 启动 Microsoft Visual Studio 2022，如果它尚未运行。
2. 打开 Selection 解决方案，它位于你文档文件夹中的 `\Microsoft Press\VCSBS\Chapter4\Selection` 文件夹。
3. 在“调试（Debug）”菜单上选择“开始调试（Start Debugging）”。

Visual Studio 2022 构建并运行应用程序。表单显示了 DatePicker 控件，名为 `firstName` 和 `secondDate`。它们被标记为 First（第一个）和 Second（第二个）。

4. 选择“比较（Compare）”。

以下文本出现在窗口下半部分的框中。

点击此处查看代码图片

```text
firstDate == secondDate : False
firstDate != secondDate : True
firstDate < secondDate : False
firstDate <= secondDate : False
firstDate > secondDate : True
firstDate >= secondDate : True
```

布尔表达式 `firstDate == secondDate` 应该是为真的，因为 `firstDate` 和 `secondDate` 都被设置为当前日期。事实上，只有小于运算符和大于等于运算符似乎工作正常。

5. 回到 Visual Studio 2022。在“调试（Debug）”菜单上，选择“停止调试（Stop Debugging）”。

6. 在代码和文本编辑器窗口中显示 `MainPage.xmlcs` 文件的代码。

7. 找到 `compareClick` 方法，它看起来应该是这样的：

点击此处查看代码图片

```csharp
private void compareClick(object sender, EventArgs e)
{
    int diff = dateCompare(first.Date.LocalDateTime,
    secondDate.Date.LocalDateTime);
    info.Text = "";
    show("firstDate = secondDate", diff == 0);
    show("firstDate != secondDate", diff != 0);
    show("firstDate < secondDate", diff < 0);
    show("firstDate <= secondDate", diff <= 0);
    show("firstDate > secondDate", diff > 0);
    show("firstDate >= secondDate", diff >= 0);
}
```

此 `compareClick` 方法在用户选择“比较（Compare）”按钮时运行。该方法在表单下半部分显示比较结果。

