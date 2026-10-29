

# 程序 9.7

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>
using namespace std;

int main()
{
    string filename = "test.dat";
    char ch;
    long offset, last;

    ifstream inFile(filename.c_str());

    if (inFile.fail())    // 检查是否成功打开
    {
        cout << "\n文件未能成功打开"
             << "\n 请检查该文件当前是否存在"
             << endl;
        exit(1);
    }

    inFile.seekg(0L, ios::end);   // 移动到文件末尾
    last = inFile.tellg();        // 保存最后一个字符的偏移量

    for(offset = 1L; offset <= last; offset++)
    {
        inFile.seekg(-offset, ios::end);
        ch = inFile.get();
        cout << ch << " ";
    }

    inFile.close();

    cout << endl;

    return 0;
}
```

假设 `test.dat` 文件包含以下字符：

The grade was 92.5

程序 9.7 的输出如下：

```
5 : . : 2 : 9 :   : s : a : w :   : e : d : a : r : g :   : e : h : T :
```

程序 9.7 首先定位到文件中的最后一个字符。该字符（即 EOF 字符）的偏移量保存在变量 `last` 中。由于 `tellg()` 返回一个长整型值，因此 `last` 被声明为长整型。

从文件末尾开始，使用 `seekg()` 定位下一个要读取的字符，该定位以文件末尾为参照。每读取一个字符，就将其显示出来，并调整偏移量以访问下一个字符。使用的第一个偏移量是 -1，它表示紧邻 EOF 标记之前的那个字符。

## 练习 9.3

+   1.（实践）a. 创建一个名为 test.dat 的文件，其中包含程序 9.7 中所使用的 test.dat 文件的数据。（你可以使用文本编辑器，或从本书网站复制 test.dat 文件。）b. 在你的计算机上输入并运行程序 9.7。
+   2.（修改）重写程序 9.7，使 for 循环中使用的 `seekg()` 方法的参照点改为文件开头，而不是文件末尾。
+   3.（修改）修改程序 9.7，如果 `seekg()` 尝试引用的位置超出文件末尾，则显示一条错误消息。
+   4.（实践）编写一个程序，读取并显示名为 test.dat 的文件中每隔一个的字符。
+   5.（实践）使用 `seek()` 和 `tell()` 方法，编写一个名为 `fileChars()` 的函数，该函数返回文件中的字符总数。
+   6.（实践）a. 编写一个名为 `readBytes()` 的函数，该函数从文件中的任意位置开始读取并显示 n 个字符。该函数应接受三个参数：文件对象名、要读取的第一个字符的偏移量以及要读取的字符数。（注意：`readBytes()` 的原型应为 `void readBytes(fstreams, long, int)`。）b. 修改练习 6a 中编写的 `readBytes()` 函数，将读取的字符存储到字符串或数组中。该函数应接受存储地址作为第四个参数。

## 9.4 文件流作为函数参数

文件流对象可以用作函数参数。唯一的要求是函数的形参必须是对正确流的引用（参见第 6.3 节）：`ifstream&` 或 `ofstream&`。例如，在程序 9.8 中，一个名为 `outfile` 的 `ofstream` 对象在 `main()` 中打开，该流对象被传递给 `inOut()` 函数。`inOut()` 的函数原型和函数头将形参声明为对 `ostream` 对象类型的引用。然后使用 `inOut()` 函数将用户输入的五行文本写入文件。

# 程序 9.8

```
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

int main()
{
    string fname = "list.dat";  // 这是你要操作的文件
    void inOut(ofstream&);       // 函数原型
    ofstream outFile;

    outFile.open(fname.c_str());

    if (outFile.fail())   // 检查是否成功打开
    {
        cout << "\n输出文件 " << fname << " 未能成功打开"
             << endl;
        exit(1);
    }

    inOut(outFile);  // 调用函数

    return 0;
}

void inOut(ofstream& fileOut)
{
    const int NUMLINES = 5;  // 文本行数
    string line;
    int count;

    cout << "请输入五行文本：" << endl;
    for (count = 0; count < NUMLINES; count++)
    {
        getline(cin,line);
        fileOut << line << endl;
    }

    cout << "\n文件已成功写入。" << endl;

    return;
}
```

在 `main()` 中，文件是一个名为 `outFile` 的 `ofstream` 对象。该对象被传递给 `inOut()` 函数，并作为形参 `fileOut` 被接收，该形参被声明为对 `ofstream` 对象类型的引用。然后，`inOut()` 函数使用其引用参数 `outFile` 作为输出文件流名称，其方式与 `main()` 使用 `fileOut` 流对象的方式相同。程序 9.8 使用了第 9.2 节中介绍的 `getline()` 方法（参见表 9.3）。

程序 9.9 在程序 9.8 的基础上进行了扩展，添加了一个 `getopen()` 函数来执行打开操作。与 `inOut()` 一样，`getOpen()` 接受一个对 `ofstream` 对象的引用参数。`getOpen()` 执行完毕后，该引用被传递给 `inOut()`，与程序 9.8 中的方式相同。尽管你可能想将 `getOpen()` 编写为返回一个对 `ofstream` 的引用，但这行不通，因为这会试图将一个返回的引用赋值给一个已存在的引用。

# 程序 9.9

```
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

int getOpen(ofstream&);   // 函数原型 - 传递一个
                          // 对 fstream 的引用
void inOut(ofstream&);    // 函数原型 - 传递一个
                          // 对 fstream 的引用

int main()
{
    ofstream outFile;     // 文件名是一个 fstream 对象

    getOpen(outFile);     // 打开文件
    inOut(outFile);       // 向其中写入

    return 0;
}

int getOpen(ofstream& fileOut)
{
    string name;

    cout << "\n请输入文件名：";
    getline(cin,name);

    fileOut.open(name.c_str());      // 打开文件
```

```
if (fileOut.fail())    // 检查是否成功打开
{
    cout << "无法打开该文件" << endl;
    exit(1);
}
else
    return 1;
}

void inOut(ofstream& fileOut)
{
    const int NUMLINES = 5;  // 行数
    int count;
    string line;

    cout << "请输入五行文本：" << endl;
    for (count = 0; count < NUMLINES; ++count)
    {
        getline(cin,line);
        fileOut << line << endl;
    }
    cout << "\n文件已成功写入。";

    return;
}
```

程序 9.9 允许用户从标准输入设备输入文件名，然后打开指向外部文件的 `ofstream` 连接。如果输入的是现有数据文件的名称，则该文件在打开进行输出时会被销毁。程序 9.2 中阴影代码所示的方法是一个防止此问题的实用技巧。

## 练习 9.4

+   1.（实践）一个名为 `pFile()` 的函数将接收一个文件名作为对 `ifstream` 对象的引用。将文件名传递给 `pFile()` 需要哪些声明？
+   2.（实践）编写一个名为 `fcheck()` 的函数，用于检查文件是否存在。该函数应接受一个 `ifstream` 对象作为形式引用参数。如果文件存在，函数应返回值 1；否则，函数应返回值 0。
+   3.（实践）已创建了一个由一组行组成的数据文件。编写一个名为 `printLine()` 的函数，用于读取并显示文件中的任意一行。例如，调用 `printLine(ifstream &fName,5);` 应显示所传递对象流的第五行。
+   4.（修改）重写程序 9.9 中使用的 `getOpen()` 函数，以纳入本节所述的文件检查过程。具体来说，如果输入的文件名已存在，应显示适当的消息。用户应可以选择输入新文件名或允许程序覆盖现有文件。在你的程序中使用为练习 2 编写的函数。

## 9.5 常见编程错误

与文件相关的常见编程错误如下：

+   1. 在尝试读取或写入文件之前忘记打开文件。
+   2. 在访问文件时，使用文件的外部名称代替内部文件流对象名称。唯一使用数据文件外部名称的流方法是 `open()` 方法。与往常一样，本章讨论的所有流方法都必须以流对象名称开头，后跟句点（点运算符）。
+   3. 在未首先检查同名文件是否已存在的情况下打开文件进行输出。如果该文件已存在且你未检查预先存在的文件名，则该文件将被覆盖。
+   4. 不了解只有在读取或越过 EOF 标记之后才能检测到文件末尾。
+   5. 尝试使用字符变量来检测 EOF 标记。任何用于接收 EOF 的变量都必须声明为整型变量。例如，如果 `ch` 被声明为字符变量，以下表达式将产生无限循环：²
+   6. 将整型参数与 `seekg()` 和 `seekp()` 函数一起使用。该偏移量必须是长整型常量或变量。传递给这些函数的任何其他值都可能导致不可预测的结果。

```
while ( ch = in.file.peek() ) != EOF
```

出现此问题的原因是字符变量永远无法接受 EOF 代码。EOF 是一个整数值（通常为 -1），没有对应的字符表示，这确保了 EOF 代码不会与文件中作为正常数据出现的合法字符混淆。要终止由上述表达式创建的循环，变量 `ch` 必须声明为整型变量。

## 9.6 章节总结

+   1. 数据文件是以共同名称存储在外部存储介质中的任何数据集合。
+   2. 数据文件通过使用文件流对象连接到文件流。

