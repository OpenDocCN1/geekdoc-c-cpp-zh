
在C++中，namespace是一个保留字。

### 示例7-8

语句

```cpp
namespace globalType
{
    const int N = 10;
    const double RATE = 7.50;
    int count = 0;
    void printResult();
}
```

将globalType定义为具有四个成员的命名空间：命名常量N和RATE、变量count以及函数printResult。

命名空间成员的作用域是相对于该命名空间本地的。通常可以通过以下两种方式之一在命名空间外部访问命名空间成员，如下所述。

访问命名空间成员的一般语法为：

```cpp
namespace_name::identifier
```

回忆一下，在C++中，::被称为作用域解析运算符。

要访问命名空间globalType的成员RATE，需要使用以下语句：

```cpp
globalType::RATE
```

要访问成员printResult（它是一个函数），需要使用以下语句：

```cpp
globalType::printResult();
```

因此，要访问命名空间的成员，需要使用命名空间名称，后跟作用域解析运算符，再跟成员名。

为了简化对命名空间成员的访问，ANSI/ISO标准C++提供了using语句的使用。使用using语句的语法如下：

- a. 为了简化对所有命名空间成员的访问：

```cpp
using namespace namespace_name;
```

- b. 为了简化对特定命名空间成员的访问：

```cpp
using namespace_name::identifier;
```

例如，using语句：

```cpp
using namespace globalType;
```

简化了对命名空间globalType所有成员的访问。语句：

```cpp
using globalType::RATE;
```

简化了对命名空间globalType成员RATE的访问。在C++中，using是一个保留字。

通常应将using语句放在命名空间声明之后。例如，对于命名空间globalType，通常编写如下代码：

```cpp
namespace globalType
{
    const int N = 10;
    const double RATE = 7.50;
    int count = 0;
    void printResult();
}
using namespace globalType;
```

在使用using语句之后，访问命名空间成员时，不必在成员前面加上命名空间名称和作用域解析运算符。但是，如果命名空间成员与程序中的全局标识符同名，则在程序中访问该命名空间成员时，必须在成员前面加上命名空间名称和作用域解析运算符。类似地，如果命名空间成员与块中的标识符同名，则在块中访问该命名空间成员时，必须在成员前面加上命名空间名称和作用域解析运算符。

示例7-9到7-12有助于阐明命名空间机制的使用。

### 示例7-9

考虑以下C++代码：

```cpp
#include <iostream>

using namespace std;
.
.
int main()
{
    .
    .
    .
}
.
.
.
```

在此示例中，可以引用头文件iostream中的全局标识符，如cin、cout和endl，而无需在标识符名称前加上前缀std::。明显的限制是，引用（头文件iostream的）全局标识符的块（或函数）不能包含与该全局标识符同名的任何标识符。

### 示例7-10

考虑以下C++代码：

```cpp
#include <cmath>

int main()
{
    double x = 15.3;
    double y;

    y = std::pow(x, 2);
    .
    .
    .
}
```

此示例访问头文件cmath中的pow函数。

### 示例7-11

考虑以下C++代码：

```cpp
#include <iostream>
.
.
int main()
{
    using namespace std;
    .
    .
    .
}
.
.
.
```

在此示例中，main函数可以引用头文件iostream中的全局标识符，而无需在标识符名称前加上前缀std::。using语句出现在main函数内部。因此，其他函数（如果有）在使用头文件iostream的全局标识符名称前应使用前缀std::，除非该函数有类似的using语句。

### 示例7-12

考虑以下C++代码：

```cpp
#include <iostream>

using namespace std;           //Line 1

int t;                         //Line 2
double u;                      //Line 3

namespace expN
{
    int x;                     //Line 4
    char t;                    //Line 5
    double u;                  //Line 6
    void printResult();        //Line 7
}

using namespace expN;

int main()
{
    int one;                   //Line 8
    double t;                  //Line 9
    double three;              //Line 10

    .
    .
    .
}

void expN::printResult() //Definition of the function printResult
{
    .
    .
    .
}
```

在这个C++程序中：

- 1. 要在main中引用第2行的变量`t`，请使用*作用域解析运算符*，即`::`（也就是说，将`t`引用为`::t`），因为函数main中有一个名为`t`的变量（在第9行声明）。例如，要将`x`的值复制到`t`中，可以使用语句`::t = x;`。

- 2. 要在main中引用命名空间expN的成员t（在第5行声明），请在t前加上前缀expN::（也就是说，将t引用为expN::t），因为存在一个名为t的全局变量（在第2行声明）以及main中名为t的变量。

- 3. 要在main中引用命名空间expN的成员u（在第6行声明），请在u前加上前缀expN::（也就是说，将u引用为expN::u），因为存在一个名为u的全局变量（在第3行声明）。

- 4. 可以在main中将命名空间expN的成员x（在第4行声明）引用为x或expN::x，因为不存在名为x的全局标识符，且函数main不包含任何名为x的标识符。

- 5. 命名空间成员函数（如printResult）的定义通常像前面的程序那样写在命名空间外部。要编写函数printResult的定义，函数头中的函数名可以是printResult或expN::printResult（因为不存在其他名为printResult的全局标识符）。

系统提供的头文件（如iostream、cmath和iomanip）中的标识符定义在命名空间std中。因此，为了简化对这些头文件中标识符的访问，我们在编写的程序中使用以下语句：

```cpp
using namespace std;
```

## string类型

在第2章中，您已经了解了string数据类型。回忆一下，在ANSI/ISO C++语言标准之前，标准C++库不提供string数据类型。编译器厂商通常提供自己程序员定义的string类型，而且字符串操作的语法和语义往往因厂商而异。

string数据类型是一种程序员定义的类型，不是C++语言的一部分；它由C++标准库提供。在使用string数据类型之前，程序必须包含头文件string，如下所示：

```cpp
#include <string>
```

回忆一下，在C++中，字符串是零个或多个字符的序列，字符串用双引号括起来。

语句：

```cpp
string name = "William Jacob";
```

将name声明为string变量，并将其初始化为"William Jacob"。name中第一个字符W的位置是0；第二个字符i的位置是1；依此类推。也就是说，字符串变量中第一个字符的位置从0开始，而不是1。

变量name可以存储（几乎）任何大小的字符串。

第3章讨论了string类型的I/O操作；第4章解释了string类型的关系操作。我们建议您重新阅读第3章和第4章，回顾string类型的I/O和关系操作。

其他运算符，如二元运算符+（用于字符串连接操作）和数组下标运算符[ ]，也已被定义为string数据类型的运算符。让我们看看这些运算符如何作用于string数据类型。

假设有以下声明：

```cpp
string str1, str2, str3;
```

语句：

```cpp
str1 = "Hello There";
```

将字符串"Hello There"存储到str1中。语句：

```cpp
str2 = str1;
```

将str1的值复制到str2中。

如果str1 = "Sunny"，语句：

```cpp
str2 = str1 + " Day";
```

将字符串"Sunny Day"存储到str2中。

假设str1 = "Hello"，str2 = "There"。语句：

```cpp
str3 = str1 + " " + str2;
```

将"Hello There"存储到str3中。此语句等效于语句：

```cpp
str3 = str1 + ' ' + str2;
```

此外，语句：

