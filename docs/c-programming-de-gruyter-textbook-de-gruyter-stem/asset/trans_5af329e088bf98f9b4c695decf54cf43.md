

## 52 2 基础 C++ 编程

注意：语句 1, 2, 3 和 4 可以是复合语句；每个层级的 if 必须与一个 else 匹配。如果你想省略一个 else，必须使用 {} 来包裹该层级的语句，以确保其正确的层级关系。

**示例 2.3：** 比较两个数字。

分析：比较两个数字 x 和 y；有三种可能：x=y, x>y 和 x<y。因此，我们需要多分支结构。我们在这里选择嵌套的 else 语句。

源代码：

```cpp
//2_3.cpp
#include<iostream>
using namespace std;
int main()
{
    int x,y;
    cout<<"Enter x and y:";
    cin>>x>>y;
    if (x!=y)
        cout<<"x>y"<<endl;
    else
        cout<<"x<y"<<endl;
}
```

结果 1:

| 输入 x 和 y: 5 8 |
| x<y |

结果 2:

| 输入 x 和 y: 8 8 |
| x=y |

结果 3:

| 输入 x 和 y: 12 8 |
| x>y |

## if...else 语句

如果所有嵌套的 if 语句都在 else 分支中，可以使用 if...else。语法形式如下：

```
if (expression) statement 1
else if (expression 2) statement 2
else if (expression 3) statement 3
...
else statement n
```

**语句 1, 2, 3,...n** 可以是复合语句。if...else 的执行顺序如图 2.6 所示。

## 2.4 算法的基本结构 — 53

![](img/561830d085ac2bf2a_70.png) 图 2.6：if...else 语句流程图。

## 3. switch 语句

在某些问题中，虽然需要多个选择，但每个判断评估同一个表达式，因此不需要嵌套的 if 语句。switch 语句设计用于解决 C++ 中的这类问题。语法如下：

```cpp
switch (expression)
  case constant expression 1: statement 1
  case constant expression 2: statement 2
  ...
  case constant expression n: statement n
  default : statement+1
```

## 54 2 基础 C++ 编程

switch 语句的执行顺序是：首先计算表达式的值，找到匹配该值的第一个 case 作为入口标签并执行。如果没有 case 匹配表达式的值，则执行 "default"：使用 switch 语句应注意以下问题：

- switch 语句中的表达式可以是 int 类型、字符类型或枚举类型。
- 每个常量表达式的值必须不同，尽管它们的顺序不影响执行结果。
- 每个 case 可以包含多个语句，不需要使用 {}。
- 每个 case 只是入口标签，不能决定执行的终点。因此需要在 case 分支末尾添加 break 语句以退出整个 switch 结构；否则，该 case 分支的代码执行完成后会执行到下一个语句。
- 当多个分支需要执行相同的操作时，可以使用相同的语句。

**示例 2.4：** 输入 0–6 之间的整数，转换为对应的星期。分析：在这个示例中，输入的数字决定输出信息，因为 0–6 代表七个条件：“Sunday”、“Monday”……因此我们需要使用多分支结构。由于是判断星期，switch 语句是最合适的。

源代码：

```cpp
//2_4.cpp
#include <iostream>
using namespace std;
int main()
{
    int day;

    cin >> day;
    switch (day)
    {
        case 0: cout << "Sunday" << endl;
            break;
        case 1: cout << "Monday" << endl;
            break;
        case 2: cout << "Tuesday" << endl;
            break;
        case 3: cout << "Wednesday" << endl;
            break;
        case 4: cout << "Thursday" << endl;
            break;
        case 5: cout << "Friday" << endl;
            break;
        case 6: cout << "Saturday" << endl;
            break;
        default: cout << "Day of range Sunday .. Saturday" << endl;
        break;
    }
}
```

运行示例：

```
2
Tuesday
```

## 2.4.3 循环结构

C++ 中有循环控制结构：

## 1. while 语句

语法形式：

```
while (expression) statement
```

执行顺序：首先评估表达式（循环条件）；如果为真，则执行循环体（语句）并重新评估表达式；持续循环直到表达式为假。使用语句时，通常循环体内应该有可以改变表达式值（即循环条件）的语句，否则将导致死循环。图 2.7：while 语句流程图。

**示例 2.5：** 计算数字 1–10 的和。

分析：在示例示例中，输入的数字决定输出信息，因为 1–10 代表条件。因此我们需要使用循环结构。

源代码：

```cpp
//2_5.cpp
#include <iostream>
using namespace std;
int main()
{
    int i(1), sum(0);
    while (i<=10)
    {
        sum+=i;
        i++;
    }
    cout<<sum<<endl;
}
```

## 2. do...while 语句

语法形式：

```cpp
do {
    statement
} while (expression);
```

执行顺序：首先执行循环体，然后评估表达式；如果为真，则继续循环。因此，循环体至少执行一次。图 2.8：do...while 语句流程图。

**示例 2.6：** 反转整数的数字。

分析：在示例中，输入的数字决定输出信息，因为我们需要提取每个数字。因此我们需要使用循环结构。

源代码：

```cpp
//2_6.cpp
#include <iostream>
using namespace std;
int main()
{
    int n, right_digit;
    cout << "Enter the number: ";
    cin >> n;
    cout << "The number is ";
    do {
        right_digit = n % 10;
        cout << right_digit;
        n /= 10;
    } while (n != 0);
    cout << endl;
}
```

结果：

| 输入数字: 365 |
| 该数字是 563 |

