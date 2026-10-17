
```csharp
using System;
using System.Windows.Forms;

public class frmMain : Form
{
    const int MAXITERATIONS = 200000; // 限制循环次数

    private Button btnClose;
    private Label lblAnswer;
    private Label label;
    private TextBox txtMax;
    private Button btnStart;
    #region Windows code

    public frmMain()
    {
        //============ 程序初始化步骤 ========
        InitializeComponent();
    }

    public static void Main()
    {
        frmMain main = new frmMain();
        Application.Run(main);
    }

    private void btnStart_Click(object sender, EventArgs e)
    {
        bool flag;
        int counter; // 计数器
        int max; // 随机数的最大值
        int last;
        Random randomNumber = new Random();

        //============ 程序输入步骤 ========
        flag = int.TryParse(txtMax.Text, out max);
        if (flag == false)
        {
            MessageBox.Show("只能输入数字字符。", "输入错误",
                MessageBox.OK, MessageBoxIcon.Stop);
            txtMax.Focus();
            return;
        }
        //============ 程序处理步骤 ========
        counter = 0;
        last = (int) randomNumber.Next(max);
        do
{
            current = randomNumber.Next(max);
            if (last == current)
            {
              break;
            }
            last = current;
            counter++;
        } while (counter < MAXITERATIONS);

        //========= 程序输出步骤 ==========
        if (counter < MAXITERATIONS)
        {
          lblAnswer.Text = "花费了 " + counter.ToString() + 次 次匹配成功";
        } else {
          lblAnswer.Text = "没有连续匹配";
        }
    }

    //========= 程序终止步骤 ==========
    private void btnClose_Click(object sender, EventArgs e)
    {
      Close();
    }
}
```

### 工作原理

图 7-4 显示了程序的示例运行。

文本框中的值 1000 表示程序应该生成 0 到 1000 之间（不包含 1000）的随机数。（即 0 到 999 之间的随机值）。图 7-4 显示，在随机生成器连续产生相同值之前，循环执行了 5017 次。现在仔细查看代码。

该程序开始使用第 2 章讨论的 C# 模板。在列表 7-3 的此语句顶部附近：

```
const int MAXITERATIONS = 200000; // 循环次数限制
```

![图 7-4：相同的随机程序](https://example.com/image)

该语句用于限制 `do-while` 循环的最大迭代次数。这是因为仍然可能在循环中执行几十亿次而没有连续生成两个相同的值。使用符号常量 `MAXITERATIONS`，你可以轻松地更改循环的限制，而无需更改循环中的代码。确实，你可以硬编码数字，但使用符号常量 `MAXITERATIONS` 可以让你在更改循环限制时，无需修改循环中的代码。硬编码 200000 这种“魔术数字”无法解释 `MAXITERATIONS` 的作用。如果你更改 `MAXITERATIONS` 的其他值，329bd7a4f8df0746abc10b6d0939f220_png

188 | 第 7 章 使用循环进行重复

用于创建名为 `randomNumber` 的对象。程序然后使用 `TryParse()` 方法来构建随机数的范围。`Random` 类的 `Next()` 方法被调用以产生 0 到减 1 之间的值。以下代码片段执行了大部分工作：

```
counter = 0;
last = randomNumber.Next(max);
do {
    current = randomNumber.Next(max);
    if (last == current) {
        break;
    }
    last = current;
    counter++;
} while (counter < MAXITERATIONS);
```

变量 `counter` 在进入循环之前初始化为 0。此语句充当 `for` 循环表达式的作用。程序然后使用 `Random` 类的 `Next()` 方法生成一个随机数并赋值给变量 `last`。然而，由于程序的目标是比较两个值，在测试它们是否相同之前必须生成另一个随机值。这就是我们使用 `do-while` 循环的原因：你需要至少执行一次循环体来产生两个随机。第二个随机值赋值给变量 `current`。现在你有两个随机数需要比较。

## 循环中的 break 关键字

`if` 语句比较 `last` 和 `current` 的值以检查它们是否相同。如果是，则语句为真并执行 `break` 语句。在循环语句中任何地方执行 `break` 语句，`break` 都会将程序控制发送到循环语句大括号之后的第一个语句。在本程序中，控制被发送到列表 7-3 所示的

```
if (counter < MAXITERATIONS)
```

语句。如果 `current` 和 `last` 的值不相同，则不执行 `break` 语句，程序评估 `do-while` 块的 `expression2` 部分：

```
while (counter < MAXITERATIONS);
```

该语句的评估决定了是否应该再次通过循环。例如，符号常量 `MAXITERATIONS` 设置为 20000，但如果你需要可以更改该常量。（注意该常量如何在后续行中再次使用，以确定显示给用户的消息。）假设计数未超过 `MAXITERATIONS`，`while` 测试会导致循环语句块的另一次通过。

循环执行的次数通过对 `MAXITERATIONS` 的测试进行限制，原因有两个。首先，整数变量可以持有超过 20 亿的值，用户可能不想等待循环处理 20 亿次通过。其次，更重要的是，可能

循环执行了超过 20 亿次，以为 `last` 和 `current` 产生匹配的值。这意味着程序可能会为 `counter` 生成一个大到整数变量无法存储的数值。这可能会导致所谓的“数值溢出异常”，而你的程序将以一种不优雅的方式崩溃！（你将在第 11 章中学习如何防止这种丑陋的情况）。

最终，要么两者匹配成功，要么 `counter` 等于 `MAXITERATIONS` 然后 `while` 循环终止。此时，将评估最后的 `if` 语句，适当的消息将显示在 `lblanswer` 标签对象中。

正如你预期的那样，随着用户增加 `max` 的值，产生匹配值所需的循环次数随之增加。事实上，如果用户输入一个很大的值（例如 200000），程序经常会产生不匹配的情况。

## CONTINUE 语句

有时会出现这样的情况：你需要在循环继续之前在内部执行某些特殊操作。例如，你可能有一个循环正在轮询本章开头提到的火灾喷淋传感器。然而，你并不是在传感器被触发时跳出循环，而是想继续读取其余传感器的状态以查看火蔓延的速度有多快。代码可能如下：

```
while (true)
{
    id++;
    state = readSensor(id);
    if (state == true)
    {
        soundAlarm();
        callFireDepartment();
        continue;
    }
    if (id == MAXSENSORS)
    {
        id = 0; // 所以递增运算符将其设置为 1
    }
}
```

在段代码片段中，你通过声明测试表达式（`expression2`）始终为 `True` 在设计上建立了一个无限 `while` 循环，如第一个程序语句所示。代码递增传感器标识符（`id`）并返回相应的传感器。如果传感器没有返回 `true`，程序将再次通过循环。如果发生火灾且传感器返回 `true`，则会响起警报、报警消防部门，然后由于 `continue` 语句，代码将在 `while` 循环的 `expression2` 处继续执行`expression2` 始终为 `True`，循环继续执行代码。

当使用 `while` 或 `do-while` 循环时，`continue` 语句会将控制传递给决定是否需要再次通过循环的表达式（即 `expression2`）。

使用 `for` 循环的相同类型代码如下：

```
for (id = 0; true; id++)
{
    state = readSensor(id);
    if (state == true) {
        soundAlarm();
        callFireDepartment();
        continue;
    }
    if (id == MAXSENSORS) {
        id = 0; // 递增运算符设置为 1
    }
}
```

在这种情况下，如果发生火灾，变量 `state` 为 `true`，则会执行警报和报警方法（查看 `for` 循环的 `expression2`）。`continue` 语句将程序控制权发送到 `expression3(id++)`，该表达式会递增传感器 `id`。随后程序控制权被发送到 `expression2` 以确定是否需要再次通过循环。因为 `expression2` 始终为逻辑上的 `True`，代码会再次通过循环。你应该让自己相信这是一个无限循环。

与将程序控制权移出循环的 `break` 语句不同，`continue` 语句将程序控制权保留在循环内，以判断是否有必要再次循环。作为一项实验，你可以为 `soundAlarm()` 和 `callFireDepartment()` 方法编写空哑方法，然后使用调试器单步执行代码。再次，使用调试器是更完整地理解代码在做什么的极佳方法。

为了完整起见，你应该知道 C# 支持 `goto` 关键字，它可以配合标签（label）来创建循环结构。然而，由于 `goto` 是一种非常糟糕的编码结构（即一种编码“黑科技”），我们没有向你展示如何编写这样的循环。如果你真的想知道，可能可以在网上找到示例。（警告：goto）

### 总结

循环结构是执行多次某些代码块的方式。你可以在本章中学习到 `for`、`while` 和 `do-while` 循环，以及 `break` 和 `continue` 语句。

- 1. 循环执行了超过 20 亿次，以为 `last` 和 `current` 产生匹配的值。这意味着程序可能会为 `counter` 生成一个大到整数变量无法存储的数值。这可能会导致所谓的“数值溢出异常”，而你的程序将以一种不优雅的方式崩溃！（你将在第 11 章中学习如何防止这种丑陋的情况）。

- 最终，要么两者匹配成功，要么 `counter` 等于 `MAXITERATIONS` 然后 `while` 循环终止。此时，将评估最后的 `if` 语句，适当的消息将显示在 `lblanswer` 标签对象中。

- 正如你预期的那样，随着用户增加 `max` 的值，产生匹配值所需的循环次数随之增加。事实上，如果用户输入一个很大的值（例如 200000），程序经常会产生不匹配的情况。

## 8 理解数组与集合

在本章中学习到：

字体 数组

- 数组索引

- 如何设置数组的大小

- 一些数组方法

- 多维数组

- 数组列表

- 锯齿数组

## 什么是数组？

数组是相同名称的相同类型。定义数组的语法如下：

```
typeSpecifier[] arrayName = new typeSpecifier[numberOfElements];
```

其中：

* `typeSpecifier` 是你想使用的数据类型。

* `arrayName` 是你想使用的名称。

* `numberOfElements` 是你需要的元素数量。

每个部分将在示例中进行解释：

假设你有一个包含100个名字的地址簿。由于你想在程序中操作这些，每个唯一的名称必须存储在唯一的变量中。由于名称是文本数据，你可以使用如下：
