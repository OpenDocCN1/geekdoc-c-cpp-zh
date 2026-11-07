
使用函数 `putback` 的语法如下：

```
istreamVar.putback(ch);
```

其中，`istreamVar` 是输入流变量，例如 `cin`，而 `ch` 是 `char` 变量。

`peek` 函数返回输入流中的下一个字符，但不会从该流中移除该字符。换言之，peek 函数会查看输入流，并检查下一个输入字符是什么。此外，在检查输入流中的下一个输入字符后，它可以将该字符存储到指定的内存位置，而不将其从输入流中移除。也就是说，使用 peek 函数时，下一个字符保持不变，即使你现在已经知道它是什么。

使用函数 `peek` 的语法如下：

```
ch = istreamVar.peek();
```

其中，`istreamVar` 是输入流变量，例如 `cin`，而 `ch` 是 `char` 变量。

注意 `peek` 函数是如何使用的。首先，`peek` 函数用在赋值语句中。它不像 `get`、`ignore` 和 `putback` 那样是独立语句。其次，`peek` 函数带有空括号。在你能够熟练使用函数并学会如何编写函数之前，请密切注意如何使用预定义函数。

下面的示例说明如何使用 `peek` 和 `putback` 函数。

### 示例 3-7

```cpp
//Functions peek and putback

#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

int main()                                               //Line 3
{
        char ch;                                         //Line 5

        cout << "Line 6: Enter a string: ";             //Line 6
        cin.get(ch);                                     //Line 7
        cout << endl;                                    //Line 8
        cout << "Line 9: After first cin.get(ch): "    //Line 9
             << "ch = " << ch << endl;

        cin.get(ch);                                     //Line 10
        cout << "Line 11: After second cin.get(ch): "  //Line 11
             << "ch = " << ch << endl;

        cin.putback(ch);                                 //Line 12
        cin.get(ch);                                     //Line 13
        cout << "Line 14: After putback and then " << "cin.get(ch); ch = " << ch << endl; //Line 14

        ch = cin.peek();                                //Line 15
        cout << "Line 16: After cin.peek(); ch = "
             << ch << endl;                              //Line 16

        cin.get(ch);                                     //Line 17
        cout << "Line 18: After cin.get(ch); ch = "
             << ch << endl;                              //Line 18

        return 0;                                        //Line 19
}                                                        //Line 20
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

- 第 6 行：输入一个字符串：`abcd`
- 第 9 行：第一次 cin.get(ch) 之后；ch = a
- 第 11 行：第二次 cin.get(ch) 之后；ch = b
- 第 14 行：执行 putback 后再执行 cin.get(ch)；ch = b
- 第 16 行：执行 cin.peek() 之后；ch = c
- 第 18 行：执行 cin.get(ch) 之后；ch = c

用户输入 abcd 可以让你看到前面程序中 get、putback 和 peek 函数的效果。第 6 行中的语句提示用户输入一个字符串。第 7 行中，语句 cin.get(ch); 从输入流中提取第一个字符，并将其存入变量 ch。因此，第 7 行执行后，ch 的值为 'a'。

第 9 行中的 cout 语句输出 ch 的值。第 10 行中的语句 cin.get(ch); 从输入流中提取下一个字符，即 'b'，并将其存入 ch。此时，ch 的值为 'b'。

第 11 行中的 cout 语句输出 ch 的值。第 12 行中的 cin.putback(ch); 语句将由 get 函数先前提取的字符（即 'b'）放回输入流。因此，接下来从输入流中提取的字符是 'b'。

第 13 行中的 cin.get(ch); 语句从输入流中提取下一个字符，该字符仍然是 'b'，并将其存入 ch。现在 ch 的值为 'b'。第 14 行中的 cout 语句将 ch 的值输出为 'b'。

第 15 行中，语句 ch = cin.peek(); 检查输入流中的下一个字符，即 'c'，并将其存入 ch。现在 ch 的值为 'c'。第 16 行中的 cout 语句输出 ch 的值。第 17 行中的 cin.get(ch); 语句从输入流中提取下一个字符，并将其存入 ch。第 18 行中的 cout 语句输出 ch 的值，该值仍为 'c'。

注意，第 15 行中的语句 ch = cin.peek(); 并没有从输入流中移除字符 'c'；它只是窥视了输入流。第 16 行和第 18 行的输出展示了这一功能。

## I/O 流变量与 I/O 函数之间的点表示法：注意事项

在前面的各节中，你学习了如何操作输入流以将数据读入程序。你还学习了如何使用 `get`、`ignore`、`peek` 和 `putback` 函数。重要的是要完全按照所示方式使用这些函数。例如，要使用 `get` 函数，你使用了如下语句：

```
cin.get(ch);
```

省略点——即变量 `cin` 与函数名 `get` 之间的句点——会导致语法错误。例如，在语句：

```
cin.get(ch);
```

`cin` 和 `get` 是由一个点分隔的两个独立标识符。在语句：

```
cinget(ch);
```

`cinget` 变成了一个新标识符。如果你在程序中使用 `cinget(ch);`，编译器会尝试解析一个未声明的标识符，从而产生错误。同样，像 `cin.get` 这样缺少括号也会导致语法错误。另外，请记住，必须将输入函数与输入流变量一起使用。如果你试图单独使用任何输入函数——即不使用输入流变量——编译器可能会生成诸如“未声明的标识符”之类的错误消息。例如，语句 `get(ch);` 可能导致语法错误。

如你所见，有多个函数与 `istream` 变量相关联，每个函数执行特定的任务。回想一下，`get`、`ignore` 等函数是数据类型 `istream` 的成员。这个点被称为**点表示法**，它将输入流变量名与成员名（或函数名）分隔开。事实上，在 C++ 中，点是一个称为**成员访问运算符**的运算符。

> **注意：** C++ 对数据类型 `istream` 和 `ostream` 有一个特殊名称。数据类型 `istream` 和 `ostream` 称为类。变量 `cin` 和 `cout` 也有特殊名称，称为对象。因此，`cin` 称为 `istream` 对象，`cout` 称为 `ostream` 对象。事实上，流变量称为流对象。你将在本书后面的第 11 章学习这些概念。

## 输入失败

程序执行期间可能有很多地方出错。语法正确的程序可能会产生不正确的结果。例如，假设一名兼职员工的工资按以下公式计算：

```
wages = payRate * hoursWorked;
```

如果你不小心将 `*` 输入成了 `+`，计算出的工资将不正确，即使包含 `+` 的语句在语法上是正确的。

那么尝试读取无效数据会怎样呢？例如，如果你试图将字母输入到 `int` 变量中，会发生什么？如果输入数据与相应的变量不匹配，程序就会遇到问题。例如，试图将字母读入 `int` 或 `double` 变量会导致**输入失败**。考虑以下语句：

```cpp
int a, b, c;
double x;
```

如果输入是：

```
W 54
```

那么语句：

```cpp
cin >> a >> b;
```

会导致输入失败，因为你试图将字符 'W' 输入到 `int` 变量 `a` 中。如果输入是：

```
35 67.93 48
```

那么输入语句：

```cpp
cin >> a >> x >> b;
```

会将 35 存入 `a`，67.93 存入 `x`，48 存入 `b`。

现在考虑使用前面的输入（包含三个值的输入）执行以下读取语句：

```cpp
cin >> a >> b >> c;
```

该语句将 35 存入 `a`，将 67 存入 `b`。读取在 `.`（小数点）处停止。由于下一个变量 `c` 的数据类型是 `int`，计算机会尝试将 `.` 读入 `c`，这是一个错误。随后输入流进入一种称为**失败状态**的状态。

当输入流进入失败状态时，实际会发生什么？一旦输入流进入失败状态，使用该流的所有后续 I/O 语句都会被忽略。不幸的是，程序会悄然继续使用变量中存储的任何值执行，并产生不正确的结果。示例 3-8 中的程序演示了输入失败。此程序在你的系统上可能会产生不同的结果。

### 示例 3-8

```cpp
//Input Failure program

#include <iostream>        //Line 1
#include <string>          //Line 2

using namespace std;       //Line 3
```
