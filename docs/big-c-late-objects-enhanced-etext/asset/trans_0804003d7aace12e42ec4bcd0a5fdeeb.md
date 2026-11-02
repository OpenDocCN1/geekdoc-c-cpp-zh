
![](img/d61019b035dd82beb581604273c0ee6b_422_0.png)

## 练习示例 7.1
### 生产批量邮件
### 问题陈述

我们希望自动化批量邮件的生产过程。

一封典型的信件可能如下所示：

```
To: Ms. Sally Smith
123 Main Street
Anytown, NY 12345

Dear Ms. Smith:

The Smith family may be the lucky winner in the C++ sweepstakes.
Wouldn't it be exciting if you were the first Anytown residents
to use ACME's new C++ development environment? etc. etc.
```

另一封使用相同模板但变量部分的值不同的信件如下所示：

```
To: Mr. Harry Morgan
456 Park Ave
Everyville, KS 67890

Dear Mr. Morgan:

The Morgan family may be the lucky winner in the C++ sweepstakes.
Wouldn't it be exciting if you were the first Everyville residents
to use ACME's new C++ development environment? etc. etc.
```

要设置此类邮件，我们从一个模板字符串开始，其中每个变量部分都用数字 0 ... 9 表示。 （我们假设数字在模板文本中没有其他用途。）

```
To: 0 1 2
3
4, 5 6

Dear 0 2:

The 2 family may be the lucky winner in the C++ sweepstakes.
Wouldn't it be exciting if you were the first 4 residents
to use ACME's new C++ development environment? etc. etc.
```

此模板设置在一个字符串中，如下所示：

```
char letter_template[] = "To: 0 1 2\n3\n4, 5 6\n\nDear 0 2: \n\n"
"The 2 family may be the lucky winner in the C++ sweepstakes.\n"
"Wouldn't it be exciting if you were the first 4 residents\n"
"to use ACME's new C++ development environment? etc. etc.\n\n";
```

（要在 C++ 中声明不适合单行的字面量字符串，您可以编写一系列字面量字符串。编译器将它们合并为一个字符串。）

当然，我们可以通过用特定收件人的值替换数字来为每次邮寄生成单独的字符串。但有一种更有效的方法。您的任务是设置一个字符指针向量，该向量指向信件的连续片段，这些片段来自模板字符串或变量部分。例如，上文信件的正文由指向以下字符串的指针表示：

- ": \n\nThe "
- Variable 2
- " family may be . . . were the first "

### 第 2 步 声明指针变量。

我们收集长度未知的 char* 指针序列。因此，我们使用指针向量：

```
vector<char*> fragments;
```

### 第 3 步 使用变量地址或自由存储内存初始化指针。

这是 prepare_mailing 函数的任务。该函数需要扫描信件模板中的变量指示符，用空终止符替换它们，并在 fragments 向量中存储指针。以下是伪代码：

- 将片段起始位置设为信件模板的开头。
- 对信件模板中的每个字符
  - 如果该字符是数字
    - 将片段起始位置添加到 fragments 向量中。
    - 将数字所表示的变量的行添加到 fragments 向量中。
    - 用空终止符替换该数字。
  - 将片段起始位置设为下一个字符。

您将在下面的代码列表中找到 C++ 代码。

### 第 4 步 使用 * 或 [] 运算符访问您的数据。

此步骤已在问题陈述中完成。要求 fragments 可以通过以下循环打印：

```
for (int i = 0; i < fragments.size(); i++)
{
    cout << fragments[i];
}
```

剩下的就是完成一个主程序，该程序打印两封信，如代码列表所示。请注意，prepare_mailing 函数只调用一次。此后，变量数组会为每次邮寄进行更新，但 fragments 向量永远不会改变。

以下是完整程序：

### worked_example_1/mail.cpp

```
#include <cctype>
#include <iostream>
#include <string>
#include <vector>

using namespace std;

const int VAR_LENGTH = 20;

/**
 * Prepares a letter template for a mass mailing.
 * @param letter a string with placeholders 0 ... 9 (which will be replaced
 * with null terminators)
 * @param vars a two-dimensional array for holding the variable parts of the letter
 * @return a vector of fragments, pointing alternately to strings in the letter
 * template and in the variable array
 */
vector<char*> prepare_mailing(char* letter, char vars[][VAR_LENGTH])
{
    vector<char*> fragments;
    char* fragment_start = letter;
    for (char* p = letter; *p != '\0'; p++)
    {
        if (isdigit(*p))
        {
            fragments.push_back(fragment_start);
            fragment_start = p + 1;
            int var_index = *p - '0';
            fragments.push_back(vars[var_index]);
            *p = '\0';
        }
    }
    fragments.push_back(fragment_start);
    return fragments;
}

int main()
{
    char variable_parts[10][VAR_LENGTH];

    strcpy(variable_parts[0], "Ms.");
    strcpy(variable_parts[1], "Sally");
    strcpy(variable_parts[2], "Smith");
    strcpy(variable_parts[3], "123 Main Street");
    strcpy(variable_parts[4], "Anytown");
    strcpy(variable_parts[5], "NY");
    strcpy(variable_parts[6], "12345");

    char letter_template[] = "To: 0 1 2\n3\n4, 5 6\n\nDear 0 2: \n\n"
    "The 2 family may be the lucky winner in the C++ sweepstakes.\n"
    "Wouldn't it be exciting if you were the first 4 residents\n"
    "to use ACME's new C++ development environment? etc. etc. \n\n\n";

    vector<char*> fragments = prepare_mailing(letter_template, variable_parts);

    for (int i = 0; i < fragments.size(); i++)
    {
        cout << fragments[i];
    }

    strcpy(variable_parts[0], "Mr.");
    strcpy(variable_parts[1], "Harry");
    strcpy(variable_parts[2], "Morgan");
    strcpy(variable_parts[3], "456 Park Ave");
    strcpy(variable_parts[4], "Everyville");
    strcpy(variable_parts[5], "KS");
    strcpy(variable_parts[6], "67890");

    for (int i = 0; i < fragments.size(); i++)
    {
        cout << fragments[i];
    }

    return 0;
}
```

## 第 8 章
### 流

![](img/d61019b035dd82beb581604273c0ee6b_426_0.png)

### 章节目标

- 能够读写文件
- 使用字符串流在字符串和数字之间转换
- 处理命令行参数
- 理解顺序访问和随机访问的概念

### 章节内容

- **8.1 读取和写入文本文件** 260
  - SYN 使用文件流 262
- **8.2 读取文本输入** 265
  - C&I 混合 >> 和 getline 输入 268
  - ST1 流失败检查 269
- **8.3 写入文本输出** 270
  - ST2 Unicode、UTF-8 和 C++ 字符串 272
- **8.4 解析和格式化字符串** 273

- **8.5 命令行参数** 274
  - C&S 加密算法 277
  - HT1 处理文本文件 278
  - WE1 查找重复项 281
- **8.6 随机访问和二进制文件** 283
  - C&S 数据库和隐私 286

![](img/d61019b035dd82beb581604273c0ee6b_427_0.png)

本章中，您将学习如何使用 C++ 流库读写文件——这对于处理现实世界数据非常有用。作为一个应用，您将学习如何加密数据。 （照片中显示的 Enigma 机器是德国在第二次世界大战中使用的加密设备。开创性的英国计算机科学家破解了密码并能够截获编码消息，这在赢得战争中起到了重要帮助。）本章后面，您将学习如何处理二进制文件，例如存储图像数据的文件。

### 8.1 读取和写入文本文件

C++ 输入/输出库基于流的概念。输入流是数据的来源，输出流是数据的目的地。数据的最常见来源和目的地是硬盘上的文件。

要读写文件，您使用类型为 fstream、ifstream 或 ofstream 的变量。

要访问文件，您使用文件流。有三种类型的文件流：ifstream（用于输入）、ofstream（用于输出）和 fstream（用于输入和输出）。使用这些文件流中的任何一个时，请包含 <fstream> 头文件。

在以下各节中，您将学习如何处理文件中的数据。文件处理在许多学科中都是一项非常有用的技能，因为分析存储在文件中的大型数据集的情况非常普遍。

![](img/d61019b035dd82beb581604273c0ee6b_427_1.png)

© nullplus/iStockphoto.

数据进入输入流的方式就像传送带上的物品一样，一次一个。

### 8.1.1 打开流

打开文件流时，您提供存储在磁盘上的文件名称。

要从文件流读取任何内容，您需要打开它。打开流时，您给出存储在磁盘上的文件名称。假设您想从与程序位于同一目录中的名为 input.dat 的文件读取数据。那么您可以使用以下函数调用打开文件：

```
in_file.open("input.dat");
```

此语句将变量 in_file 与名为 input.dat 的文件关联起来。请注意，所有流都是对象，您使用点表示法调用操作它们的函数。要打开文件进行写入，您使用 ofstream 变量。要同时打开同一文件进行读写，您使用 fstream 变量。文件名可以包含目录路径信息，例如 ~/homework/input.dat（UNIX）c:\homework\input.dat（Windows）

