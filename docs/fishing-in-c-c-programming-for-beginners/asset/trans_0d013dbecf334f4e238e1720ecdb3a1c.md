
## 按位异或运算符

^ 是按位异或运算符。该运算符在以下情况下返回零：

| x | y | x^y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

请参考以下程序：

```
#include<iostream>
using namespace std;
int main()
{
    int a = 9, b = 5;
    int c = a ^ b;
    cout << c;
}
```

在此，输出将为 12。

a = 9 = 1001, b = 5 = 101
因此，c = a ^ b = 1001 ^ 101
= 1001 ^ 0101
= 1100
= 12

## 左移运算符

<< 是左移运算符。这是一个非常神奇的运算符。它将一个数的二进制等效形式左移指定的位数。例如，5 << 2 表示将数字 5 左移 2 位。

```
e.g. 5 << 2 = 101 << 2
= 00101 << 2
= 10100
= 20
```

请参考以下程序：

```
#include<iostream>
using namespace std;
int main()
{
    int a = 5;
    int c = a << 2;
    cout << c;
}
```

在此，输出将为 20

## 右移运算符

>> 称为右移运算符。例如，15 >> 2 表示将数字 15 的二进制等效形式向右移动 2 位。

```
e.g. 15 >> 2 = 1111 >> 2
= 0011
= 3
```

请参考以下程序：

```
#include<iostream>
using namespace std;
int main()
{
    int a = 15;
    int c = a >> 2;
    cout << c;
}
```

在此，输出将为 3

## 非运算符

! 是非运算符

| x | !(x) |
|---|---|
| 0 | 1 |
| 1 | 0 |

现在，请参考以下这个精彩的程序

```
#include<iostream>
using namespace std;
int main()
{
    int a = 13;
    int c = (!a);
    cout << c;
    return 0;
}
```

在此，输出为 0，而它应该是 !(13) = !(1101) = 0010 = 2。原因是非运算符将除零以外的所有值视为真。因此 13 不是零。所以，它为真，因此其否定为假。所以，输出为零。在上述程序中，如果将 13 替换为 (-13)，则输出仍将为零。而如果将 13 替换为 0，则输出将为 1。

那么，如何获取 13 的否定或补码呢。让我们看看下一个程序。

## 一的补码

要获取一的补码，使用 ~ 运算符。

请参考以下程序：

```
#include<iostream>
using namespace std;
int main()
{
    int a = 13;
    int c = (~a);
    cout << ("%d", c);
    return 0;
}
```

其输出将为 -14。

![](img/5340985153962870d4e4a3b9453b9146_240_0.png)

## 异常

异常为我们提供了一种检测并响应各种运行时错误的方法。当遇到错误时，错误会被抛给特殊的处理程序。本章最有用的部分是 try...catch 块。要捕获错误，我们将代码放在 try 块中，catch 定义在 try 块之后。catch 接收错误并做出相应响应。一旦捕获异常，它就会被抛出。

使用 try...catch 的语法如下：

```
try
{
//statements
throw exception;
}
catch(argument)
{
//statements
}
```

其中 argument 是抛出的值，可以是整型或字符型。如果你不知道类型，应该使用三个点（...）作为参数，称为省略号，因为它接受所有类型的参数。因此，你可以说它是默认参数。

请参考以下程序：

```
#include<iostream>
using namespace std;
int main()
{
    try
    {
        long double* array = new long double[10000000000000000000];
    }
    catch(...)
    {
        cout << "Error occurred";
    }
    return 0;
}
```

### 输出

发生错误

如果未捕获整型或字符型错误，省略号用作 catch 的最后一个参数。因此，你可以将上述程序重写如下：

```
#include<iostream>
using namespace std;
int main()
{
    try
    {
        long double* array = new long double[100000000000000000];
    }
    catch(int a)
    {
        cout << "Integral Error occurred";
    }
    catch(char a)
    {
        cout << "Char Error occurred";
    }
    catch(...)
    {
        cout << "Error occurred";
    }
    return 0;
}
```

### 输出

发生错误

## 嵌套 try...catch

try...catch 可以相互嵌套。以下程序说明了这一点：

```
#include<iostream>
using namespace std;
int main()
{
    try
    {
    int* arr = new int;
    try
    {
    long double* array = new long double[100000000000000000];
    }
    catch(...)
    {
    cout << "Internal error occurred";
    }
    }
    catch(...)
    {
    cout << "External Error occurred";
    }
    return 0;
}
```

### 输出

发生内部错误

很多时候，我们希望在外部捕获内部错误。对于上述程序，如果你想执行外部 catch，只需在内部 catch 中使用不带任何值的 throw 关键字抛出错误即可。

例如，请参考以下程序：

```
#include<iostream>
using namespace std;
int main()
{
    try
    {
        int* arr = new int;
        try
        {
            long double* array = new long double[1000000000000000000];
        }
        catch(...)
        {
            throw;
        }
    }
    catch(...)
    {
        cout << "External Error occurred";
    }
    return 0;
}
```

### 输出

发生外部错误

## 限制函数的异常类型

在声明函数时，可以通过在函数声明后添加 throw 后缀来限制其可能直接或间接抛出的异常类型。因此，函数可以以下列三种方式之一声明：

- return_type func_name(arg1, arg2, ...) throw(int); // 仅允许整型异常
- return_type func_name(arg1, arg2, ...) throw(char); // 仅允许字符型异常
- return_type func_name(arg1, arg2, ...) throw(); // 不允许异常
- return_type func_name(arg1, arg2, ...); // 允许所有异常

请注意，如果向 throw 传递了无参数，则不会向 catch 抛出任何异常。如果不编写 throw()，则允许所有类型的异常。

示例如下：

```
#include<iostream>
using namespace std;
void allocate_memory() throw();
void allocate_memory() throw()
{
    long double* array = new long double[10000000000000000];
}
```

```
int main()
{
    try
    {
        allocate_memory();
    }
    catch(...)
    {
        cout << "Error occurred";
    }

    return 0;
}
```

## 标准异常

针对标准情况定义了各种预定义异常。C++ 标准库甚至提供了一个专门设计的基类，用于声明作为异常抛出的对象，其名为 exception，定义在 <exception> 头文件中。该类有一个名为 what 的额外虚拟成员函数，它返回一个以空字符结尾的字符序列（char *），即一个字符串，即抛出错误的详细信息，并且可以在派生类中重写以包含某种异常描述。该类定义如下：

```
class exception
{
public:
    exception() _GLIBCXX_USE_NOEXCEPT {}
    virtual ~exception() _GLIBCXX_USE_NOEXCEPT;
/** Returns a C-style character string describing the general cause
* of the current error. */
virtual const char* what() const _GLIBCXX_USE_NOEXCEPT;
};
/** If an %exception is thrown which is not listed in a function's
 * %exception specification, one of these may be thrown. */
class bad_exception : public exception
{
public:
  bad_exception() _GLIBCXX_USE_NOEXCEPT { }
  // This declaration is not useless:
  // http://gcc.gnu.org/onlinedocs/gcc-3.0.2/gcc_6.html#SEC118
  virtual ~bad_exception() _GLIBCXX_USE_NOEXCEPT;
  // See comment in eh_exception.cc.
  virtual const char* what() const _GLIBCXX_USE_NOEXCEPT;
};
```

这些包括：

| 异常 | 描述 |
|---|---|
| bad_alloc | new 在分配失败时抛出 |
| bad_cast | dynamic_cast 在引用类型失败时抛出 |
| bad_exception | 当异常类型与任何 catch 都不匹配时抛出 |
| bad_typeid | 由 typeid 抛出 |
| ios_base::failure | 由 iostream 库中的函数抛出的失败 |

由于 bad_alloc 派生自标准基类 exception，我们可以通过捕获 exception 类的引用来处理相同的异常，其他异常也是如此。

请参考以下程序：

```
#include <iostream>
#include <exception>
using namespace std;
```
