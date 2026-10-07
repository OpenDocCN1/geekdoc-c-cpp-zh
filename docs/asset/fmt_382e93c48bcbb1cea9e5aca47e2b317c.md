
`delegate void DisplayInt(int x);`

以下语句创建了一个名为 `Display` 的 `DisplayInt` 委托：

```csharp
DisplayInt Display = x => MessageBox.Show(x.ToString());
```

此 Lambda 表达式有一个参数 `x`。调用该表达式时，会在消息框中显示 `x` 的值

## 显式声明参数类型

不需要指定 Lambda 表达式参数的数据类型，因为编译器通常能够从委托声明中确定。但是，C# 允许你显式声明参数类型。例如，假设有如下委托声明：

```csharp
delegate IntOperation(int x);
```

以下语句声明了 `x` 参数的数据类型：

```csharp
IntOperation Square = (int x) => x * x;
```

注意，参数声明的声明必须放在括号内。这里有一个涉及两个参数的示例：

```csharp
delegate IntCalculator(int a, int b);

IntCalculator Sum = (int a, int b) => a + b;
```

## Lambda 表达式体中使用多个语句

你可以在 Lambda 表达式体中使用多个语句，但如果这样做，必须将语句放在大括号中，并且如果表达式有返回值则必须编写 `return` 语句。例如，考虑此委托声明：

```csharp
delegate int IntOperation(int x);
```

以下语句创建了一个名为 `TimesTwo` 的 `IntOperation` 类型委托：

```csharp
IntOperation TimesTwo = (x) => {
    int a = x * 2;
    return a;
};
```

## Lambda 表达式访问外部变量

Lambda 表达式可以访问包含该表达式方法的局部变量，只要这些变量在作用范围内并且已经赋值。以下代码演示了这一点。注意第 9 行的 Lambda 表达式访问了赋值为 `10` 的局部变量 `factor`：

```csharp
private void demoButton_Click(object sender, EventArgs e)
{
    int factor = 10;
    int result;
    // 创建一个将其参数乘以 factor 的委托。
    IntOperation Multiplier = x => x * factor;
    result = Multiplier(5);
    MessageBox.Show(result.ToString());
}
```

## 作为参数传递 Lambda 表达式

你可以在任何期望委托的地方使用 Lambda 表达式。例如，如果你调用一个期望传递委托的方法，你可以传递兼容的 Lambda 表达式。程序 13-6 显示了一个示例。

### 程序 13-6 LambdaPassingDemo 程序的 Form1 代码

```csharp
using System;
using System.Windows.Forms;

namespace LambdaDemo
{
delegate void IntRefOperation(ref int x);

public partial class Form1 : Form
    {
    public Form1()
    {
        InitializeComponent();
    }

    private void ArrayStepper(int[] array,
 IntRefOperation op)
    {
        for (int index = 0; index < array.Length; index++)
        {
            op(ref array[index]);
        }
    }
    private void demoButton_Click(object sender, EventArgs e)
    {
        // 创建包含 4 个元素的 int 数组；
        int[] numbers = { 10, 20, 30, 40 };

        // 显示数组的内容。
        ArrayStepper(numbers, (ref int x) => MessageBox.Show(x.ToString()));

        // 将数组每个元素设置为 0。
        x = 0;

        // 显示数组的内容。
        ArrayStepper(numbers, (ref int x) => MessageBox.Show(x.ToString()));
    }
}
}
```

- 第 15 行是名为 `ArrayStepper` 的方法头。该方法有两个参数：一个名为 `array` 的 int 数组和一个名为 `op` 的 `IntRefOperation` 委托。
- 第 26 行创建一个名为 `numbers` 的 int 数组，并初始化值为10, 20, 30, 40。
- 第 29 行调用 `ArrayStepper` 方法，将 `numbers` 数组和以下 lambda 表达式作为参数：

```csharp
(ref int x) => MessageBox.Show(x.ToString())
```

- 因为 `ArrayStepper` 方法期望第二个参数是 `IntRefOperation` 委托，所以该 lambda 表达式被转换为 `IntRefOperation` 委托。结果 `ArrayStepper` 方法会在消息框显示数组的每个元素。
- 第 32 行调用 `ArrayStepper` 方法，将 `numbers` 数组和以下 lambda 表达式作为参数：

```csharp
(ref int x) => x = 0
```

- 因为 `ArrayStepper` 方法期望第二个参数是 `IntRefOperation` 委托，所以该 lambda 表达式被转换为 `IntRefOperation` 委托。结果 `ArrayStepper` 方法调用将每个数组元素设置为 0。
- 第 35 行执行了与第 29 行相同的操作：它显示数组的每个元素。

## 使用 Lambda 表达式定义类方法

Lambda 表达式提供了一种在类声明内部定义简单方法的快速且简洁的方法。例如，查看下面的 `SimpleMath` 类：

```csharp
class SimpleMath
{
public int Add(int a, int b) => a + b;
public int Sub(int a, int b) => a - b;
public int Mult(int a, int b) => a * b;
public double Div(int a, int b) => (double) a /
b;
}
```

该类使用 lambda 表达式定义了四个名为 `Add`、`Mult` 和 `Div` 的方法。将此代码与下面这个使用普通方法定义的类声明进行比较：

```csharp
class SimpleMath
{
public int Add(int a, int b)
{
return a + b;
}

public int Sub(int a, int b)
{
return a - b;
}

public int Mult(int a, int b)
{
```

```
return a * b;
)
public double Div(int a, int b)
{
return (double) a / b;
}
}
```

如你所示，第一个版本的类仅占用七行代码，比占用二二行代码的第二个版本要简洁得多。

### 检查点

- **13.8** 什么是 lambda 表达式？
- **13.9** 查看以下表达式并回答后续问题：

```
x => x * 2
```

- **a.** lambda 运算符是什么？
**b.** lambda 表达式的参数是什么？
**c.** lambda 表达式返回什么？
- **13.10** 下面代码是正确的，还是包含一个错误？
如果包含错误，错误是什么？

```csharp
delegate int IntOperation(int a);
IntOperation Sum = (a, b) => a + b;
```

- 13.11 在 lambda 表达式外部声明的哪些变量可以被 lambda 表达式访问？

## 13.4 内置委托：Action、Func 和 Predicate

> 概念
> .NET Framework 提供了某些委托类型，简化了创建特定类型委托的过程。

到目前为止，你已经学习了实现委托是一个两步过程：首先声明一个委托类型，然后创建委托的实例。.NET Framework 提供了了一些内置委托类型，这些类型在许多情况下简化了创建委托的过程。我们将查看这些：

- `Action`—调用一个接受 0 到 16 个参数的 void 方法
- `Func`—调用一个接受 0 到 16 个参数并返回值的方法
- `Predicate`—调用一个接受一个参数并返回布尔值的方法

当你创建一个 `Action`、`Func` 或 `Predicate` 委托时，你不需要声明该委托类型，因为这些类型已经在 .NET Framework 中声明了。让我们仔细查看每种类型。

### Action 委托

你可以使用 `Action` 委托调用接受 0 到 16 个参数的 void 方法。要使用 `Action` 委托，你不需要声明委托类型，因为它是内置在 .NET Framework 中的。你只需要创建委托的实例。这里有一个使用 lambda 表达式创建一个不接受参数的 `Action` 委托的示例：

```csharp
ActionDisplayTest = () => MessageBox.Show("Testing, 1, 2, 3...");
```

我们可以使用匿名方法创建一个等等的 `Action` 委托，如下所示：

```csharp
ActionDisplayTest = delegate()
(
    MessageBox.Show("Testing, 1, 2, 3...");
);
```

在这两个示例中，委托的名称都是 `DisplayTest`。当调用此委托时，它会在消息框中显示字符串 "Testing, 1, 2, 3..."。无论我们使用的是 lambda 表达式还是匿名方法，该委托看起来如下：

```csharp
DisplayTest();
```

让我们来看一个演示此 `Action` 的完整应用程序。

```csharp
using System;
using System.Forms;
namespace ActionDemo
{
partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
    }

    Action ActionDisplayTest = () =>
        MessageBox.Show("Testing, 1, 2, 3...");
    }

    private void button1_Click(object sender, EventArgs e)
    {
        ActionDisplayTest();
    }
}
```

### 向 Action 传递参数

如果你想向 `Action` 传递参数，必须指定每个参数的数据类型。这是一个使用 lambda 表达式创建具有两个参数的 `Action` 委托的示例：

```csharp
Action<int, int> ShowSum = (a, b) => {
    int result = a + b;
    MessageBox.Show(result.ToString());
};
```

在该语句中，委托类型为 `Action<int, int>`。这指定我们正在创建一个具有两个 int 参数的 Action 。注意在 `=` 运算符右侧，lambda 表达式有两个名为 `a` 和 `b` 的参数。

这是另一个示例：

```csharp
Action<string, int> ShowMessage = (str, x) => (
    MessageBox.Show(str + x.ToString());
);
```

在该语句中，委托类型为 `Action<string, int>`。这指定我们正在创建一个具有两个参数的 Action ：第一个参数是 string，第二个参数是 int。

`Action` 委托最多可以有 16 个参数。你只需要在括号内列出每个参数的数据类型，按照参数声明的顺序。例如，以下代码创建了一个具有四个参数的 `Action` 委托：

```csharp
Action<int, double, string> ShowValues = (a, b, c) => (
    MessageBox.Show(a.ToString() + b.ToString() + c);
);
```

### Func 委托

你可以使用 `Func` 委托来调用接受 0 到 16 个参数并返回返回值的方法。以下是一个使用 Lambda 表达式创建一个不接受参数并返回字符串的 `Func` 委托的示例：

```csharp
Func<string> GetString = () => "This is a test.";
```

我们可以使用匿名方法来创建一个等效的 `Action` 委托，如下所示：

```csharp
Func<string> GetString = delegate()
{
    return "This is a test.";
};
```

在这两个示例中，委托的名称都是 `GetString`。当调用此委托时，它会返回字符串 "This is a test"。以下是我们如何调用该方法的示例：

```csharp
MessageBox.Show(GetString());
```

该语句将在消息框中显示字符串 "This is a test."。

#### 向 Func 委托传递参数

如果你想向 `Func` 委托传递参数，你必须指定委托每个参数的数据类型，以及委托返回的数值的数据类型。以下是一个创建一个返回 `double` 且有一个参数（类型为 `int`）的 `Func` 委托的示例：

```c
Func<int, double> Half = x => x * 0.5;
```

在括号内部，`int` 是参数 `x` 的数据类型，`double` 是委托的返回类型。这如图 13-6 所示。

> 图 13-6 带有一个参数的 Func 委托（Lambda 表达式版本）

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1759_0.png)

我们可以使用匿名方法来创建一个等效的 `Func<int, double>` 委托，如下所示：

```csharp
Func<int, double> Half = delegate(int x)
{
    return x * 0.5;
};
```

注意，在匿名方法中我们指定了两次参数数据类型，如[图 13-7](#)所示。

# **图 13-7** 带有一个参数的 Func 委托（匿名方法版本）

```csharp
Func<int, double> Half = delegate(int x)
{
    return x * 0.5;
};
```

在这两个示例中，委托的名称都是 `Half`。当调用此委托时，它接受一个 `int` 参数并返回参数值的一半，类型为 `double`。以下是我们如何调用该委托的示例（假设 `result` 是已经声明的 `double` 类型）：

```csharp
result = Half(5);
```

该语句将值 2.5 赋值给变量 `result`。让我们来看一个演示此 `Func` 委托的完整应用程序。

程序 13-8 显示了 `FuncDelegateDemo` 应用程序的 `Form1` 代码。当应用程序运行且用户点击 `demoButton` 控件时，第 18 行的语句将在消息框中显示 "Half of 25 is 12.5"。

# 程序 13-8 FuncDelegateDemo 的 Form1 代码

```csharp
using System;
using System.Windows.Forms;
namespace FuncDelegateDemo
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        private void demoButton_Click(object sender, EventArgs e)
        {
            Func<int, double> Half = x => x * 0.5;
            double result = Half(25);
            MessageBox.Show("Half of 25 is " + result.ToString());
