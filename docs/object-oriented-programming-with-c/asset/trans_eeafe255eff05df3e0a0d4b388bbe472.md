
-   [用于格式化两个或多个值的输出语句](https://en.cppreference.com/w/cpp/io/manip/setw) 例如，下面的语句

```cpp
cout << setw(5) << setprecision(2) << 1.2345
     << setw(10) << setprecision(4) << sqrt(2)
     << setw(15) << setiosflags(ios::scientific) << sqrt(3)
     << endl;
```

将在一行中输出所有三个值，分别使用 5、10、15 的字段宽度。注意，每个输出都由不同的格式规格控制。

我们可以在程序中同时使用 **ios** 函数和操作符。下面的代码片段是合法的：

```cpp
cout.setf(ios::showpoint);

cout.setf(ios::showpos);
cout << setprecision(4);
cout << setiosflags(ios::scientific);
cout << setw(10) << 123.45678;
```

> **NOTE:** *与操作符相比，ios 成员函数的实现方式有重大区别。ios 成员函数会返回之前的格式状态，可以在需要时使用；而操作符不会返回之前的格式状态。如果需要保存旧的格式状态，必须使用 ios 成员函数而不是操作符。例如：*

```cpp
cout.precision(2); // 之前的状态
int p = cout.precision(4); // 当前状态;
```

执行这两条语句后，p 保存的是 2（之前的状态），新的格式状态为 4。我们可以通过以下方式恢复之前的格式状态：

程序 10.10 通过 **操作符** 和 **ios** 函数共同使用来演示输出值的格式化。

### 程序 10.10：使用操作符的格式化

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    cout.setf(ios::showpoint);

    cout << setw(5) << "n"
         << setw(15) << "Inverse_of_n"
         << setw(15) << "Sum_of_terms\n\n";

    double term, sum = 0;
    for(int n=1; n<=10; n++)
    {
        term = 1.0 / float(n);
        sum = sum + term;
        cout << setw(5) << n
             << setw(14) << setprecision(4)
             << setiosflags(ios::scientific) << term
             << setw(13) << resetiosflags(ios::scientific)
             << sum << endl;
    }
    return 0;
}
```

程序 10.10 的输出如下：

| n | Inverse_of_n | Sum_of_terms |
|---|--------------|--------------|
| 1 | 1.0000e+000 | 1.0000 |
| 2 | 5.0000e-001 | 1.5000 |
| 3 | 3.3333e-001 | 1.8333 |
| 4 | 2.5000e-001 | 2.0833 |
| 5 | 2.0000e-001 | 2.2833 |
| 6 | 1.6667e-001 | 2.4500 |
| 7 | 1.4286e-001 | 2.5929 |
| 8 | 1.2500e-001 | 2.7179 |
| 9 | 1.1111e-001 | 2.8290 |
| 10 | 1.0000e-001 | 2.9290 |

## 设计我们自己的操作符

我们可以为特定用途设计自己的操作符。创建无参数操作符的通用形式如下：

```cpp
ostream & manipulator (ostream & output)
{
    ....
    ... (代码)
    ....
    return output;
}
```

这里的 *manipulator* 是正在创建的操作符名称。下面的函数定义了一个名为 **unit** 的操作符，用于显示 “inches”：

```cpp
ostream & unit (ostream & output)
{
    output << " inches";
    return output;
}
```

语句

```cpp
cout << 36 << unit;
```

会产生以下输出：

```
36 inches
```

我们也可以创建表示一系列操作的操作符。例如：

```cpp
ostream & show(ostream & output)
{
    output.setf(ios::showpoint);
    output.setf(ios::showpos);
    output << setw(10);
    return output;
}
```

该函数定义了一个名为 **show** 的操作符，它打开 **showpoint** 和 **showpos** 标志（在 **ios** 类中声明），并将字段宽度设置为 10。

程序 10.11 演示了自定义操作符的创建和使用。程序创建了两个操作符：**currency** 和 **form**，并在 **main** 程序中使用它们。

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

// 用户定义的操作符

ostream & currency(ostream & output)
{
    output << "Rs";
    return output;
}

ostream & form(ostream & output)
{
    output.setf(ios::showpos);
    output.setf(ios::showpoint);
    output.fill('*');
    output.precision(2);
    output << setiosflags(ios::fixed)
           << setw(10);
    return output;
}

int main()
{
    cout << currency << form << 7864.5;
    return 0;
}
```

程序 10.11 的输出为：

注意，**form** 代表一系列复杂的格式函数和操作。

## 总结

- 在 C++ 中，I/O 系统设计用于与不同 I/O 设备配合工作。该系统通过名为 ‘stream’ 的接口提供给程序员，该接口独立于实际使用的设备。
- 流是字节序列，充当 I/O 数据的来源或目的地。
- 向程序提供数据的源流称为 _input stream_，向程序发送输出的流称为 _output stream_。
- C++ I/O 系统包含用于输入和输出操作的流类层次结构。这些类声明在头文件 ‘_iostream_’ 中。
- **cin** 表示与标准输入设备相连的输入流，**cout** 表示与标准输出设备相连的输出流。
- **istream** 和 **ostream** 类定义了两个成员函数 **get()** 和 **put()**，用于处理单字符的 I/O 操作。
- **>>** 运算符在 **istream** 类中被重载为提取运算符，**<<** 运算符在 **ostream** 类中被重载为插入运算符。
- 我们可以使用面向行的 I/O 函数 **getline()** 和 **write()** 更高效地读取和写入一行文本。
- **ios** 类包含 width()、precision()、fill()、setf()、unsetf() 等成员函数，用于格式化输出。
- 头文件 ‘iomanip’ 提供一组操作符函数，用于操作输出格式，功能与 **ios** 类的成员函数相同。
- 我们还可以为特定目的设计自己的操作符。

## 关键术语

- adjustfield | basefield | bit-fields | console I/O operations | decimal base | destination stream | field width | fill() | filling | fixed point notation | flags | floatfield | formatted console I/O | formatting flags | formatting functions | get() | getline() | hexadecimal base | input stream | internal | ios | iomanip | iostream | istream | left-justified | manipulator | octal base | ostream | output stream | padding | precision() | put() | resetiosflags() | right-justified | scientific notation | setf() | setfill() | setiosflags() | setprecision() | setting precision | setw() | showbase | showpoint | showpos | skipws | source stream | standard input device | standard output device | stream classes | streambuf | streams | unitbuf | unsetf() | width() | write()

## 复习问题

- 10.1 什么是流？
- 10.2 简要描述 C++ I/O 系统支持的特性。
- 10.3 C++ 的 I/O 设施与 C 的有何不同？
- 10.4 为什么 **cin** 和 **cout** 不被视为关键字？
- 10.5 为什么 **cout** 能够在不进行特殊指令的情况下显示各种数据类型？
- 10.6 为什么必须在所有程序中包含头文件 iostream？
- 10.7 讨论 **get()** 函数的各种形式及其用法。
- 10.8 下面两条语句在操作上有何区别？

```cpp
cin >> c;
cin.get(c);
```

- 10.9 **cin** 和 **getline()** 都可以用于读取字符串，请评论。
- 10.10 讨论以下语句中 size 参数的含义：

```cpp
cout.write(line, size);
```

- 10.11 下面的语句起什么作用？

```cpp
cout.write(s1,m).write(s2,n);
```

- 10.12 iomanip 文件起什么作用？
- 10.13 **fill()** 函数的作用是什么？何时使用该函数？
- 10.14 讨论 **setf()** 函数的语法。
- 10.15 操作符与 **ios** 成员函数在实现上有何根本区别？请举例说明。
- 10.16 判断下面的语句是 TRUE 还是 FALSE。
  - (a) 一个 C++ 流是一个文件。
