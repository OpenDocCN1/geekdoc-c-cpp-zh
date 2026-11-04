
## 19 重复执行程序步骤

计算机最大的优势之一，是能够一遍又一遍地执行完全相同的计算，而不会感到厌烦，也不会犯粗心错误。它可以计算十几名学生的平均测验成绩、打印一百份广告，或者为一百万客户计算月度账单，而不会遇到麻烦，也不会抱怨。

不过，你到目前为止读过的课程并没有告诉你如何做到这些。到目前为止，计算机执行的每一步都需要单独一行代码。要为一百万客户计算账单，你至少需要编写一百万行代码！

在本课中，你将学习如何让计算机多次执行相同的代码行。你将学习如何遍历数组和项集合，以便对它们执行操作或进行计算。

以下各节介绍 C# 提供的各种循环。最后一节介绍两个可用于改变循环工作方式的语句：break 和 continue。

### for 循环

for 循环使用一个变量来控制其执行一系列语句的次数。

for 循环的语法如下：

```
for (initialization; doneTest; next)
{
    statements...
}
```

其中：

- *初始化* 让循环准备好开始。通常，这部分声明并初始化循环变量。
- *结束测试* 是一个布尔表达式，用于确定循环何时停止。只要该表达式为 true，循环就会继续运行。
- *下一步* 为循环的下一次迭代做准备。通常，这会递增在 *初始化* 中声明的循环变量。
- *语句* 是你希望循环执行的语句。

请注意，*初始化*、*结束测试* 或 *下一步* 语句都不是必需的，尽管最简单的 *for* 循环都会用到它们。

例如，以下代码在“控制台”窗口中显示数字 0 到 9 及其平方：

```csharp
for (int i = 0; i < 10; i++)
{
    int iSquared = i * i;
    Console.WriteLine(string.Format("{0}: {1}", i, iSquared));
}
```

在这段代码中，*初始化* 语句声明变量 *i* 并将其设置为 0，*下一步* 语句将 *i* 加 1，而 *结束测试* 在 *i* < 10 时让循环继续运行。

下面是一个稍微复杂一点的示例，用于计算阶乘。程序将名为 *numberNumericUpDown* 的 NumericUpDown 控件中选定的值转换为长整数，并保存到变量 *n* 中。它将变量 *factorial* 初始化为 1，然后使用循环将 *factorial* 依次乘以 2 到 *n* 之间的每个数。结果是 1 * 2 * 3 * ... * *n*，也就是 *n*!：

```csharp
// Get the input value N.
long n = (long)numberNumericUpDown.Value;

// Calculate N!.
long factorial = 1;
for (int i = 2; i <= n; i++)
{
    checked
    {
        factorial *= i;
    }
}

// Display the result.
resultTextBox.Text = factorial.ToString();
```

你可能还记得，第 16 课使用代码计算斐波那契数，而在该课的练习 1 中，你计算了阶乘。那些程序使用 20 行代码来计算并存储 20 个值，然后程序将这些值用作一种查找表。

这里展示的阶乘代码使用的代码少得多。它不需要大型数组来保存值。它也不要求你预先知道可能需要计算多少个值（对于前面的程序是 20 个），尽管阶乘函数增长得如此之快，以至于该程序只能计算到 20!，再大的结果就无法放入 *long* 中。

> 注意 如果你确切知道需要循环执行多少次，*for* 循环通常是最佳选择。

### while 循环

while 循环在某个条件为 true 时执行。while 循环的语法如下：

```
while (condition)
{
    statements...
}
```

其中：

- *条件* 是一个布尔表达式。只要该表达式为 true，循环就会执行。
- *语句* 是你希望循环执行的语句。

例如，以下代码计算一个数的质因数：

```csharp
// Find the number's prime factors.
private void factorButton_Click(object sender, EventArgs e)
{
    // Get the input number.
    long number = long.Parse(numberTextBox.Text);

    // Find the factors.
    string result = "1";

    // Consider factors between 2 and the number.
    for (long factor = 2; factor <= number; factor++)
    {
        // Pull out as many copies of this factor as possible.
        while (number % factor == 0)
        {
            result += " x " + factor.ToString();
            number = number / factor;
        }
    }

    // Display the result.
    resultTextBox.Text = result;
}
```

代码首先获取用户输入的数字。它构建一个结果字符串，并将其初始化为“1”。接下来，代码使用 for 循环将 2 到用户输入数字之间的数作为可能的因数进行考察。

对于每个可能的因数，它使用 while 循环从该数中除去这个因数。只要该因数能整除剩余的数，程序就把该因数添加到结果中，并用该因数除用户输入的数。

代码最后显示其结果。

> **注意** *使用递增整数来决定何时停止的循环，通常用 for 循环编写比用 while 循环更容易。当停止条件出现的时间不太可预测时，while 循环特别有用，如因式分解示例所示。*

### do 循环

*do* 循环与 *while* 循环类似，只不过它在循环末尾而不是开头检查停止条件。*do* 循环的语法如下：

```
do
{
    statements...
} while (condition);
```

其中：

- *语句* 是你希望循环执行的语句。
- *条件* 是一个布尔表达式。只要该表达式为 true，循环就会继续执行。

以下代码使用 *do* 循环计算两个数的最大公约数（GCD），即能同时整除这两个数的最大数：

```csharp
// Calculate GCD(A, B).
private void calculateButton_Click(object sender, EventArgs e)
{
    // Get the input values.
    long a = long.Parse(aTextBox.Text);
    long b = long.Parse(bTextBox.Text);

    // Calculate the GCD.
    long remainder;
    do
    {
        remainder = a % b;
        if (remainder != 0)
        {
            a = b;
            b = remainder;
        }
    } while (remainder > 0);

    resultTextBox.Text = b.ToString();
}
```

> **注意** 请注意，用于结束循环的变量 remainder 声明在循环外部，尽管它在循环外部实际上并不起任何作用。通常，为了尽可能限制作用域，如果可以的话，你会希望把这个变量声明在循环内部。
>
> 但是，结束测试是在位于循环外部的作用域中执行的，因此循环内部声明的任何变量对它来说都是不可见的。

任何循环最终都必须结束，这一点很重要；而在这段代码中，循环为什么会结束并不是完全显而易见的。事实证明，每次循环（第一次可能例外）之后，a 和 b 都会变小。如果你用几个例子逐步推演，就能说服自己。

如果循环运行得足够久，b 最终会达到 1。此时，无论 a 是什么，b 都必定能整除 a，因此循环结束。如果 b 确实达到 1，那么 1 就是用户最初输入的两个数的最大公约数，而这两个数被称为 *互质*。

### 欧几里得算法

这个算法由希腊数学家欧几里得（约公元前 300 年）描述，因此被称为 *欧几里得算法* 或 *欧几里得算法*。我不想解释这个算法为什么有效，因为它很复杂，而且与这里关于循环的讨论无关（你可以在 primes.utm.edu/glossary/xpage/EuclideanAlgorithm.html 找到很好的讨论），但我确实想解释这段代码做了什么。

代码首先将用户输入的数字存储到变量 a 和 b 中。然后声明变量 remainder，并进入 do 循环。

在循环内部，程序计算 a 除以 b 的余数。如果该值不为 0（也就是说，b 不能整除 a），那么程序设置 a = b，b = remainder。

现在代码到达循环末尾。如果 remainder 为 0，while 语句会使循环结束。此时，b 保存的就是最大公约数。

你可能想在调试器中逐步执行这段代码，看看这些值如何变化。

> **注意** do 循环至少会执行一次其代码，因为它在最后才检查条件。通常，正是这一特性让你选择 do 循环而不是 while 循环。如果你可能不希望循环执行哪怕一次，就使用 while 循环。如果你需要先运行一次循环才能判断是否停止，就使用 do 循环。

