
```csharp
namespace SquaredValues
{
    class SquaredValues
    {
        static void Main()
        {
            int counter = 0;
            string result = "\n\t\t\t\tSquared\n";
            while (counter < 10)
            {
                counter++;
                result += " \t"    // Notice the use of += to build
                    + counter       // the string for the MessageBox.
                    + " \t"
                    + Math.Pow(counter, 2)
                    + "\n";
            }
            MessageBox.Show(result, "1 - 10 and their "
                + "squares");
        }
    }
}
```

图6-3展示了该程序的输出。图中包含表示程序循环输出的文本和一个标题栏。两个按钮，即表示“关闭”的“X”按钮和“OK”按钮，是由预定义的 `MessageBox.Show()` 方法自动添加的。

![](img/e33ae760e23d89eac66541252ad65de8_339_0.png)

图6-3 MessageBox 对话框输出

要在控制台应用程序中使用 `MessageBox` 类，必须做两件事：

- 1. 在项目中添加对 `System.Windows.Forms.dll` 程序集的引用。这可以通过在 Visual Studio 中打开“解决方案资源管理器”选项卡，然后右键单击“引用”文件夹来完成，如图6-4所示。

> 本章稍后创建 Windows 应用程序项目时，会自动为你添加对 `System.Windows.Forms.dll` 的引用。这是通过选择 Windows 应用程序项目类型模板而不是控制台应用程序类型模板来实现的。现在需要添加引用，因为你正在将此添加到控制台应用程序中。

如果“解决方案资源管理器”未显示在屏幕上，可以从“视图”菜单中打开它。

![](img/e33ae760e23d89eac66541252ad65de8_340_0.png)

图6-4 向项目添加引用

如图6-5所示，如有必要，单击“.NET”选项卡；在“解决方案资源管理器”窗口中右键单击“引用”文件夹并选择“添加引用”后，会出现一个 .NET 程序集列表。向下滚动列表并选择 `System.Windows.Forms.dll`。`MessageBox` 类位于此程序集中。单击“确定”关闭“添加引用”对话框。

![](img/e33ae760e23d89eac66541252ad65de8_341_0.png)

### 图6-5 .NET 类库

选择 `System.Windows.Forms.dll` 组件后，就可以使用 `MessageBox` 类，但需要从 `System` 级开始指定该类所在命名空间的完全名称。如果不执行后面的第2步，任何对 `MessageBox` 的 `Show()` 方法的引用都需要使用完全限定名：`System.Windows.Forms.MessageBox.Show()`

- 2. 通过添加 using 指令，可以使用 `System.Windows.Forms` 命名空间中定义的类型，而无需限定名称。以下 using 指令被添加到示例6-5程序中：

```csharp
using System.Windows.Forms;
```

注意，仅包含 using 指令是不够的；还必须添加对程序集的引用。

`MessageBox` 类的 `Show()` 方法显示一个预定义的对话框，其中可以包含文本、标题栏的标题、特殊按钮和图标。消息框通常用于显示小消息，但也可以用于接受输入，即允许用户从按钮中做出选择。消息框被视为对话框，可以显示并接受对 Yes、No、Cancel、Abort 和 OK 按钮的简单单击。使用选择语句，可以编写表达式来确定单击了哪个按钮。在后面的章节中，你将学习为更大量的输入创建窗体。你的窗体将包含文本框、标签、列表框、组合框、菜单、单选按钮以及许多其他类型的控件。目前，`MessageBox` 将输入限制为对话框类型的控件。

`MessageBox` 类的 `Show()` 方法是重载的。在其最简单的形式中，对话框窗口中显示一个文本字符串。示例6-5中对 `MessageBox.Show()` 方法的调用包括如下两个参数：

```csharp
MessageBox.Show(result, "1 - 10 and their squares");
```

第一个参数 `result` 是显示在窗口中的字符串。变量 `result` 从循环体内部获得其值。每次通过循环体时，文本都会连接到 `result` 的末尾。为进行间距调整，添加了制表符和换行符（`'\t'` 和 `'\n'`）。每次通过循环时，制表符作为第一个字符连接。每次通过循环时，换行符（Enter 键）作为最后一个字符连接。所有值都放入 `result` 后，当调用 `Show()` 方法时，其内容会显示在窗口中。由于制表符和换行符，内容以表格形式显示。

第二个参数 `"1 - 10 and their squares"` 作为标题放在窗口的标题栏中，如图6-3所示。如前所述，`Show()` 是重载的；你可以将按钮作为第三个参数包含在内。表6-1列出了可作为 `Show()` 方法参数的按钮的有效选项。

### 表6-1 对话框按钮参数

| MessageBox 按钮 | 内容说明 |
|---|---|
| MessageBoxButtons.AbortRetryIgnore | Abort、Retry 和 Ignore 按钮 |
| MessageBoxButtons.OK | OK 按钮 [默认] |
| MessageBoxButtons.OKCancel | OK 和 Cancel 按钮 |
| MessageBoxButtons.RetryCancel | Retry 和 Cancel 按钮 |
| MessageBoxButtons.YesNo | Yes 和 No 按钮 |
| MessageBoxButtons.YesNoCancel | Yes、No 和 Cancel 按钮 |

![](img/e33ae760e23d89eac66541252ad65de8_342_0.png)

> 使用 Visual Studio 中的 IntelliSense，可以看到表6-1中所示的按钮属性值，以及可包含在 `MessageBox` 中的不同图标的选项。

可以如下将按钮添加为第三个参数：

```csharp
MessageBox.Show(result, "1 - 10 and their "
    + "squares",
    MessageBoxButtons.YesNoCancel);
```

MessageBox 对话框中包含 Yes、No 和 Cancel 按钮。

在查看图6-3时，注意最后一行输出是值10。然而，条件表达式表明只要计数器小于10，循环就会执行。当计数器变为10时，循环终止。那么，为什么打印了10及其平方？另外，请注意变量 `counter` 初始化为0，但图6-3中显示的第一行是值1。示例6-6中再次包含了该循环，以便你仔细检查它。

### 示例6-6

```csharp
while (counter < 10)
{
    counter++;
    result += "\t"
            + counter
            + "\t"
            + Math.Pow(counter, 2)
            + "\n";
}
```

注意计数器在哪里递增以及连接在哪里发生。由于计数器作为第一条语句递增为1，因此零从未被连接。条件表达式最后一次求值为 true 是在计数器等于9时，因为 (9 < 10) 为 true。由于计数器在循环内部、连接之前递增为10，因此值10被打印。你应该特别注意循环控制变量更新语句的位置，以及为允许正常终止而编写的条件表达式。

MessageBox 是一个对话框。如你所知，对话意味着两个或更多人之间的交谈，因此对话框是为用户干预而设计的。当执行包含 `MessageBox.Show()` 方法的代码行时，处理会停止，直到用户通过单击 MessageBox 上的 OK 按钮作出响应。此方法调用放在示例6-5中循环的外部。如果放在循环内部，则每次执行 `MessageBox.Show()` 调用时都需要用户单击。如果该方法调用包含在循环体内，用户将不得不单击 OK 10次。这就是为什么循环体内产生的值被连接到一个字符串变量的末尾。只包含一次对 `MessageBox.Show()` 方法的调用，而且是在循环体外部。

`MessageBox.Show()` 的重载方法可以接收表6-1中的一种按钮类型，以及第四个图标参数，如示例6-7所示。

### 示例6-7

```csharp
MessageBox.Show(result, "1 - 10 and their "
                    + "squares",
                    MessageBoxButtons.YesNoCancel,
                    MessageBoxIcon.Information);
```

