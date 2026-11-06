
**float.h** 等。这些由编译器软件提供，因此应放在尖括号内，而不是引号内，如下所示：

```cpp
#include <stdlib.h>
#include <float.h>
```

## 2. 主方法

主方法充当程序的入口点。每个独立的 C++ 程序都必须有一个主方法，否则程序将不知道从哪里开始执行。主方法本质上是一个包含在花括号（{ }）内的函数块。主方法的一般语法如下：

```cpp
int main()
{
    Statements...
    return 0;
}
```

结合本节所学内容，下面是一个什么都不做、但能正确编译和执行的 C++ 程序。

```cpp
#include <iostream>
int main()
{
    //No meaningful statements, just a comment.
    return 0;
}
```

你可以尝试编译并执行上述程序。过程会顺利进行，但屏幕上不会看到任何有意义的内容，因为该程序什么都不做。编译和执行后，你将看到如下内容：

![](img/cda5b023e23ffd0b87fc37b1da33973d_32_0.png)

### 3.7.1 第一个 C++ 程序

现在，让我们学习编写一个简单的 C++ 程序，在屏幕上显示一条消息。*iostream* 头文件提供了一个名为 *cout* 的对象，用于在*标准字符输出*设备上显示数据，大多数情况下该设备就是计算机屏幕。有一种方法可以使用 *I/O 流*将输出重定向到其他设备，而不是默认的计算机屏幕，但这属于相当高级的主题，超出了本书的范围。在本书的整个学习过程中，你将始终使用 *cout* 仅在屏幕上显示数据。*cout* 属于 *iostream* 头文件的 *std* 命名空间，因此需要在 *cout* 前加上 `std::`。

使用 *cout* 的一般语法是：

```cpp
std::cout << {data};
```

*cout* 后跟一个*插入运算符*（`<<`），再后跟要显示的数据。该数据可以是常量、表达式或变量。要显示一条消息，可以使用用双引号括起来的常量字符串。例如：

```cpp
std::cout << "This is a test message";
```

你可以使用新的插入运算符显示任意多个表达式：

```cpp
std::cout << "This is message 1 " << " This is message 2";
```

要在屏幕上插入换行，可使用 *endl*，它属于 *std* 命名空间，因此需要加上 `std::` 前缀。它不是字符串的一部分；因此它应放在引号之外，但要位于新的插入运算符之后：

```cpp
std::cout << "This is line 1" << std::endl <<
"This is line 2" << std::endl;
```

既然我们已经学习了基本的程序结构以及如何在屏幕上显示消息，现在让我们把所有概念结合起来，编写一个在屏幕上显示一些文本的 C++ 程序。如果你已经理解了到目前为止涵盖的章节，理解以下代码不会有问题：

```cpp
int main()
{
    std::cout << std::endl <<
               ;
    std::cout << std::endl <<
               ;
    std::cout << std::endl <<
               ;
    std::cout << std::endl;
    return 0;
}
```

该程序的输出应如下所示：

![](img/cda5b023e23ffd0b87fc37b1da33973d_34_0.png)

在 `cout`、`endl` 以及 `std` 命名空间的其他成员前加上 `std::` 可能很繁琐。有一种方法可以避免这种情况：在开头告诉编译器你将使用 `std` 命名空间。这可以借助 `using` 关键字完成；应在 include 语句之后插入以下语句：

```cpp
using namespace std;
```

如果你在代码中包含了这条语句，`std::cout` 就变成 `cout`，`std::endl` 就变成 `endl`，并且 `std` 命名空间的所有其他成员都可以在不加 `std::` 的情况下使用。

除了 `endl`，还可以在字符串内使用转义序列 `\n` 来插入换行。另一个有用的转义序列是 `\t`，用于插入制表符空格。

让我们编写另一个 C++ 程序，加入 `using namespace std` 语句以摆脱 `std::` 前缀。该程序还将演示 `\n` 和 `\t` 转义序列的用法：

## 3. 语法

```cpp
// get rid of std:: prefix
using namespace std;

// ... main method
int main()
{
    cout << "\nThis is my second C++ program.";
    cout << endl <<
    cout << endl <<

    cout << endl;

    return 0;
}
```

上述程序的输出应如下所示：

![](img/cda5b023e23ffd0b87fc37b1da33973d_36_0.png)

值得注意的是，在包含 *using namespace std* 语句后，代码在没有 `std::` 前缀时看起来多么简洁。我们后续的所有程序都应包含这条语句。

### 3.8 编译错误

如果你不遵循 C++ 语法和规则，就会遇到编译错误。有时编译器会告诉你哪里出错，有时不会，错误消息会笼统而模糊。密切关注你编写的代码并严格遵循语法很重要。

让我们举一个例子，为了演示编译错误，我们故意不遵循语法。下面这段代码中，我没有用分号结束 *cout* 语句：

```cpp
using namespace std;

int main()
{
    cout << "This is a test"
    return 0;
}
```

编译时会发生以下情况：

![](img/cda5b023e23ffd0b87fc37b1da33973d_37_0.png)

在这种情况下，错误消息相当准确，并告诉你到底哪里出错了。编译过程未成功，因此不会生成输出文件。*dir* 命令列出了当前目录中存在的所有文件，证实了这一点：

![](img/cda5b023e23ffd0b87fc37b1da33973d_38_0.png)

## 4. 数据类型

数据类型用于定义我们所处理的数据类型。编程时，我们使用各种变量来存储数据。声明变量时，会在内存位置中为其分配一些内存。根据所用数据的类型，分配适当的内存。C++ 提供内置数据类型以及用户定义的数据类型。用户定义的数据类型使用类和对象构成。如果你熟悉编程，一定已经听说过 *int*（用于整数值）、*float*（用于浮点/小数值）、*char*（用于字符值）等数据类型。以下是内置数据类型的列表：

| 类型 | 大小 | 范围 |
|---|---|---|
| char | 1 字节 | -127 到 127 或 0 到 255 |
| unsigned char | 1 字节 | 0 到 255 |
| signed char | 1 字节 | -127 到 127 |
| int | 4 字节 | -2147483648 到 2147483647 |
| unsigned int | 4 字节 | 0 到 4294967295 |
| signed int | 4 字节 | -2147483648 到 2147483647 |
| short int | 2 字节 | -32768 到 32767 |
| unsigned short int | 2 字节 | 0 到 65,535 |
| signed short int | 2 字节 | -32768 到 32767 |
| long int | 4 字节 | -2,147,483,648 到 2,147,483,647 |
| signed long int | 4 字节 | -2,147,483,648 到 2,147,483,647 |
| unsigned long int | 4 字节 | 0 到 4,294,967,295 |
| float | 4 字节 | 1.17549e-38 到 3.40282e+38 |
| double | 8 字节 | 2.22507e-308 到 1.79769e+308 |
| long double | 12 字节 | 因操作系统而异 |

这些是内置的原始数据类型。如你所见，其中没有提到字符串数据类型。这是因为字符串只是字符序列，而字符数组可以很好地充当字符串。不过，C++ 提供了一种单独的非原始数据类型，称为 *string 类*，它是 *std 命名空间*的一部分。

*注意：* 虽然大多数时候大小和范围值与上述相同，但可能因编译器和/或操作系统而异。除非你在嵌入式系统等受限环境中编写对性能至关重要的低级应用程序，否则这不算什么大问题。

### 趣味练习

为了展示不同操作系统间数据类型大小的差异，这里有一个趣味练习——有一个名为 *sizeof()* 的运算符，它返回所提及的数据、数据类型、变量或常量的大小。以下代码使用 GCC 分别在 Windows 和 Linux 操作系统上编译并执行：

```cpp
using namespace std;

int main()
{
    cout << "Size of int: " << sizeof(int) << endl;
    cout << "Size of long int: " << sizeof(long int) << endl;
    cout << "Size of char: " << sizeof(char) << endl;
    cout << "Size of float: " << sizeof(float) << endl;
    cout << "Size of long double: " << sizeof(long double) << endl;
}
```
