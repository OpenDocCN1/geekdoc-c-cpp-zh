
`cin.get` 成为一个新的标识符。如果在程序中使用 `cin.get(ch);`，编译器会尝试解析一个未声明的标识符，从而产生错误。同样，缺少圆括号，如 `cin.getch;`，会导致语法错误。还要记住，输入函数必须与输入流变量一起使用。如果你试图单独使用任何输入函数——也就是说，不使用输入流变量——编译器可能会生成诸如“未声明的标识符”之类的错误消息。例如，语句 `get(ch);` 可能导致语法错误。

如你所见，多个函数与 `istream` 变量相关联，每个函数执行特定任务。回想一下，函数 `get`、`ignore` 等是数据类型 `istream` 的成员。点号将输入流变量名与成员（或函数）名分隔开，这称为**点表示法**。事实上，在 C++ 中，点号是一个运算符，称为**成员访问运算符**。

> **注意** C++ 对数据类型 `istream` 和 `ostream` 有一个特殊名称。数据类型 `istream` 和 `ostream` 称为类。变量 `cin` 和 `cout` 也有特殊名称，称为对象。因此，`cin` 称为 `istream` 对象，`cout` 称为 `ostream` 对象。事实上，流变量称为流对象。你将在本书后面题为*继承与组合*的章节中学习这些概念。

## 输入失败

程序执行期间可能出很多问题。语法正确的程序也可能产生错误结果。例如，假设兼职工资按以下公式计算：

```cpp
wages = payRate * hoursWorked;
```

如果你不小心把 `*` 打成了 `+`，计算出的工资就会不正确，即使包含 `+` 的语句在语法上是正确的。

如果尝试读取无效数据会怎样？例如，如果你试图将字母输入到 `int` 变量中会发生什么？如果输入数据与相应变量不匹配，程序就会遇到问题。例如，试图将字母读入 `int` 或 `double` 变量会导致**输入失败**。考虑以下语句：

```cpp
int a, b, c;
double x;
```

如果输入是：

```text
W 54
```

那么语句：

```cpp
cin >> a >> b;
```

会导致输入失败，因为你试图将字符 `W` 输入到 `int` 变量 `a` 中。如果输入是：

```text
35 67.93 48
```

那么输入语句：

```cpp
cin >> a >> x >> b;
```

会将 35 存储到 `a`，67.93 存储到 `x`，48 存储到 `b`。

现在考虑以下读取语句，使用前面的输入（含三个值的输入）：

```cpp
cin >> a >> b >> c;
```

该语句将 35 存储到 `a`，将 67 存储到 `b`。读取在 `.`（小数点）处停止。因为下一个变量 `c` 是 `int` 数据类型，计算机试图将 `.` 读入 `c`，这是一个错误。输入流随后进入一种称为失败状态的状态。

输入流进入失败状态时实际会发生什么？一旦输入流进入失败状态，使用该流的所有后续 I/O 语句都会被忽略。不幸的是，程序会静默地继续使用变量中存储的值执行，并产生错误结果。示例 3-8 中的程序演示了输入失败。该程序在你的系统上可能会产生不同结果。

### 示例 3-8

```cpp
//Input Failure program

#include <iostream>

using namespace std;

int main()
{
    int a = 10;                         //Line 1
    int b = 20;                         //Line 2
    int c = 30;                         //Line 3
    int d = 40;                         //Line 4

    cout << "Line 5: Enter four integers: ";       //Line 5
    cin >> a >> b >> c >> d;                      //Line 6
    cout << endl;                                  //Line 7
    cout << "Line 8: The numbers you entered are:"; //Line 8
    cout << endl;
    cout << "Line 9: a = " << a << ", b = " << b
         << ", c = " << c << ", d = " << d << endl; //Line 9

    return 0;
}
```

**示例运行：** 在这些示例运行中，用户输入以阴影显示。

**示例运行 1**

```text
Line 5: Enter four integers: 34 K 67 28

Line 8: The numbers you entered are:
Line 9: a = 34, b = 20, c = 30, d = 40
```

第 1、2、3、4 行的语句分别声明变量 `a`、`b`、`c`、`d` 并将其初始化为 10、20、30、40。第 5 行的语句提示用户输入四个整数；第 6 行的语句将这四个整数输入到变量 `a`、`b`、`c`、`d` 中。

在此示例运行中，第二个输入值是字符 'K'。`cin` 语句试图将该字符输入到变量 `b`。然而，因为 `b` 是 `int` 变量，输入流进入失败状态。注意，如第 9 行语句的输出所示，`b`、`c`、`d` 的值保持不变。

**示例运行 2**

```text
Line 5: Enter four integers: 37 653.89 23 76

Line 8: The numbers you entered are:
Line 9: a = 37, b = 653, c = 30, d = 40
```

在此示例运行中，第 6 行的 `cin` 语句将 37 输入到 `a`，将 653 输入到 `b`，然后试图将小数点输入到 `c`。因为 `c` 是 `int` 变量，小数点被视为字符，所以输入流进入失败状态。在此示例运行中，如第 9 行语句的输出所示，`c` 和 `d` 的值保持不变。

### `clear` 函数

当输入流进入失败状态时，系统会忽略使用该流的所有后续 I/O。你可以使用流函数 `clear` 将输入流恢复到工作状态。

使用函数 `clear` 的语法是：

```cpp
istreamVar.clear();
```

这里，`istreamVar` 是输入流变量，例如 `cin`。

使用函数 `clear` 将输入流恢复到工作状态后，你仍然需要清除输入流中剩余的垃圾数据。这可以通过使用函数 `ignore` 来完成。示例 3-9 说明了这种情况。

### 示例 3-9

```cpp
//Input failure and the clear function
#include <iostream>

using namespace std;

int main()
{
    int a = 23;                                  //Line 1
    int b = 34;                                  //Line 2

    cout << "Line 3: Enter a number followed"
         << " by a character: ";                 //Line 3
    cin >> a >> b;                               //Line 4
    cout << endl << "Line 5: a = " << a
         << ", b = " << b << endl;              //Line 5

    cin.clear();                 //Restore input stream; Line 6

    cin.ignore(200,'\n');        //Clear the buffer; Line 7

    cout << "Line 8: Enter two numbers: ";       //Line 8
    cin >> a >> b;                               //Line 9
    cout << endl << "Line 10: a = " << a
         << ", b = " << b << endl;              //Line 10

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Line 3: Enter a number followed by a character: 78 d

Line 5: a = 78, b = 34
Line 8: Enter two numbers: 65 88

Line 10: a = 65, b = 88
```

第 1 行和第 2 行的语句分别声明变量 `a` 和 `b`，并将它们初始化为 23 和 34。第 3 行的语句提示用户输入一个数字后跟一个字符；第 4 行的语句将该数字输入到变量 `a`，然后试图将该字符输入到变量 `b`。因为 `b` 是 `int` 变量，试图将字符输入到 `b` 会导致输入流进入失败状态。如第 5 行语句的输出所示，`b` 的值保持不变。

第 6 行的语句通过使用函数 `clear` 恢复输入流，第 7 行的语句忽略其余输入。第 8 行的语句再次提示用户输入两个数字；第 9 行的语句将这两个数字存储到 `a` 和 `b`。接着，第 10 行的语句输出 `a` 和 `b` 的值。

## 输出与格式化输出

除了编写高效的程序外，生成期望的输出是程序员最重要的任务之一。第 2 章简要介绍了在标准输出设备上生成输出的过程。更准确地说，你学习了如何使用插入运算符 `<<` 和操纵符 `endl` 在标准输出设备上显示结果。

然而，输出远不止显示结果这么简单。有时，浮点数必须以特定方式输出。例如，工资支票必须打印到两位小数，而科学实验的结果可能要求浮点数输出到六位、七位，甚至十位小数。此外，你可能希望将数字按特定列对齐，或用空白以外的字符填充字符串与数字之间的空白。例如，在编制目录时，章节标题和页码之间的空白可能需要用点或短横线填充。在本节中，你将学习各种输出函数和操纵符，它们允许你按期望的方式格式化输出。

回想一下，`cout` 与插入运算符 `<<` 一起使用时的语法是：

```cpp
cout << expression or manipulator << expression or manipulator...;
```

这里，`expression` 会被求值，其值被打印，而 `manipulator` 用于格式化输出。你目前使用过的最简单的操纵符是 `endl`，它用于将插入点移到下一行的开头。

其他值得关注的输出操纵符包括 `setprecision`、`fixed`、`showpoint` 和 `setw`。接下来几节将介绍这些操纵符。

### `setprecision` 操纵符

你使用操纵符 `setprecision` 控制浮点数的输出。通常，浮点数的默认输出是科学记数法。某些集成开发环境（IDE）可能将浮点数默认输出的最大小数位数设为六位。然而，打印员工工资支票时，期望输出最多两位小数。要将浮点输出打印到两位小数，你使用 `setprecision` 操纵符将精度设置为 2。

`setprecision` 操纵符的一般语法是：

```cpp
setprecision(n)
```

其中 `n` 是小数位数。

