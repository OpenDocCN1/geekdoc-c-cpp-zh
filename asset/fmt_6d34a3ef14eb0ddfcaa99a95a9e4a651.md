
# 第 3 章 决策与循环

当然，`loop_statement` 可以是一个单独语句，也可以是大括号之间的语句块。执行 `for` 循环的事件序列如图 3-3 所示。

你输入的 3 个值的平均数是 20。

在声明并初始化你将使用的变量后，你启动了一个没有任何表达式的 `for` 循环，因此没有结束机制。紧随其后的代码块是即将执行的循环体。

该循环执行三个基本操作：

- 读取一个值。
- 将读取到的值加到 `sum` 中。
- 检查你是否想要继续。

块中的第一个操作是提示你输入，并将一个值读入变量 `value` 中。你输入的值会被加到 `sum` 中，数值计数 `i` 会递增。在 `sum` 中累加该值后，系统会询问你是否想输入另一个值，如果你已完成，则提示输入 'y' 或 'n'。你输入的字符存储在 `indicator` 中，用于语句中与 'n' 或 'N' 进行测试。如果这两者都不匹配，循环将继续；否则，执行 `break`。`break` 在循环中的作用与 `switch` 语句的作用相似。它通过将控制权转移到循环括号之后的语句来立即退出循环。

最后，你输出输入的数值个数及其平均值，平均值是通过将 `sum` 除以 `i` 计算得。当然，在计算之前，`i` 被转换为 `double` 类型，正如你记得第 2 章中关于类型转换的讨论一样。

## 使用 continue 语句

你编写 `continue` 语句非常简单：

```cpp
continue;
```

在循环中执行 `continue` 会立即开始下一次循环迭代，跳过循环体中剩余任何语句。你可以通过以下代码证明其有效：

```cpp
#include <iostream>

using std::cin;
using std::cout;
using std::endl;

int main()
{
    int value(0), product(1);

    for(int i = 1; i <= 10; i++)
    {
        cout << "Enter an integer: ";
        cin >> value;

        if(0 == value)          // 如果 value 为 0
            continue;            // 跳到下一次迭代

        product *= value;
        cout << "Product (ignoring zeros): " << product << endl;
    }
    return 0;              // 退出循环
}
```

此循环读取 10 个值，意在产生所输入的值。`if` 语句检查每个值，如果为真，则 `continue` 语句将跳到下一次迭代。这样做是为了防止在其中一个值为 0 时导致乘积变为 0。显然，如果在最后一次迭代中出现 0，还有其他方法实现相同的结果，但 `continue` 提供了一种非常实用的功能，特别是在复杂的循环中，你可能需要从循环中的多个点跳到当前迭代的末尾。

`break` 和 `continue` 语句对 `for` 循环逻辑的影响如图 3-4 所示。

![](img/80f387749861c6bfa7acfcf4c2583ff5_164_0.png)

图 3-4

显然，在实际情况下，你会结合条件测试逻辑使用 `break` 和 `continue` 语句来判断何时应该跳过循环，或者何时退出循环迭代。你也可以在其他类型的循环中使用这两个语句（我将在本章稍后部分讨论它们），它们的工作方式完全相同。

## 尝试尝试：在循环中使用其他类型

到目前为止，你只使用了整数来计数迭代。对于使用什么类型的变量进行计数，你并没有更多限制。看以下示例：

```cpp
// Ex3_11.cpp
// 显示字母的 ASCII 码
#include <iostream>
#include <iomanip>

using std::cout;
using std::endl;
using std::hex;
using std::dec;
using std::setw;

int main(){
    for(char capital = 'A', small = 'a'; capital <= 'Z'; capital++, small++)
    {
        cout << "\t" << capital; // 以字符输出 capital
        cout << hex << setw(10) << static_cast<int>(capital); // 以十六进制形式输出
        cout << dec << setw(10) << static_cast<int>(capital); // 以十进制形式输出
        cout << "\t" << small; // 以字符输出 small
        cout << hex << setw(10) << static_cast<int>(small); // 以十六进制形式输出
        cout << dec << setw(10) << static_cast<int>(small); // 以十进制形式输出
    }
    cout << endl;
    return 0;
}
```

### 工作原理

在这里，我们对程序中使用的新的操纵符名称使用了 `using` 声明，以影响输出的呈现方式。
此示例中的循环由变量 `char capital` 控制，你在初始化表达式中与变量 `small` 一起声明了它。你还在循环的第三个控制表达式中递增加了这两个变量，使得 `capital` 的值从 'A' 变为 'Z'，而 `small` 的值相应地从 'a' 变为 'z'。
循环包含一个跨越七行的输出语句。第一行是：

```cpp
cout << endl;
```

这会在屏幕上开启新行。

接下来的三行是：

```cpp
<< "\t" << capital // 以字符输出 capital
<< hex << setw(10) << static_cast<int>(capital) // 以十六进制形式输出
<< dec << setw(10) << static_cast<int>(capital) // 以十进制形式输出
```

在每次迭代重复该代码块后，`capital` 的值会被显示三次：作为字符、十六进制值和十进制值。

将 `hex` 操纵符插入 `cout` 流中会导致后续的整数值以十六进制形式显示，而不是默认的十进制表示；第二个输出（即 `dec` 操纵符）会让后续值以十进制显示。

```cpp
<< "The average of the " << i
<< " values you entered is " << sum/i << "."
<< endl;
return 0;
}
```

### 工作原理

对于相同的输入，该版本的程序产生的输出与之前相同。其中一条语句已更新，另一条添加了——它们在代码中被高亮显示。`for` 循环语句被 `while` 语句替换，`if` 循环中对指示符的测试被删除，因为该测试被 `while` 条件取代了。你将指示符初始化为 'y'，而不是之前出现的 'n'——否则 `while` 循环将终止。只要 `while` 中的条件返回 `true`，循环就会继续。

你可以使用 `true` 或 `false` 中的任何表达式作为 `while` 循环的条件。如果将循环条件扩展为允许输入 'y' 来继续循环，那么这个用例会更好。你可以如下所示修改 `while` 语句：

```cpp
while(('y' == indicator) || ('Y' == indicator))
```

你还可以通过始终为真的条件创建一个可能无限执行的 `while` 循环。这可以写成：

```cpp
while(true)
{
}
```

你也可以将循环控制表达式写为整数值 1，它会被转换为布尔值 `true`。自然，这里的要求与无限 `for` 循环相同：即你必须在循环块内部提供退出循环的方法。你将在第 4 章中看到使用 `while` 循环的其他方法。

## do-while 循环

`do-while` 循环与 `while` 循环相似，只要指定的循环条件保持为真，循环就会继续。主要的区别在于是在循环结束后检查条件——这与在开始检查条件的 `while` 和 `for` 循环形成对比。因此，`do-while` 语句至少会被执行一次。`do-while` 循环的一般形式为：

```cpp
do
{
  loop_statements;
}while(condition);
```

这种形式循环的逻辑如图 3-6 所示。

### 重复语句块 | 129

![](img/80f387749861c6bfa7acfcf4c2583ff5_170_0.png)

图 3-6

你可以用 `do-while` 循环替换程序最后一个版本中计算平均值的 `while` 循环：

```cpp
do
{
  cout << endl
  << "Enter a value: ";
  cin >> value; // 读取一个值
  ++i; // 计数加
  sum += value; // 将当前输入加到总和
  cout << "Do you want to enter another value (y or n)?";
  cin >> indicator; // 读取指示符
} while(('y' == indicator) || ('Y' == indicator));
```

这两个版本的循环之间有微小的区别，这个版本的正确运行不依赖于 `indicator` 中设置的初始值。只要你想至少输入一个值（这对于所讨论的计算是合理的），这个版本更优。

## 基于范围的 for 循环

我在这里介绍这种循环是为了让你所有可用的循环都出现在一起。基于范围的 `for` 循环允许你以非常简单的方式遍历集合中的每个项目。到目前你还没有遇到过任何可以应用此循环的集合，但你将在下一章遇到数组，可以在那里使用这种循环。届时我将详细讨论基于范围的 `for` 循环如何工作，你将在第 10 章学习其他可以使用基于范围的 `for` 循环遍历的集合。

www.it-ebooks.info

## 嵌套循环

你可以将一个循环嵌套另一个循环内部。这种通常用途将在第 4 章变得更加明显——它通常用于不同级别的重复操作。一个例子可能是计算班上每个学生的总分，然后对学校的每个班重复该过程。

## 尝试嵌套循环

你可以通过嵌套一个循环来看到另一个循环的效果。阶乘是从 1 到整数所有整数的乘积；例如，3 的阶乘是 1 乘以 2 乘以 3。以下程序计算整数的阶乘（直到输入足够）：

```cpp
// Ex3_13.cpp
// 使用嵌套循环计算阶乘
#include <iostream>

using std::cin;
using std::cout;
using std::endl;

int main() {
    char indicator('n');
    long value(0), factorial(0L);

    do {
        cout << endl << "Enter an integer: ";
        cin >> value;
        factorial = 1L;
        for(long i = 2L; i <= value; i++)
            factorial *= i;
        cout << "Factorial " << value << " is " << factorial << endl;
        cout << endl << "Do you want to enter another value (y or n)?";
        cin >> indicator;
    } while('y' == indicator || ('Y' == indicator));
    return 0;
}
```

如果你编译并执行这个示例，典型的输出是：

```
Enter an integer: 5
Factorial 5 is 120
Do you want to enter another value (y or n)? y
Enter an integer: 10
Factorial 10 is 3628800
Do you want to enter another value (y or n)? y
Enter an integer: 13
Factorial 13 is 6227020800
Do you want to enter another value (y or n)? y
Enter an integer: 22
Factorial 22 is 112400072777607800
Do you want to enter another value (y or n)? n
```

### 工作原理

阶乘增长得非常快。事实上，12 是此示例中能产生正确结果的最大输入值。13 的阶乘实际上是 6,227,020,800。如果你运行较大的输入，存储在变量中的数字将会丢失，你得到的 22 的阶乘可能是错误值。这种情况不会引起任何错误消息，前提是你确定处理的值在范围内。你还需要考虑错误输入的影响。这种错误很难发现。外部循环是 `do-while` 循环，它控制程序。只要你在提示处继续输入 y 或 n，程序就会继续。整数的阶乘是在内部循环中计算的。这是执行。

## 尝试另一个嵌套循环

嵌套循环有点混乱，让我们尝试另一个例子。这个程序生成一个大小为的乘法表：

```cpp
// Ex3_14.cpp
// 使用嵌套循环生成乘法表
#include <iostream>
#include <iomanip>

using std::cout;
using std::endl;
using std::setw;

int main() {
    const int size(12); // 表格大小
    int i(0);
    // ... 代码片段省略 ...
}
```

### 第 3 章 判定与循环

该示例的输出是：

| | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
| 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
| 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
| 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 |
| 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 |
| 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 |
| 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 |
| 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 |
| 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 |
| 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 |
| 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 |

```cpp
cout << endl;
cout << setw(3) << i << " *"; // 输出行标签
```

跳转到新行以开始新行，并以宽度为三的字段宽度输出由 `i` 的值给定的行标题，后面跟一个空格和一个垂直线。

一行值由内层循环生成：

```cpp
for(j = 1; j < size; j++)
    cout << setw(3) << i*j << " *"; // 行剩余部分的内层循环
// 内层循环结束
```
