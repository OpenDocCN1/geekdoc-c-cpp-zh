
注意 `peek` 函数的使用方式。首先，`peek` 函数用于赋值语句中。它不是像 `get`、`ignore` 和 `putback` 那样的独立语句。其次，`peek` 函数的括号是空的。在你熟练使用函数并学会编写函数之前，请密切注意如何使用预定义函数。

下面的示例说明了如何使用 `peek` 和 `putback` 函数。

### 示例 3-7

```cpp
// Functions peek and putback

#include <iostream>

using namespace std;

int main()
{
    char ch;

    cout << "Line 1: Enter a string: ";                 //Line 1
    cin.get(ch);                                        //Line 2
    cout << endl;                                       //Line 3
    cout << "Line 4: After first cin.get(ch); "         //Line 4
         << "ch = " << ch << endl;

    cin.get(ch);                                        //Line 5
    cout << "Line 6: After second cin.get(ch); "
         << "ch = " << ch << endl;                     //Line 6

    cin.putback(ch);                                    //Line 7
    cin.get(ch);                                        //Line 8
    cout << "Line 9: After putback and then "
         << "cin.get(ch); ch = " << ch << endl;        //Line 9

    ch = cin.peek();                                    //Line 10
    cout << "Line 11: After cin.peek(); ch = "
         << ch << endl;                                //Line 11

    cin.get(ch);                                        //Line 12
    cout << "Line 13: After cin.get(ch); ch = "
         << ch << endl;                                //Line 13

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Line 1: Enter a string: abcd

Line 4: After first cin.get(ch); ch = a
Line 6: After second cin.get(ch); ch = b
Line 9: After putback and then cin.get(ch); ch = b
Line 11: After cin.peek(); ch = c
Line 13: After cin.get(ch); ch = c
```

用户输入 `abcd` 让你能够看到上述程序中 `get`、`putback` 和 `peek` 函数的效果。第1行的语句提示用户输入一个字符串。在第2行，语句 `cin.get(ch);` 从输入流中提取第一个字符并将其存储到变量 `ch` 中。因此，在第2行执行后，`ch` 的值是 `'a'`。

第4行的 `cout` 语句输出 `ch` 的值。第5行的 `cin.get(ch);` 语句从输入流中提取下一个字符，即 `'b'`，并将其存储到 `ch` 中。此时，`ch` 的值是 `'b'`。

第6行的 `cout` 语句输出 `ch` 的值。第7行的 `cin.putback(ch);` 语句将 `get` 函数先前提取的字符（即 `'b'`）放回输入流。因此，接下来要从输入流中提取的字符是 `'b'`。

第8行的 `cin.get(ch);` 语句从输入流中提取下一个字符（仍然是 `'b'`），并将其存储到 `ch` 中。现在 `ch` 的值是 `'b'`。第9行的 `cout` 语句输出 `ch` 的值为 `'b'`。

在第10行，语句 `ch = cin.peek();` 检查输入流中的下一个字符，即 `'c'`，并将其存储到 `ch` 中。现在 `ch` 的值是 `'c'`。第11行的 `cout` 语句输出 `ch` 的值。第12行的 `cin.get(ch);` 语句从输入流中提取下一个字符并将其存储到 `ch` 中。第13行的 `cout` 语句输出 `ch` 的值，该值仍然是 `'c'`。

注意，第10行的语句 `ch = cin.peek();` 并未从输入流中移除字符 `'c'`；它只是窥视了输入流。第11行和第13行的输出演示了此功能。

## I/O 流变量与 I/O 函数之间的点表示法：注意事项

在前面几节中，你学习了如何操作输入流以将数据读入程序。你还学习了如何使用 `get`、`ignore`、`peek` 和 `putback` 函数。按照所示方式准确使用这些函数非常重要。例如，要使用 `get` 函数，可以使用如下语句：

```cpp
cin.get(ch);
```

省略点——即变量 `cin` 与函数名 `get` 之间的句点——会导致语法错误。例如，在语句：

```cpp
cin.get(ch);
```

`cin` 和 `get` 是由一个点分隔的两个独立标识符。在语句：

```cpp
cinget(ch);
```

`cinget` 变成了一个新标识符。如果你在程序中使用 `cinget(ch);`，编译器将尝试解析一个未声明的标识符，从而产生错误。类似地，缺少括号（如 `cin.getch;`）会导致语法错误。另外，请记住，必须将输入函数与输入流变量一起使用。如果你尝试单独使用任何输入函数——即没有输入流变量——编译器可能会生成诸如“未声明的标识符”之类的错误消息。例如，语句 `get(ch);` 可能导致语法错误。

如你所见，多个函数与 `istream` 变量相关联，每个函数执行特定的任务。回想一下，`get`、`ignore` 等函数是数据类型 `istream` 的成员。这被称为**点表示法**。点将输入流变量名与成员（或函数）名分隔开。实际上，在 C++ 中，点是一个运算符，称为**成员访问运算符**。

> **注意**  
> C++ 为数据类型 `istream` 和 `ostream` 指定了专门的名称。数据类型 `istream` 和 `ostream` 被称为类。变量 `cin` 和 `cout` 也有专门的名称，称为对象。因此，`cin` 被称为 `istream` 对象，`cout` 被称为 `ostream` 对象。实际上，流变量被称为流对象。你将在本书后文题为 *继承和组合* 的章节中学习这些概念。

## 输入失败

在程序执行过程中，很多事情都可能出错。一个语法正确的程序可能会产生不正确的结果。例如，假设通过以下公式计算一名兼职工人的工资：

```cpp
wages = payRate * hoursWorked;
```

如果你不小心输入了 `+` 而不是 `*`，即使包含 `+` 的语句在语法上是正确的，计算出的工资也会不正确。

那么，尝试读取无效数据会怎样呢？例如，如果你试图向 `int` 变量输入一个字母，会发生什么？如果输入数据与相应的变量不匹配，程序就会遇到问题。例如，尝试将字母读入 `int` 或 `double` 变量会导致**输入失败**。考虑以下语句：

```cpp
int a, b, c;
double x;
```

如果输入是：

```text
w 54
```

那么语句：

```cpp
cin >> a >> b;
```

将导致输入失败，因为你试图将字符 `'w'` 输入到 `int` 变量 `a` 中。如果输入是：

```text
35 67.93 48
```

那么输入语句：

```cpp
cin >> a >> x >> b;
```

会将 35 存储到 `a`，67.93 存储到 `x`，48 存储到 `b`。

现在考虑使用之前的输入（包含三个值的输入）的以下读取语句：

```cpp
cin >> a >> b >> c;
```

该语句将 35 存储到 `a`，将 67 存储到 `b`。读取在 `.`（小数点）处停止。由于下一个变量 `c` 的数据类型是 `int`，计算机试图将 `.` 读取到 `c` 中，这是一个错误。输入流随后进入一种称为**失败状态**的状态。

当输入流进入失败状态时，实际上会发生什么？一旦输入流进入失败状态，所有使用该流的后续 I/O 语句都将被忽略。不幸的是，程序会悄悄地继续执行，并使用变量中已存储的值，从而产生不正确的结果。示例 3-8 中的程序演示了输入失败。该程序在您的系统上可能产生不同的结果。

### 示例 3-8

```cpp
// Input Failure program

#include <iostream>

using namespace std;

int main()
{
    int a = 10;                              //Line 1
    int b = 20;                              //Line 2
    int c = 30;                              //Line 3
    int d = 40;                              //Line 4

    cout << "Line 5: Enter four integers: ";  //Line 5
    cin >> a >> b >> c >> d;                 //Line 6
    cout << endl;                             //Line 7
    cout << "Line 8: The numbers you entered are:"
         << endl;                             //Line 8
    cout << "Line 9: a = " << a << ", b = " << b
         << ", c = " << c << ", d = " << d << endl; //Line 9

    return 0;
}
```

