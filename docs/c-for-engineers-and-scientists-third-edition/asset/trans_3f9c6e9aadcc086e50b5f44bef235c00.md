

## 第 9 章 499

异常与文件检查

```cpp
try // 简单打开一个基础输入流以检查文件是否存在
{
    infile.open(filename.c_str());
}
```

```cpp
if (inFile.fail()) throw 1; // 这意味着文件不存在
// 只有到达这里代码块才会接管控制权
cout << "名为 " << filename << " 的当前存在。\n"
     << "你确定要用新数据覆盖它吗 (y 或 n): ";
cin >> response;

if (tolower(response) == 'n')
{
    infile.close();
    cout << "现有文件未被覆盖。" << endl;
    exit(0);
}
```

```cpp
catch(int e) {}; // 一个什么都不做的块，允许
// 程序继续执行
```

```cpp
try
{
    // 以写入模式打开文件并继续写入文件
    outfile.open(filename.c_str());

    if (outfile.fail()) throw filename;
    // 设置输出文件流格式
    outfile << setiosflags(ios::fixed << ios::showpoint)
            << setprecision(2);
    // 将数据写入文件
    outfile << "Mats" << 39.95 << endl
            << "Bulbs" << 3.22 << endl
            << "Fuses" << 1.08 << endl;
    outfile.close();
    cout << "文件 " << filename << "已成功写入。" << endl;
    return 0;
}
catch(string e)
{
    cout << "文件 " << filename << " 未能打开输出且未写入。" 
         << endl;
}
```

500 完成基础知识

在程序 9.4 中，`try` 块是独立的。因为 `catch` 块与最近的前一个 `try` 块关联，所以未匹配的 `try` 和 `catch` 块不存在歧义。

## 打开多个文件

为了理解如何将异常处理应用于同时打开两个文件，假设你想要从一个名为 info.txt 的字符文件中读取数据（一次一个字符），并将这些数据写入一个名为 info.bak 的文件中。本质上，这个应用程序是一个文件复制程序，它以字符逐个的方式从一个文件读取数据，并将数据写入第二个文件。图 9.1 显示了输入文件中存储的字符。

现在是所有好人伸出援手的时候。
请拨打 (555) 888-6666 获取更多信息。

**图 9.1** 存储在 info.txt 文件中的数据

图 9.2 展示了生成文件副本所需的流结构。图中，由变量 `inFile` 引用的输入流对象从 info.txt 文件读取数据，由变量 `outFile` 引用的输出流对象将数据写入 info.bak 文件。

现在查看程序 9.5，它使用图 9.2 所示的步骤创建 info.bak 文件作为 info.txt 文件的副本。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_519_0.png)

**图 9.2** 文件复制流结构

## 程序 9.5

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>    // exit() 需要此头文件
#include <string>
using namespace std;
```

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
    catch (string in) // 针对外部 try 块的 catch
    {
        cout << "输入文件 " 未能成功打开。" << endl
             << "未进行备份。" << endl;
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
    catch (string out) // 针对内部 try 块的 catch
    {
        cout << "备份文件 " 未能成功打开。" << endl;
        exit(1);
    }

    cout << "名为 " << fileTwo << " 的 " << fileOne << 备份已成功完成。" << endl;

    return 0;
}
```

502 完成基础知识

## 知识点

## 嵌套 try 块

当涉及多个文件流时，在各自的 `try` 块中打开每个文件流，可以在发生异常时隔离并确确定位是哪一个文件导致了异常。`try` 块可以嵌套。例如，程序 9.5 已经使用嵌套的 `try` 块进行了重写。注意，内部 `try` 块的代码块必须嵌套在与 `try` 块相同的块作用域内：

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib> // exit() 需要此头文件
#include <string>
using namespace std;

int main() {
    string fileOne = "info.txt"; // 将文件名放在前面
    string fileTwo = "info.bak";
    char ch;
    ifstream inFile;
    ofstream outfile;

    try // 此块尝试打开输入文件
    {
        inFile.open(fileOne.c_str());
        if (inFile.fail()) throw fileOne;
        try // 此块尝试打开输出文件并

继续...
```

为了简单起见，程序 9.5 尝试在分开且未设置的 `try` 块中打开输入输出文件。更通用地说，第二个文件是在嵌套内部 `try` 块中打开的，因此如果第一个文件抛出异常，则不会尝试打开第二个文件（知识点，解释了如何嵌套代码块）。

在复程序 9.5 时，请特别注意此语句：

```cpp
while (ch = inFile.get()) != EOF
```

该语句从输入流中读取值直到遇到 EOF。`(ch = inFile.get())` 外围的括号是必要的，因为返回值会被赋值给变量。

## 知识点

嵌套 try 块（续）

```cpp
try
{
    // 执行所有文件处理
    outfile.open(fileTwo.c_str());

    if (outfile.fail()) throw fileTwo;

    while ((ch = inFile.get()) != EOF)
        outfile.put(ch);

    infile.close();
    outfile.close();
}
catch (string out) // 针对内部 try 块的 catch
{
    cout << "备份文件 " 未能成功打开。" << endl;
    exit(1);
}
```

```cpp
catch (string in) // 针对外部 try 块的 catch
{
    cout << "输入文件 " 未能成功打开。" << endl
         << "未进行备份。" << endl;
    exit(1);
}
```

```cpp
cout << "名为 " << fileTwo << " 的 " << fileOne << "备份已成功完成。" << endl;
```

## 练习 9.2

1. （复习）列出两种导致以输入模式打开文件时失败的条件。
2. （复习）列出两种导致以输出模式打开文件时失败的条件。
3. （复习）如果以写入模式打开文件，会发生什么？
4. （修改）修改 9.3，使用你选择的标识符代替字母 `e`。
5. （练习）输入执行 9.4。
6. （调试）确定为什么 9.4 中未嵌套的两个 try 块没有产生问题。（提示：将声明放在第一个块中。）
7. （调试）a. 如果将嵌套块分开为非嵌套块，程序将无法编译。确定原因。b. 7a 中的程序需要进行哪些更改才能允许非嵌套编写？提示：见第 6。）

## 9.3 String 类

书中的程序大量使用了 `istream` 对象，但你还没有详细研究该类，也没有学习它是如何构造的。然而，对象设计的优势在于你可以在不了解类如何构造的情况下彻底使用类。你可以使用 C++ 标准库定义的任何类：string 类。

类是用户创建的数据类型。与内置数据类型一样，类定义了一组有效的数据值以及对这些值执行的操作。作为编译器组成部分的用户创建数据类型与程序员使用 C++ 代码构造的类之间的区别在于除了这一点和术语外，两种数据类型的使用方式非常相似。区别在于，内置数据类型的存储被称为变量，而类的存储区域被称为对象。

类允许的值被称为字符串字面量。字符串字面量也被称为字符串值、常量，更通俗地称为字符串。字符串的示例包括 "This is a string" "Hello World" "xyz 123 #&*" 引号表示字符串的开始和结束并不随字符串一起。

9.3 显示了字符串 Hello 作为 string 类对象创建时的程序表示。按照惯例，字符串中的第一个字符始终被指定为位置 0。这个位置值既是字符的值也是它的偏移值。

| 位置: | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| | H | e | l | l | o |

图 9.3 作为字符序列存储的字符串

