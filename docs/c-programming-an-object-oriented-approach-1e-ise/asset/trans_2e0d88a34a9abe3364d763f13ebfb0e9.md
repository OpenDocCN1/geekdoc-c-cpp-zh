

## 程序 16.24 使用两个自定义操纵器的程序

```cpp
{
ios.unsetf(ios::boolalpha);
return os;
}

int main()
{
    // Declaration and initialization of two boolean variables
    bool b1 = false;
    bool b2 = true;
    // Printing values of variables with alpha and noalpha manipulators
    cout << alpha << b1 << " " << b2 << endl;
    cout << noalpha << b1 << " " << b2 << endl;
    return 0;
}

Run:
false true
0 1
```

了解如何模拟系统操纵器有助于我们创建自己的操纵器。假设我们想要创建一个名为*currency*的无参数操纵器，它能够以美元符号 `$` 开头打印值，并在字段开头用前导星号填充，同时在小数点后保留两位小数。程序 16.25 展示了这样一个自定义操纵器。

## 程序 16.25 创建并测试自定义操纵器

```cpp
/***************************************************************
 * A program that uses a customized manipulator                 *
 ***************************************************************/
#include <iostream>
#include <iomanip>
using namespace std;

ostream& currency(ostream& stream)
{
    stream << '$';
    stream.precision(2);
    stream.fill('*');
    stream.setf(ios::fixed, ios::floatfield);
    return stream;
}

int main()
{
    cout << currency << setw(12) << 12325.45 << endl;
    cout << currency << setw(12) << 0.36 << endl;
    return 0;
}

Run:
$*****12325.45
$********0.36
```

这些值按照支票上的通常方式打印，在空白位置填充星号，从而防止他人篡改支票金额。

## 带参数的操纵器

模拟带参数的操纵器稍微复杂一些。函数指针不能带参数。换句话说，我们不能拥有一个指向带参数函数的指针，例如 `setw(4)`；指针只能命名为 `setw`。这意味着我们必须改变策略。我们可以不使用函数指针，而将短语 `setw(4)` 看作对一个构造函数的调用，该构造函数属于一个只有一个整型数据成员的类。换句话说，我们将语句

```cpp
cout << setw(4);
```

解释为一个具有两个操作数的运算符。第一个操作数是 `ostream` 类型的实例；第二个操作数是 `setw` 类型的实例。现在，我们可以通过以下步骤创建一个带参数的操纵器：

- 1. 我们需要一个类，其名称与操纵器的名称相同，并且包含一个数据成员，该数据成员的类型与操纵器参数的类型相同。
- 2. 我们需要为该类重载插入运算符或提取运算符，其中第一个参数为流类型（`ostream` 或 `istream`），第二个参数与步骤 1 中的类相同。
- 3. 在重载运算符的函数体中，编写用于实现操纵器功能的操作。

> 可以通过定义一个包含一个数据成员的类来创建带参数的操纵器，
> 并对插入运算符或提取运算符进行重载。

我们模拟操纵器 `setw(n)`，但将其命名为 `length(n)`，这样它就会被当作一个新的操纵器。程序 16.26 展示了类 `length` 的接口（为了与操纵器保持一致，我们使用小写字母作为类名）。

## 程序 16.26 接口文件（length.h）

```cpp
/**************************************************************
 * Interface file for a class named length                    *
 **************************************************************/
#ifndef LENGTH_H
#define LENGTH_H
#include <iostream>
using namespace std;

class length
{
private:
    int n;
public:
    length(int n);
    friend ostream& operator<<(ostream& stream, const length& len);
};
#endif
```

我们还按照程序 16.27 所示实现类 `length`。注意，我们希望运算符 `<<` 使用类 `length` 中数据成员 `n` 的值设置宽度格式变量。

我们编写程序 16.28 来应用并测试这个新的操纵器。

## 程序 16.27 实现文件（length.cpp）

```cpp
/**************************************************************
 * Implementation of the class length                         *
 **************************************************************/
#include "length.h"

// Definition of the length member function
length::length(int n1)
: n(n1)
{
}

// Overloaded operator <<
ostream& operator<<(ostream& stream, const length& len)
{
    stream.width(len.n);
    return stream;
}
```

## 程序 16.28 应用程序文件（application.cpp）

```cpp
/**************************************************************
 * An application program to use the manipulator length(n)     *
 **************************************************************/
#include "length.h"

int main()
{
    cout << length(10) << 123 << endl;
    cout << length(20) << 234 << endl;
    return 0;
}

Run:
    123
    234
```

## 16.6 程序设计

在本节中，我们设计三个程序，以展示输入/输出流的应用。

### 16.6.1 合并两个有序文件

我们希望对两个整数文件执行归并排序。假设我们有两个整数文件，其中的整数已经排序（按照从小到大的顺序排列）。我们希望合并这两个文件，创建一个新文件，使其中的整数仍然保持有序，并且保留所有重复项。图 16.15 展示了 `infile1`、`infile2` 和 `outfile` 的内容。

![](img/d68f6199646ca63591a6d8419e0ed4ba_784_0.png)

**注意：**

只有一个名为*first*的变量和一个名为*second*的变量，但随着排序的进行，它们的值和条件会发生变化。

**图 16.15。** 归并排序中的数据流。

合并这些文件的过程需要进行 13 次迭代。在每次迭代中，变量*first*或变量*second*中的内容会被移动到输出文件，但不会同时移动两者。有些整数会在相应变量中保留几次迭代，之后才能移动到输出文件。注意，将整数移动到输出文件的比较和决策始终基于变量*first*和*second*中的内容。

程序 16.29 展示了代码。在第 14 行，我们声明了两个变量*first*和*second*，用于在处理过程中分别保存第一个输入文件和第二个输入文件中的整数。在第 15 行，我们创建了一个哨兵值（一个非常大的整数，正如前面章节中所学）。

## 程序 16.29 应用于两个文件的归并排序过程

```cpp
/************************************************************/
/* A program to merge two files of sorted integer to create  */
/* a file of sorted integers                                */
/************************************************************/
#include <iostream>
#include <fstream>
#include <assert.h>
#include <limits>
using namespace std;

int main()
{
    // Declaration and Initialization
    int first, second;
    int sentinel = numeric_limits<int>::max();
    // Instantiating streams and opening files
    ifstream strm1("infile1");
    ifstream strm2("infile2");
    ofstream strm3("outfile");
    if (!strm1.is_open())
    {
        cout << "Error opening infile1!" << endl;
        assert(false);
    }
    if (!strm2.is_open())
    {
        cout << "Error opening infile2!" << endl;
        assert(false);
    }
    if (!strm3.is_open())
    {
        cout << "Error opening outfile!" << endl;
        assert(false);
    }
    // Processing
36    strm1 >> first;
37    strm2 >> second;
38    while (strm1 || strm2)
39    {
40        if (first <= second)
41        {
42            strm3 << first << " ";
43            strm1 >> first;
44            if (!strm1)
45            {
46                first = sentinel;
47            }
48        }
49        else
50        {
51            strm3 << second << " ";
52            strm2 >> second;
53            if (!strm2)
54            {
55                second = sentinel;
56            }
57        }
58    }
59    // Closing files
60    strm1.close();
61    strm2.close();
62    strm3.close();
63    return 0;
64 }
```

### 16.6.2 对称密码

必须以安全的方式处理使用文件传输的信息。为此，常用的技术之一是密码学。**密码学**一词源自希腊语，意为“秘密书写”。它涉及两种不同的机制：对称密钥密码学和非对称密钥密码学。密码学使用密钥将称为*明文*的原始消息转换为称为*密文*的秘密消息。

密码学主要分为两大类：*对称密码学*和*非对称密码学*。本节将讨论并使用第一类密码学的示例；下一节将使用第二类密码学的示例。

在*对称密钥密码学*中，加密和解密使用同一个密钥。该密钥可以用于双向通信，这也是它被称为*对称*密钥的原因。图 16.16 展示了对称密钥密码的基本思想。

在图 16.16 中，一个实体 Alice 通过不安全信道向另一个实体 Bob 发送消息，并假设攻击者即使通过窃听信道，也无法理解消息的内容。

