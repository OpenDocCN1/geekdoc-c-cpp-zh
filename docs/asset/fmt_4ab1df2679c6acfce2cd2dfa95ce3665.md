
`cout << numerator << "/" << denominator`

`<< " = " << numerator/denominator << endl;`

并执行修改后的程序。输入 12 和 5，并从用户的角度解释为什么结果是错误的。

- 4. (修改) 修改程序 9.1，使其抛出并捕获消息 "Invalid input - A denominator value of zero is not permitted"。（提示：回顾本节末尾的 `catch`。）
- 5. (练习) 输入并执行程序 9.2。
- 6. (修改) 修改程序 9.2，使其继续除以两个数，直到用户输入字符 `q`（作为分子或分母）来终止程序执行。

## 496 完成基础

- 7. (验证) 在程序 9.1 中包含本节提供的异常处理代码，以确保用户输入有效的整数值。

### 9.2 异常与文件检查

使用一个或多个文件的 C++ 程序广泛使用异常处理进行错误检测和处理。例如，在尝试打开文件进行处理之前，确保文件已打开。回顾第 9.1 节，通用异常处理的代码如下：

```cpp
try {

    // 一个或多个语句

    // 至少包含一个

// 抛出一个异常

} catch(exception dataTypeName){

    // 一个或多个语句

}
```

在这段代码中，`try` 块中的语句被执行。如果没有发生错误，则会跳过 `catch` 块。然而，如果 `try` 块中的任何语句抛出了异常，则会执行与该异常类型匹配的 `catch` 块。如果没有为 `try` 块定义 `catch` 块，则会导致编译器错误。如果不存在能捕获抛出类型的 `catch` 块，当异常抛出时，程序将会崩溃。大多数情况下，`catch` 块会显示错误消息并通过调用 `exit()` 终止处理。程序 9.3 显示了以读模式打开文件所需的语句，并包含了异常处理。

## 程序 9.3

```cpp
#include <iostream>

#include <fstream>

#include <cstdlib> // exit() 需要的

#include <string>

using namespace std;
```

![](img/023360499b401b1e52ce9fc94a17f42d_515_0.png)

## 第9章 497 异常与文件检查

```cpp
int main()
{
  string filename = "prices.dat"; // 将文件名放在前面
  string descrip;
  double price;

  ifstream inFile;

  try // 此块尝试打开文件、读取文件，
      // 并显示文件数据
  {
    inFile.open(filename.c_str());

    if (inFile.fail()) throw filename; //正在被检查的异常

    // 读取并显示文件内容
    inFile >> descrip >> price;
    while (inFile.good()) // 检查下一个字符
    {
      cout << descrip << ' ' << price << endl;
      inFile >> descrip >> price;
    }
    inFile.close();

    return 0;
  }
  catch (string e)
  {
    cout << "\nThe file " << e << " was not opened.";
    cout << "check that the file currently exists." << endl;
    exit(1);
  }
}
```

当未找到 `prices.dat` 文件时，程序 9.3 显示的消息为：

```
The file prices.dat was not opened.

Please check that the file currently exists.
```

## 完成基础

## 信息：检查文件是否成功打开

使用异常处理，检查文件是否打开的最常用方法是程序 9.3 中的代码。为了方便，这里重复了关键点：

异常处理是检查文件是否打开的方法。程序 9.3 中的代码可以用于输出，但在不需要覆盖现有文件时，通常需要更严格的检查。在这些情况下，如果文件存在，它可以打开；如果不存在，操作系统会创建一个（除非指定了追加模式）。程序 9.4 显示了如何进行这种检查。

## 程序 9.4

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib> // exit() 需要的
#include <string>
#include <iomanip>    // 格式化需要的
using namespace std;

int main()
{
    char response;
    string filename = "prices.dat"; // 将文件名放在前面
    ifstream inFile;
    ofstream outfile;
```

![](img/023360499b401b1e52ce9fc94a17f42d_517_0.png)

## 第9章 499 异常与文件检查

```cpp
try // 打开输入流以检查文件是否存在
(inFile.open(filename.c_str()));

if (inFile.fail()) throw 1; // 这意味着文件不存在
// 只有此处块才会接管控制
cout << "A file by name " << filename << " currently exists.\n"
<< "Do you want to overwrite it with the new data (y or n): ";
cin >> response;

if (tolower(response) == 'n')
{
    inFile.close();
    cout << "The existing file has not been overwritten." << endl;
    exit(1);
}

catch(int e) {}; // 一个空块，允许处理继续
```

```cpp
try
// 以写入模式打开文件并继续写入
outfile.open(filename.c_str());

if (outfile.fail()) throw filename;
// 设置输出流格式
outfile << setiosflags(ios::fixed<< showpoint)
<< setprecision(2);
// 将数据写入文件
```

```cpp
outfile << "Mats" << 39.95 << endl

<< "Bulbs" << 3.22 << endl

<< "Fuses" << 1.08 << endl;
```

```cpp
outfile.close();
cout << "The file " << filename
<< " has been successfully written." << endl;
return 0;
}
catch(string e)
{
cout << "The file " << filename
<< " was not opened for output and has not been written."
<< endl;
}
```

## 500 完成基础知识

在程序 9.4 中，`try` 块是独立的。由于 `catch` 块与最近的上一个 `try` 块关联，因此对于未匹配的 `try` 和 `catch` 块不存在歧义。

## 打开多个文件

为了理解如何将异常处理应用于同时打开两个文件，假设你想从一个名为 `info.txt` 的字符文件中读取数据（一次读取一个字符），并想将数据写入一个名为 `info.bak` 的文件。基本上，这个应用程序是一个文件复制程序，它以逐个字符的方式从一个文件读取数据，并将这些数据写入第二个文件。图 9.1 显示了输入文件中存储的字符。

现在是所有好人来伸援伙伴的时候了。请拨打 (555) 888-6666 获取更多信息。

**图 9.1** 存储在 `info.txt` 文件中的数据

图 9.2 展示了生成文件副本所需的流结构。在图中，由变量 `inputFile` 引用的输入流从 `info.txt` 文件读取数据，而由变量 `outFile` 引用的输出流将数据写入 `info.bak` 文件中。

现在查看程序 9.5，它使用图 9.2 中的过程创建 `info.bak` 文件作为 `info.txt` 文件的副本。

![](img/023360499b401b1e52ce9fc94a17f42d_519_0.png)

**图 9.2** 文件复制流结构

## 程序 9.5

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>    // 需要 exit()
#include <string>
using namespace std;
```

![](img/023360499b401b1e52ce9fc94a17f42d_519_1.png)

![](img/023360499b401b1e52ce9fc94a17f42d_519_2.png)

## 第 9 章 501 异常与文件检查

```cpp
int main()
{
    string fileOne = "info.txt"; // 将文件名放在前面
    string fileTwo = "info.bak";
    char ch;
    ifstream infile;
    ofstream outfile;

    try // 此块尝试打开输入文件
    {
        // 打开基础输入流
        infile.open(fileOne.c_str());
        if (infile.fail()) throw fileOne;
    } // 外部 try 块结束
    catch (string in) // 捕获外部 try 块的异常
    {
        cout << "输入文件 *" << in
             << " 未能成功打开。" << endl
             << " 未进行备份。" << endl;
        exit(1);
    }

    try // 此块尝试打开输出文件
    {
        // 执行所有文件处理
        outfile.open(fileTwo.c_str());

        if (outfile.fail()) throw fileTwo;

        while ((ch = infile.get()) != EOF)
            outfile.put(ch);

        infile.close();
        outfile.close();
    }
    catch (string out) // 捕获内部 try 块的异常
    {
        cout << "备份文件 *" << out
             << " 未能成功打开。" << endl;
        exit(1);
    }

    cout << "文件 *" << fileOne
         << 的成功备份文件 *" << fileTwo << " 已成功创建。" << endl;

    return 0;
}
```

## 502 完成基础知识

## 信息要点

### 嵌套 try 块

当涉及多个文件流时，每个文件流都在其自己的 `try` 块中，允许发生异常时隔离并确切识别是哪个文件导致了异常。`try` 块是可以嵌套的。例如，程序 9.5 已使用嵌套的 `try` 块重写。注意，内部 `try` 块的 `catch` 块必须嵌套在与 `try` 块相同的作用域内：

为了简单起见，程序 9.5 尝试在独立的且未匹配的 `try` 块中打开输入输出文件。此外，第二个文件是在嵌套的 `try` 块中打开的，因此如果打开第一个文件抛出异常，则不会尝试打开第二个文件。（信息要点框解释了如何嵌套 `try` 块）。

在检查程序 9.5 时，特别注意此语句：

```cpp
while (ch = inFile.get()) != EOF
```

该语句持续从输入流读取值，直到检测到 `EOF` 值。由于返回的值不等于 `EOF` 值，该值被写入输出流。表达式 `(ch = inFile.get())` 周围的括号是必要的，以确保在将检索的值与 `EOF` 比较之前先读取值并赋值给变量 `ch`；如果没有括号，复杂的表达式将是 `ch = inFile.get() != EOF`，该表达式的结果是 `inFile.get() != EOF`（一个布尔值）。

## 信息要点

嵌套 try 块

```cpp
try
{
    // 执行所有文件处理
    try
    {
        // 打开基础输入流
        infile.open(fileOne.c_str());
        if (infile.fail()) throw fileOne;

        while ((ch = infile.get()) != EOF)
            outfile.put(ch);

        infile.close();
    }
    catch (string in) // 捕获内部 try 块的异常
    {
        cout << "输入文件 *" << in
             << " 未能成功打开。" << endl;
             << " 未进行备份。" << endl;
        exit(1);
    }

    // 打开输出文件
    outfile.open(fileTwo.c_str());
    if (outfile.fail()) throw fileTwo;

    outfile.close();
    }
    catch (string out) // 捕获外部 try 块的异常
    {
        cout << "备份文件 *" << out
             << " 未能成功打开。" << endl;
        exit(1);
    }

    cout << "文件 *" << fileOne
         << 的成功备份文件 *" << fileTwo << " 已成功创建。" << endl;
```

*(注：原文中的 `while` 语句 `while (ch = inFile.get()) != EOF` 存在逻辑错误，缺少括号，应为 `while ((ch = inFile.get()) != EOF)`，翻译时保留了代码逻辑结构)*

### 9.3 字符串类

- `string` 类是用户自定义的类型类型。
- `string` 类的成员被称为字符串字面量。
- `string` 类的变量被称为对象。

## 练习 9.2

- 1. 回复习：列出在输入模式下导致失败的条件。
- 2. 回复习：列出在输出模式下导致失败的条件。
- 3. 回复习：如果字符串在写入模式下打开，会发生什么？![](img/023360499b401b1e52ce9fc94a17f42d_522_png)

## 504 完成基础知识

- 4. 修改：修改程序 9.3，使用你自己的标识符代替 `e`。
- 5. 练习：输入并运行 9.4。
- 6. 调试：确定为什么 9.4 中未嵌套的块不会产生问题。（提示：见第 节。）
- 7. 调试：a. 为什么 7a 中的块被拆分为独立的块后，程序无法编译？b. 7a 需要哪些额外的更改才能允许编译？（提示：见第 6 节。）

### 9.3 字符串类

书中的程序已经广泛使用了 `cout` 对象，但你还没有详细研究这个类，也没有学习 `cout` 是如何构造的。然而，面向对象设计的优势在于，你可以在不知道类如何构造的情况下充分使用它。你使用 C++ 标准库提供的任何类：字符串类。

类是用户自定义的数据类型。与内置类型一样，类定义了一组有效的数据值以及对这些值执行的操作。区别在于内置类型作为编译器的组成部分创建，而类是由程序员使用 C++ 代码构造的。除此之外，这两种数据类型的使用方式非常相似。术语上的区别在于：对于变量，为类定义的存储区域被称为对象。

字符串类的成员被称为字符串字面量。字符串字面量也被称为字符串值、常量，以及更多习惯名称。字符串的示例有 "This is a string"、Hello World!" 和 "xyz 123 *##&"。引号表示字符串的起始和结束点，但本身并不与字符串一起存储。

9.3 显示了当 Hello 作为类对象创建时的程序表示表示。按照惯例，字符串中的第一个字符总是被指定为位置 0。这个位置值也被称为字符的值和它的偏移值。

| | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| 位置: | H | e | l | l | o |

图 9.3 字符序列的存储

## string 类函数

`string` 类提供了许多用于声明、创建和初始化字符串的函数。在 C++ 的早期版本中，创建新对象的过程被称为实例化一个对象（instantiating an object），在这种情况下，这意味着实例化一个字符串对象，或者说，创建一个字符串。表 9.2 列出了用于创建和初始化对象的 `string` 类函数。在类术语中，这些被正式称为方法（methods），而执行创建和初始化任务的方法称为构造函数（constructors），或析构函数（destructors）。

表 9.2 `string` 类构造函数（需要头文件 `string`）

| 构造函数 | 描述 | 示例 |
| --- | --- | --- |
