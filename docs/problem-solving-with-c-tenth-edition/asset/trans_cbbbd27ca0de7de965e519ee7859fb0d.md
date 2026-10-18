

# 自测练习

5. 当以下代码嵌入到完整的程序中时，会产生什么输出？

```
int x = 2;
cout << "Start\n";
if (x <= 3)
    if (x != 0)
        cout << "Hello from the second if.\n";
    else
        cout << "Hello from the else.\n";
cout << "End\n";

cout << "Start again\n";
if (x > 3)
    if (x != 0)
        cout << "Hello from the second if.\n";
    else
        cout << "Hello from the else.\n";
cout << "End again\n";
```

6. 当以下代码嵌入到完整的程序中时，会产生什么输出？

```
int extra = 2;
if (extra < 0)
    cout << "small";
else if (extra == 0)
    cout << "medium";
else
    cout << "large";
```

7. 如果自测练习 6 中的赋值改为如下，自测练习 6 的输出会是什么？

```
int extra = -37;
```

8. 如果自测练习 6 中的赋值改为如下，自测练习 6 的输出会是什么？

```
int extra = 0;
```

9. 当以下代码嵌入到完整的程序中时，会产生什么输出？

```
int x = 200;
cout << "Start\n";
if (x < 100)
    cout << "First Output.\n";
else if (x > 10)
    cout << "Second Output.\n";
else
    cout << "Third Output.\n";
cout << "End\n";
```

10. 如果自测练习 9 中的布尔表达式 (x > 10) 改为 (x > 100)，自测练习 9 的输出会是什么？

11. 当以下代码嵌入到完整的程序中时，会产生什么输出？

```
int x = SOME_CONSTANT;
cout << "Start\n";
if (x < 100)
    cout << "First Output.\n";
else if (x > 100)
    cout << "Second Output.\n";
else
    cout << x << endl;
cout << "End\n";
```

SOME_CONSTANT 是类型为 int 的常量。假设既没有输出 "First Output" 也没有输出 "Second Output"。因此，你知道 x 的值会被输出。

12. 编写一个多路 if-else 语句，将 int 变量 n 的值分类为以下类别之一并输出适当的提示信息：

n < 0 or 0 ≤ n ≤ 100 or n > 100

13. 给定以下声明和输出语句，假设它已嵌入到正确的程序中并运行。输出是什么？

```
enum Direction { N, S, E, W };
//...
cout << W << " " << E << " " << S << " " << N << endl;
```

14. 给定以下声明和输出语句，假设它已嵌入到正确的程序中并运行。输出是什么？

```
enum Direction { N = 5, S = 7, E = 1, W };
// ...
cout << W << " " << E << " " << S << " " << N << endl;
```

# switch 语句

你已经看到 if-else 语句用于构造多路分支。switch 语句是另一种 C++ 语句，也实现了

多路分支。Display 3.6 中显示了一个示例 switch 语句。这个特定的 switch 语句有四个常规分支和一个用于非法输入的第五个分支。变量 grade 决定执行哪个分支。每个成绩 'A'、'B' 和 'C' 各有一个分支。成绩 'D' 和 'F' 导致同一个分支被执行，而不是为 'D' 和 'F' 各自设置单独的动作。如果 grade 的值是除 'A'、'B'、'C'、'D' 或 'F' 之外的任何字符，则执行 default 标识符之后的 cout 语句。

# DISPLAY 3.6 switch 语句 (第 1 部分，共 2 部分)

```
//Program to illustrate the switch statement.
#include <iostream>
using namespace std;
int main()
{
    char grade;
    cout << "Enter your midterm grade and press Return: ";
    cin >> grade;
    switch (grade)
    {
        case 'A':
            cout << "Excellent. "
                << "You need not take the final.\n";
            break;
        case 'B':
            cout << "Very good. ";
            grade = 'A';
            cout << "Your midterm grade is now "
                << grade << endl;
            break;
        case 'C':
            cout << "Passing.\n";
            break;
        case 'D':
        case 'F':
            cout << "Not good. "
                << "Go study.\n";
            break;
        default:
            cout << "That is not a possible grade.\n";
    }
    cout << "End of program.\n";
    return 0;
}
```

# DISPLAY 3.6 switch 语句 (第 2 部分，共 2 部分)

# 示例对话 1

```
Enter your midterm grade and press Return: A
Excellent. You need not take the final.
End of program.
```

# 示例对话 2

```
Enter your midterm grade and press Return: B
Very good. Your midterm grade is now A.
End of program.
```

# 示例对话 3

```
Enter your midterm grade and press Return: D
Not good. Go study.
End of program.
```

# 示例对话 4

```
Enter your midterm grade and press Return: E
That is not a possible grade.
End of program.
```

![](img/88b1f375f11336dbd9dac8b1675d0698_164_0.png)

switch 语句的语法和首选缩进模式在 Display 3.6 中的示例 switch 语句以及标题为 "switch Statement" 的框中显示。

当执行 switch 语句时，会执行多个不同分支中的一个。执行哪个分支的选择由 switch 关键字后括号中的控制表达式决定。Display 3.6 中显示的示例 switch 语句中的控制表达式的类型为 char。switch 语句的控制表达式必须始终返回 bool 值、enum 常量、整数类型之一或字符。当执行 switch 语句时，会计算该控制表达式，计算机查看各个 case 标识符之后给出的常量值。如果它找到一个等于控制表达式值的常量，它就会执行该 case 的代码。例如，如果表达式求值为 'B'，那么它会查找以下内容并执行此行之后的语句：

```
case 'B':
```

请注意，常量后面跟着一个冒号。还要注意，你不能有两个 case 之后带有相同常量值的出现，因为那将是模棱两可的指令。

break 语句由关键字 break 后跟分号组成。当计算机执行 case 标签之后的语句时，它会一直继续直到遇到 break 语句。当计算机遇到 break 语句时，switch 语句结束。如果你省略 break 语句，那么在执行完一个 case 的代码后，计算机将继续执行下一个 case 的代码。

请注意，你可以为同一段代码使用两个 case 标签。在 Display 3.6 的 switch 语句中，对值 'D' 和 'F' 执行相同的操作。这种技术也可以用来允许大小写字母。例如，要允许 Display 3.6 程序中的小写 'a' 和大写 'A'，你可以将

```
case 'A':
    cout << "Excellent. "
        << "You need not take the final.\n";
    break;
```

替换为以下内容：

```
case 'A':
case 'a':
    cout << "Excellent. "
        << "You need not take the final.\n";
    break;
```

当然，对所有其他字母也可以这样做。

如果没有 case 标签的常量与控制表达式的值匹配，则执行 default 标签之后的语句。你不必有 default 部分。如果没有 default 部分并且找不到与控制表达式值匹配的情况，则执行 switch 语句时不会发生任何事情。然而，最安全的做法是始终拥有 default 部分。如果你认为你的 case 标签列出了所有可能的结果，那么你可以在 default 部分放置一条错误消息。这就是我们在 Display 3.6 中所做的。

# switch Statement

# SYNTAX

```
switch (Controlling_Expression)
{
    case Constant_1:
        Statement_Sequence_1
        break;
```

(continued)

# EXAMPLE

```
case Constant_2:
    Statement_Sequence_2
    break;
.
.
.
case Constant_n:
    Statement_Sequence_n
    break;
default:
    Default_Statement_Sequence }
int vehicleClass;
cout << "Enter vehicle class: ";
cin >> vehicleClass;

switch (vehicleClass)
{
    case 1:
        cout << "Passenger car.";
        toll = 0.50;
        break;
    case 2:
        cout << "Bus.";
        toll = 1.50;
        break;
    case 3:
        cout << "Truck.";
        toll = 2.00;
        break;
    default:
        cout << "Unknown vehicle class!";
}
```

# PITFALL Forgetting a break in a switch Statement

如果你在 switch 语句中忘记了 break，编译器不会发出错误消息。你编写了一个语法正确的 switch 语句，但它不会按你的预期工作。考虑标题为 "switch Statement" 的框中的 switch 语句。如果省略了 break 语句，如箭头所示，那么当变量 vehicleClass 的值为 1 时，标记为

```
case 1:
```
