

![](img/36e48639a06772bcb0fa1ea2525b33a3_367_0.png)

**图 6-5** .NET 的类库

选择 `System.Windows.Forms` 组件后，你可以使用 `MessageBox` 类，但需要从系统级别开始指定该类所在命名空间的完整名称。如果不执行后面的步骤 2，那么对 `MessageBox` 的 `Show()` 方法的任何引用都需要使用如下完全限定名：

```
System.Windows.Forms.MessageBox.Show()
```

- 2. 通过添加 `using` 指令，你可以使用 `System.Windows.Forms` 命名空间中定义的类型，而无需限定名称。将以下 `using` 指令添加到示例 6-6 程序中：

    ```
    using System.Windows.Forms;
    ```

> **注意** 仅仅包含 `using` 指令是不够的；还必须添加对程序集的引用。

`MessageBox` 类的 `Show()` 方法显示一个预定义对话框，该对话框可以包含文本、标题栏标题、特殊按钮和图标。消息框通常用于显示简短消息，但也可用于接受输入，其形式是允许用户从按钮中做出选择。消息框被视为对话框，可以显示并接受对“是”、“否”、“取消”、“中止”和“确定”按钮的简单单击。使用选择语句，你可以编写表达式来确定单击了哪个按钮。在后续章节中，你将学习为更大量的输入创建窗体。你的窗体将包含文本框、标签、列表框、组合框、菜单、单选按钮以及许多其他类型的控件。目前，MessageBox 将输入限制为对话框类型的控件。

`MessageBox` 类的 `Show()` 方法已重载。在其最简单的形式中，一个文本字符串显示在对话框窗口中。示例 6-6 中对 `MessageBox.Show()` 方法的调用包含如下两个参数：

```
MessageBox.Show(result, "1 - 10 and their squares");
```

第一个参数 result 是显示在窗口中的字符串。变量 result 的值来自循环体内部。每次经过循环体时，文本都会连接到 result 的末尾。为进行间隔，添加了制表符和换行符（'\t' 和 '\n'）。每次经过循环时，制表符作为第一个字符被连接。换行符（Enter 键）在每次经过循环时作为最后一个字符被连接。所有值都放入 result 后，调用 `Show()` 方法时，其内容会显示在窗口中。由于制表符和换行符，内容以表格形式显示。

第二个参数“1 - 10 及其平方”被放置为窗口标题栏中的标题，如图 6-3 所示。如前所述，`Show()` 已重载；你可以将按钮作为第三个参数包含进来。表 6-1 列出了可作为 `Show()` 方法参数出现的按钮的有效选项。

**表 6-1** 对话框按钮参数

| MessageBox 按钮 | 内容说明 |
|---|---|
| MessageBoxButtons.AbortRetryIgnore | 中止、重试和忽略按钮 |
| MessageBoxButtons.OK | 确定按钮 [默认] |
| MessageBoxButtons.OKCancel | 确定和取消按钮 |
| MessageBoxButtons.RetryCancel | 重试和取消按钮 |
| MessageBoxButtons.YesNo | 是、否按钮 |
| MessageBoxButtons.YesNoCancel | 是、否和取消按钮 |

> **注意** 在 Visual Studio 中使用 IntelliSense，可以看到表 6-1 中显示的按钮属性值，以及可包含在 MessageBox 中的不同图标的选项。

你可以按如下方式添加按钮作为第三个参数：

```
MessageBox.Show(result, "1 - 10 and their squares", MessageBoxButtons.YesNoCancel);
```

MessageBox 对话框中包含“是”、“否”和“取消”按钮。

当你查看图 6-3 或图 6-6 时，注意最后一行输出是值 10。然而，条件表达式表明，只要计数器小于 10，循环就会执行。当计数器变为 10 时，循环终止。那么，为什么 10 及其平方会被打印出来？另外，请注意变量 counter 被初始化为 0，但图 6-3 中显示的第一行对应值 1。示例 6-7 中再次包含了该循环，以便你仔细检查。

### 示例 6-7

```
while (counter < 10)
{
    counter++;
    result += " \t" 
        + counter
        + " \t"
        + Math.Pow(counter, 2)
        + "\n";
}
```

注意 counter 在何处递增，以及连接操作在何处发生。因为 counter 作为第一条语句被递增到 1，所以 0 从未被连接。条件表达式最后一次求值为真是在 counter 等于 9 时，因为 (9 < 10) 为真。因为 counter 在循环内、连接之前被递增到 10，所以 10 的值被打印。你应该特别注意循环控制变量更新语句的位置，以及你编写的用于允许正常终止的条件表达式。

MessageBox 是一个对话框。如你所知，对话意味着两个或更多个人之间的交谈，因此对话框是为用户干预而设计的。当执行包含 `MessageBox.Show()` 方法的代码行时，处理会停止，直到用户通过单击 MessageBox 上的“确定”按钮作出响应。在示例 6-6 中，此方法调用放在循环外部。如果放在循环内部，则每次执行 `MessageBox.Show()` 调用时，都需要用户单击。如果方法调用包含在循环体内部，用户将不得不单击 **确定** 10 次。这就是为什么循环体内产生的值被连接到字符串变量的末尾。只包含一次对 `MessageBox.Show()` 方法的调用，而且是在循环体外部。

`MessageBox.Show()` 的重载方法可以接收表 6-1 中的一种按钮类型，以及第四个图标参数，如示例 6-8 所示。

### 示例 6-8

```
MessageBox.Show(result, "1 - 10 and their "
                 + "squares",
                 MessageBoxButtons.YesNoCancel,
                 MessageBoxIcon.Information);
```

图 6-6 显示了当示例 6-8 中的 `Show()` 方法替换示例 6-6 完整程序中出现的 `Show()` 方法时产生的输出。

![](img/36e48639a06772bcb0fa1ea2525b33a3_370_0.png)

**图 6-6** 传给 `MessageBox.Show()` 的按钮和图标参数

.NET Framework 类库包含若干预定义图标，可将它们作为 `MessageBox.Show()` 方法的第四个参数包含进来。表 6-2 列出了你可能会想在应用程序中包含的一些图标。

**表 6-2** 对话框图标参数

| MessageBoxIcons | 符号内容说明 |
|---|---|
| MessageBoxIcon.Asterisk | 圆圈内的小写字母 i |
| MessageBoxIcon.Error | 红色背景圆圈内的白色 X |
| MessageBoxIcon.Exclamation | 黄色背景三角形内的感叹号 |
| MessageBoxIcon.Hand | 红色背景圆圈内的白色 X |
| MessageBoxIcon.Information | 圆圈内的小写字母 i |
| MessageBoxIcon.None | 无符号 |
| MessageBoxIcon.Question | 圆圈内的问号 |
| MessageBoxIcon.Stop | 红色背景圆圈内的白色 X |
| MessageBoxIcon.Warning | 黄色背景圆圈内的感叹号 |

## 状态控制循环

与哨兵控制循环类似，**状态控制循环**在达到某种状态时停止。状态控制循环不要求在处理完所有值后输入一个哑值（这通常是哨兵控制循环的要求），而是使用另一种特殊变量。这个特殊变量用于循环的条件表达式。对它进行求值，以确定其状态何时改变。

与状态控制循环一起使用的变量通常不同于用于存储正在处理的数据的变量。必须对它进行初始化，然后进行求值，以查看它何时改变状态。当它改变状态时，循环终止。在示例 6-9 中，使用了特殊的布尔变量 moreData。本示例使用了布尔数据类型；然而，这并不是该变量的要求。它可以是任何类型。

