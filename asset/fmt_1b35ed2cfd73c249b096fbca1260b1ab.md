
`switch` 语句使用了四个关键字：`switch`、`case`、`break` 和 `default`。
下面的讨论解释了这些关键字的作用。
`switch` 语句标识 `switch` 语句的开始。`switch` 后括号中的表达式会被求值，该表达式必须求出整数结果，否则会导致编译错误。

## 第 4 章 209

## switch 语句

在 `switch` 语句中，`case` 关键字标识与 `switch` 表达式的值进行比较的值。`case` 值按照列出的顺序进行比较，直到找到匹配项，然后从匹配项后的语句开始执行。如图 4.5 所示，`switch` 表达式的值决定了执行的实际开始点。

```
switch (expression) // 求表达式的值
{
    case value_1:
        .
        break;
    case value_2:
        .
        break;
    case value_3:
        .
        break;
    case value_n:
        .
        break;
    default:
        .
} // switch 语句结束
```

**图 4.5** 表达式决定了执行的入口点

`switch` 语句可以顺序包含任意数量的 `case` 标签。然而，如果表达式的值不匹配任何 `case` 值，除非遇到 `default` 情况，否则将没有语句被执行。`default` 关键字是可选的，其作用类似于 `if-else` 链中的最后一个分支。如果表达式的值不匹配任何 `case` 值，程序执行将从 `default` 关键字后的语句开始。

在 `switch` 语句找到入口点后，所有的后续 `case` 值评估都会被忽略。执行将继续到复合语句的结束，除非遇到 `break` 关键字，`break` 关键字标识一个 `case` 的结束并导致立即退出 `switch` 语句。正如 `case` 关键字标识复合语句中可能的入口点一样，`break` 关键字决定了终止点。

## 选择结构

如果省略了 `break` 语句，则匹配的 `case` 值之后的所有情况包括 `default` 情况都将被执行。
在编写 `switch` 语句时，你可以使用多个 `case` 值来引用相同的语句；`default` 关键字是可选的。例如，查看：

```
switch (number)
{
  case 1:
    cout << "Good Morning\n";
    break;
  case 2:
    cout << "Happy Day\n";
    break;
  case 3:
  case 4:
  case 5:
    cout << "Nice Evening\n";
}
```

当 `number` 的值为 1 时，执行 `Good Morning`。同样，当其值为 2 时，执行 `Happy Day`。最后，当其值为 3、4 或 5 时，执行 `Nice Evening`。如果 `number` 的值不匹配任何 `case` 且没有 `default` 分支，则没有语句被执行。

由于字符类型在表达式中总是转换为整数，因此 `switch` 语句也可以用于根据字符的值进行“切换”。例如，假设 `choice` 是一个字符变量，以下 `switch` 语句是有效的：

```
switch(choice)
{
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
        cout << "The character in choice is a vowel\n";
        break;
    default:
        cout << "The character in choice is not a vowel\n";
        break;
} // switch 语句结束
```

如果省略了 `break` 语句，则匹配的 `case` 值之后的所有情况包括 `default` 情况都将被执行。在编写 `switch` 语句时，你可以使用多个 `case` 值来引用相同的语句；`default` 关键字是可选的。例如，查看：

```
switch (number)
{
  case 1:
    cout << "Good Morning\n";
    break;
  case 2:
    cout << "Happy Day\n";
    break;
  case 3:
  case 4:
  case 5:
    cout << "Nice Evening\n";
}
```

当 `number` 的值为 1 时，执行 `Good Morning`。同样，当其值为 2 时，执行 `Happy Day`。最后，当其值为 3、4 或 5 时，执行 `Nice Evening`。如果 `number` 的值不匹配任何 `case` 且没有 `default` 分支，则没有语句被执行。

## 程序 4.7

```cpp
#include <iostream>
using namespace std;
int main() {
    int opselect;
    double fnum, snum;
    cout << "Please type in numbers: ";
    cin >> fnum >> snum;
    cout << "Enter a select: ";
    cout << "1 for addition";
    cout << "\n2 for multiplication";
    cout << "\n3 for division ";
    cin >> opselect;
    switch (opselect) {
        case 1:
            cout << "The sum of numbers is " << fnum + snum;
            break;
        case 2:
            cout << "The product of the numbers is " << fnum * snum;
            break;
        case 3:
            cout << "The first number divided by the second is " << fnum / snum;
            break;
    } // end of switch
    cout << endl;
    return 0;
}
```

## 4.4 练习

- 1. 使用 `switch` 语句重写以下 `if-else` 链：

```cpp
if (letterGrade == 'A')
    cout << "The numerical grade is between 90 and 100\n"
else if (letterGrade == 'B')
    cout << "The numerical grade is between 80 and 89.9\n"
else if (letterGrade == 'C')
    cout << "The numerical grade is between 70 and 79.9\n"
else if (letterGrade == 'D')
    cout << "How are you going to explain this?\n"
else
{
    cout << "Of course I had nothing to do with my grade.\n"
    cout << "It must have been the professor's fault.\n";
}
```

- 2. 使用 `switch` 语句重写以下 `if-else` 链：

```cpp
if (factor == 1)
    pressure = 25.0;
else if (factor == 2)
    pressure = 36.0;
else if (factor == 3)
    pressure = 45.0;
else if (factor == 4) || (factor == 5) || (factor == 6)
    pressure = 49.0;
```

# 第 4 章 213

3. 数据处理 批货物中的每个硬盘驱动器都刻有 1 到 4 的代码，用于指示制造商，如下：

| 代码 | 硬盘驱动器制造商 |
| :--- | :--- |
| 1 | 3M 公司 |
| 2 | Maxell 公司 |
| 3 | 索尼公司 (Sony) |
| 4 | Verbatim 公司 |

编写一个 C++ 程序，接受代码号作为输入，并根据输入的值显示正确的硬盘驱动器制造商。

- 4. 使用 `switch` 语句重写程序 4.5。
- 5. 调试 解释为什么程序 4.6 中的 `if-else` 链不能用 `switch` 语句替换。
- 6. 调试 使用字符变量作为选择代码重写程序 4.7。

## 4.5 案例研究：求解二次方程

C++ 语句的一个重要用途是通过通过检查明显的无效情况来验证数据。例如，日期 `53/06` 包含一个显然无效的日期。同样，程序中任何数字除以零如 `14/0` 是不应该被允许的。这两个例子说明了这种**防御性编程**技术的必要性，即程序在尝试处理输入数据之前，包含代码来检查输入数据是否不合理，这种技术被称为**输入验证**。

选择语句的第二个主要用途是根据数据确定计算的类型。本案例研究展示了这两种用途，并演示了一个确定二次方程根的 C++ 程序。二次方程的形式为 $ax^2 + bx + c = 0$，或者可以通过代数变形化为这种形式。在方程方程中，$x$ 是未知变量，$a, b$ 和 $c$ 是已知常数。虽然常量 $b$ 和 $c$ 可以是任意数字，但常量 $a$ 的值不能为 0。如果 $a$ 为 0，则方程将变为 $x$ 的一次方程。以下是二次方程的示例：

```
$5x^2 + 6x + 2 = 0$
$x^2 - 7x + 20 = 0$
$3x^2 - 16 = 0$
```

在第一个方程中，$a = 5, b = 6,$ 和 $c = 2$；在第二个方程中，$a = 1, b = -7,$ 和 $c = 20$；在第三个方程中，$a = 3, b = 0,$ 和 $c = 16$。

## 214 选择结构

二次方程的实根可以通过以下二次方程公式计算：

```
x = \frac{-b + \sqrt{b^2 - 4ac}}{2a}
和
x = \frac{-b - \sqrt{b^2 - 4ac}}{2a}
```

使用这些公式，你将按照软件开发流程编写一个 C++ 程序来求解二次方程的根。

### 步骤 1 分析问题

该问题要求接受三个输入——二次方程的系数 $a, b$ 和 $c$。输出是使用公式找到的方程根。

### 步骤 2 开发解决方案

解决方案的首次尝试是使用用户输入的 $a, b$ 和 $c$ 值来计算每个根的值，如下伪代码所示：

- **显示程序目的信息**
- **接受用户输入的 $a, b$ 和 $c$ 值**
- **计算两个根**
- **显示计算出的根的值**

然而，必须对此解决方案进行改进以考虑可能的输入条件。例如，如果用户对 $a$ 和 $b$ 都输入 0，则方程既不是二次方程也不是一次方程，无解被称为“退化情况”。另一种可能性是用户对 $a$ 输入 0，对 $b$ 输入非零值。在这种情况下，方程变为一次方程，只有一个解。如果 $b^2 - 4ac$ 称为**判别式**为负数，则无法对负数开平方根，方程没有实根被称为“虚根”。最后，当判别式为 0 时，两个根是相同的被称为“重复根”。

## 215 案例研究：求解二次方程

考虑到所有限制情况，以下伪代码显示了确定二次方程根的改进后的解决方案：

```
显示目的信息
接受用户输入的 a, b, 和 c 值
if a = 0 且 b = 0 则
    显示一条信息说明方程是退化的
else if a = 0 则
    显示一个等于 b 的单根
else
    计算判别式
    if (disc > 0) 则
        显示两个根
    else if (disc < 0) 则
        显示根是虚数
    else
endif
```

注意这里使用了嵌套的 `if-else` 语句。外部 `if-else` 语句验证输入的系数并确定是否为二次方程。内部 `if-else` 则确定...

### 步骤 4 测试并修正程序

测试值应包括产生实根的 $a, b$ 和 $c$ 值，以及产生一次方程 $a=0$ 的 $a$ 和 $b$ 值、退化方程 $a=0, b=0$ 以及判别式的情况。程序 4.8 的两次运行如下：

```
该程序计算方程为 ax + bx + c = 0 的二次方程的根
请输入 a, b, 和 c 的值: 1 2 -35
两个根为 5 和 -7
```

```
该程序计算方程为 ax + bx + c = 0 的二次方程的根
请输入 a, b, 和 c 的值: 0 0 16
方程是退化的且无解
```

## 步骤 3 代码

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    double a, b, c, disc, root1, root2;
    cout << "该程序计算方程为" << endl;
    cout << "ax + bx + c = 0 的二次方程的根" << endl;
    cout << "请输入 a, b, 和 c 的值: ";
    cin >> a >> b >> c;
    if (a == 0 && b == 0) {
        cout << "该方程是退化的且无解。" << endl;
    } else if (a == 0) {
        cout << "这是一个一次方程。单根为 " << -c / b << endl;
    } else {
        disc = pow(b, 2) - 4 * a * c;
        if (disc > 0) {
            root1 = (-b + sqrt(disc)) / (2 * a);
            root2 = (-b - sqrt(disc)) / (2 * a);
            cout << "两个根为 " << root1 << " 和 " << root2 << endl;
        } else if (disc < 0) {
            cout << "根是虚数。" << endl;
        } else {
            root1 = -b / (2 * a);
            cout << "重复根为 " << root1 << endl;
        }
    }
    return 0;
}
```

## 218 选择结构

e. 修改练习 2a 中编写的程序，使其不允许除以 0，并且当尝试进行此类除法时，会显示一条消息。

3. 数据处理 编写一个程序显示以下两个提示：

```
输入月份（使用 1 表示 1 月，以此类推）：
输入月份的日期：
```
