
```cpp
using namespace std;
int main()
{
    // 布尔变量的声明与初始化
    bool b = true;
    int i = 12000;
    double d = 12067.372;
    // 打印值
    cout << "Printing without using formatting" << endl;
    cout << "Value of b: " << b << endl;
    cout << "Value of i: " << i << endl;
    cout << "Value of d: " << d << endl;
    // 格式化布尔数据并再次打印
    cout << "Printing the Boolean data" << endl;
    cout.setf(ios::alpha);
    cout << b << endl;
    // 格式化整数数据并再次打印
    cout << "Formatting the integer data type" << endl;
    cout.setf(ios::showbase);
    cout.setf(ios::uppercase);
    cout.setf(ios::right, ios::adjustfield);
    cout.width(16);
    cout << i << endl;
    // 格式化浮点数据并再次打印
    cout << "Formatting the floating-point data type" << endl;
    cout.setf(ios::showpoint);
    cout.setf(ios::right, ios::adjustfield);
    cout.setf(ios::fixed, ios::floatfield);
    cout.width(16);
    cout.precision(2);
    cout.fill('*');
    cout << d << endl;
    return 0;
}
```

运行结果：

不使用格式化打印

Value of b: 1

Value of i: 12000

Value of d: 12467.4

（续）

# 程序 16.22 打印三个数据项（续）

| 格式化布尔数据 | |

| :--- | :--- |

| true | ✓ |

| 格式化整数数据类型 | |

| 02EE0 | ✓ |

| 格式化浮点数据类型 | |

| 1267.37 | ✓ |

## 16.5.2 预定义操纵符

在本节中，我们将讨论书中多次使用的标准操纵符。我们的目标是更深入地回顾它们，并找到它们是为了实现什么目标而被编写的。这将我们编写操纵符。

## 与格式标志相关的操纵符

在表 16.13 中，我们列出了七个格式化操纵符。我们在表 16.18 中再次列出了它们。对于七个标志，我们正好有十四个格式标志操纵符（每个一个设置和一个取消）。彩色标记的部分是默认值。

## 与格式字段相关的操纵符

在表 16.15 中，我们列出了三个格式字段。对于这些字段中的标志，我们正好有八个操纵符。彩色标记的部分是默认值（表 16.19）。

| 表 16.18 使用格式标志的操纵符 | | | | |

| 标志 | 操纵符 | 效果 | 输入 | 输出 |

| :--- | :--- | :--- | :--- | :--- |

| boolalpha | noobalpha | 将布尔值显示为 0/1。 | ✓ | |

| | boolalpha | 将布尔值显示为 false/true。 | | ✓ |

| skipws | noskipw | 不跳过输入中的空白。 | ✓ | |

| | skipws | 跳过输入中的空白。 | | ✓ |

| showbase | noshowbase | 不显示进制基。 | ✓ | |

| | showbase | 显示进制基。 | | ✓ |

| showpoint | noshowpoint | 不显示小数点。 | ✓ | |

| | showpoint | 显示小数点。 | | ✓ |

| showpos | noshowpos | 不显示正号 (+)。 | ✓ | |

| | showpos | 显示正号 (+)。 | | ✓ |

| unitbuf | noununitbuf | 不刷新输出。 | ✓ | |

| | unitbuf | 写入后刷新输出。 | | ✓ |

| uppercase | nouppercase | 不显示大写字母字符。 | ✓ | |

| | uppercase | 显示大写字母字符。 | | ✓ |

## 表 16.19 使用格式字段的操纵符

| 标志 | 效果 | 输入 | 输出 |

| :--- | :--- | :--- | :--- |

| basefield | dec | 以十进制显示整数。 | ✓ | |

| | hex | 以十六进制显示整数。 | | ✓ |

| | oct | 以八进制显示整数。 | ✓ | |

| floatfield | fixed | 以固定点格式显示类型。 | | ✓ |

| | scientific | 以科学计数法显示类型。 | | ✓ |

| adjustfield | right | 字段内右对齐数据。 | | ✓ |

| | left | 字段内左对齐数据。 | | ✓ |

| | internal | 字段内内部对齐数据。 | | ✓ |

## 与格式变量相关的操纵符

在 16.17 中，我们提到了三组设置字段变量的成员函数。我们三个三个带参数函数的操纵符（表 16.20）。

## 与标志或字段无关的操纵符

有四个与任何标志或字段无关的操纵符。它们对流执行特定操作（表 16.21）。

我们使用操纵符代替格式标志、字段和变量来重复该程序以实现与程序 16.23 相同的目标。

## 16.5.3 操纵符的定义

在 16.17 中，我们提到了三组设置字段变量的成员函数。我们有三个带参数函数的操纵符（表 16.20）。

如果我们想创建新的操纵符，必须首先学习预定义操纵符如何

## 表 16.20 使用变量的操纵符

| 变量 | 操纵符 | 效果 |

| :--- | :--- | :--- |

| width | setw(n) | 设置 n 个字符宽。 |

| precision | precision(n) | 设置 n 位小数。 |

| fill | fill(c) | 设置 c 为填充字符。 |

| align | left/right | 设置对齐方式。 |

不带参数的操纵符可以使用接受流参数并返回流的函数使用。

## 表 16.21 使用标志的操纵符

| 操纵符 | 效果 |

| :--- | :--- |

| ws | 提取空白字符。 |

| endl | 插入换行。 |

| ends | 插入字符串末尾。 |

| flush | 刷新流缓冲区。 |

## 表 16.22 使用字段的操纵符

| 操纵符 | 效果 |

| :--- | :--- |

| setw | 设置 n 个字符宽。 |

| precision | 设置 n 位小数。 |

| fill | 设置 c 为填充字符。 |

| align | left/right | 设置对齐方式。 |

## 不带参数的操纵符

并不很难发现不带参数的操纵符（表 16.18、16.19 和 16.21）是如何实现的。系统有两个重载运算符，其中一个接受函数指针，所示：

```cpp
istream ::operator ((istream& (*pf) (istream));
ostream& ::operator (ostream& (*pf) (ostream));
```

第一个重载运算符使用指向 *istream* 对象的指针并返回 *istream* 对象的引用（用于链式调用）。第二个重载运算符使用指向 *ostream* 对象的指针并返回 *ostream* 对象的引用（用于链式调用）。

每个不带参数的操纵符都可以像下面所示通过函数实现。函数名作为指针传递给先的重载运算符。

```cpp
istream name (istream& is)
ostream name (ostream& os)
{
    action;
    return is;
}
{
    action;
    return os;
}
```

# 程序 16.24 带有自定义操纵符的程序

```cpp
************************************************************
* 模拟 boolalpha 和 noalpha 操纵符的程序
************************************************************
#include <iostream>
using namespace std;
// 定义名为 alpha 的函数
ostream& alpha (ostream& os)
{
    os.setf(ios::boolalpha);
    return os;
}
n// 定义名为 noalpha 的函数
ostream& noalpha (ostream& os);
```

## 程序 16.24 使用自定义操符的程序（续）

```cpp
{
  os.unsetf(ios::boolalpha);
  return os;
}
int main() {
  // 两个布尔变量的声明和初始化
  bool b1 = false;
  bool b2 = true;
  // 使用 alpha 和 noalpha 操符打印变量值
  cout << alpha << " " << b1 << " " << b2 << endl;
  cout << noalpha << b1 << " " << b b << endl;

}
```

运行结果：

false true

了解如何模拟系统操符有助于我们创建自己的操符。假设我们想要有一个名为 `currency`（不带参数）的操符，它会打印以 `$` 符号开头的值，随后跟上前导的星号以填充字段开头，并在小数点后保留两位数字。程序 16.25 展示了这样一个自定义操符。

## 程序 16.25 创建并测试自定义操符

```cpp
********************************************
* 使用自定义操符的程序
********************************************
#include <iostream>
#include <iomanip>
using namespace std;

ostream& currency (ostream & stream) {
  cout << '$';
  stream.precision(2);
  stream.fill('*');
  stream.setf(ios::fixed, ios::noalpha);
  return stream;
}
```

（续）

## 程序 16.25 创建并测试自定义操符（续）

```cpp
int main() {
    cout << currency << setw(12) << 12325.45 << endl;
    cout << currency << setw(12) << 0.36 << endl;
    return 0;
}
```

$******12325.45

*******0.36

这些值的打印方式与支票上的做法一样，用星号填充空位，以防止有人更改支票金额。

## 带参数的操符

模拟带参数的操符要复杂一些。函数指针不能带有参数。换句话说，我们无法拥有参数的指针，例如 `setw(4)`；指针只能命名为 `setw`。这意味着我们必须改变策略。我们不再使用函数指针，而是将 `setw(4)` 视为对一个具有整数类型数据成员的类的构造函数的调用。换句话说，我们将语句

```cpp
out << setw(4);
```

解释为具有两个操作数的运算符。第一个操作数是 `ostream` 类型的实例；第二个操作数是 `setw` 类型的实例。现在我们可以通过以下步骤创建一个带参数的操符：

- 1. 我们需要一个类，其名称与操符的名称相同，并且拥有一个与操符类型相同类型的数据成员。

- 2. 我们需要为该类重载插入或提取运算符，其中第一个参数的类型为 `stream`（`ostream` 或 `istream`），第二个参数与步骤 1 中的类类型相同。

- 3. 在重载运算符的函数体中，我们编写实现该操符目的的代码。

> 通过定义一个带有一个数据成员的类并在类中重载插入或提取运算符，可以创建一个带参数的操符。

我们模拟操符 `setw(n)`，但调用 `length(n)`，这样它会被视为一个新的操符。程序 16.26 显示了类 `length` 的接口（为了与操符保持一致，我们对类名使用小字母）。

## 程序 16.26 接口文件 (length.h)

```cpp
/* 名为 length 的类的接口文件 **/
#ifndef LENGTH_H
#define LENGTH_H
#include <iostream>
using namespace std;

class length {
private:
    int n;
public:
    length(int n);
    friend ostream& operator << (ostream& stream, const length len);
}
#endif
```

我们按照程序 16.27 所示实现该类。注意，我们希望运算符 `<<` 使用 `length` 类中数据成员 `n` 的值设置宽度变量。

我们编写程序 16.28 来应用这个新的操符并对其测试。

## 程序 16.27 实现文件 (length.cpp)

```cpp
/* 类的实现 **/
#include "length.h"

// length 成员函数的定义
length::length(int n1)
    : n(n1)
{}

ostream& operator << (ostream& stream, const length& len)
{
    stream.width(len.n);
    return stream;
}
```

## 程序 16.28 应用文件 (application.cpp)

```cpp
/* 使用操符 length(n) 的应用程序 *
*****************************************************************/
#include "length.h"

int main() {
    cout << length(10) << 123 << endl;
    cout << length(20) << 234 << endl;
    return 0;
}
```

| 运行结果: | 123 |

## 16.6 程序设计

在本节中，我们设计了三个程序来展示输入/输出流的应用。

## 16.6.1 合并两个排序后的文件

我们想要对两个整数文件进行合并。假设我们有两个整数文件，其中的整数已经过过（按从小到大排列）。我们想要合并这两个文件以创建一个新文件，新文件中的整数仍然保持排序，并保留重复项。图 16.15 显示了 `infile1`、`infile2` 和 `outfile` 的内容。

图 16.15 注意：`infile1`、`infile2` 和 `outfile` 的内容。

16.6 程序设计 16.15 注意：`infile1`、`infile2` 和 `outfile` 的内容。

16.6.1 合并两个排序后的文件 16.15 注意：`infile1`、`infile2` 和 `outfile` 的内容。

16.6.1 合并两个排序后的文件 16.15 注意：`infile1`、`infile2` 和 `outfile` 的内容。

16.6.1 合并两个排序后的文件 16.15 注意：`infile1`、`infile2` 并在 16.15在第 14 行我们创建一个哨兵（我们在之前的章节中学习过的整数）。程序 16.29 显示了代码。

程序 16.29 合并两个排序文件的程序

```cpp
********************************************
* 合并两个排序文件的程序
********************************************
#include <iostream>
#include <fstream>
#include <assert>
#include <limits>
using namespace std;

int main() {
    // 声明和初始化
    int first, second;
    int sentinel = numeric_limits<int>::max();
    // 实例化并打开文件
    ifstream strm1("infile1");
    ifstream strm2("infile2");
    ofstream strm3("outfile");
    if (!stm1.is_open()) {
        cout << "Error opening infile1!" << endl;
        assert(false);
    }
    if (!stm2.is_open()) {
        cout << "Error opening infile2!" << endl;
        assert(false);
    }
    if (!stm3.is_open()) {
        cout << "Error opening outfile!" << endl;
        assert(false);
    }
    // 处理
```

（续）
