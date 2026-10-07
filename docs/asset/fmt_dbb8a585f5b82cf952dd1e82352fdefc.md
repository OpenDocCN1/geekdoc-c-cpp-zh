
$r$ 是距离坐标，$\theta$ 是 `polar.dat` 文件中角度坐标的弧度值。

### 4. （数据处理）
a. 编写一个 `C++` 程序来创建一个包含以下信息的数据文件，或者使用本书网站提供的 `grades.dat` 文件。

| 学生学号 | 学生姓名 | 课程代码 | 课程学分 | 课程成绩 |
| :--- | :--- | :--- | :--- | :--- |
| 2333021 | BOKOW, R. | NS201 | 3 | A |
| 2333021 | BOKOW, R. | MG342 | 3 | A |
| 2333021 | BOKOW, R. | FA302 | 1 | A |
| 2574063 | FALLIN, D. | MK106 | 3 | C |
| 2574063 | FALLIN, D. | MA208 | 3 | B |
| 2574063 | FALLIN, D. | CM201 | 3 | C |
| 2574063 | FALLIN, D. | CP101 | 2 | B |
| 2663628 | KINGSLEY, M. | QA140 | 3 | A |
| 2663628 | KINGSLEY, M. | CM245 | 3 | B |
| 2663628 | KINGSLEY, M. | EQ251 | 3 | A |
| 2663628 | KINGSLEY, M. | MK341 | 3 | A |
| 2663628 | KINGSLEY, M. | CP101 | 2 | B |

b. 使用练习 4a 中创建的文件，编写一个 `C++` 程序生成学生成绩单。每个学生的成绩单应包含学生的姓名和学号、课程列表、每门课程的成绩以及学期平均绩点（GPA）。例如，这是第一个学生的成绩单：

学生姓名：BOKOW, R.
学生学号：2333021

| 课程代码 | 课程学分 | 课程成绩 |
| :--- | :--- | :--- |
| NS201 | 3 | A |
| MG342 | 3 | A |
| FA302 | 1 | A |

本学期已修完总学分：7
学期 GPA：4.0

GPA 的计算分为两个步骤。首先，为每门课程的成绩分配一个值（A = 4, B = 3, C = 2, D = 1, F = 0），并计算这些成绩的和。计算每门课程的学分。将此总和除以该学期修读的总学分数。

+. 5. （文件更新）a. 编写一个 `C++` 程序创建一个包含以下信息的数据文件，或者使用本书网站提供的 `gradeUpdate.dat` 文件。

| 学生学号 | 学生姓名 | 课程学分 | 课程 GPA |
| :--- | :--- | :--- | :--- |
| 2333021 | BOKOW, R. | 48 | 4.0 |
| 2574063 | FALLIN, D. | 12 | 1.8 |
| 2663628 | KINGSLEY, M. | 36 | 3.5 |

b. 编写一个 `C++` 程序，使用练习 4a 中创建的数据更新练习 5a 中的文件。

## 8.6 深入观察：iostream 类库

正如你所看到的，`iostream` 类库中的类通过被称为“流”的实体进行访问。对于大多数情况，流上传输的字节数据代表 ASCII 字符或二进制数。从文件读取字节流或向文件写入字节流的机制已使用 `C++` 等高级语言隐藏起来。尽管如此，了解这一机制是有用的，以便你可以将 `iostream` 类提供的服务置于上下文中。

### 文件传输机制

图 8.5 展示了程序与文件之间传输数据的机制。所示，这涉及计算机内存中的一个中间文件缓冲区（file buffer）。每个打开的文件都会分配其自己的文件缓冲区，它是一个用于在程序和文件之间传输数据的存储区域。

![](img/d5a225ca53b347501e86d72212077531_522_0.png)

图 8.5 数据传输机制

> 第一次阅读时可以跳过此主题，而不会影响后续阅读的连贯性。

所有所有 (C) 2012 Cengage Learning. 保留所有权利。未经许可，不得复制、存储或分发部分……某些第三方内容。

# 第 8 章
### 501

### 深入观察：iostream 类库

## I/O 流与数据文件

`iostream` 类库提供了一组用于输入输出操作的类。这些类中最重要的类是 `iostream`，它是所有输入输出流的基类。其他重要的类是 `istream`（用于输入）和 `ostream`（用于输出）。

`iostream` 库还提供了几个用于格式化输出的实用函数，例如 `setw`、`set` 和 `fixed`。这些函数可以控制数据在打印到屏幕或写入文件时的外观。

# 504 I/O 流与数据文件

# 程序 8.11

```cpp
#include <iostream>
#include <sstream>
#include <iomanip>
using namespace std;
int main() {
    const int MAXCHARS = 81; // 比行最大字符数多一个
    int units = 10;
    double price = 36.85;
    char buf[MAXCHARS];
    stringstream inem(buf, MAXCHARS, ios::out); // 打开内存流
    // 通过流写入缓冲区
    inem << "No. of units = "
         << setw(3) << units
         << " Price per unit = $"
         << setw(6) << setprecision(2) << fixed << price << ' \0';
    cout << "|" << buf << "|";
    cout << endl;
    return 0;
}
```

程序 8.11 产生以下输出：
|No. of units = 10 Price per unit = $ 36.85|

此输出说明字符缓冲区已经通过向 `inem` 流插入数据正确填充。（注意字符串末尾的 NULL 字符 `'\0` 是向流的最后一次插入，它被记录以正确结束 C 字符串。）在字符数组填充后，它被写入单个文件中。

以简单的方法，`stringstream` 可以以输入模式打开。该流可以用作工作存储或缓冲区，用于存储来自文件或标准输入的完整文本列表。缓冲区填充后，可以使用提取器运算符将字符串“拆分”成部分，并将每条数据转换为其指定的数据类型。这样做允许在将项目分配给其相应变量后，按行从文件输入数据。

# 第 8 章

# 505

本章总结

## 8.7 常见编程错误

与文件的常见编程错误如下：

- 在尝试从读取或写入文件之前忘记打开文件。
- 在访问文件时，使用文件的外部名称代替内部流对象名称。唯一使用数据文件外部名称的流函数是 `open()`。一如既往，本章讨论的所有流函数必须以前跟一个流对象并跟一个点（点运算符）。
- 以输出模式打开文件时，没有先检查是否存在同名文件，且你没有检查已存在的文件名，导致文件被覆盖。
- 不理解文件结束是在读取或跳过 EOF（文件结束）标记后才检测到的。
- 尝试使用字符变量作为 EOF 标记来检测文件结束。对于用于接受 EOF 的任何变量，如果 `ch` 声明为字符变量，以下表达式将产生无限循环：

```cpp
while ((ch = in.file.peek()) != EOF)
```

出现这个问题的原因是字符永远无法赋予 EOF 代码。EOF 是一个整数值（通常为 -1），它没有字符表示，这确保了 EOF 代码不会与文件中作为正常数据遇到的合法字符混淆。要终止由前述表达式创建的循环，变量 `ch` 必须声明为整数变量。
- 在 `seek()` 和 `seekg()` 函数中使用整数偏移量。该偏移量可能是一个长整数常量或变量。传递给这些函数的任何其他值都产生不可预测的结果。

## 8.8 本章总结

- 文件是存储在共同名称下的、存储在外部存储介质的数据集合。
- 数据文件通过 `fstream::open()` 函数连接到文件流，该函数将文件的外部名称与内部对象连接起来。文件打开后，所有对文件的后续访问都需要内部对象名称。
- 文件可以以输入或输出模式打开。打开的输出文件流创建一个新的数据文件或擦除已打开文件中的数据。如果文件不存在则会产生错误条件，可以使用 `fail()` 检测。

> ³这种无限循环在 UNIX 系统上不会发生，因为在那里字符是以整数形式存储的。

Copyright 2012 Cengage Learning. All Rights Reserved. 未经出版社书面许可，不得以任何形式或通过任何手段复制、存储或传输。除非另有说明，电子书或章节可能会抑制第三方内容。编辑已确定，任何被抑制的内容对整体没有实质性影响，并保留在后续限制需要时随时恢复额外内容的权利。

WOW! eBook

WWW.www.cengage.com

# I/O 流与数据文件

- 所有文件流必须声明为 `ifstream` 或 `ofstream` 类的对象。因此，必须包含与以下任一类似的声明：
```cpp
ifstream inFile;
ofstream outFile;
```
- 除外，标准流对象 `cin`、`cout` 和 `cerr` 也用于输入。
- 使用 `seek()`、`seekg()`、`tell()` 和 `tellp()` 随机访问数据文件。这些函数的 `g` 版本用于输入，`p` 版本用于输出。
- 这些函数的 `g` 版本用于输入，`p` 版本用于输出。

# 表 8.6 文件操作

| 函数名称 | 说明 |
|---|---|
| get() | 从输入提取下一个字符。 |
| get(char charVar) | 从输入流中提取下一个字符并赋值给 `charVar`。 |
| getline(stringObj, termChar) | 提取字符串直到遇到终止字符。如果省略，默认是换行符。 |
| peek() | 返回输入流中的下一个字符而不提取它。 |
| put(char charExp) | 将 `charExp` 指定字符推入流。 |
| putback(char charExp) | 将 `charExp` 指定字符推入输入流。 |
| ignore(int n) | 跳过后续 *n* 个字符；如果省略 *n*，默认跳过下一个字符。 |
| eof() | 如果尝试读取文件末尾，则返回布尔真；否则返回布尔假。 |
| good() | 当文件可供程序使用时返回布尔真。如果尝试读取文件末尾，则返回布尔假。 |
| bad() | 如果在读取或写入流时发生导致数据丢失的错误，返回布尔真；否则返回布尔假。 |
| fail() | 如果文件未成功打开，则返回布尔真；否则返回布尔假。 |

# 第8章编程项目

**1. (数据处理)** a. 创建一个包含以下数据的文本（不包含标题），或使用在该网站提供的 `pay.dat` 文件。

| 姓名 | 费率 | 小时 |
|---|---|---|
| Callaway, G. | 16.00 | 40 |
| Hanson, P. | 15.00 | 48 |
| Lasard, D. | 16.50 | 35 |
| Stillman, W. | 18.00 | 50 |

**b.** 写一个 `C++` 程序，利用练习 1a 中创建的文件信息，为每位员工生成以下报告：

姓名 工资费率 常规工资 加班费 总工资

...

## 第 9 章
## 异常处理

表 9.1 异常处理术语

| 术语 | 说明 |
| --- | --- |
| 异常 (Exception) | 用于识别程序运行期间发生的特定错误的值、变量或对象 |
| 抛出异常 (Throw an exception) | 将异常发送到能够捕获检测到的错误的代码中 |
| 捕获或处理异常 (Catch or handle an exception) | 接收被抛出的异常并对其进行处理 |
|  catch 句 (Catch clause) | 处理错误的代码段 |
| 异常处理器 (Exception handler) | 抛出和捕获异常的代码 |

抛出和捕获异常所需的代码通用语法如下：

```
try {
  // 一个或多个语句，其中至少有一个语句
  // 应该能够抛出异常
}
catch(exceptionDataType parameterName) {
  // 一个或多个语句
}
```

此示例使用了两个新关键字：`try` 和 `catch`。`try` 关键字标识异常处理代码块的开始。该代码块大括号内部至少有一条语句能够抛出异常。例如，查看以下代码部分的 `try` 块：

```
try {
  cout << "Enter the numerator (whole numbers only):";
  cin >> numerator;
  cout << "Enter the denominator (whole numbers only):";
  cin >> denominator;
  result = numerator/denominator;
}
```

`try` 块包含五条语句，其中三条可能会导致需要捕获的错误。在编写专业程序时，请确保对两个提示都输入了有效整数，并且输入的第二个值为 0。对于此示例，你只需检查第二个输入的值是否为 0。

## 514 完成基础知识

在这种情况下，这是一个 0 值，会发生。”要检查第二个值是否不为 0，你需要在 `try` 块中添加一个 `throw` 语句，如下：

```
try
{
    cout << "Enter the numerator: (whole number only): ";
    cin >> numerator;
    cout << "Enter the denominator: (whole number only): ";
    cin >> denominator;
    if (denominator == 0)
        throw denominator;
}
else
    result = numerator/denominator;
```

在这个 `try` 块中，抛出的是一个整数值。也可以使用字符串字面量、变量或对象，但任何单个语句只能抛出这些项目中的一个。`try` 块中的前四条语句不一定包含在代码中；这样做可以将所有相关的语句保持在一起，从而便于在同一个 `try` 块中添加 `throw` 语句，以确保两个输入值都是整数。

一个代码块后面必须紧跟一个或多个 `catch` 块，这些块用作 `try` 块中语句抛出的任何异常的异常处理器。以下是一个处理抛出的异常（一个整数）的 `catch` 块：

```
catch(int e)
{
    cout << "A denominator value of " << e << " is invalid." << endl;
    exit(1);
}
```

该 `catch` 块的异常处理是一个输出语句，它识别被捕获的异常并终止程序执行。注意关键字后的括号。括号内部是所抛出的异常的数据类型和用于接收异常的参数名。该参数是程序员选择的标识符（但习惯上使用字母 `e` 表示 exception），用于在抛出异常时保存异常值。

可以使用多个 `catch` 块，只要每个 `catch` 捕获唯一的数据类型。唯一的要求是为每个 `try` 块至少提供一个 `catch` 块。同一个 `try` 块能捕获越多的异常越好。程序 9.1 是一个完整的程序，包含一个 `try` 块和一个 `catch` 块，用于检测除零错误。

![](img/d5a225ca53b347501e86d72212077531_535_0.png)

## 第 9 章
## 515 异常处理

## 程序 9.1

```cpp
#include <iostream>
using namespace std;
int main()
{
    int numerator, denominator;
    try {
        cout << "Enter the numerator (whole number only): ";
        cin >> numerator;
        cout << "Enter the denominator (whole number only): ";
        cin >> denominator;
        if (denominator == 0)
            throw denominator; // 抛出一个整数值
        else
            cout << "/ = " << (double)(numerator)/double(denominator) << endl;
    }
    catch(int e) {
        cout << "A denominator value of " << e << " is invalid." << endl;
        exit(1);
    }
    return 0;
}
```
