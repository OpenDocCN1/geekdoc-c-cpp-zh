
写入文件 `demofile.txt`：
Jones
Smith
Willis
Davis

文件第一次被打开时，名称的写入方式如图 12-2。

## 图 12-2 原始文件内容

| J | o | n | e | s | \n | S | m | i | t | \n<EOF> |
|---|---|---|---|---|---|---|---|---|---|---|

文件被关闭，并自动写入一个文件结束字符。当文件被重新打开时，新的输出被追加到文件末尾，如图 12-3 所示。

## 图 12-3 追加到文件

| J | o | n | e | s | \n | S | m | i | t | \n | W | i | l | l | s | \n | D | a | v | s | \n | <EOF> |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

*(注：由于原文文本中图 12-3 的表格内容不完整，此处根据上下文推断并补全了逻辑结构)*

## 打开文件前检查文件是否存在

有时你想在打开文件之前确定文件是否存在。这可以通过首先尝试以输入模式打开文件来实现。如果文件不存在，你可以以输出模式创建它。

```cpp
ifstream dataFile;

dataFile.open("values.txt", ios::in);

if (dataFile.fail()) {

    // 文件不存在，所以创建它。

    dataFile.open("values.txt", ios::out);

} else {

    // 文件已经存在。

    dataFile.close();

}
```

## 使用流定义打开文件

使用 `open` 函数的替代方案是使用流定义来打开文件。这是一个示例：

```cpp
ifstream dataFile("names.txt", ios::in | ios::out);
```

这种技术你也可以在流定义打开文件后测试错误。如下代码所示：

```cpp
ifstream inputFile("SalesData.txt");

if (!inputFile)

    cout << "Error opening SalesData.txt.\n";
```

## 思考题

- 12.1 如果你想将所有输出写入现有文件，应该使用哪个文件标志？
- 12.2 如何使用多个文件标志？
- 12.3 假设 `diskInfo` 是一个 `fstream` 对象，写一个语句打开 `names.txt` 文件进行输出。
- 12.4 假设 `diskInfo` 是一个 `fstream` 对象，写一个语句打开 `customers.txt` 文件进行输出，且所有输出都写入文件末尾。
- 12.5 假设 `diskInfo` 是一个 `fstream` 对象，写一个语句以输入和输出模式打开 `payable.txt` 文件。
- 12.6 写一个语句定义名为 `dataFile` 的 `fstream` 对象并打开名为 `salesfigures.txt` 的文件。（注意：文件应该用定义语句打开而不是 `open` 调用。）

## 12.2 文件输出格式

> 概念：文件输出的格式化可以与屏幕输出相同。

在第 3 章中的用于 `cout` 的相同输出格式化技术也可以用于文件流对象。例如，可以使用 `setprecision` 和 `fixed` 操纵符来确定浮点值舍入的精度。程序 12-3 展示了这一点。

## 程序 12-3

```cpp
// 此程序使用 setprecision 和 fixed
// 操纵符格式化文件输出。
#include <iostream>
#include <iomanip>
#include <fstream>
using namespace std;
int main() {
    fstream dataFile;
    double num = 17.813692;
    dataFile.open("numfile.txt", ios::out); // 以输出模式打开
// (程序继续)
```

### 程序 12-3 (续)

```cpp
dataFile << fixed; // 设置为定点计数法
dataFile << num << endl; // 写入数字
dataFile << setprecision(4); // 设置为4位小数精度
dataFile << num << endl; // 写入数字
dataFile << setprecision(3); // 设置为3位小数精度
dataFile << num << endl; // 写入数字
dataFile << setprecision(2); // 设置为2位小数精度
dataFile << num << endl; // 写入数字
dataFile << setprecision(1); // 设置为1位小数精度
dataFile << num << endl; // 写入数字
cout << "Done.\n";
dataFile.close(); // 关闭文件
return 0;
}
```

### 文件 myfile.txt 的内容

```
17.816392
17.8164
17.816
17.82
17.8
```

注意，文件的输出格式与屏幕输出的格式完全一致。程序 12-4 展示了如何使用 `setw` 操符将文件输出格式化为列。

## 程序 12-4

```cpp
// 此程序向文件写入三行数字。
#include <iostream>
#include <fstream>
#include <iomanip>
using namespace std;
int main() {
    const int ROWS = 3; // 写入行数
    const int COLS = 3; // 写入列数
    int nums[ROWS][COLS] = { 2897, 5, 837,
                             34, 7, 1623,
                             390, 3456, 12 };
    ofstream outFile("table.txt", ios::out);
// 写入三行数字，每个数字
// 占据8个字符宽的字段。
    for (int row = 0; row < ROWS; row++)
    {
      for (int col = 0; col < COLS; col++)
      {
        outFile << setw(8) << nums[row][col];
        outFile << endl;
      }
    }
    outFile.close();
    cout << "Done.\n";
    return 0;
}
```

### 文件 table.txt 的内容

| 2897 | 5 | 837 |
| 34 | 7 | 1623 |
| 390 | 3456 | 12 |

图 12-4 显示了字符在文件中的呈现方式。

## 图 12-4 文件内容

| 2 8 9 7 | | 5 | 8 3 7 |
| | 3 4 | | 7 | 1 6 2 3 |
| | 3 9 0 | 3 4 5 6 | | 1 2 |

## 12.3 将文件流对象传递给函数

概念：文件流对象可以按引用方式传递给函数。

在编写实际程序时，你可能希望创建模块化的代码来处理文件操作。文件流对象可以传递给函数，但始终应该通过引用的方式传递。下面显示的 `openFile` 函数使用了一个 `fstream` 引用参数：

```cpp
bool openFile(fstream &file, string name)
{
  bool status;
  file.open(name, ios::in);
  if (file.fail())
    status = false;
  else
    status = true;
  return status;
}
```

文件流对象的内部状态会在几乎每次操作中发生变化。它们应该始终通过引用传递给函数，以确保内部的一致性。程序 12-5 展示了如何将文件流对象作为参数传递给函数的示例。

## 程序 12-5

```cpp
// 此程序演示了如何将文件流对象
// 按引用传递给函数。
#include <iostream>
#include <fstream>
#include <string>
using namespace std;
// 函数原型
bool openFile(fstream &, string);
void showContents(fstream &);
int main() {
    fstream dataFile;
    if (openFile(dataFile, "demofile.txt")) {
        cout << "文件打开成功。\n";
        cout << "正在从文件中读取数据。\n";
        showContents(dataFile);
        dataFile.close();
        cout << "\nDone.\n";
    } else {
        cout << "文件打开错误!" << endl;
    }
    return 0;
}
// 函数 openFile 的定义。接受一个
// fstream 对象的引用作为参数。以输入模式打开文件。
// 成功时返回 true，失败返回 false。
```

## 12.4 更详细的错误测试

```cpp
37 bool openFile(fstream &file, string name)
38 {
39     file.open(name, ios::in);
40     if (file.fail())
41         return false;
42     else
43         return true;
44 }
45 
46 //***************************************
47 // 函数 showContents 的定义。接受一个 fstream
48 // 引用作为参数。使用循环从文件中
49 // 读取每个名称并显示在屏幕上。
50 //***************************************
51 
52 void showContents(fstream &file)
53 {
54     string line;
55     while (file >> line)
56     {
57         cout << line << endl;
58     }
59 }
```

### 高级操作

#### 流状态

| 位 | 说明 |
| :--- | :--- |
| `eof()` | 当遇到文件末尾时设置。 |
| `fail()` | 当尝试的操作失败时设置。 |
| `bad()` | 当发生不可恢复的错误时设置。 |
| `good()` | 当上述标志均未设置时设置。 |

## 程序 12-6（续）

```cpp
// 函数 showState 的定义。该函数使用一个
// fstream 引用作为其参数。显示了
// eof(), fail(), bad() 和 good() 成员函数的返回值。
// 在函数返回之前调用了 clear() 函数.
void showState(fstream& file) {
    cout << "File Status:\n";
    cout << " eof bit: " << file.eof() << endl;
    cout << " fail bit: " << file.fail() << endl;
    cout << " bad bit: " << file.bad() << endl;
    cout << " good bit: " << file.good() << endl;
    file.clear(); // 清除任何错误位
}
```

## 程序输出

## 12.5 用于读写文件的成员函数

**概念：** 文件流对象具有更专门的读写成员函数。

如果空白字符是文件中数据的一部分，当使用 `>>` 运算符读取文件时就会出现问题。因为该运算符将空白字符视为分隔符，所以它不会读取它们。例如，考虑文件 `murphy.txt`，它包含以下数据：

Jayne Murphy
47 Jones Circle
Almond, NC 28702

图 12-5 显示了数据在文件中记录的方式。

## 图 12-5 文件内容

| J | a | y | n | e | | M | u | r | p | h | y | \n | 4 | 7 |
| J | o | n | e | s | | C | i | r | c | l | e | \n | A |
| l | m | o | n | d | , | | N | C | | 2 | 8 | 0 |
| 2 | \n | <EOF> |

使用 `>>` 运算符产生的问题在程序 12-7 的输出中显而易见。

## 程序 12-7

```cpp
// 此程序演示了不应如何使用 >> 运算符
// 读取文件中包含空白字符的数据。
#include <iostream>
#include <fstream>
#include <string>
using namespace std;
int main()
{
    string input; // 用于存储文件输入
    fstream fileName; // 文件流对象
    // 以输入模式打开文件。
    fileName.open("murphy.txt", ios::in);
    // 如果文件成功打开，则继续。
    if (fileName)
    {
        // 读取文件内容。
        while (fileName >> input)
        {
            cout << input;
        }
    }
```

### 程序 12-7（续）

```cpp
26      // 关闭文件。
27      fileName.close();
28
29  else
30  {
31      cout << "ERROR: Cannot open file.\n";
32  }
33      return 0;
34 }
```

### 程序输出

```
JayneMurphy
47
Jones
Circle
Almond,
NC
28702
```

## getline 函数

程序 12-7 的问题可以通过使用 `getline` 函数来解决。该函数读取一“行”数据，包括空白字符。以下是函数调用的示例：

```cpp
getline(dataFile, str, '\n');
```

该语句中的三个参数解释如下：

- `dataFile`：这是文件流对象的名称。它指定了要从中读取数据的流对象。
- `str`：这是一个字符串对象的名称。从文件中读取的数据将存储在这里。
- `'\n'`：这是你选择的分隔符字符。如果遇到此分隔符，会导致函数停止读取（此参数是可选的。如果省略，默认值为 `'\n'`）。

该语句是从文件中读取一行字符的指令。该函数将一直读取，直到遇到 `\n`。该行字符将存储在 `str` 对象中。

程序 12-8 是程序 12-7 的修改。它使用 `getline` 函数从文件中读取整行数据。

## 程序 12-8

```cpp
// 此程序使用 getline 函数从文件中读取一行
// 数据。
#include <iostream>
#include <fstream>
#include <string>
using namespace std;
int main()
{
    string input; // 用于存储文件输入
    fstream nameFile; // 文件流对象
    // 以输入模式打开文件。
    nameFile.open("murphy.txt", ios::in);
    // 如果文件成功打开，则继续。
    if (nameFile) {
        // 从文件中读取一个项。
        getline(nameFile, input);
        // 如果上次读取操作成功
        if (was_successful) continue;
        while (nameFile) {
            // 显示最后读取的项。
            cout << input << endl;
            // 读取下一个项。
            getline(nameFile, input);
        }
        // 关闭文件。
        nameFile.close();
    } else {
        cout << "ERROR: Cannot open file.\n";
    }
    return 0;
}
```

### 程序输出

```
Jayne Murphy
47 Jones Circle
Almond, NC 28702
```

## 程序 12-10 (续)

```cpp
// Display the last character read.
```
