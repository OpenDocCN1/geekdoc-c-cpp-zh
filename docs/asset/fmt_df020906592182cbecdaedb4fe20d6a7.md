
```csharp
if (grandMaster)
{
    powerLevel += 500;
}
```

这段代码执行以下操作：如果 `grandMaster` 为 `true`，则给 `powerLevel` 加 500。这里是另一个示例：

```csharp
if (!grandMaster)
{
    powerLevel = 100;
}
```

这段代码执行以下操作：如果 `grandMaster` 不为 `true`，则将 `powerLevel` 设置为 100。

## 检查点

- 4.18 你可以在 `bool` 变量中存储哪些特殊值？
- 4.19 什么是标志变量？

# 字符串比较

> **概念：** 你可以使用某些关系运算符和方法来比较字符串。

## 4.6 比较字符串

你可以使用 `==` 运算符来比较两个字符串。例如，请看下面的代码示例：

```csharp
string name1 = "Mary";
string name2 = "Mark";

if (name1 == name2)
{
    MessageBox.Show("名字是相同的。");
}
else
{
    MessageBox.Show("名字是不相同的。");
}
```

你可以将字符串变量与字符串字面量进行比较。假设 `month` 是字符串变量。下面的代码示例使用 `==` 运算符来判断 `month` 是否等于 `"October"`。

```csharp
if (month == "October")
{
    statement;
}
```

查看本书示例程序 `Chap04` 文件夹中的“Secret Word”应用程序。对于控件的名称，表单提示你向 `inputTextBox` 输入秘密单词。当你检查 `checkButton` 时，应用程序会将你输入的字符串与 `"Ariel"` 进行比较。

图 4-18 “Secret Word”应用程序的表单

![](img/8a88e1d8c69a687988c05f162ce32cac_245_0.png)

下面的代码示例显示了 `checkButton_Click` 事件处理器。第 5 行声明了一个字符串变量 `secretWord`，并用输入 `TextBox` 控件的值进行初始化。如果第 8 行的语句将 `secretWord` 与字符串字面量 `"Ariel"` 进行比较，如果两者相等，则执行第 10 行的语句。

```csharp
1 private void checkButton_Click(object sender, EventArgs e)
2 {
3 // 声明一个字符串变量并用
4 // 用户的输入初始化。
5 string secretWord = inputText.Text;
6 // 用户输入了正确的秘密吗？
7 if (secretWord == "Ariel") {
9
{
Message.Show("那是正确的秘密单词。");
}
else
{
Message.Show("抱歉，那不是秘密单词。");
}
```

# 其他字符串比较

除了判断字符串是否相等或不等，你还可以使用 `String.Compare` 方法来判断一个字符串是否大于或小于另一个字符串。当你有时需要对字符串进行某种排序时，这是一种非常有用的功能。在查看该方法如何工作之前，我们应该回顾字符在内存中是如何存储的。

回想第 1 章，计算机并没有在内存中实际存储如 A、B、C 等字符。相反，它们存储的是代表字符的数字代码。我们在第 1 章中提到过 C# 使用 Unicode 来表示字符。以下是关于 Unicode 系统的一些事实：

- 大写字母 A 到 Z 由数字 65 到 90 表示。
- 小写字母 a 到 z 由数字 97 到 122 表示。
- 当数字 0 到 9 作为字符存储在内存中时，它们由数字代码 48 到 57 表示。（例如，字符串 `"abc123"` 在内存中存储的代码为 97, 98, 99, 48, 50 和 51）。
- 空格由数字 32 表示。

除了建立一组用于表示内存中字符的数字代码外，Unicode 还为字符建立了顺序。字符 A 在于字符 B 之前，B 在于字符 C 之前，依此类推。

当程序比较字符时，它实际上是在比较字符的代码。字符 A 会小于字符 B，因为字符 A 的数字代码小于字符 B 的数字代码。

让我们来看看包含多个字符的字符串是如何被比较的。假设我们在内存中存储了字符串 `"Mary"` 和 `"Mark"`，如下：

```csharp
string name1 = "Mary";
string name2 = "Mark";
```

图 4-19 显示了字符串 `"Mary"` 和 `"Mark"` 的字符代码 ![](img/8a88e1d8c69a687988c05f162ce32cac_246_0.png)

当程序程序比较这些字符串时，它们是逐字符比较的，从第一个（或最左侧的）字符开始。这如图 4-20 所示。

图 20 比较字符串中的每个字符 ![](img/8a88e1d8c69a687988c05f162ce32cac_247_0.png)

以下是 `"Mary"` 和 `"Mark"` 的比较过程：

1. 将 `"Mary"` 中的 M 与 `"Mark"` 中的 M 进行比较。它们是相同的，所以比较下一个字符。
2. 将 `"Mary"` 中的 a 与 `"Mark"` 中的 a 进行比较。它们是相同的，所以比较下一个字符。
3. 将 `"Mary"` 中的 r 与 `"Mark"` 中的 r 进行比较。它们是相同的，所以比较下一个字符。
4. 将 `"Mary"` 中的 y 与 `"Mark"` 中的 k 进行比较。由于 y 的数字代码大于 k 的数字代码，因此 y 大于 k。

（注：此处原文逻辑在描述中略有错乱，已根据比较逻辑进行通顺翻译）

## 4.7 使用 TryParse 方法防止数据转换异常

在第 3 章中，你已经学习了当尝试尝试使用 `Parse` 方法将非数字数据转换为数值类型时，它们会抛出异常。如果你使用其中一个 `Parse` 方法将 `TextBox` 控件的 `Text` 属性转换为数字，始终存在抛出异常的可能性。毕竟，用户可以自由地在 `TextBox` 中输入任何内容。为了处理由 `Parse` 方法引起的异常，我们一直以来使用 `try-catch` 语句。

虽然许多异常的产生是有程序员无法预料的原因的（例如系统故障），但某些异常是可以预料的。例如，你使用 `Parse` 方法将非数字输入转换为数值数据类型将抛出异常。在那种可以预见的异常情况下，你应该编写代码来防止异常发生。与其允许异常发生并让 `try-catch` 语句对其做出反应，不如预防异常是更好的做法。你应该主要将 `try-catch` 语句用于那些你无法控制的异常。

> 注意：到为止，我们只是简单地允许异常发生并让 `try-catch` 语句对其进行响应。读完上一段话后，你可能会奇怪我们为什么要防止异常。原因是你需要知道如何编写 `if` 语句，以执行在本节中讨论的技术。现在你已经知道如何编写 `if` 语句，就可以使用 .NET Framework 中的一组方法了。通过 `TryParse` 方法，你可以在字符串转换为特定数据类型之前，确定字符串（例如控件的 `Text` 属性）是否包含可以转换为该类型的值。`TryParse` 方法不会抛出异常，因此你可以在不使用 `try-catch` 语句的情况下使用它们。

.NET Framework 中有几个 `TryParse` 方法，分别用于 `int` 和 `decimal` 数据类型，因此我们将讨论其中三个：

- 我们使用 `int.TryParse` 方法将字符串转换为 `int`。
- 我们使用 `double.TryParse` 方法将字符串转换为 `double`。
- 我们使用 `decimal.TryParse` 方法将字符串转换为 `decimal`。

当你调用 `TryParse` 方法时，你会传递两个参数：（你想要转换的字符串，以及你想要存储转换后的值的变量名）。首先，让我们来看 `int.TryParse` 方法。这里是调用 `int.TryParse` 方法的通用格式：

```
int.TryParse(string, out targetVariable)
```

在通用格式中，`string` 是你想要转换的字符串，`targetVariable` 是 `int` 变量名。该方法尝试将字符串转换为 `int`。如果转换成功，转换后的值将存储在 `targetVariable` 中，并且方法返回布尔值表示转换成功。如果转换失败，该方法不会抛出异常。相反，它会在 `targetVariable` 中存储 0 并返回 `false` 值，表示该字符串无法转换。

仔细观察通用格式，注意 `out` 出现在 `targetVariable` 之前。输出变量是一个作为参数传递给方法的变量，当方法完成后，一个值将存储在该变量中。

由于 `TryParse` 方法返回 `true` 或 `false`，它们通常作为 `if` 语句中的布尔表达式调用。下面的代码是一个使用 `int.TryParse` 方法的示例。在示例中，假设 `inputTextBox` 是 `TextBox` 控件的。

```
1 int number;
2
3 if (int.TryParse(inputTextBox.Text
```

此代码示例的目的是转换 `inputTextBox` 控件的 `Text` 属性的值并赋值给 `number` 变量。在第 3 行，`if` 语句调用 `int.TryParse` 方法，将 `inputTextBox.Text` 作为参数 1 和参数 2。以下是发生的情况：

- 如果 `inputTextBox.Text` 成功转换为 `int`，结果的值将被赋值给 `number` 变量，方法返回 `true`。这导致第 5 行的语句执行。
- 如果 `inputTextBox.Text` 无法转换为 `int`，则值 0 被赋值给 `number` 变量，方法返回 `false`。这导致第 9 行（`else` 子句）执行。

其他的 `TryParse` 方法以类似的方式。。是 `double.TryParse(string, out targetVariable)` 的通用格式：

在通用格式中，`string` 是你想要转换的字符串，`targetVariable` 是 `double` 变量名。如果字符串可以转换为 `double`，值将存储在 `targetVariable` 中，方法返回布尔值 `true` 表示转换成功。如果转换失败，该方法在 `targetVariable` 中存储 0 并返回布尔值 `false` 表示该字符串无法转换。

下面的代码是一个使用 `double.TryParse` 方法的示例。在示例中，假设 `inputTextBox` 是 `TextBox` 控件的。

```
1 double number;
2
3 if (double.TryParse(inputTextBox.Text, out number))
4 {
5     Message.Show("Success!");
6 }
7 else
8 {
9     Message.Show("Enter a valid double.");
10 }
```

这里是 `decimal.TryParse` 方法调用的通用格式：

```
decimal.TryParse(string, out targetVariable)
```

在通用格式中，`string` 是你想要转换的字符串，`targetVariable` 是 `decimal` 变量名。如果字符串可以转换为 `decimal`，值将存储在 `targetVariable` 中，方法返回布尔值 `true` 表示转换成功。如果转换失败，该方法在 `targetVariable` 中存储 0 并返回布尔值 `false` 表示该字符串无法转换。

## 4.7 使用 TryParse 方法防止数据转换异常

下面的代码显示了一个使用 `decimal.TryParse` 方法的示例。在示例中，假设 `inputTextBox` 是 `TextBox` 控件的。

```
decimal number;
if (decimal.TryParse(inputTextBox.Text, out number))
{
    Message.Show("Success!");
}
else
{
    Message.Show("Enter a valid double.");
}
```

### 多个 TextBox 中的数据验证

下面的代码显示了验证每个 `TextBox` 的逻辑。例如，假设表有两个 `TextBox`。这种技术需要一组嵌套的 `if` 语句。

> 如果第一个 `TextBox` 的数据良好，那么
>
>     如果第二个 `TextBox` 的数据良好，那么
>
>         处理数据
>
>     否则
>
>         显示关于第二个 `TextBox` 的错误消息
>
> 否则
>
>     显示关于第一个 `TextBox` 的错误消息

让我们看看逻辑在 C# 代码中是怎样的。这是图 4-21 加法表

![8a881d8c69a687988c05f162322cac251_0]

## 第 4 章

这里是 `addButton_Click` 事件处理程序的代码：

```csharp
private void addButton_Click(object sender, EventArgs e)
{
    // 局部变量
    int first, second, sum;
    if (int.TryParse(firstTextBox.Text, out first))
    {
        if (int.TryParse(secondTextBox.Text, out second))
        {
            // 将两个数字相加并显示和。
            sum = first + second;
            MessageBox.Show(sum.ToString());
        }
        else
        {
            // 显示关于第二个 TextBox 的错误消息。
            MessageBox.Show("The second TextBox contains invalid data.");
        }
    }
    else
    {
        // 显示关于第一个 TextBox 的错误消息。
        MessageBox.Show("The first TextBox contains invalid data.");
    }
}
```

让我们仔细观察：

- 第 4 行声明了三个变量：`first`、`second` 和 `sum`。
- 第 6 行的 `if` 语句尝试将 `firstTextBox.Text` 转换为 `int`。如果转换成功，结果存储在 `first` 中，程序继续执行第 8 行。如果转换失败，程序跳转到第 20 行的 `else` 子句，第 23 行显示关于第一个 `TextBox` 控件的错误。
- 第 8 行的 `if` 语句尝试将 `secondTextBox.Text` 转换为 `int`。如果转换成功，结果存储在 `second` 中，程序继续执行第 10 行。如果转换失败，程序跳转到第 14 行的 `else` 子句，第 17 行显示关于第二个 `TextBox` 控件的错误。

这里是伪代码：

![8a881d8c69a687988c05f162322cac252_0]

## 4.7 使用 TryParse 方法防止数据转换异常

在教程 4-4 中，你将完成一个应用程序，该程序使用 `TryParse` 方法来验证输入到两个 `TextBox` 控件的数据。

### 教程 4-4：计算燃油经济

![](img/8a88e1d8c69a687988c05f162ce32cac_253_0.png)

在教程 3-2 中，你创建了一个按每加仑英里（MPG）计算汽车燃油经济的应用程序。回一下，该程序允许用户输入行驶里程和消耗油量。程序计算并显示汽车的 MPG。在本教程中，你将创建一个应用程序的新版本，用于验证用户输入的数据。

为了节省时间，项目已经为你启动，应用程序的表单也已创建。要完成项目，请遵循本教程中的步骤：

- 步骤 1：启动 Visual Studio（或 Visual Studio Express）。在本书的第 4 章学生示例程序打开名为 `Fuel Economy with TryParse` 的项目。
- 步骤 2：在设计器中打开表单。图 4-22 显示了表单以及重要控件的名称。

#### 图 4-22 燃油经济

![](img/8a88e1d8c69a687988c05f162ce32cac_253_1.png)

- 步骤 3：现在你将为按钮创建 Click 事件处理程序。在本教程的示例中，Program 4-4 显示了表单完成代码。在编写事件处理程序时，将被指示注册 Program 4-4。

在设计器中，双击控件。这将打开代码编辑器，你有一个名为 `cancelButton_Click` 的空事件处理程序。通过输入 Program 4-4 中第 22–48 行的代码来完成 `cancelButton_Click` 事件处理程序。

让我们来看代码：

第 22-24 行：这些行声明了双精度点变量 `miles`、`gallons` 和 `mpg`。这些变量分别存储行驶的里程、消耗的油量和 MPG。

第 27 行：`if` 语句将 `milesText.Text` 转换为 `double`。如果转换成功，结果存储在 `miles` 变量中，程序继续执行第 29 行。如果转换失败，程序跳转到第 44 行的 `else` 子句，第 47 行显示错误消息“Invalid input for miles.”。

第 32-36 行：这些行仅在 `milesTextBox` 和 `gallonsTextBox` 都包含数据时执行。第 33 行计算 MPG并将结果赋值给 `mpg` 变量，第 36 行在 `mpgLabel` 控件中显示 `mpg` 变量的值。
