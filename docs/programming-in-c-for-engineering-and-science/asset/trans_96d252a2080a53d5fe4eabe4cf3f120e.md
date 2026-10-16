

例如，下面是求两个值最大值的一种替代方法：

```
double maximum = value1;
if (value1 < value2)
    maximum = value2;
```

在某些问题中，if 语句中的一个或两个语句本身也可能是其他 if 语句。为了说明这一点，假设在第 5.1 节的问题中，有三种不同的污染条件——良好、一般、较差——由两个不同的截止值确定；例如，

```
const int CUTOFF1 = 40; // cutoff for good condition
        CUTOFF2 = 70; // cutoff for fair condition
```

我们可以使用以下“嵌套 if”语句来确定与污染水平相对应的条件：

```
if (index < CUTOFF1)
    cout << "Good condition\n";
else
    if (index < CUTOFF2)
        cout << "Fair condition\n";
    else
        cout << "Bad condition\n";
```

然而，更常见的是将其重新格式化如下，以更清晰地显示三种不同的替代方案：

```
if (index < CUTOFF1)
    cout << "Good condition\n";
else if (index < CUTOFF2)
    cout << "Fair condition\n";
else
    cout << "Bad condition\n";
```

一般来说，if 语句的形式可以总结如下：

## if 语句

if 形式（无 else）：

```
if (boolean_expression)
    statement
```

## if-else 形式：

```
if (boolean_expression)
    statement₁
else
    statement₂
```

## if-else if 形式：

```
if (boolean_expression₁)
    statement₁
else if (boolean_expression₂)
    statement₂
    .
    .
else if (boolean_expressionₙ)
    statementₙ
else
    statementₙ₊₁
```

其中
if 和 else 是关键字；
statement₁, statement₂, ... 都是 C++ 语句（并且可以是复合的，如下所述）。

## 目的：

在第一种形式中，如果 boolean_expression 为真，则 statement 将被执行；否则将被跳过。

在第二种形式中，如果 boolean_expression 为真，则 statement₁ 将被执行而 statement₂ 被跳过；否则，statement₁ 将被跳过而 statement₂ 被执行。

在最后一种形式中，如果 boolean_expressionᵢ 是第一个为真的布尔表达式，则 statementᵢ 将被执行而所有其他语句被跳过。如果所有 boolean_expressionᵢ 都不为真，则 statementₙ₊₁（如果存在）将被执行。

## 5.4.1 块

当一组语句必须被选中执行时，我们用大括号 { 和 } 将它们括起来形成单个语句。这称为块或复合语句：

## 块（复合语句）

## 形式：

```
{
    statement₁
```

```
statement₂
.
.
.
statementₙ
}
```

其中
每个 statementᵢ 都是 C++ 语句（并且本身也可能是复合的）。

## 目的：

语句序列被视为单个语句，其中 statement₁, statement₂, . . ., statementₙ 按顺序执行。

请注意，块不需要在最后一个右大括号后加分号；它本身就是一个完整的语句。

当 if 语句中的某个替代方案包含多于一个语句时，必须使用块。下面的示例中的二次方程求解器说明了这一点。

## 5.4.2 示例：二次方程求解器

二次方程具有形式 ax² + bx + c = 0，其中系数 a、b 和 c 是实数且 a ≠ 0，可以使用二次公式求解，该公式指出根由

−b ± √b² − 4ac
2a

给出，前提是判别式 b² − 4ac 为非负。示例 5.4 中的程序使用此方法求解二次方程。

## 示例 5.4 二次方程求解器

```
/* This program solves quadratic equations using the quadratic formula.

Input: the three coefficients of a quadratic equation
Output: the roots of the equation or a message that there are
        no real roots
------------------------------------------------------------*/
```

```
#include <iostream> // cout, cin, <<, >>
#include <cassert>  // assert()
#include <cmath>    // sqrt()
using namespace std;
```

```
int main()
{
    double a, b, c;
    cout << "Enter the coefficients of a quadratic equation: ";
    cin >> a >> b >> c;
    assert (a != 0);

    double discriminant = b*b - 4*a*c,
            root1, root2;

    if (discriminant >= 0)
    {
        root1 = (-b + sqrt(discriminant)) / (2*a);
        root2 = (-b - sqrt(discriminant)) / (2*a);
        cout << "Roots are " << root1 << " and " << root2 << endl;
    }
    else
        cout << "There are no real roots, only complex ones" << endl;
}
```

## 示例运行：

Enter the coefficients of a quadratic equation: 1 4 3
Roots are -1 and -3

Enter the coefficients of a quadratic equation: 2 -8 8
Roots are 2 and 2

Enter the coefficients of a quadratic equation: 1 2 3
There are no real roots, only complex ones

## 5.4.3 风格

程序员在编写 if 语句时没有一种通用的风格，但本教材中使用的是常见的一种，旨在促进可读性：

- 1. 对齐 if 和 else。
- 2. 使用空白和缩进来清晰地标识 if 语句中的替代方案。

当替代方案是单个语句时，我们通常将其缩进在 if 或 else 的下一行；例如，

```
if (index < CUTOFF)
    cout << "Safe condition\n";
else
    cout << "Hazardous condition\n";
```

对于由语句块组成的替代方案，大括号将放在单独的行上，与 if 和 else 对齐，并且它们所包含的语句将被缩进；例如，

```
if (discriminant >= 0)
{
    root1 = (-b + sqrt(discriminant)) / (2*a);
    root2 = (-b - sqrt(discriminant)) / (2*a);
    cout << "Roots are " << root1 << " and " << root2 << endl;
}
else
    cout << "There are no real roots, only complex ones" << endl;
```

在另一种常用的风格中，左大括号放在 if（或 else）关键字同一行上，右大括号与该关键字对齐而不是与左大括号对齐。

```
if (discriminant >= 0) {
    root1 = (-b + sqrt(discriminant)) / (2*a);
    root2 = (-b - sqrt(discriminant)) / (2*a);
    cout << "Roots are " << root1 << " and " << root2 << endl;
}
else
    cout << "There are no real roots, only complex ones" << endl;
```

对于 if-else-if 语句（第三种形式），每个 else 和其后的 if 将放在同一行，从而形成 else if，并且各部分中的语句缩进；例如，

```
if (index < CUTOFF1)
    cout << "Good condition\n";
else if (index < CUTOFF2)
    cout << "Fair condition\n";
else
    cout << "Bad condition\n";
```

## 5.5 重复：for 和 while 语句

在前几章和本章开头，我们的程序只需要按顺序处理指令，但在前一节中，我们看到了一些

8 这被称为 One True Brace（OTB）风格。其变体将关键字 else 放在关闭大括号的同一行上：

```
if (condition) {
    statements
} else {
    statements
}
```

问题的解决方案需要 *选择*。在本节中我们介绍第三种控制结构，*重复*。

## 5.5.1 示例：计算阶乘

非负整数 *n* 的 **阶乘**，记为 *n!*，定义为

*n!* = { 1 if *n* = 0
1 × 2 × ⋯ × *n* if *n* > 0 }

通过手工计算 *n!*，我们可能会从 1 开始，将其乘以 2，将该乘积乘以 3，依此类推，直到乘以 *n*。例如，要求 5!，我们可能会进行以下计算，其中我们保持一个运行乘积并从一步到下一步递增计数：

|  |  |
|---|---|
| 1 | ← 初始运行乘积 |
| × 2 | ← 初始计数 |
| 2 | ← 新运行乘积 |
| × 3 | ← 新计数 |
| 6 | ← 新运行乘积 |
| × 4 | ← 新计数 |
| 24 | ← 新运行乘积 |
| × 5 | ← 新计数 |
| 120 | ← 新运行乘积 |

如果我们分析这个 5! 的计算，我们会看到这种重复机制（也称为 **循环**）中有三个部分：

- 1. *初始化：* 为运行乘积和计数分配起始值。
- 2. *重复执行：* 反复将乘积乘以计数并递增计数。
- 3. *终止：* 当计数达到最终值 5 时停止。

我们可以将计算一般描述如下：

## 阶乘计算算法

- 1. 将 *product* 初始化为 1。
- 2. 对 *count* 在 2 到 *n* 范围内的每个值重复以下操作
- 将 *product* 乘以 *count.*

