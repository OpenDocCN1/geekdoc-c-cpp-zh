
`out.seekp(4, ios::beg);` // 进入输出文件的第五个字符

`inFile.seekg(4, ios::cur);` // 在输入文件中向前移动五个字符

`out.seekp(4, ios::cur);` // 在输出文件中向前移动五个字符

`inFile.seekg(-4, ios::cur);` // 在输入文件中向后五个字符

`out.seekp(-4, ios::cur);` // 在输出文件中向移动五个字符

`inFile.seekg(0L, ios::beg);` // 到输入文件的开头

`out.seekp(0L, ios::beg);` // 到输出文件的开头

`inFile.seekg(0L, ios::end);` // 到输入文件的末尾

`out.seekp(0L, ios::end);` // 到输出文件的末尾

`inFile.seekg(-10L, ios::end);` // 在输入文件末尾前 10 个字符

`out.seekp(-10L, ios::end);` // 在输出文件末尾前 10 个字符

与移动文件位置标记的`seek()`方法不同，`tell()`返回位置标记的值。例如，如果从输入流`inFile`读取了 10 个字符，该方法调用将返回`long`整数 10：

```
inFile.tellg();
```

这意味着下一个要读取的字符位于文件起始位置第 10 位，即文件中的第 11 个字符。

程序 8.7 显示了如何使用`seek()`和`tellg()`反向读取文件，从最后一个字符到第一个字符。每读取一个字符，它也会被显示出来。

假设`test.dat`文件包含以下内容：

程序 8.7 的输出如下：

```
5 : 2 : 9 : s : a : w : e : d : a : r : g : : e : h : T :
```

## 程序 8.7

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>
using namespace std;

int main() {
    string filename = "test.dat";
    char ch;
    long offset, last;
    ifstream infile(filename.c_str());
    if (infile.fail()) // 检查是否成功打开
    {
        cout << "\n未成功打开文件\n"
             << "\请检查文件当前是否存在\n"
             << endl;
        exit(1);
    }
    infile.seekg(0, ios::end); // 移动到文件末尾
    last = infile.tellg(); // 保存最后一个字符的偏移量
    for (offset = last; offset > 0; offset--) {
        infile.seekg(offset, ios::beg);
        ch = infile.get();
        cout << ch << " : ";
    }
    cout << endl;
    infile.close();
    return 0;
}
```

## 8.3 练习

1. 创建一个名为`test.dat`的文件，8.7 中的数据。
2. 在你的计算机上输入并执行 8.7。
3. 修改 8.7，使其起始于文件开头。
4. 编写一个程序显示`test.dat`中的每第二个字符。
5. 使用`seek()`和`tell()`方法编写一个名为`fileChars()`的函数，返回文件的总字符数。
6. 从任意位置编写名为`readBytes()`的函数。该函数应接受三个参数：文件对象、起始字符名称以及要读取的字符数。
7. 修改`readBytes()`以将字符存储在字符串或数组中。该函数应接受字符串作为第四个参数。（注意：`readBytes`的原型为`void(fstream, long, int)`。）

## 8.4 作为函数参数的文件

文件对象可以作为函数参数。唯一的要求是函数的正式参数必须是相应流（`ifstream`或`ofstream`）的引用（见 6.3）。例如，在程序 8.8 中，`main()`中打开了一个名为`outFile`的`ofstream`对象，并将此流传递给`inOut()`函数。

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

int main() {
    string filename = "list.dat"; // 你正在处理的文件
    void inOut(ostream& outFile); // 函数原型
    ofstream outFile;
    outFile.open(filename.c_str());
    if (outFile.fail()) {
        cout << "\n文件 " << filename << " 未成功打开" << endl;
        exit(1);
    }
    inOut(outFile); // 调用函数
    return 0;
}

void inOut(ostream& outFile) {
    const int NUMLINES = 5; // 文本行数
    string line;
    int count;
    cout << "请输入五行文本：" << endl;
    for (count = 0; count < NUMLINES; count++) {
        getline(cin, line);
        outFile << line << endl;
    }
    cout << "\n文件已成功写入。" << endl;
    return;
}
```

在`main()`中，文件是一个名为`outFile`的`ofstream`对象。该对象被传递给`inOut()`函数，并作为形式参数`fileOut`被接收，该参数被声明为`ofstream`对象的引用。`inOut()`函数随后使用其引用参数`outFile`作为输出文件流，方式与`main()`使用`outFile`流对象相同。程序 8.8 使用了第 8.2 节（表 8.3）引入的`getOpen()`方法。

程序 8.8 通过添加一个执行操作的`getOpen()`函数进行了扩展。与`inOut()`类似，`getOpen()`接受一个`ofstream`对象的引用参数。在`getOpen()`函数执行完成后，该引用会被传递给`inOut()`，如程序 8.8 所示。虽然你可能会编写`getOpen()`返回一个`ofstream`的引用，但这将不起作用，因为会导致尝试将返回的引用赋值给已有的引用。

## 程序 8.9

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

int getOpen(ofstream&); // 函数原型 - 传递一个 fstream 的引用
void inOut(ofstream&); // 函数原型 - 传递一个 fstream 的引用

int main()
{
    ofstream outFile; // 文件流是一个 ofstream 对象
    getOpen(outFile); // 打开文件
    inOut(outFile); // 写入内容
    return 0;
}
```

```cpp
int getOpen(ostream& fileOut)
{
    string name;
    cout << "\nEnter一个文件名: ";
    getline(cin, name);
    fileOut.open(name.c_str()); // 打开文件
    if (fileOut.fail()) // 检查是否成功打开
    {
        cout << "无法打开文件" << endl;
        exit(1);
    } else
        return 1;
}

void inOut(ostream& fileOut)
{
    const int NUMPLIES = 5; // 行数
    int count;
    string line;
    cout << "请输入五行文本：" << endl;
    for (count = 0; count < NUMPLIES; ++count)
    {
        getline(cin, line);
        fileOut << line << endl;
    }
    cout << "\n文件已成功写入.";
    return;
}
```

程序 8.9 允许用户从标准输入设备输入文件名，然后打开到外部文件的`ofstream`连接。如果输入了已存在的数据文件名，该文件在以输出模式打开时会被销毁。防止这种意外情况的一个实用技巧是使用输入流来打开输入的文件。如果文件存在，`fail()`方法将指示操作成功（即打开未失败），这表明文件可用于输入。这种技术可以用于提醒用户输入的名称在系统中存在，并请求确认是否可以销毁文件中的数据并重新为输出打开该文件；在重新为输出打开之前，应该关闭输入文件流。实现这一技巧留给你在练习 4 中尝试。

## 练习题 8.4

1. （练习题）有一个名为`pFile()`的函数，接收一个作为`istream`对象引用的文件名。将文件名传递给`pFile()`需要哪些声明？
2. （练习题）编写一个名为`fcheck()`的函数，用于检查文件是否存在。该函数接受一个`istream`对象作为形式引用参数。如果文件存在，函数应返回值 1；否则，函数应返回值 0。
3. （练习题）已创建了一个由若干行组成的文件。编写一个名为`printLine()`的函数，读取并显示文件的任意行。例如，调用`printLine(fstream& fName, 5)`应该显示传递对象的第五行。
4. （修改题）重写程序 8.9 中使用的`Open`函数，以包含本节的文件检查程序。具体来说，如果输入的文件名存在，应显示适当的消息。用户应被提供输入新文件名或允许程序覆盖现有文件的选项。在你的程序中使用练习 2 中的函数。

## 8.5 案例研究：花粉计数文件更新

在创建文件后，通常会编写应用程序来读取并用当前数据更新文件。在这个案例研究中，一个文件被用作存储最近 10 次花粉计数的数据库，这些计数在夏天被用于“易怒性”衡量。作为新的读数，它被添加到文件中，而旧的记录会被删除。

### 第一步 分析问题

花粉计数读取采集于美国东北部的 8 月至 9 月，由空气中的不规则花粉颗粒组成。

- 最近花粉计数的平均值
- 输入文件流
- 最近的 10 个值
- 这种存储类型格式化为先进先出（FIFO）列表，也称为“队列”。如果文件按后进先出（LIFO）顺序维护，则它是一个“栈”。

### 第二步 开发解决方案

该问题的算法非常直观，由如下伪代码描述：

```
main() 函数
  显示关于程序功能的消息。
  调用输入流函数。
  调用输出流函数。
  调用更新函数。
  显示周平均值。

输入流函数
  请求输入文件名。
  打开输入文件流并验证连接。

输出流函数
  请求输出文件名。
  打开输出文件流并验证连接。
```

在回顾此算法时，注意旧的花粉计数被“捕捉”但未用于任何计算。剩余的花粉计数被添加到输出文件中。最后，计算并显示最近花粉计数的平均值，并关闭所有文件。

### 代码实现

程序 8.10 展示了所选设计的 C++ 表示；算法已编码为`pollenUpdate()`函数。

## 程序 8.10

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

void openInput(ifstream&); // 传递一个 istream 的引用
void openOutput(ofstream&); // 传递一个 ofstream 的引用
double pollenUpdate(ifstream&, ofstream&); // 传递两个引用

int main() {
    ifstream inputFile; // inputFile 是一个 ifstream 对象
    ofstream outFile; // outFile 是一个 ofstream 对象
    double average;

    // 显示用户消息
    cout << "\n此程序读取旧的花粉计数文件，"
         << "\n创建一个当前花粉"
         << "计数文件，并计算并显示 "
         << "\n最新的 10 周平均值。";

    openInput(inputFile);
    openOutput(outFile);
    average = pollenUpdate(inputFile, outFile);
    cout << "\n新的 10 周平均值是: " << average << endl;
    return 0;
}
```

```cpp
// 此函数获取一个外部文件名并打开文件进行输入
void openInput(ifstream& fname)
{
    string filename;
    cout << "\nEnter the input pollen count filename: ";
    cin >> filename;
    fname.open(filename.c_str());
    if (fname.fail()) // 检查是否成功打开
    {
        cout << "\nFailed to open the file named " << filename << " for input"
             << "\nPlease check that this file exists"
             << endl;
        exit(1);
    }
    return;
}
```

```cpp
// 此函数获取一个外部文件名并打开文件进行输出
void openOutput(ofstream& fname)
{
    string filename;
    cout << "Enter the output pollen count filename: ";
    cin >> filename;
    fname.open(filename.c_str());
    if (fname.fail()) // 检查是否成功打开
    {
        cout << "\nFailed to open the file named " << filename << " for output"
             << endl;
        exit(1);
    }
    return;
}
```

```cpp
// 以下函数读取花粉文件，
// 写入新文件，
// 并返回新的周平均值
double pollenUpdate(ifstream& inFile, ofstream& outFile)
{
    const int POLNUMS = 10; // 花粉计数最大数量
    int i, polreading;
    int oldreading, newcount;
    double sum = 0;
    double average;

    // 获取最新的花粉计数
    cout << "Enter the latest pollen count reading: ";
    cin >> newcount;

    // 读取最旧的花粉计数
    inFile >> oldreading;
```
