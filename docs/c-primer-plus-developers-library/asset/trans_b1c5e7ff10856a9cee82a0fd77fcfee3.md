
C 风格字符串与常规数组的一个重要区别是，字符串带有内置的终止字符。（回想一下，包含字符但没有空字符的 char 数组只是一个数组，而不是字符串。）这意味着你不必把字符串的大小作为实参传入。相反，函数可以使用循环依次检查字符串中的每个字符，直到循环到达终止空字符。程序清单 7.9 用一个函数说明了这种方法，该函数统计给定字符在字符串中出现的次数。由于程序不需要处理负值，因此使用 `unsigned int` 作为计数类型。

### 程序清单 7.9 `strgfun.cpp`

```cpp
// strgfun.cpp -- functions with a string argument
#include <iostream>
unsigned int c_in_str(const char * str, char ch);
int main()
{
    using namespace std;
    char mmm[15] = "minimum";    // string in an array
    // some systems require preceding char with static to
    // enable array initialization

    char *wail = "ululate";     // wail points to string

    unsigned int ms = c_in_str(mmm, 'm');
    unsigned int us = c_in_str(wail, 'u');
    cout << ms << " m characters in " << mmm << endl;
    cout << us << " u characters in " << wail << endl;
    return 0;
}

// this function counts the number of ch characters
// in the string str
unsigned int c_in_str(const char * str, char ch)
{
    unsigned int count = 0;

    while (*str)        // quit when *str is '\0'
    {
        if (*str == ch)
            count++;
        str++;           // move pointer to next char
    }
    return count;
}
```

下面是程序清单 7.9 中程序的输出：

```text
3 m characters in minimum
2 u characters in ululate
```

### 程序说明

由于程序清单 7.9 中的 `c_in_str()` 函数不应修改原始字符串，因此它在声明形参 `str` 时使用了 `const` 修饰符。这样，如果你误让函数修改字符串的某一部分，编译器就会捕获你的错误。当然，你也可以改用数组表示法在函数头中声明 `str`：

```cpp
unsigned int c_in_str(const char str[], char ch)  // also okay
```

不过，使用指针表示法可以提醒你：实参不必是数组名，也可以是其他形式的指针。

该函数本身演示了处理字符串中字符的标准方式：

```cpp
while (*str)
{
    statements
    str++;
}
```

最初，`str` 指向字符串中的第一个字符，因此 `*str` 表示第一个字符本身。例如，在第一次函数调用之后，`*str` 的值为 `m`，即 `minimum` 中的第一个字符。只要该字符不是空字符（`\0`），`*str` 就非零，因此循环继续。在每次循环结束时，表达式 `str++` 将指针增加 1 个字节，使其指向字符串中的下一个字符。最终，`str` 指向终止空字符，使 `*str` 等于 0，也就是空字符的数值编码。该条件会终止循环。（为什么字符串处理函数如此“无情”？因为它们不达目的不罢休。）

## 返回 C 风格字符串的函数

现在假设你想编写一个返回字符串的函数。嗯，函数不能直接这样做。但它可以返回字符串的地址，而且这样更高效。例如，程序清单 7.10 定义了一个名为 `buildstr()` 的函数，它返回一个指针。该函数接受两个实参：一个字符和一个数字。函数使用 `new` 创建一个长度等于该数字的字符串，然后将每个元素初始化为该字符。接着，它返回指向新字符串的指针。

### 程序清单 7.10 `strgback.cpp`

```cpp
// strgback.cpp -- a function that returns a pointer to char
#include <iostream>
char * buildstr(char c, int n);    // prototype
int main()
{
    using namespace std;
    int times;
    char ch;

    cout << "Enter a character: ";
    cin >> ch;
    cout << "Enter an integer: ";
    cin >> times;
    char * ps = buildstr(ch, times);
    cout << ps << endl;
    delete [] ps;                 // free memory
    ps = buildstr('+', 20);       // reuse pointer
    cout << ps << "-DONE-" << ps << endl;
    delete [] ps;                 // free memory
    return 0;
}

// builds string made of n c characters
char * buildstr(char c, int n)
{
    char * pstr = new char[n + 1];
    pstr[n] = '\0';           // terminate string
    while (n-- > 0)
        pstr[n] = c;          // fill rest of string
    return pstr;
}
```

下面是程序清单 7.10 中程序的一次示例运行：

```text
Enter a character: V
Enter an integer: 46
VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVV
++++++++++++++++++++-DONE-++++++++++++++++++++
```

### 程序说明

要创建一个包含 n 个可见字符的字符串，你需要存储 n + 1 个字符，以便为空字符留出空间。因此，程序清单 7.10 中的函数请求 n + 1 个字节来保存该字符串。接下来，它将最后一个字节设置为空字符。然后，它从后向前填充数组的其余部分。在程序清单 7.10 中，下面的循环在 n 递减到 0 的过程中循环 n 次，填充 n 个元素：

```cpp
while (n-- > 0)
    pstr[n] = c;
```

在最后一次循环开始时，n 的值为 1。由于 `n--` 表示先使用该值再将其递减，`while` 循环的测试条件会将 1 与 0 比较，发现测试为真，于是继续执行。但在完成测试后，函数会将 n 递减为 0，因此 `pstr[0]` 是最后一个被设置为 c 的元素。从后向前而不是从前向后填充字符串的原因，是为了避免使用额外的变量。如果采用另一种顺序，就会涉及类似下面的代码：

```cpp
int i = 0;
while (i < n)
    pstr[i++] = c;
```

注意，变量 `pstr` 是 `buildstr` 函数的局部变量，因此当该函数终止时，用于 `pstr` 的内存（但不是用于字符串的内存）会被释放。但由于函数返回 `pstr` 的值，程序能够通过 `main()` 中的 `ps` 指针访问新字符串。

程序清单 7.10 中的程序在字符串不再需要后，使用 `delete` 释放用于该字符串的内存。然后它复用 `ps`，使其指向为下一个字符串获得的新内存块，并释放该内存。这种设计（让函数返回指向由 `new` 分配的内存的指针）的缺点是，它让程序员有责任记住使用 `delete`。在第 12 章“类和动态内存分配”中，你将看到 C++ 类如何通过使用构造函数和析构函数来替你处理这些细节。

## 函数和结构

让我们从数组转向结构。为结构编写函数比为数组编写函数更容易。尽管结构变量与数组相似，二者都能保存多个数据项，但在函数方面，结构变量的行为就像基本的单值变量。也就是说，与数组不同，结构将其数据绑定到一个单一实体或数据对象中，并作为一个单元来处理。回想一下，你可以将一个结构赋给另一个结构。同样，你可以按值传递结构，就像传递普通变量一样。在这种情况下，函数处理的是原始结构的副本。此外，函数还可以返回结构。这里没有像数组名就是其首元素地址那样的古怪行为。结构的名称就是结构的名称；如果你想获得它的地址，就必须使用 `&` 地址运算符。（C++ 和 C 都使用 `&` 符号表示地址运算符。C++ 还使用该运算符来标识引用变量，这将在第 8 章讨论。）

使用结构编程最直接的方法，就是像对待基本类型那样对待它们——也就是说，将它们作为实参传递，并在必要时用作返回值。然而，按值传递结构有一个缺点。如果结构很大，制作结构副本所涉及的空间和工作量可能会增加内存需求并拖慢系统。出于这些原因（也因为 C 最初不允许按值传递结构），许多 C 程序员更愿意传递结构的地址，然后使用指针访问结构内容。C++ 提供了第三种选择，称为按引用传递，这将在第 8 章讨论。现在让我们考察另外两种选择，先从传递和返回整个结构开始。
