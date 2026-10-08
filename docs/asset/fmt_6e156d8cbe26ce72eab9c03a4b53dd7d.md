
```
Enter string #1:this is a string
Enter string #2:THIS IS A STRING
```

```
this is a string - THIS IS A STRING
Press Enter to continue...
```

### 添加一些库函数

C++ 程序员经常需要处理零终止字符串。C++ 提供了许多标准字符串处理函数来使工作变得简单。其中一些函数列在表 7-1 中。

| 表 7-1 字符串处理函数 |

| 名称 | 操作 |

| :--- | :--- |

| int `strlen(string)` | 返回字符串中的字符数（不包括终止空字符）； |

| char* `strcpy(target, source)` | 将字符串复制到目标数组中。 |

| char* `strcat(target, source)` | 将源字符串拼接到目标字符串之后。 |

| char* `strncpy(target, source, n)` | 将源中的最多 n 个字符复制到目标数组中。 |

| char* `strncat(target, source, n)` | 将源字符串拼接到目标字符串之后或达到 n 个字符，以先者为准。 |

| char* `strstr(str, pattern)` | 返回 pattern 在字符串中首次出现的地址。如果未找到 pattern，则返回空。 |

| int `strcmp(source1, source2)` | 比较两个字符串。如果 source1 在字典序中于 source2 则返回 -1，在之后则返回 1。如果两个字符串完全匹配，则返回 0。 |

| int `strncmp(source1, source2, n)` | 比较两个字符串的前 n 个字符。 |

![](img/b52206ee80ddcd0d5f11a03376f21b9d_133_0.png)

你需要在任何使用 `str...` 函数的程序开头添加 `#include <cstring>` 语句，因为该头文件包含了 C++ 处理你的工作所需的原型声明。

`str...` 函数的参数对任何理性的人来说似乎都是反的（你可能会认为这这是一项对“理性”的审计测试）。例如，函数 `strcat(target, source)` 将源字符串追踪到第一个参数 `target` 的末尾。

`strncpy()` 和 `strcat()` 与 `strcpy()` 和 `strcat()` 的对应项相似，它们接受目标缓冲区长度作为参数之一。调用 `strcpy(szTarget, szSource, 128)` “将 szSource 中的字符复制到 szTarget，直到遇到空字符或复制了 128 个字符，以先者为准。”避免了超出源字符串。

### 为宽字符留空间

标准 C++ 库包含了类似的函数来处理宽字符。其中一些函数列在表 7-2。

| 表 7-2 宽字符串处理函数 |

| 名称 | 操作 |

| :--- | :--- |

| int `wcslen(string)` | 返回字符串中宽字符的数量，不包括终止空。 |

| char* `wcscpy(target, source)` | 将源字符串复制到目标数组。 |

| char* `wcat(target, source)` | 将源字符串拼接到目标字符串之后。 |

| char* `wcsncpy(target, source, n)` | 将源字符串中的最多 n 个宽字符复制到目标数组。 |

| char* `wcscat(target, source, n)` | 将源字符串拼接到目标字符串之后或达到 n 个字符，以先者为准。 |

| char* `wcsstr(string, pattern)` | 查找 pattern 在字符串中首次出现的地址。如果未找到则返回空。 |

| int `wcmp(source1, source2)` | 比较两个宽字符串。如果 source1 在字典序中于 source2 则返回 -1，在之后则返回 1。如果两个字符串完全匹配，则返回 0。 |

| int `wcsncmp(source1, source2)` | 比较两个字符串中的前 n 个宽字符。 |

![](img/b52206ee80ddcd0d5f11a03376f21b9d_134_0.png)

记得第 2 章，宽字符用于必须支持外语的应用程序，此时字符可能不够。以下是 Concatenate 程序的宽字符版本：

```cpp
// ConcatenateWide - 使用库拼接两个宽字符串
// 中间带有 " - "
#include <cstdio>
#include <cstdlib>
#include <iostream>
using namespace std;

int main(int argc, char* argv[])
{
    // 读取第一个字符串...
    wchar_t wsString1[128];
    wcout << L"Enter string #1:";
    wcin.getline(wsString1, 128);

    // ...现在读取第二个字符串...
    wchar_t wsString2[128];
    wcout << L"Enter string #2:";
    wcin.getline(wsString2, 128);

    // 现在将序列追踪到第一个的末尾
    // 中间带一个连字符
    wcat(wsString1, L" - ");
    wcat(wsString1, wsString2);

    wcout << L"\n" << wsString1 << endl;

    // 在终止前等待用户准备好
    // 让用户看到结果
    wcout << L"Press Enter to continue..." << endl;
    wcin.ignore(10, '\n');
    wcin.get();
    return 0;
}
```

宽字符字符串与其单字节字符版本相似，有以下不同：

- 变量声明为 `wchar_t` 而不是 `char`。

- 常量字符和常量字符串前带有 `L`，例如 `L"This is a wide string"`。

- 使用 `wcin` 和 `wcout` 代替 `cin` 和 `cout` 进行输入输出。

- `wcs...` 函数代替了 `str` 函数。

对于大多数使用欧洲语言进行输入输出的人来说，ConcatenateWide 的输出与基于 `char` 的 Concatenate 程序相同。编写能够处理不同字母和语法规则的多语言程序的主被称为本地化（localization），超出了入门书籍的范围。

ANSI C++ 包含了一个 `string` 类型，旨在更方便地处理文本字符串。然而，这种类型使用了你尚未看到的语言特性。我在第 13 章回到 `string` 类型。

![](img/b52206ee80ddcd0d5f11a03376f21b9d_135_0.png)

## 第 8 章：初探 C++ 指针

在本章中：

- 内存中的变量寻址

- 声明和使用指针变量

- 识别指针固有的危险性

- 将指针传递给函数

- 在堆（heap）上分配对象（无论那是什么）

到目前为止，C++ 语言与其他编程语言相比是相当常规的。诚然，某些语言缺乏第 4 章中那样的逻辑运算符，且 C++ 对某些事物有自己独特的符号，但在概念上并没有新东西。C++ 通过使用指针变量与众中脱颖而出。指针是一个“指向”其他变量的变量。我知道这是一个循环论证，但在进入章节之前，请暂不要置信。

本章引入了指针变量。它从一些概念定义开始，流指针语法，然后引入了引发 C++ 编程界指针狂热的一些原因。

### 变量大小

我的体重一直在变化，但在这里我实际上指的是变量的大小，而不是我自己的变量大小。内存以字节（bytes）或位（bits）为单位。`sizeof` 关键字返回其参数按字节的大小。以下程序使用此来确定不同类型的大小：

# 122 第二部分：成为一名功能丰富的 C++ 程序员

```cpp
int main(int nNumberOfArgs, char* pszArgs[])
{
    bool b; char c; int n; long l;
    long long l11; float f; double d; long long ld;

    cout << "sizeof b" << " = " << b << endl;
    cout << "sizeof a char" << " = " << c << endl;
    cout << "sizeof an int" << " = " << n << endl;
    cout << "sizeof a long" << " = " << l << endl;
    cout << "sizeof a long long" << " = " << l11 << endl;
    cout << "sizeof a float" << " = " << f << endl;
    cout << "sizeof a double" << " = " << d << endl;
    cout << "sizeof a long double" << " = " << ld << endl;

    // 等待用户准备好后再终止程序
    // 允许用户看到程序结果
    cout << "Press Enter to continue..." << endl;
    cin.ignore(10, '\n');
    return 0;
}
```

`VariableSizeSize` 程序产生以下输出：

sizeof bool = 1

sizeof a char = 1

sizeof an int = 4

sizeof a long = 4

sizeof a long long = 8

sizeof a float = 4

sizeof a double = 8

sizeof a long double = 12

Press Enter to continue...

> 正如人们所说，“你的结果可能会有所不同。” 使用除 Windows gcc 的编译器可能会得到不同的结果。你可能会发现 `int` 比 `long` 小。C++ 并没有明确说明变量类型到底有多大；它只是说 `long` 的大小与 `int` 相同或更大，且大于 `float`。这里显示的尺寸对于 32 位 80-x 处理器是典型的值。

### 地址中包含什么？

俗话说，“每个人都必须在某处。”每个 C++ 变量都存储在计算机内存的某个地方。内存被划分为单个字节，每个字节都带有其地址数字 0、1、2 等。

![](img/b52206ee80ddcd0d5f11a03376f21b9d_137_0.png)

## 第 8 章：初探 C++ 指针

变量 `intReader` 可能位于地址 `0x100`，而 `floatReader` 可能位于位置 `0x180`。（根据惯例，内存地址用十六进制表示。）当然，`intReader` 和 `floatReader` 可能在内存中完全不同的其他地方——只有计算机在程序执行时才确切知道。

这有点像酒店。当你预订房间时，你可能会被分配到 `0x100` 房间。（我知道套房号通常不用十六进制表示，但请听我说。）你的朋友可能被分配在 80 扇门之外的 `0x180` 房间。每个变量在创建时都会被分配一个地址（关于这一点，在本章讨论作用域时会详细介绍）。

# 地址运算符

表 8-1 所示了两个与指针相关的运算符。`&` 运算符表示“告诉我地址”，而 `*` 表示“后续地址处的值”。

| 表 8-1 | 指针运算符 |

|---|---|

| 运算符 | 含义 |

| & (一元) | (在表达式中) ……的地址 |

| & (一元) | (在声明中) ……的引用 |

| * (一元) | (在表达式中) ……指向的内容 |

| * (一元) | (在声明中) 指向……的指针 |

不要与第 3 和第 4 章讨论的二进制 `&` 和 `*` 运算符混淆。

下面的 `Layout` 程序演示了如何使用 `&` 运算符显示变量在内存中的布局：

```cpp
// Layout - 此程序试图让
// 读者了解编译器中
// 局部内存的布局
#include <stdio>
#include <stdlib>
#include <iostream>
using namespace std;
```

![](img/b52206ee80ddcd0d5f11a03376f21b9d_138_0.png)

# 124 第二部分：成为一名功能丰富的 C++ 程序员

```cpp
int main(int nNumberOfArgs, char* pszArgs[])
{
    int start;
    int n;
    long l;
    long long l1;
    float f;
    double d;
    long long ld;
    int end;

    // 将输出设置为十六进制
    cout.set(ios::hex);
    cout.unset(ios::dec);

    // 输出每个变量的地址
    // 以了解变量在内存
    // 中的布局情况
    cout << "-start = " << start << endl;
    cout << "-n = " << n << endl;
    cout << "-l = " << l << endl;
    cout << "-f = " << f << endl;
    cout << "-d = " << d << endl;
    cout << "-ld = " << ld << endl;

    // 等待用户准备好后再终止程序
    // 允许用户看到结果
    cout << "Press Enter to continue..." << endl;
    cin.ignore(10, '\n');
    cin.get();
    return 0;
}
```

该程序声明了变量，并输出它们的地址，以了解变量在内存中是如何布局的。该程序声明了变量，并输出它们的地址，以了解变量在内存中是如何布局的。其输出如下：

sizeof bool = 1

sizeof a char = 1

sizeof an int = 4

sizeof a long = 4

sizeof a long long = 8

sizeof a float = 4

sizeof a double = 8

sizeof a long double = 12

Press Enter to continue...

## 第 8 章：初探 C++ 指针

### 按值传递

默认情况下，参数是通过值传递给函数的。这带来了一个有些出乎意料的结果：在函数中更改变量的值通常不会改变其在调用函数中的值。考虑以下示例段：

```
void fn(int nArg)
{
  nArg = 10;
  // 此时 nArg 的值是 10
}
void parent(void)
{
  int n1 = 0;
  // 此时 n1 的值仍然是 0
}
```

`parent()` 函数将整数变量 `n1` 初始化为 0。然后将 `n1` 的值传递给 `fn()`。进入 `fn()` 后，`nArg` 等于传递的值 0。更改了 `n1` 的值，返回 `parent()` 后，`n1` 的值仍然是 0。

这种行为的原因是 C++ 并没有将变量直接传递给函数。（我甚至不确定那意味着什么。）相反，C++ 传递的是调用时变量所包含的值。然而，即使只是一个变量名，该表达式也会被求值，并传递结果。

在示例中，`n1` 的值 0 被传递给 `fn()`。函数对该值进行的任何操作对 `n1` 都没有影响。

### 传递指针值

像任何其他内置类型一样，指针也可以作为参数传递给函数：

```
void fn(int* pnArg)
{
  *pnArg = 10;
}
void parent(void)
{
  int n = 0;
  fn(&n);
  // 这传递了 i 的地址
// 现在 n 的值是 10
}
```

第 II 部分：成为一名功能型 C++ 程序员

在这种情况下，传递给函数 `fn()` 的 `n` 的地址而不是 `n` 的值。当你考虑到 `fn()` 内的赋值时，这种差异的意义显而易见。

假设 `n` 位于地址 0x100。调用 `fn(n)` 传递的是值 0x100, 而不是值 10。在 `fn()` 内部，赋值 `*pnArg = 10` 将值 10 存储在位于位置 0x100 的 `int` 变量中，覆盖了值 0。返回到 `parent()` 后，`n` 的值为 10，因为 `n` 仅仅是 0x100 的另一个名字。

### 按引用传递

C++ 提供了一种通过地址传递参数的简写——这种简写让你能够避免使用指针。该声明创建了一个变量 `n1` 和一个指向同一个 `n1` 的第二个引用，但使用了新名称 `nRef`：

```
int n1; // 声明一个 int 变量
int& nRef = n1; // 声明对 n1 的第二个引用
nRef = 1; // 现在为引用赋值
// 效果与访问 n1 相同；
// 现在 n1 等于 1
```

像 `nRef` 这样的变量在声明时必须初始化，因为每当使用它的名称时，C++ 都会认为你指的是的是 `nRef` 所引用的变量。

引用变量的主要应用是在函数调用中：

```
void fn(int& rnArg) // 声明引用参数
{
    rnArg = 10; // 更改变量的值...
    //...即 rnArg 引用的变量
}
void parent(void)
{
    int n = 0; // 传递 n 的引用
    fn(n); // 这里 n 的值是 10
}
```
