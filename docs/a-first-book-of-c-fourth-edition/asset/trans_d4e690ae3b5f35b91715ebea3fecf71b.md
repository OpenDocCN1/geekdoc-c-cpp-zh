

using namespace std;

namespace dataChecks
{
    bool isvalidInt(string str)
    {
        int start = 0;
        int i;
        bool valid = true;  // assume a valid
        bool sign = false;  // assume no sign

        // check for an empty string
        if (int(str.length()) == 0) valid = false;

        // check for a leading sign
        if (str.at(0) == '-' || str.at(0) == '+')
        {
            sign = true;
            start = 1;  // start checking for digits after the sign
        }

        // check that there's at least one character after the sign
        if (sign && int(str.length()) == 1) valid = false;

        // check the string, which has at least one non-sign char
        i = start;
        while(valid && i < int(str.length()))
        {
            if(!isdigit(str.at(i))) valid = false; //found a nondigit character
            i++;  // move to next character
        }
        return valid;
    }

    int getanInt()
    {
        bool isvalidInt(string);  // function prototype
        bool notanint = true;
        string svalue;

        while (notanint)
        {
            try
            {
                cin >> svalue;  // accept a string input
```

程序 14.20 中 `#include` 语句的唯一要求是，文件名和位置必须对应于指定路径中存在的一个同名文件；否则会发生编译错误。如果您想为源代码文件命名并使用文件扩展名，只要遵循以下规则，任何扩展名都可以使用：

- 代码存储的文件名包含扩展名。
- `#include` 语句中使用相同的包含扩展名的文件名。

因此，如果用于存储函数的文件名是 dataLib.cpp，则程序 14.20 中的 `#include` 语句应为如下形式：

```
#include <c:\\mylibrary\\dataLib.cpp>
```

请注意，文件中并不需要命名空间。使用命名空间可以使您将特定代码隔离在一个命名区域中，并在需要时向文件中添加更多命名空间。在 using 语句中指定命名空间可告诉编译器仅包含指定命名空间中的代码，而不是文件中的所有代码。在程序 14.20 中，如果数据检查函数未被包含在命名空间中，则用于 dataChecks 命名空间的 using 语句就必须省略。

将之前编写并测试过的数据检查函数作为单独文件包含在程序 14.20 中，可以让您专注于为正在编程的任务使用这些函数的代码，而不必担心命名空间的代码。在程序 14.20 中，main() 函数练习数据检查函数并产生与程序 14.19 相同的输出。在创建 dataChecks 命名空间时，您已包含了这两个函数的源代码。包含此代码不是必需的，并且可以改为保存源代码的编译版本。最后，一个命名空间可以通过添加 #include 和 using 语句的相同技术访问另一个命名空间。

## EXERCISES 14.8

- 1. (练习) 输入并编译程序 14.20。 (提示：命名空间文件 dataChecks 和程序文件可与本书网站上提供的源代码一起使用。有关 URL，请参阅本书介绍。)
- 2. (思考) a. 命名空间的优点是什么？
- b. 命名空间的可能缺点是什么？
- 3. (思考) 您会在个人库中包含哪些类型的类和函数？为什么？
- 4. (思考) 为什么程序员会以编译形式而不是源代码形式提供命名空间文件？
- 5. (实用工具) a. 编写一个名为 whole() 的 C++ 函数，该函数返回传递给该函数的任何数字的整数部分。 (提示：将传递的参数赋给一个整数变量。)
- b. 将练习 5a 中编写的函数包含在一个工作程序中。确保您的函数从 main() 调用并正确地向 main() 返回一个值。让 main() 使用 cout 语句显示返回的值。通过向其传递各种数据来测试该函数。

## Chapter 14

第 14 章补充：命名空间和创建个人库

c. 当您确信为练习 5a 编写的 whole() 函数工作正确时，将其保存在您选择的命名空间和个人库中。

- 6. **(实用工具)**
- **a.** 编写一个名为 `fracpart()` 的 C++ 函数，该函数返回传递给该函数的任何数字的小数部分。例如，如果数字 256.879 传递给 `fracpart()`，则应返回数字 .879。让 `fracpart()` 函数调用您在练习 5a 中编写的 `whole()` 函数。然后返回的数字可以确定为传递给 `fracpart()` 的数字减去将同一参数传递给 `whole()` 时返回的值。
- **b.** 将练习 6a 中编写的函数包含在一个工作程序中。确保该函数从 `main()` 调用并正确地向 `main()` 返回一个值。让 `main()` 使用一个 `cout` 语句显示返回的值。通过向其传递各种数据来测试该函数。
- **c.** 当您确信为练习 6a 编写的 `fracpart()` 函数工作正确时，将其保存在为练习 5c 选择的相同命名空间和个人库中。

此页故意留空

## 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法能够高效地从复杂布局中提取结构化信息。

随着数字化办公的普及，文档格式日益多样化，传统的解析技术面临巨大挑战。

## 2. 方法概述

- 步骤一：图像预处理
- 步骤二：版面分析
- 步骤三：内容提取
- 步骤四：结构化输出

上述步骤中，版面分析是核心环节，它决定了后续内容提取的准确性。

## 3. 实验结果

| 方法 | 准确率 | 召回率 |
|------|--------|--------|
| 传统方法 | 85.2% | 82.1% |
| 本文方法 | 94.7% | 93.5% |

实验结果表明，本文方法在各项指标上均优于传统方法。

## 15.1 C-String Fundamentals

C-string，即“字符字符串”，是一个以特殊结束符 NULL 字符结尾的字符数组。¹ NULL 字符由转义序列 '\0' 表示，是标记字符串结束的哨兵。

C-string 可以通过多种方式创建。例如，以下每个声明都创建相同的 C-string。

```
char test[5] = "abcd";
char test[] = "abcd";
char test[5] = {'a', 'b', 'c', 'd', '\0'};
char test[] = {'a', 'b', 'c', 'd', '\0'};
```

每个声明都为恰好五个字符的数组创建存储空间，并用字符 'a'、'b'、'c'、'd' 和 '\0' 初始化该存储空间。当使用字符串字面量进行初始化时，如前两个声明中所示，编译器会自动提供结束符 NULL 字符。图 15.1 显示了通过这些声明中的每一个创建的字符串在内存中的存储方式。

![](img/202cface8244f523c2641baa2e00d7dd_685_0.png)

如图所示，图 15.1 中此字符串使用五个存储位置，最后一个字符是结束符 '\0'。如图所示，包围字符串的引号在前两个声明中并不作为字符串的一部分存储。因为它是一个数组，所以字符可以通过使用标准数组处理技术，包括下标和指针表示法进行输入、操作或输出。

# C-String Input and Output

从键盘输入 C-string 并显示它需要使用标准库函数或类方法。除了标准输入输出流 cin 和 cout 之外，还提供了用于逐字符和完整 C-string 输入/输出的库函数。表 15.1 列出了常用的方法，这些方法需要 iostream 头文件。

## Point of Information

**Should You Use a C-String or a string Class Object?**

使用 C-string 的原因如下：

- 程序员可以控制 C-string 的存储和操作方式。
- 可用于输入、检查和处理 C-string 的有用函数很多。
- C-string 是探索使用指针的高级编程技术的绝佳方式（参见第 15.2 节）。
- 您将在整个编程生涯中遇到它们，因为它们嵌入在几乎所有现有的 C++ 代码中。
- 编程它们很有趣。

使用 string 类对象的理由如下：

- string 类对用于访问字符串元素的每个索引进行自动边界检查。对于 C-string 来说并非如此，使用无效的 C-string 下标可能导致系统崩溃。
- string 类根据需要自动扩展和收缩存储空间。C-string 长度固定，容易超出分配的存储空间。
- string 类提供了用于操作字符串的广泛方法。C-string 几乎总是需要一组辅助函数。
- 在必要时，可以使用 string 类的 `c_str()` 方法轻松转换为 C-string。相反，C-string 可以通过简单地将其分配给 string 对象轻松转换为 string 类对象。

**Table 15.1  String and Character I/O Methods (Require the Header File iostream)**

| C++ Method | Description | Example |
|---|---|---|
| `cin.getline(str,n,ch)` | 从键盘输入一个 C-string (`str`)，最多 n 个字符，以字符 ch 终止（通常是换行符 `\n`） | `cin.getline(str, 81, '\n');` |
| `cin.get()` | 从输入流中提取下一个字符 | `nextKey = cin.get();` |
| `cin.peek()` | 返回输入流中的下一个字符，但不从流中提取该字符 | `nextKey = cin.peek();` |
| `cout.put(charExp)` | 将 charExp 的字符值放在输出流上 | `cout.put('A');` |

