

或者，你必须使用指定名称和命名空间的其他方法，例如以下：

```
#include <iomanip>
using std::setw;
using std::setprecision;
```

## 保存标志设置

函数不应有不需要的或意外的副作用。例如，用于输出货币金额的函数可能包含

```
cout.setf(ios::fixed);
cout.setf(ios::showpoint);
cout.precision(2);
```

在函数调用结束后，这些设置仍会生效。如果不想产生此类副作用，可以保存并恢复原始设置。

函数 precision 已被重载，因此在不带参数时返回当前的精度设置，以便日后恢复设置。

使用 setf 设置的标志很容易保存和恢复。成员函数 flags 被重载以提供保存然后恢复标志设置的方法。成员函数 cout.flags( ) 返回一个类型为 long 的值，该值编码了所有标志设置。可以使用此 long 值作为 cout.flags 的参数来重置标志。这些技术对文件输出流的工作方式与对 cout 相同。

例如，保存和恢复这些设置的函数可以结构如下：

```
void outputStuff(ofstream& outStream)
{
    int precisionSetting = outStream.precision();
    long flagSettings = outStream.flags();
    outStream.setf(ios::fixed);
    outStream.setf(ios::showpoint);
    outStream.precision(2);
    //Do whatever you want here.
    outStream.precision(precisionSetting);
    outStream.flags(flagSettings);
}
```

另一种恢复设置的方法是

```
cout.setf(0, ios::floatfield);
```

使用这些参数调用成员函数 setf 将恢复默认的 setf 设置。请注意，这些是默认值，而不一定是上次更改前的设置。另请注意，默认设置值是实现相关的。最后请注意，这不会重置精度设置或任何不是用 setf 设置的设置。

## 更多输出流成员函数

Display 12.6 总结了类 ostream 的一些格式化成员函数以及一些操纵符。请记住，要使用操纵符，你需要以下内容（或类似内容）：

```
#include <iomanip>
using namespace std;
```

**Display 12.6  类 ostream 的格式化工具**

| FUNCTION | DESCRIPTION | CORRESPONDING MANIPULATOR |
|---|---|---|
| `setf(ios_Flag)` | 设置如 Display 12.5 中所述的标志 | `setiosflags(ios_Flag)` |
| `unsetf(ios_Flag)` | 取消设置标志 | `resetiosflags(ios_Flag)` |
| `setf(0, ios::fmtflags)` | 恢复默认标志设置 | None |
| `precision(int)` | 设置浮点数输出的精度 | `setprecision(int)` |
| `precision()` | 返回当前精度设置 | None |
| `width(int)` | 设置输出字段宽度，仅适用于下一个输出项 | `setw(int)` |
| `fill(char)` | 指定当输出字段大于输出值时使用的填充字符；默认为空白 | `setfill(char)` |

## 自测练习

- 8. 执行以下行时会产生什么输出？

```
cout << "*";
cout.width(5);
cout << 123
     << "*" << 123 << "*" << endl;
cout << "*" << setw(5) << 123
     << "*" << 123 << "*" << endl;
```

## 自测练习（续）

9. 执行以下行时会产生什么输出？

```
cout << "**" << setw(5) << 123;
cout.setf(ios::left);
cout << "**" << setw(5) << 123;
cout.setf(ios::right);
cout << "**" << setw(5) << 123 << "**" << endl;
```

10. 执行以下行时会产生什么输出？

```
cout << "**" << setw(5) << 123 << "**"
<< 123 << "**" << endl;
cout.setf(ios::showpos);
cout << "**" << setw(5) << 123 << "**"
<< 123 << "**" << endl;
cout.unsetf(ios::showpos);
cout.setf(ios::left);
cout << "**" << setw(5) << 123 << "**"
<< setw(5) << 123 << "**" << endl;
```

11. 执行以下行时会将什么输出发送到文件 stuff.txt？

```
ofstream fout;
fout.open("stuff.txt");
fout << "**" << setw(5) << 123 << "**"
<< 123 << "**" << endl;
fout.setf(ios::showpos);
fout << "**" << setw(5) << 123 << "**"
<< 123 << "**" << endl;
fout.unsetf(ios::showpos);
fout.setf(ios::left);
fout << "**" << setw(5) << 123 << "**"
<< setw(5) << 123 << "**" << endl;
```

12. 执行以下行时会产生什么输出（假设该行嵌入在一个完整且正确的程序中，并具有适当的 include 和 using 指令）？

```
cout << "**" << setw(3) << 12345 << "**" << endl;
```

## **示例：清理文件格式**

Display 12.7 中的程序从文件 `rawdata.txt` 读取输入，并将输出以整洁的格式同时写入屏幕和文件 `neat.txt`。程序将数字从文件 `rawdata.txt` 复制到文件 `neat.txt`，但它使用格式化指令以整洁的方式写入它们。数字每行一个，字段宽度为 12，这意味着每个数字前面都有足够的空格，使空格加上数字占 12 个空格。数字以普通记数法写入；即不以 e-记数法写入。每个数字写入小数点后五位，并带有一个正负号。程序使用一个名为 `makeNeat` 的函数，该函数对输入文件流和输出文件流具有形式参数。

## Display 12.7  格式化输出（第 1 部分，共 3 部分）

//Reads all the numbers in the file rawdata.dat and writes the numbers
//to the screen and to the file neat.dat in a neatly formatted way.
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <iomanip>

using std::ifstream;
using std::ofstream;
using std::cout;
using std::endl;
using std::ios;
using std::setw;

void makeNeat(ifstream& messyFile, ofstream& neatFile,
              int numberAfterDecimalpoint, int fieldWidth);
//Precondition: The streams messyFile and neatFile have been
//connected to two different files. The file named messyFile contains
//only floating-point numbers.
//Postcondition: The numbers in the file connected to messyFile have
//been written to the file connected to the stream
//neatFile. The numbers are written one per line, in fixed-point
//notation (that is, not in e-notation), with numberAfterDecimalpoint
//digits after the decimal point; each number is preceded by a plus or
//minus sign and each number is in a field of width fieldWidth. (This
//function does not close the file.)
int main()

![](img/c76bba8c1d927f399768ffe2ab5f5bee_576_0.png)

## Display 12.7 格式化输出（第 2 部分，共 3 部分）

```
25 {
26     ifstream fin;
27     ofstream fout;
28
29     fin.open("rawdata.txt");
30     if (fin.fail())
31     {
32         cout << "Input file opening failed.\n";
33         exit(1);
34     }
35
36     fout.open("neat.txt");
37     if (fout.fail())
38     {
39         cout << "Output file opening failed.\n";
40         exit(1);
41     }
42     makeNeat(fin, fout, 5, 12);
43
44     fin.close();
45     fout.close();
46     cout << "End of program.\n";
47     return 0;
48 }
49 //Uses <iostream>, <fstream>, and <iomanip>:
50 void makeNeat(ifstream& messyFile, ofstream& neatFile,
51             int numberAfterDecimalpoint, int fieldWidth)
52 {
53     neatFile.setf(ios::fixed);
54     neatFile.setf(ios::showpoint);
55     neatFile.setf(ios::showpos);
56     neatFile.precision(numberAfterDecimalpoint);
57
58     cout.setf(ios::fixed);
59     cout.setf(ios::showpoint);
60     cout.setf(ios::showpos);
61     cout.precision(numberAfterDecimalpoint);
62
63     double next;
64     while (messyFile >> next)
65     {
66         cout << setw(fieldWidth) << next << endl;
67         neatFile << setw(fieldWidth) << next << endl;
68     }
69 }
```

setf 和 precision 对文件输出流的行为与对 cout 相同。

满足如果有下一个数字可读

对文件流的工作方式与对 cout 相同

