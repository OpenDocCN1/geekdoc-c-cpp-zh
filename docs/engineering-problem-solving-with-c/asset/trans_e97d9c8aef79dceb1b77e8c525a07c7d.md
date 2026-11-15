

## 循环

这些问题与在第 3 章中开发的用于生成真值表的程序 `chapter_3_1` 有关。

- 32. 重写在第 3 章中开发的程序 `chapter_3_1`，并使用嵌套 `for` 循环。
- 33. 修改在本章中开发的程序 `chapter_4_5`，将 `for` 循环替换为 `do/while` 循环。
- 34. 修改在本章中开发的程序 `chapter_4_5`，将 `for` 循环替换为 `while` 循环。

![](img/0235a4ea835dc4575bd036e024a533b3_218_0.png)

来源：NASA/Science Source

## 工程挑战：天气预测

天气卫星为科学家和气象学家提供信息。会收集和分析大量数据，并使用历史数据来测试天气预测模型。可以分析数据以识别与全球气候变化相关的因素，例如云和温室气体。例如，了解云如何影响大气中的太阳能分布，可以帮助科学家更好地理解天气模式，并有助于开发用于天气预测和模拟全球气候变化的工具。

## 使用数据文件

## 章节大纲

- 目标
- 5.1 定义文件流
- 5.2 读取数据文件
- 5.3 生成数据文件
- 5.4 问题求解应用：数据过滤器——修改 HTML 文件
- 5.5 错误检查
- 5.6 数值技术：线性建模
- 5.7 问题求解应用：臭氧测量
- 5.8 使用 IDE 构建 C++ 解决方案：Xcode-天气模式
- 摘要、关键术语、C++ 语句摘要、样式说明、调试说明、问题

## 目标

在本章中，我们开发的问题求解方案将：

- 打开和关闭用于输入和输出的数据文件
- 使用常见的循环结构从文件中读取数据
- 检查输入流的状态
- 从输入流错误中恢复
- 应用线性建模的数值技术

### 5.1 定义文件流

工程问题求解方案通常涉及大量数据。这些数据可以由程序作为输出生成，也可以是程序使用的输入数据。通常既不现实将大量数据打印到屏幕上，也不现实从键盘读取大量数据。在这些情况下，我们通常使用数据文件来存储数据。这些数据文件与我们用于存储 C++ 程序的程序文件类似。事实上，C++ 程序文件是 C++ 编译器的输入数据文件，而目标程序是 C++ 编译器的输出文件。在本节中，我们将讨论与数据文件交互的 C++ 语句，并给出生成和读取数据文件中信息的示例。

### 流类层次结构

在第 2 章中，我们介绍了标准流对象 cin 和 cout。请回顾，这些类对象由编译器定义，分别对应系统的标准输入设备和标准输出设备。我们将在本章及后续章节中使用的另一个标准流类对象是 **cerr**。流对象 **cerr** 由编译器定义，用于将输出流式传输到系统的 **标准错误** 设备。**cerr** 是一个无缓冲流，这意味着输出将直接流式传输到标准错误。带缓冲的流，例如 **cout**，将数据流式传输到缓冲区，并在缓冲区刷新时显示数据。程序必须包含头文件 `iostream` 才能使用这些标准流。

在使用数据文件时，必须定义新流，这些流不仅支持读取 (>>) 和写入 (<<) 的一般属性，还支持附加到特定文件的功能。C++ 标准库提供了 **文件流类** 来支持文件输入和文件输出。`ifstream` 类用于定义可以从文件流式传输数据的输入文件流，而 `ofstream` 类用于定义可以将输出流式传输到文件的输出文件流。图 5.1 说明了 C++ 流类层次结构的一部分。

![](img/0235a4ea835dc4575bd036e024a533b3_220_0.png)

图 5.1 使用有向箭头指示 `ios` 继承自 `ios_base`。`istream` 和 `ostream` 均继承自 `ios`，而 `ifstream` 和 `ofstream` 分别派生自 `istream` 和 `ostream`。我们还看到 `iostream` 同时继承自 `istream` 和 `ostream`。这是 **多重继承** 的一个示例。我们将在后续章节中讨论 `ifstream` 类和 `ofstream` 类，但首先我们将在程序 Chapter5_1 中说明这些类的用法。要使用 `ifstream` 和 `ofstream` 类，程序必须包含头文件 `fstream`。程序 Chapter5_1 还使用 C++ 标准库函数 `exit()`。函数 `exit()` 需要一个整数参数。与 `main()` 的返回值类似，`exit()` 将其整数参数返回给系统。因此，以下程序中对 `exit(1)` 的调用将终止程序，并将 1 作为 `main()` 的返回值返回。

```cpp
/* Program 5_1                                                        */
/*                                                                    */
/* This program reads data pairs from the */
/* file sensor.txt and writes valid data pairs */
/* to the file checkedSensor.txt. Valid data pairs */
/* may not be negative. Invalid data is written to */
/* standard error (cerr). */
/*
#include <iostream> //Required for cerr
#include <fstream> //Required for ifstream, ofstream
using namespace std;

int main()
{
//Define file streams for input and output.
ifstream fin("sensor.txt");
ofstream fout("checkedSensor.txt");

//Check for possible errors.
if(fin.fail())
{
cerr << "could not open input file sensor.txt\n";
exit(1);
}
if(fout.fail())
{
cerr << "could not open output file checkedSensor.txt\n";
exit(1);
}

//All files are open.
double t, motion;
int count(0);
fin >> t >> motion;
while(!fin.eof())
{
++count;

//Write valid data to output file.
if(t >= 0 && motion >= 0)
{
fout << t << " " << motion << endl;
}
//Write invalid data to standard error output.
else
{
cerr << "Bad data encountered on line"
<< count << endl
<< t << " " << motion << endl;
}

//Input next data pair.
fin >> t >> motion;
}//end while
//close all files.
fin.close();
fout.close();
return 0;
}
```

如果数据文件 sensor.txt 包含以下数据，

| 0 | 45 |
|---|---|
| 1 | 48 |
| 2 | 56 |
| 3 | -1 |
| 4 | 10 |
| -5 | 8 |
| -6 | -4 |
| 6 | 12 |

显示到标准错误（在此情况下为屏幕）的输出将如下所示：

```
Bad data encountered on line 4
3 -1
Bad data encountered on line 6
-5 8
Bad data encountered on line 7
-6 -4
```

数据文件 checkedSensor.txt 将随后包含以下数据：

| 0 | 45 |
|---|---|
| 1 | 48 |
| 2 | 56 |
| 4 | 10 |
| 6 | 12 |

### ifstream 类

ifstream 类派生自 istream 类，因此它继承了 istream 类的所有功能，包括输入运算符和成员函数 eof() 和 fail()。ifstream 类中还提供了打开和关闭数据文件所需的其他成员函数。

程序中用于输入的每个数据文件都必须有一个与之关联的 ifstream 对象。使用类型声明语句来定义 ifstream 类型的对象，如下所示：

```cpp
ifstream sensor1;
```

定义 ifstream 对象后，必须将其与特定文件关联。

ifstream 类包含一个名为 open() 的成员函数。该函数由 ifstream 对象调用，并将文件名作为参数传递给该函数。因此，以下语句指定 ifstream 对象 sensor1 将用于名为 sensor1.txt 的文件，我们将从中读取信息：

```cpp
sensor1.open("sensor1.txt");
```

也可以在定义 ifstream 对象时对其进行初始化：

```cpp
ifstream sensor1("sensor1.txt");
```

在此，当创建 ifstream 对象 sensor1 时，会自动调用 open() 函数。

当指定用于输入的数据文件时，该文件必须存在并包含程序将使用的数据值。如果无法打开文件，将设置错误标志。不会生成错误消息，程序将继续执行，但所有从数据文件读取的尝试都将被忽略。因此，在打开用于输入的文件时，检查文件流对象的状态以确保文件打开成功始终是良好的做法。检查文件流对象状态的一种方法是让对象调用成员函数 fail()。如果数据文件打开失败，fail() 函数返回 true，如以下示例所示：

```cpp
ifstream sensor1;
sensor1.open("sensor1.txt");
if ( sensor1.fail() ) //open failed
{
   cerr << "File sensor1.txt could not be opened";
   exit(1); //end execution of the program
}
```

也可以直接检查文件流对象的状态：

```cpp
ifstream sensor1("sensor1.txt");
if ( !sensor1 ) //open failed
{
   cerr << "File sensor1.txt could not be opened";
   exit(1); //end execution of the program
}
```

为了清晰起见，我们通常使用第一种方法打开数据文件并检查文件流的状态。流状态将在第 5.5 节中更详细地讨论。

在打开用于输出的数据文件时，必须提供完整的文件名，包括文件的扩展名和路径。如果找不到文件，文件流将处于错误状态。下面提供的代码段使用 string 类型的变量和 do while 循环，允许用户输入完整的文件名，验证文件打开是否成功，并在打开不成功时可能进行恢复。图 5.2 提供了该代码段的流程图。

```cpp
/* This code segment attempts to open a data file for input. */
/* The file name is input by the user. */
/* */
//Define file stream for input
ifstream fin;

//Define variables for opening input file
char ch;
string filename;
```

