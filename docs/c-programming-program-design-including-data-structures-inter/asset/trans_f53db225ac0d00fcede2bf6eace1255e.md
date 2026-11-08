

```
Account Balance: $892.85
Eighth (from the end) customer's data:
ID: 11111
First Name: Rita
Last Name: Gupta
Account Balance: $14863.50
```

示例 E-6 中的程序演示了函数 seekg 的工作方式。使用函数 seekg，可以将文件中的读取位置移动到文件中的任意位置。类似地，函数 seekp 可用于将文件中的写入位置移动到任意位置。此外，这些函数可用于创建二进制文件，其中的数据按照某个变量的值或结构体的某个特定分量的值来组织。例如，假设一个班级中最多有，比如说，100 名学生。每名学生都有一个 1 到 100 范围内的唯一 ID。使用学生 ID，我们可以创建随机访问二进制文件，使得在文件中，某个学生的数据被写入其 ID 所指定的位置。这就像把文件当作一个数组来处理。优点在于，文件创建后，可以直接使用学生 ID 从文件中读取该学生的数据。另一个优点是，在文件中，数据按 ID 排序。

这里，我们假设学生 ID 在 1 到 100 的范围内。然而，如果你使用，比如说，三位、四位或五位数字作为学生 ID，而班级中只有少数几名学生，那么文件中的数据可能会分散。换句话说，可能会用大量空间只存储少数几名学生数据。在这种情况下，会使用更高级的技术来组织数据，以便能够高效地访问。

示例 E-7 中的程序演示了如何使用学生 ID 来组织二进制文件中的数据。该程序还展示了如何输出该文件。

## 示例 E-7

```cpp
//Creating and reading a random access file.

#include <iostream>
#include <fstream>
#include <iomanip>

using namespace std;

struct studentType
{
    char firstName[15];
    char lastName[15];
    int ID;
    double GPA;
};

void printStudentData(const studentType& student);

//read the data at location 0 in the file
inFile.read(reinterpret_cast<char *> (&st),
            sizeof(st));
while (inFile)
{
    if (st.ID != 0)
        printStudentData(st);

    //read the data at the current reading position
    inFile.read(reinterpret_cast<char *> (&st),
                sizeof(st));
}

return 0;
}

void printStudentData(const studentType& student)
{
    cout << left << setw(3) << student.ID
         << setw(16) << student.firstName
         << setw(16) << student.lastName
         << right << setw(10) << student.GPA
         << endl;
}
```

### 示例运行：

| ID | 名 | 姓 | 当前 GPA |
|---:|---|---|---:|
| 2 | Sheila | Duffy | 4.00 |
| 10 | Ajay | Kumar | 3.60 |
| 12 | Ashley | White | 3.90 |
| 16 | Tommy | Pitts | 2.40 |
| 23 | Rita | Gupta | 3.40 |
| 34 | Brad | Smith | 3.50 |
| 36 | Salma | Quade | 3.90 |
| 41 | Steve | Sharma | 3.50 |
| 45 | Sheila | Robinson | 2.50 |
| 56 | Lisa | Johnson | 2.90 |
| 67 | Jose | Ramey | 3.80 |
| 75 | Jennifer | Ackerman | 4.00 |

文件 studentData.txt 中的数据如下：

```text
12 Ashley White 3.9
34 Brad Smith 3.5
56 Lisa Johnson 2.9
45 Sheila Robinson 2.5
23 Rita Gupta 3.4
10 Ajay Kumar 3.6
67 Jose Ramey 3.8
2 Sheila Duffy 4.0
16 Tommy Pitts 2.4
```

## ANSI/ISO 标准 C++ 和标准 C++ 中头文件的命名约定

本书中的程序使用 ANSI/ISO 标准 C++ 编写。正如第 1 章所述，C++ 有两个版本——ANSI/ISO 标准 C++ 和标准 C++。在很大程度上，这两个标准是相同的。标准 C++ 中的头文件扩展名为 `.h`，而 ANSI/ISO 标准 C++ 中的头文件没有扩展名。此外，在 ANSI/ISO 标准 C++ 中，某些头文件（例如 `math.h`）的名称以字母 c 开头。C++ 语言由 C 演变而来。因此，某些头文件——例如 `math.h`、`stdlib.h` 和 `string.h`——从 C 引入到了 C++ 中。头文件——例如 `iostream.h`、`iomanip.h` 和 `fstream.h`——是为 C++ 专门设计的。回想一下，当头文件被包含到程序中时，该头文件的全局标识符也会成为程序的全局标识符。在 ANSI/ISO 标准 C++ 中，为了利用命名空间机制，所有头文件都经过了修改，使标识符在命名空间内声明。回想一下，这个命名空间的名字是 `std`。

在 ANSI/ISO 标准 C++ 中，为 C++ 专门设计的头文件的扩展名 `.h` 被去掉了。对于从 C 引入到 C++ 的头文件，扩展名 `.h` 被去掉，并且这些头文件的名称以字母 c 开头。以下是标准 C++ 和 ANSI/ISO 标准 C++ 中最常用头文件的名称：

| 标准 C++ 头文件名称 | ANSI/ISO 标准 C++ 头文件名称 |
|---|---|
| `assert.h` | `cassert` |
| `ctype.h` | `cctype` |
| `float.h` | `cfloat` |
| `fstream.h` | `fstream` |
| `iomanip.h` | `iomanip` |
| `iostream.h` | `iostream` |
| `limits.h` | `climits` |
| `math.h` | `cmath` |
| `stdlib.h` | `cstdlib` |
| `string.h` | `cstring` |

要包含一个头文件，比如 `iostream`，需要以下语句：

```cpp
#include <iostream>
```

此外，要使用诸如 `cin`、`cout`、`endl` 等标识符，程序应使用以下语句之一：

```cpp
using namespace std;
```

或者在标识符前加上前缀 `std::`。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1590_0.png)

## 附录 F

## 头文件

C++ 标准库包含许多预定义函数、命名常量和专用数据类型。本附录讨论一些最常用的库例程（以及若干命名常量）。有关函数、命名常量等的更多说明和信息，请查阅系统文档。标准 C++ 头文件的名称显示在括号中。

### 头文件 `cassert` (`assert.h`)

下表描述函数 `assert`。其规范包含在头文件 `cassert` (`assert.h`) 中。

| 函数 | 描述 | 行为 |
|---|---|---|
| `assert(expression)` | `expression` 是任意 int 表达式；`expression` 通常是逻辑表达式 | - 如果 `expression` 的值非零（真），程序继续执行。<br>- 如果 `expression` 的值为 0（假），程序执行立即终止。会显示该表达式、包含源代码的文件名以及源代码中的行号。 |

> 要禁用所有 `assert` 语句，请将预处理指令 `#define NDEBUG` 放在指令 `#include <cassert>` 之前。

### 头文件 `cctype` (`ctype.h`)

下表显示了头文件 `cctype` (`ctype.h`) 中的各种函数。

| 函数名和参数 | 参数类型 | 函数返回值 |
|---|---|---|
| `isalnum(ch)` | `ch` 是一个 char 值 | 函数返回一个 `int` 值，如下所示：<br>• 如果 `ch` 是字母或数字字符，即（`'A'`–`'Z'`、`'a'`–`'z'`、`'0'`–`'9'`），则返回非零值（`true`）<br>• 否则返回 `0`（`false`） |
| `iscntrl(ch)` | `ch` 是一个 char 值 | 函数返回一个 `int` 值，如下所示：<br>• 如果 `ch` 是控制字符（在 ASCII 中，字符值为 0–31 或 127），则返回非零值（`true`）<br>• 否则返回 `0`（`false`） |
| `isdigit(ch)` | `ch` 是一个 char 值 | 函数返回一个 `int` 值，如下所示：<br>• 如果 `ch` 是数字（`'0'`–`'9'`），则返回非零值（`true`）<br>• 否则返回 `0`（`false`） |
| `islower(ch)` | `ch` 是一个 char 值 | 函数返回一个 `int` 值，如下所示：<br>• 如果 `ch` 是小写字母（`'a'`–`'z'`），则返回非零值（`true`）<br>• 否则返回 `0`（`false`） |
| `isprint(ch)` | `ch` 是一个 char 值 | 函数返回一个 `int` 值，如下所示：<br>• 如果 `ch` 是可打印字符，包括空白字符（在 ASCII 中，从 `' '` 到 `'~'`），则返回非零值（`true`）<br>• 否则返回 `0`（`false`） |
| `ispunct(ch)` | `ch` 是一个 char 值 | 函数返回一个 `int` 值，如下所示：<br>• 如果 `ch` 是标点字符，则返回非零值（`true`）<br>• 否则返回 `0`（`false`） |
| `isspace(ch)` | `ch` 是一个 char 值 | 函数返回一个 `int` 值，如下所示：<br>• 如果 `ch` 是空白字符（空格、换行、制表符、回车、换页），则返回非零值（`true`）<br>• 否则返回 `0`（`false`） |

