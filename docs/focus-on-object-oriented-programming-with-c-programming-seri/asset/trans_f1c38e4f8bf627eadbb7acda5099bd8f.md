
暂时不用担心语法，但我们在这里使用作用域解析运算符来识别我们正在为哪个 `foo()` 函数提供定义。一种看待作用域解析运算符的方式是将其视为提供到标识符的路径。稍后详述！

## Structures

在 C 语言中，结构名称不是类型名称。每当引用结构时，都必须使用关键字 `struct`：

```
struct Employee {
    int salary;
    struct Employee *reportsTo;
};

struct Employee Haley;

struct Employee* updateReportsTo(struct Employee*, struct Employee*);
```

在 C++ 中，结构名称是类型名称，就像它们被 typedef 一样。`struct` 关键字是多余的：

```
struct Employee {
    int salary;
    Employee *reportsTo;
};

Employee Haley;

Employee* updateReportsTo(Employee*, Employee*);
```

## Operator Precedence

在下面的运算符优先级表中，C++ 运算符被分为 13 个类别。第 #1 类别具有最高优先级，第 #2 类别（一元运算符）位居第二，依此类推，直到优先级最低的逗号运算符。每个类别内的运算符具有相同的优先级。一元运算符（第 #2 类别）、条件运算符（第 #11 类别）和赋值运算符（第 #12 类别）自右向左结合；所有其他运算符自左向右结合。

| # | 类别 | 运算符 | 它是什么（或做什么） |
|---|---|---|---|
| 1. | 最高 | () | 函数调用 |
| | | [] | 数组下标 |
| | | -> | C++ 间接成员选择符 |
| | | :: | C++ 作用域访问/解析 |
| | | . | C++ 直接成员选择符 |
| 2. | 一元 | ! | 逻辑非（NOT） |
| | | ~ | 按位（1的）补码 |
| | | + | 一元加 |
| | | - | 一元减 |
| | | ++ | 前递增或后递增 |
| | | -- | 前递减或后递减 |
| | | & | 取地址 |
| | | * | 间接寻址 |
| | | sizeof | 返回操作数的大小，以字节为单位 |
| | | new | 动态分配 C++ 存储 |
| | | delete | 动态释放 C++ 存储 |
| 3. | 成员访问 | .* | C++ 解引用 |
| | | ->* | C++ 解引用 |
| 4. | 乘法 | * | 乘 |
| | | / | 除 |
| | | % | 余数（模） |
| 5. | 加法 | + | 二元加 |
| | | - | 二元减 |
| 6. | 移位 | << | 左移 |
| | | >> | 右移 |
| 7. | 关系 | < | 小于 |
| | | <= | 小于或等于 |
| | | > | 大于 |
| | | >= | 大于或等于 |
| 8. | 相等 | == | 等于 |
| | | != | 不等于 |
| 9. | 按位 | & | 按位与 |
| | | \| | 按位或 |
| | | ^ | 按位异或 |
| 10. | 逻辑 | && | 逻辑与 |
| | | \|\| | 逻辑或 |
| 11. | 条件 | ?: | 条件运算符 |
| 12. | 赋值 | = | 简单赋值 |
| | | \*= | 赋积 |
| | | /= | 赋商 |
| | | %= | 赋余数（模） |
| | | += | 赋和 |
| | | -= | 赋差 |
| | | &= | 赋按位与 |
| | | ^= | 赋按位异或 |
| | | \|= | 赋按位或 |
| | | <<= | 赋左移 |
| | | >>= | 赋右移 |
| 13. | 逗号 | , | 求值 |

表中的所有运算符都可以重载，但以下运算符除外：

- . C++ 直接成员选择符
- .* C++ 解引用
- :: C++ 作用域访问/解析
- ?: 条件运算符

## First C++ Program

本练习旨在确保你能让 C++ 编译器正常工作，并演示 C++ I/O 系统的几个简单特性。当你想在 C++ 程序中将输出发送到标准输出设备时，可以使用标准 C 库中的某个输出函数。例如，下面这一行：

```cpp
printf("String = %s\n", buf);
```

在标准输出设备上显示字符串 buf 的值。但是，由于我们正在编写 C++ 代码，我们使用 ostream 类中的 cout 将输出发送到标准输出设备。例如，下面这一行：

```cpp
cout << "String = " << buf << '\n';
```

在标准输出设备上显示相同的字符串 buf。输入、编译并执行以下 C++ 程序的源代码：

```cpp
// test.cpp - simple i/o test program
#include <iostream>
using namespace std;
int main() {
    char buf[80];
    cout << "Type your first name: ";
    cin >> buf;
    cout << "Congratulations, " << buf
         << ", you have successfully compiled a C++ program.\n";
    return 0;
}
```

在这个程序中，cin 和 cout 是输入和输出对象，而 << 和 >> 运算符（在 C 中通常用于位移）已被重载为表示从中获取（插入）和向中放入（提取）。所有这些都在标准 C++ I/O 库 iostream 中处理。请注意，C++ 程序文件的后缀为 .cpp。

现在，注释掉预处理器指令：

```cpp
// #include <iostream>
```

然后编译 C++ 程序。注意由此产生的错误消息。

## Output Streams

虽然你可以使用 `printf()` 或 `cout` 中的任意一个，但在同一个程序中同时使用两者可能会导致问题。为了了解可能出现的问题，请输入、编译并执行以下 C++ 程序：

```cpp
// bad.cpp - uses both printf() and cout to send output to the
// standard output device

#include <iostream>
#include <stdio.h>

using namespace std;

int main() {
    // turn on buffered output for cout
    cout.unsetf(ios::unitbuf);

    printf("Print this first.\n");
    cout << "Print this second.\n";
    printf("Print this third.\n");
    cout << "Print this last.\n";
    return 0;
}
```

仔细查看 bad.cpp，你可以看到我们交替使用了 `printf()` 和 `cout` 来显示四个字符串。乍一看，`bad.cpp` 中的代码似乎没有错误。但是，一些较旧的 C++ 编译器会产生以下输出：

```
Print this first.
Print this third.
Print this second.
Print this last.
```

而较新的 C++ 编译器会产生以下输出：

```
Print this first.
Print this second.
Print this third.
Print this last.
```

注意：为了学习 C++ 输出流的一些重要元素，我们将重点关注较旧 C++ 编译器的输出。

显然，bad.cpp 并没有产生我们期望的输出。程序似乎不是按顺序执行其行，而是先调用 printf() 行，然后再调用 cout 行。实际上，bad.cpp 确实正确执行了其代码行。问题在于 bad.cpp 对 cout 使用了缓冲输出。当 cout（或任何 ostream 对象）使用缓冲输出时，cout 不会显示你发送的内容，直到其输出缓冲区满或缓冲区被刷新为止。bad.cpp 中使用 cout 的两行没有填充输出缓冲区，因此程序在终止时刷新 cout 流之前不会输出这些字符串。了解这一点后，我们可以跟踪 bad.cpp 的代码来看看发生了什么。

首先，bad.cpp 调用 printf() 显示字符串“首先打印这个”，并立即显示它。接下来，bad.cpp 将字符串“其次打印这个”插入到 cout 中。由于该字符串没有填满 cout 的缓冲区，它只是将字符串存储在内存中以供稍后显示。接下来，bad.cpp 带有字符串“第三打印这个”调用 printf()，并立即显示它，尽管“其次打印这个”仍在 cout 的缓冲区中。最后，bad.cpp 将字符串“最后打印这个”插入到 cout 中，cout 也将其存储在内存中以供稍后输出。当 bad.cpp 终止时，它会调用 cout 的析构函数，该析构函数会自动刷新任何非空缓冲区。此时，程序会显示它插入到 cout 中的两个字符串。

幸运的是，有一种方法可以强制 cout 在每次插入输出时刷新其缓冲区的内容。（请注意，刷新缓冲区输出的能力是使用输出流时的一项非常重要的任务。）ostream 类定义了 flush() 成员函数，你可以随时调用它。ostream 类还定义了 flush 操纵符，你可以将其与输出流中的其他数据一起插入。以下程序 ok1.cpp 使用 flush 操纵符来强制显示它插入到 cout 中的字符串。

输入、编译并执行以下 C++ 程序：

```cpp
// ok1.cpp - uses flush with cout
#include <iostream>
#include <stdio.h>
using namespace std;
int main() {
    // turn on buffered output for cout
    cout.unsetf(ios::unitbuf);
    printf("Print this first.\n");
    cout << "Print this second.\n" << flush;
    printf("Print this third.\n");
    cout << "Print this last.\n" << flush;
    return 0;
}
```

如你所见，你只需在希望 cout 刷新缓冲区内容时插入 flush 操纵符即可。当你编译并运行 ok1.cpp 时，你会在所有编译器上得到你期望的输出：

```
Print this first.
Print this second.
Print this third.
Print this last.
```

与其在每个输出字符串后插入 flush 操纵符，不如添加一行调用 ostream::flush() 成员函数。例如，下面这一行：

```cpp
cout.flush();
```

直接刷新 cout 的缓冲区。
