
MessageBox.Show(s2);

}

```

# 7 使用 TryParse 方法防止数据转换异常

> 概念：尽可能防止异常。你可以使用 `TryParse` 方法防止由于用户输入无效数据而导致的异常。

当你使用 `Parse` 方法将非数字数据转换为数字类型时，会抛出异常。如果你使用其中一个 `Parse` 方法将 `TextBoxControl` 的属性转换为数字，始终存在抛出异常的可能性。毕竟，用户可以自由输入无效数据。

`TryParse` 方法允许你尝试将字符串转换为数字类型，如果转换失败时不抛出异常。相反，它们返回一个布尔值来表示转换是否成功，并通过 `out` 参数输出转换后的值。

`TryParse` 的通用格式为：

```cs
bool success = Type.TryParse(string, out Type result);
```

这里是一个示例：

```cs
string input = "123";

int number;

if (int.TryParse(input, out number))
{
    MessageBox.Show("The number is: " + number);
}
else
{
    MessageBox.Show("The input is not a valid number.");
}
```

通过使用 `TryParse`，你可以使代码更加健壮，并优雅地处理无效的用户输入。

```text
以下代码展示了使用 `decimal.TryParse` 方法的示例。在示例中，假设 `inputTextBox` 是一个 TextBox 控件的。
```
1 decimal number;
3 if (decimal.TryParse(inputTextBox.Text, out number))
4 {
5 Message.Show("Success!");
6 } else
8 {
9 Message.Show("Enter a valid decimal.");
10 }
```

## 在多个 TextBox 中验证数据

如果表单有多个 `TextBox`，用户就有多次机会输入有效数据。设计良好的程序应该逐个验证每个 `TextBox` 的内容。当发现无效数据时，程序应该显示错误消息，明确告诉用户是哪个 `TextBox` 包含了错误输入。

这种技术需要一组嵌套的 `if` 语句。例如，假设一个表单有两个 `TextBox`。以下伪代码显示了验证每个 `TextBox` 的逻辑。在伪代码中，使用虚线将每个 `If` 语句与其对应的 `Else` 及其结束标记连接起来。

```
如果第一个 TextBox 中的内容是正确的，那么
    如果第二个 TextBox 中的内容是正确的，那么
        处理两个 TextBox 中的数据
    否则
        显示关于第二个 TextBox 的错误消息
    结束 If
否则
    显示关于第一个 TextBox 的错误消息
结束 if
```

让我们看看逻辑在实际 C# 中是如何工作的。在随本书附的学生示例程序 `Chapter4` 文件夹中，你会找到一个名为 `Add Two Numbers` 的项目。应用程序的表单如图 21 所示。运行程序时，在每个 `TextBox` 控件中输入一个整数并点击 `Add` 按钮。将弹出一个消息框显示两个数字之和。如果你在 `TextBox` 中输入整数以外的任何内容，将出现一条错误消息，告知哪个 `TextBox` 包含了无效数据。

## 图 21 Add Two Numbers 表单

![](img/9467d25da5679b16515c9401daaae36c_243_0.png)

## 做出决策

以下是 `addButton_Click` 事件处理程序的代码：

```csharp
1 private void addButtonClick(object sender, EventArgs e)
2 {
3     // 局部变量
4     int first, second, sum;
5 
6     if (int.TryParse(firstTextBox.Text, out first))
7     {
8         if (int.TryParse(secondTextBox.Text, out second))
9         {
10             // 将两个数字相加并显示和。
11             sum = first + second;
12             MessageBox.Show(sum.ToString());
13         }
14         else
15         {
16             // 显示关于第二个 TextBox 的错误消息。
17             MessageBox.Show("The second TextBox contains invalid data.");
18         }
19     }
20     else
21     {
22         // 显示关于第一个 TextBox 的错误消息。
23             MessageBox.Show("The first TextBox contains invalid data.");
24     }
25 }
```

让我们来看：

- 第 4 行声明了三个 `int` 变量：`first`、`second` 和 `sum`。

- 第 6 行的语句尝试将 `firstTextBox.Text` 转换为 `int`。如果转换成功，结果将存储在变量 `first` 中，程序继续执行第 8 行。如果转换失败，程序跳转到第 20 行的 `else` 子句，第 23 行显示关于第一个控件的错误消息。

- 第 8 行的语句尝试将 `secondTextBox.Text` 转换为 `int`。如果转换成功，结果将存储在变量 `second` 中，程序继续执行第 10 行。如果转换失败，程序跳转到第 14 行的 `else` 子句，第 17 行显示关于第二个控件的错误消息。

- 第 11 行和第 12 行的语句在两个 `TextBox` 控件都包含有效整数值时执行。这些语句将两个变量相加并显示和。

如果你需要验证输入，将编写一组嵌套的 `if` 语句。以下是伪代码：

```
如果第一个 TextBox 中的数据是正确的，那么
    如果第二个 TextBox 中的数据是正确的，那么
        如果第三个 TextBox 中的数据是正确的，那么
            处理三个 TextBox 中的数据
        否则
            显示关于第三个 TextBox 的错误消息
    否则
        显示关于第二个 TextBox 的错误消息
否则
    显示关于第一个 TextBox 的错误消息
```

### 教程4：计算油耗

在教程 4 中，你将看到一个使用 `TryParse` 来验证输入到两个 `TextBox` 中的数据的。为了节省时间，表单已如图 22 所示。

- 第 1 步：打开学生示例程序的 `Chapter4` 文件夹。
- 第 2 步：打开名为 `Fuel Economy` 的应用程序。
- 第 3 步：在设计器中双击 `addButton` 控件。
- 第 4 步：切换到代码视图查看事件处理程序。
- 第 5 步：保存项目并运行应用程序。

![](img/9467d25da5679b16515c9401daaae36c_245_0.png)

# 决策

```csharp
{
    public Form1()
    {
        InitializeComponent();
    }

    private void validateCalculateButton_Click(object sender, EventArgs e)
    {
        double miles; // 用于存储里程数
        double gallons; // 用于存储加油量
        double mpg; // 用于存储 MPG

        // 验证 milesTextBox 控件。
        if (double.TryParse(milesTextBox.Text, out miles))
        {
            // 验证 gallonsTextBox 控件。
            if (double.TryParse(gallonsTextBox.Text, out gallons))
            {
                // 计算 MPG。
                mpg = miles / gallons;
            }
            // 在 mpgLabel 控件中显示 MPG。
            mpgLabel.Text = mpg.ToString("\nl");
        }
        else
        {
            // 为 gallonsTextBox 显示错误信息。
            MessageBox.Show("Invalid input for gallons.");
        }
    }
    else
    {
        // 为 milesTextBox 显示错误信息。
        MessageBox.Show("Invalid input for miles.");
    }
    }

    private void exitButton_Click(object sender, EventArgs e)
    {
        // 关闭表单。
        this.Close();
    }
}
```

### 单元测试

- 如果字符串参数成功转换，`TryParse` 方法返回什么值？如果字符串未转换，它又返回什么值？
- 如果 `TryParse` 方法成功转换了字符串参数，结果存储在何处？
- 如果 `TryParse` 方法无法转换字符串参数，第二个参数中存储了什么？
- 当 `out` 关键字写在方法调用的参数之前时，它表示什么意思？

# 决策

### 输入验证

**概念：** 输入验证是对输入到程序中的数据进行检查的过程，以确保这些数据在用于计算之前是合法的。

在上一节节中，你学习了如何使用 `TryParse` 方法来验证用户输入的数据类型。你还应该验证用户输入数据的准确性。程序员之间最著名的格言之一是“垃圾进，垃圾出”（garbage in, garbage out）。这个格言有时缩写为 GIGO，指的是计算机无法区分良好的输入和糟糕的输入。如果用户向程序提供了坏数据输入，程序将处理这些坏数据，并产生糟糕的输出。

例如，考虑一个工资程序，它接受员工在某周内工作的小时数。如果工资不小心输入了 400 小时而不是 40 小时，就会开出一张异常巨大的支票，因为一周中没有 400 小时。计算机并不知道这一事实，除非程序编写得能够捕捉此类错误，否则它将像处理好数据一样处理坏数据。

新闻中报道了一些关于计算机错误的故事，这些错误误导致人们在进行小额购买时被收了数千美元，或者收到了他们不享的大额退款。这些“计算机错误”很少是由计算机引起的；它们更多是由软件漏洞或作为程序输入读取到程序中的坏数据引起的。

程序输出的完整性完全取决于输入的完整性。出于这些原因，你应该以此方式编写程序，使其永远不会接受坏输入。当给程序提供输入时，应该在处理之前对其进行检查。如果输入无效，程序应该丢弃它并提示用户输入正确的数据。这一过程被称为**输入验证**。

例如，在工资程序中，我们可能像这样验证工作小时数：

```csharp
1 if (int.TryParse(workedTextBox.Text, out int hours))
2 {
3 if (hours > 0 && hours <= 168)
4 {
5     // 继续处理输入。
6 }
7 else
8 {
9 
10 MessageBox.Show("Invalid number of hours entered.");
11 }
12 else
13 {
14 
15 MessageBox.Show("Invalid number of hours entered.");
16 }
```

假设程序使用 `workedTextBox` 控件来验证工作小时数。如果 `TryParse` 方法成功转换了字符串参数，结果存储在 `hours` 变量中。如果 `TryParse` 方法无法转换字符串参数，第二个参数中存储了什么？当 `out` 关键字写在方法调用的参数之前时，它表示什么意思？

# 决策

> 提示：当你创建一组 RadioButton（单按钮）控件时，应始终在属性窗口将其中一个控件的 Checked 属性设置为 True。如果一组中所有 RadioButton 的 Checked 属性都设置为 False，那么当你运行应用程序时，Tab 值最低的 RadioButton 的 Checked 属性将自动设置为 True。

# 在代码中使用单按钮

在代码中，你可以通过测试 Checked 属性来确定 RadioButton 控件是否被选中。例如，假设表单有一个名为 `choice1RadioButton` 的 RadioButton 控件。以下语句判断它是否被选中：

```
if(choice1RadioButton.Checked)
{
    MessageBox.Show("You selected Choice 1");
}
```

注意，我们没有使用 == 运算符显式地将 Checked 属性与 true 值进行比较。这段代码等同于以下：

```
if(choice1RadioButton.Checked == true)
{
    MessageBox.Show("You selected Choice 1.");
}
```

让我们来看一个使用 RadioButton 控件的示例。打开随本书的学生示例程序第 4 章中的 RadioButton 项目。应用程序的表单如图 26 所示。当你运行应用程序时，选择一个单按钮并点击 OK 按钮。会出现一个消息框，显示你选择的运动。

图 26 RadioButton 示例表单

![](img/9467d25da5679b16515c9401daaae36c_251_0.png)

以下是 okButton_Click 事件处理程序的代码：

```csharp
private void okButton_Click(object sender, EventArgs e)
{
    if (footballRadioButton.Checked)
    {
        MessageBox.Show("You selected Football.");
    }
    else if (basketballRadioButton.Checked)
    {
        MessageBox.Show("You selected Basketball.");
    }
    else if (baseballRadioButton.Checked)
12 {
13 MessageBox.Show("You selected Baseball.");
14 }
15 }
```

当事件处理程序执行时，第 3 行的语句判断 `footballRadioButton` 的 Checked 属性是否为 true。如果是，在第 5 行显示消息“selected Football”。否则，第 7 行判断 `basketballButton` 的 Checked 属性是否为 true。如果是，在第 9 行显示消息“selected Basketball”。否则，第 11 行判断 `baseballRadioButton` 的 Checked 属性是否为 true。如果是，在第 13 行显示消息“selected Baseball”。

### 复选框（Check Boxes）

复选框是一个带有随附文本的小框。图 27 显示了一个示例。它们之所以被称为复选框，是因为点击一个空的复选框会在其中出现一个勾号。如果复选框中出现了勾号，点击它即可移除勾号。

![](img/9467d25da5679b16515c9401daaae36c_252_0.png)

复选框与单按钮类似，不同之处复选框不是互斥的。你可以在一组中拥有一个或多个复选框，并且可以随时选中其中的任何数量。当你需要在表单上创建复选框时，你可以使用 Checkbox 控件，它位于工具箱的 Common Controls 区域。

### CheckBox 控件的 Text 属性

CheckBox 有一个 Text 属性，该属性持有显示在复选框旁文本。例如，图 27 显示的 CheckBox 控件的 Text 属性为 Pepperoni。

### CheckBox 控件的 Checked 属性

像单按钮一样，控件也有一个 Checked 属性。当 CheckBox 被选中或勾选时，其 Checked 属性设置为 True。当 CheckBox 控件被取消选中或取消勾选时，其 Checked 属性设置为 False。

### 在代码中使用复选框

在代码中，你可以通过测试 Checked 属性来确定 CheckBox 控件是否被选中。例如，假设表单有一个名为 `option1Checkbox` 的复选框控件。以下语句判断它是否被选中：

```
if (option1Checkbox.checked)
{
    MessageBox.Show("You selected Option 1.");
}
```

让我们来看一个示例。打开随本书的学生程序第 4 文件夹中的 CheckBox 项目。应用程序的表单如图 28 所示。当你运行应用程序时，选择任何复选框然后点击 OK。会出现一个或多个消息框，显示你选择的内容。

图 28 CheckBox 示例表单
