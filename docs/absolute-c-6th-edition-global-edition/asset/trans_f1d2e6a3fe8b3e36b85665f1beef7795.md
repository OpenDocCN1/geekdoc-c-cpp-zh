

寻找位置的约束以及用新数据替换文件某一部分的数据意味着大多数此类随机访问 I/O 都是通过读写记录（以结构体或类的形式）来完成的。每次定位指针后都会读取或写入一个记录（或若干个完整的记录）。

每个 fstream 对象都有一个名为 seekp 的成员函数，用于将 put 指针定位到你希望写入（“put”）数据的地址。函数 seekp 接受一个参数，即下一个要写入的第一个字节的地址。文件的第一个字节编号为零。例如，要将连接到 fstream rwStream 的文件中的指针定位到第 1000 个字节，调用方式如下：

```
rwStream.seekp(1000);
```

当然，你需要知道一个记录需要多少字节。sizeof 运算符可用于确定类或结构体的对象所需的字节数。实际上，sizeof 可应用于任何类型、对象或值。它以字节为单位返回其参数的大小。运算符 sizeof 是 C++ 核心语言的一部分，不需要包含指令或 using 指令。一些示例调用如下：

```
sizeof(s) (where s is string s = "Hello;")
sizeof(10)
sizeof(double)
sizeof(MyStruct) (where MyStruct is a defined type)
```

其中每一个都返回一个整数，表示其参数以字节为单位的大小。

要将 put 指针定位到仅包含 MyStruct 类型记录的文件中第 100 个 MyStruct 类型记录处，seekp 的调用为

```
rwStream.seekp(100*sizeof(MyStruct) - 1);
```

成员函数 seekg 用于定位 get 指针，以指示下一个字节的读取（“getting”）将在何处进行。它与 seekp 完全类似。按照我们所示的设置，你可以使用 fstream rwStream 的成员函数 put 和 get 向文件“stuff”写入并从文件“stuff”读取。还有一个成员函数 write 可以写入多个字节，以及一个成员函数 read 可以读取多个字节。

理论上，你现在已经知道足够多的知识来执行随机访问文件 I/O。实际上，这只是其中涉及内容的冰山一角。本节旨在以一种概括的方式让你了解其大致内容。如果你打算进行任何真正的随机访问文件 I/O 编程，你应该查阅一本更高级、更专业的书籍。

## Chapter Summary

- 类型为 ifstream 的流可以通过调用成员函数 open 连接到文件。你的程序随后可以从该文件获取输入。
- 类型为 ofstream 的流可以通过调用成员函数 open 连接到文件。你的程序随后可以将输出发送到该文件。
- 你应该使用成员函数 fail 来检查 open 调用是否成功。
- 流成员函数，例如 width、setf 和 precision，可用于格式化输出。这些输出函数对于连接到屏幕的流 cout 以及连接到文件的输出流的工作方式相同。
- 一个函数可以具有流类型的形式参数，但它们必须是传引用参数。它们不能是传值参数。类型 ifstream 可用于输入文件流，类型 ofstream 可用于输出文件流。（请参阅下一个摘要点，了解其他类型可能性。）
- 如果你使用 istream（不带“f”拼写）作为输入流参数的类型，则与该形式参数对应的参数可以是流 cin 或类型为 ifstream（带“f”拼写）的输入文件流。如果你使用 ostream（不带“f”拼写）作为输出流参数的类型，则与该形式参数对应的参数可以是流 cout、流 cerr 或类型为 ofstream（带“f”拼写）的输出文件流。
- 成员函数 eof 可用于测试程序何时到达输入文件的末尾。
- 你用来操作文件的相同输入和输出函数可通过 stringstream 类来操作字符串。stringstream 类提供了一种简单的方法，可将其他数据类型变量创建为字符串，或从字符串读取其他数据类型变量。

## Answers to Self-Test Exercises

1. 流 fin 和 fout 声明如下：

```
ifstream fin;
ofstream fout;
```

放在文件顶部的包含指令是

```
#include <fstream>
```

由于定义放在 std 命名空间中，你还应该有以下之一（或类似内容）：

```
using std::ifstream;
using std::ofstream;

or

using namespace std;
```

2. 
```
fin.open("stuff1.txt");
if (fin.fail())
{
    cout << "Input file opening failed.\n";
    exit(1);
}

fout.open("stuff2.txt");
if (fout.fail())
{
    cout << "Output file opening failed.\n";
    exit(1);
}
```

3. 
```
fin.close();
fout.close();
```

4. 你需要用流 cout 替换流 outStream。请注意，你不需要声明 cout，你不需要用 cout 调用 open，并且你不需要关闭 cout。

5. 这是“重新开始”。文件必须关闭并再次打开。此操作将读取位置置于文件开头，准备再次读取。

6. 
```
1
2
3
3
```

7. 
```
void toScreen(ifstream& fileStream)
{
    int next;
    while (fileStream >> next)
        cout << next << endl;
}
```

8. 
```
* 123*123*
   * 123*123*
```

每个空格包含恰好两个空白字符。请注意，对 width 或 setw 的调用仅对一个输出项有效。

9. 
```
* 123*123 * 123*
```

每个空格由恰好两个空白字符组成。

## 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法能够高效地从复杂布局的图片中提取结构化信息。

- 支持多种文档元素识别
- 支持表格与图片的自动标注
- 输出标准 JSON 格式

## 2. 方法概述

我们采用基于深度学习的视觉模型，结合版面分析技术，对文档中的标题、段落、表格等元素进行定位与识别。

| 元素类型 | 识别准确率 | 平均耗时 |
|----------|------------|----------|
| 标题     | 98.2%      | 12ms     |
| 段落     | 97.5%      | 15ms     |
| 表格     | 95.8%      | 30ms     |

> 注意：所有坐标均采用相对坐标，范围在 0 到 1 之间。

![](img/c76bba8c1d927f399768ffe2ab5f5bee_594_0.png)

```
```cpp
int num;
string s = "10";
stringstream ss(s);
ss >> num;
```
```

20. 用于将 field 转换为 double 的 stringstream 变量 ssNum 需要为每个新处理的字符串进行清除。这可以通过在 while 循环内部调用 clear 函数来实现。

```
```cpp
stringstream ssList, ssNum;
string numbers = "1.1, 1.2, 1.3";

double total = 0;
double num;

ssList.clear();
ssList.str(numbers);

string field;
while (getline(ssList, field, ','))
{
    ssNum.clear();
    ssNum.str(field);
    ssNum >> num;
    total += num;
}
cout << total << endl;
```
```

## Programming Projects

- 1. 编写一个程序，搜索一个包含 int 类型数字的文件，并在屏幕上打印该文件中所有的质数。文件仅包含用空格或换行符分隔的 int 类型数字。
- 2. 编写一个程序，从包含 double 类型数字的文件中读取输入，并将文件中的数字平均值输出到屏幕。文件仅包含用空格和/或换行符分隔的 double 类型数字。
- 3. a. 计算数据文件的中位数。*中位数*是大于该数字的数据元素数量与小于该数字的数据元素数量相同。针对此问题，你应假设数据已排序（即按递增顺序排列）。如果元素个数为奇数，中位数是文件的中间元素；如果文件元素个数为偶数，中位数是两个中间元素的平均值。你需要打开文件，计数成员，关闭文件并计算文件中间的位置，再次打开文件（回顾本章开头“重新开始”的讨论），计数到你需要的条目，并计算中间值。

