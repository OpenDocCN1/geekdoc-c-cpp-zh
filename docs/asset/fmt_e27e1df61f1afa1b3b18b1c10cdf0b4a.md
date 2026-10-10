
或者，你必须使用以下其他指定名称和命名空间的方法：

```cpp
#include <iomanip>
using std::setw;
using std::setprecision;
```

## 保存标志设置

函数不应该产生意外或意想不到的副作用。例如，输出金额的函数可能包含：

```cpp
cout.setf(ios::fixed);
out.setf(ios::showpoint);
```

调用函数后，这些设置仍然有效。如果你不想副作用，可以保存并恢复原始设置。`precision`函数被重载，因此不带参数时它返回当前精度，以便恢复设置。`cout.flags()`成员函数返回一个所有标志的`long`值。使用此`long`值作为`cout.flags()`的参数可以重置标志。这些技术对于文件流和`cout`一样有效。例如，保存和恢复这些设置的结构如下：

```cpp
void outputStream(ostream out)
{
    int precisionSetting = out.precision();
    long flagSettings = out.flags();
    out.setf(ios::fixed);
    out.setf(ios::showpoint);
    out.precision(2);
    // 在此处执行任何你想的操作
    out.precision(precisionSetting);
    out.flags(flagSettings);
}
```

另一种恢复设置的方法：

```cpp
cout.setf(0, ios::floatfield);
```

带有这些参数的成员函数调用`set`将恢复默认设置（注意，而不是最后更改的设置）。此外，默认设置值取决于实现。最后，注意这不会重置`precision`设置或任何通过`setf`设置的设置。

## 更多输出流成员函数

显示 12.6 总结了`ostream`类的一些格式化成员函数和操纵符。记得使用以下操纵符（或类似的）：

```cpp
#include <iomanip>
using namespace std;
```

显示 12.6 `ostream`类格式化工具

| 函数 | 描述 | 对应的操纵符 |
|---|---|---|
| `setf(ios_Flag)` | 设置 12.5 中描述的标志 | `setiosflags(ios_Flag)` |
| `unsetf(ios_Flag)` | 取消标志 | `resetiosflags(ios_Flag)` |
| `setf(0, ios::floatfield)` | 恢复默认标志设置 | 无 |
| `precision(int)` | 设置浮点数输出精度 | `setprecision(int)` |
| `precision()` | 返回当前精度 | 无 |
| `width(int)` | 设置输出字段；仅适用于下一个项目 | `setw(int)` |
| `fill(char)` | 当输出字段大于值时指定填充字符；默认是空白 | `setfill(char)` |

### 自测练习

- 8. 执行以下行代码将产生什么输出？

```cpp
cout << "*";
cout.width(5);
cout << 123;
cout << "*" << 123 << "*" << endl;
cout << "*" << setw(5) << 123
cout << "*" << 123 << "*" << endl;
```

### 自测练习（续）

- 9. 执行以下行代码将产生什么输出？

```cpp
cout << "*" << setw(5) << 123;
cout.setf(ios::left);
cout << "*" << setw(5) << 123;
cout.setf(ios::right);
cout << "*" << setw(5) << 123 << "*" << endl;
```

- 10. 执行以下行代码将产生什么输出？

```cpp
cout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
cout.setf(ios::showpos);
cout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
cout.unsetf(ios::showpos);
cout.setf(ios::left);
cout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
```

- 11. 执行以下行代码时，将向内容发送到文件 `stuff.txt`？

```cpp
ofstream fout;
out.open("stuff.txt");
fout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
fout.setf(ios::showpos);
fout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
fout.unsetf(ios::showpos);
fout.setf(ios::left);
fout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
```

- 12. 执行以下行代码时将产生什么输出（假设该行嵌入在具有正确指令的完整程序中）？

```cpp
cout << "*" << setw(3) << 12345 << "*" << endl;
```

# 第 12 章 流与文件 I/O

## 示例：清理文件格式

显示 12.7 中的程序从文件`rawdata.txt`读取输入，并以整洁的格式将输出写入到屏幕和`neat.txt`文件。该程序将数字从`rawdata.txt`文件复制到`neat.txt`文件，但它使用了格式化指令以整洁的方式写入它们。数字每行写入一个，位于宽度为 12 的字段中，这意味着每个数字前面都有足够的空格，使得这些空格占据了 12 个空间。数字是以普通记法写入的；即它们不是以科学计数法（e-notation）写入。每个数字在小数点后保留五位，并带有正号或负号。程序使用了`makeNeat`函数，该函数为输入文件流和输出文件流设有形参参数。

显示 12.7 格式化输出（共 3 部分）

```cpp
// 读取文件 rawdata.dat 中的所有数字，并将数字
// 以整洁的格式写入屏幕和 neat.dat 文件。
#include <iostream>
#include <fstream>
#include <cstdio>
#include <iomanip>

using std::ifstream;
using std::ostream;
using std::cout;
using std::endl;
using std::ios;
using std::setw;

void makeNeat(ifstream messyFile, ostream& neatFile,
    int numberAfterDecimalpoint, int fieldWidth);
// 前置条件：流 messyFile 和 neatFile 已经
// 连接到两个不同的文件。名为 messyFile 的文件包含
// 只有浮点数。
// 后置条件：连接到 messyFile 的文件中的数字已
// 写入屏幕和连接到流 neatFile 的文件。
// 数字每行写入一个，使用固定点记法
//（即不是科学计数法），小数点后有 numberAfterDecimalpoint
// 各位数字；每个数字前面都有正号或
// 负号，且每个数字都在一个宽度为 fieldWidth 的字段中。（此
// 函数不关闭文件。）
int main() {
```

## 流 I/O 工具 543

### 12.7 格式化输出（共 3 部分，第 2 部分）

```cpp
ifstream fin;
ofstream fout;

fin.open("rawdata.txt");
if (fin.fail()) {
    cout << "\输入文件打开失败。\n";
    exit(1);
}

fout.open("neat.txt");
if (fout.fail()) {
    cout << "\输出文件打开失败。\n";
    exit(1);
}
makeNeat(fin, fout, 5, 12);

fin.close();
fout.close();
cout << "\n程序结束。\n";
return 0;
```

```cpp
// 使用 <iostream>, <fstream>, 和 <iomanip>
void makeNeat(ifstream& messyFile, ofstream& neatFile,
int numberAfterDecimalPoint, int fieldWidth)
```

```cpp
neatFile.setf(ios::fixed);
neatFile.set(ios::showpoint);
neatFile.set(ios::showpos);
neatFile.precision(numberAfterDecimalPoint);

out.setf(ios::fixed);
out.set(ios::showpoint);
out.precision(numberAfterDecimalPoint);

double next;
while (messyFile >> next) {
    cout << setw(fieldWidth) << next << endl;
    neatFile << setw(fieldWidth) << next << endl;
}
```

> `setf`和`precision`对于文件输出流的作用与`cout`相同。

> 如果有可读取的 ext 数字，则满足条件。

> 对于文件输出流的作用与`cout`一致。

## 544 第 12 章 流与文件 I/O

显示 12.7 格式化输出（共 3 部分，第 3 部分）

示例对话

| Rawdata.txt | （未被程序修改） |
| :--- | :--- |
| 10.37 | -9.88987 |
| 2.313 | -8.950 15.0 |
| 7.33333 | 92.87654 |
| -1.237568432e2 |  |

neat.txt（程序运行后）

屏幕输出

| +10.37000 | +10.37000 |
| :--- | :--- |
| -9.88987 | -9.88987 |
| +2.31300 | +2.31300 |
| -8.95000 | -8.95000 |
| +15.00000 | +15.00000 |
| +7.33333 | +7.33333 |
| +92.87654 | +92.87654 |
| -123.75684 | -131.75684 |
| 程序结束。 |  |

## 示例：编辑文本文件

这里讨论的程序是应用于文件的文本编辑的一个简单示例。该程序可以从现有的 C 广告材料自动生成 C++ 广告材料（以一种非常简单的方式）。程序从一个包含 C 语言优点的文件读取输入，并在另一个文件中写入关于 C 的类似广告文案。包含 C 广告语的文件名为`cad.txt`，接收 C++ 文案的新文件名为`cpp.txt`。程序简单地从`cad.txt`文件读取每个字符并复制到`cpp.txt`文件。每个字符都被复制了，但当从输入文件中读取大写字母 'C' 时，程序向输出文件写入 "C++"。该程序假设每当输入文件中出现字母 'C' 时，指的都是 C 编程语言；因此这种更改是产生更新后广告文案所需的。该程序假设输入文件中只要出现字母 'C'，就指代 C 编程语言；因此这种更改是产生更新后广告文案所需要的。注意，当程序从输入文件读取并写入输出文件时，换行符被保留了。这种方法在处理文件时是有效的，除了当从输入文件中读取大写字母 'C' 时，程序向输出文件写入 "C++"。这种方法在处理文件时是有效的。该程序假设输入文件中只要出现字母 'C' 时，就指代 C 编程语言。流 I/O 工具 544所有的 'C' 都被替换为 "C++"。

```cpp
#include <fstream>
#include <iostream>
#include <cstdlib>

using std::ifstream;
using std::ofstream;
using std::cout;

// 使用 <iostream>, <fstream>, 和 <iomanip>
void makeNeat(ifstream& messyFile, ofstream& neatFile,
int numberAfterDecimalPoint, int fieldWidth) {
    // 前置条件：流 messyFile 和 neatFile 已经
    // 连接到两个不同的文件。名为 messyFile 的文件包含
    // 只有浮点数。
    // 后置条件：连接到 messyFile 的文件中的数字已
    // 写入屏幕和连接到流 neatFile 的文件。
    // 数字每行写入一个，使用固定点记法
    //（即不是科学计数法），小数点后有 numberAfterDecimalPoint
    // 各位数字；每个数字前面都有正号或
    // 负号，且每个数字都在一个宽度为 fieldWidth 的字段中。（此
    // 函数不关闭文件。）
}
```
