

## 34. 模板

模板是泛型编程的基础，泛型编程是指以一种与任何特定类型无关的方式编写代码。

模板是创建泛型类或泛型函数的蓝图或公式。库容器（如迭代器和算法）就是泛型编程的示例，它们都是基于模板概念开发的。

每个容器（例如 `vector`）只有一个定义，但我们可以定义许多不同类型的向量，例如 `vector <int>` 或 `vector <string>`。

你可以使用模板来定义函数和类，下面我们看看它们是如何工作的：

### 函数模板

模板函数定义的一般形式如下所示：

```cpp
template <class type> ret-type func-name(parameter list)
{
    // body of function
}
```

这里，`type` 是函数所使用的数据类型的占位符名称。这个名称可以在函数定义中使用。

下面是一个函数模板的示例，它返回两个值中的最大值：

```cpp
#include <iostream>
#include <string>

using namespace std;

template <typename T>
inline T const& Max (T const& a, T const& b)
{
    return a < b ? b : a;
}

int main ()
{
    int i = 39;
    int j = 20;
    cout << "Max(i, j): " << Max(i, j) << endl;

    double f1 = 13.5;
    double f2 = 20.7;
    cout << "Max(f1, f2): " << Max(f1, f2) << endl;

    string s1 = "Hello";
    string s2 = "World";
    cout << "Max(s1, s2): " << Max(s1, s2) << endl;

    return 0;
}
```

如果我们编译并运行上述代码，将会产生以下结果：

```text
Max(i, j): 39
Max(f1, f2): 20.7
Max(s1, s2): World
```

### 类模板

正如我们可以定义函数模板一样，我们也可以定义类模板。泛型类声明的一般形式如下所示：

```cpp
template <class type> class class-name {
.
.
.
};
```

这里，`type` 是占位符类型名称，将在实例化类时指定。你可以使用逗号分隔的列表来定义多个泛型数据类型。

以下示例定义了类 `Stack<>`，并实现了从栈中推入和弹出元素的泛型方法：

```cpp
}
    // remove last element
    elems.pop_back();
}

template <class T>
T Stack<T>::top () const
{
    if (elems.empty()) {
        throw out_of_range("Stack<>::top(): empty stack");
    }
    // return copy of last element
    return elems.back();
}

int main()
{
    try {
        Stack<int>          intStack;  // stack of ints
        Stack<string> stringStack;    // stack of strings

        // manipulate int stack
        intStack.push(7);
        cout << intStack.top() <<endl;

        // manipulate string stack
        stringStack.push("hello");
        cout << stringStack.top() << std::endl;
        stringStack.pop();
        stringStack.pop();
    }
    catch (exception const& ex) {
        cerr << "Exception: " << ex.what() <<endl;
        return -1;
    }
}
```

如果我们编译并运行上述代码，将会产生以下结果：

```text
7

hello

Exception: Stack<>::pop(): empty stack
```

现在，如果你检查 `test.p`，它会包含大量信息，在底部你会看到替换后的值如下：

```text
$gcc -E test.cpp > test.p

...

int main ()
{

    cout << "Value of PI :" << 3.14159 << endl;

    return 0;
}
```

### 函数式宏

你可以使用 `#define` 定义一个带参数的宏，如下所示：

```cpp
#include <iostream>
using namespace std;

#define MIN(a,b) (((a)<(b)) ? a : b)

int main ()
{
    int i, j;
    i = 100;
    j = 30;
    cout << "The minimum is " << MIN(i, j) << endl;

    return 0;
}
```

如果我们编译并运行上述代码，将会产生以下结果：

```text
The minimum is 30
```

### 条件编译

有几个指令可以用来选择性地编译程序源代码的某些部分。这个过程称为条件编译。

条件预处理器结构很像 `if` 选择结构。考虑以下预处理器代码：

```cpp
#ifndef NULL

    #define NULL 0

#endif
```

你可以为了调试目的编译程序。你也可以使用一个宏来打开或关闭调试，如下所示：

```cpp
#ifdef DEBUG

    cerr << "Variable x = " << x << endl;

#endif
```

如果在指令 `#ifdef DEBUG` 之前已经定义了符号常量 `DEBUG`，这会导致 `cerr` 语句被编译到程序中。你可以使用 `#if 0` 语句来注释掉程序的一部分，如下所示：

```cpp
#if 0

    code prevented from compiling

#endif
```

让我们尝试以下示例：

```cpp
#include <iostream>

using namespace std;

#define DEBUG

#define MIN(a,b) (((a)<(b)) ? a : b)

int main ()
{

    int i, j;
    i = 100;
    j = 30;

#ifdef DEBUG

    cerr << "Trace: Inside main function" << endl;

#endif

#if 0
    /* This is commented part */
    cout << MKSTR(HELLO C++) << endl;
#endif

    cout << "The minimum is " << MIN(i, j) << endl;

#ifdef DEBUG
    cerr << "Trace: Coming out of main function" << endl;
#endif
    return 0;
}
```

如果我们编译并运行上述代码，将会产生以下结果：

```text
Trace: Inside main function

The minimum is 30

Trace: Coming out of main function
```

### # 和 ## 运算符

`#` 和 `##` 预处理器运算符在 C++ 和 ANSI/ISO C 中均可使用。`#` 运算符会将替换文本标记转换为带引号的字符串。

考虑以下宏定义：

```cpp
#include <iostream>

using namespace std;

#define MKSTR( x ) #x

int main ()
{
    cout << MKSTR(HELLO C++) << endl;

    return 0;
}
```

如果我们编译并运行上述代码，将会产生以下结果：

```text
HELLO C++
```

让我们看看它是如何工作的。不难理解，C++ 预处理器会将这一行：

```cpp
cout << MKSTR(HELLO C++) << endl;
```

转换为下面这一行：

```cpp
cout << "HELLO C++" << endl;
```

`##` 运算符用于连接两个标记。下面是一个示例：

```cpp
#define CONCAT( x, y )  x ## y
```

当 `CONCAT` 出现在程序中时，它的参数会被连接起来并用于替换宏。例如，`CONCAT(HELLO, C++)` 在程序中被替换为 `"HELLO C++"`，如下所示。

```cpp
#include <iostream>

using namespace std;

#define concat(a, b) a ## b
int main()
{
    int xy = 100;

    cout << concat(x, y);
    return 0;
}
```

如果我们编译并运行上述代码，将会产生以下结果：

```text
100
```

让我们看看它是如何工作的。不难理解，C++ 预处理器会将：

```cpp
cout << concat(x, y);
```

```text
Value of __LINE__ : 6
Value of __FILE__ : test.cpp
Value of __DATE__ : Feb 28 2011
Value of __TIME__ : 18:52:48
```

## 36. 信号处理

信号是操作系统传递给进程的中断，它可能会提前终止程序。你可以在 UNIX、LINUX、Mac OS X 或 Windows 系统上按 Ctrl+C 来产生中断。

有些信号无法被程序捕获，但以下列表中的信号你可以捕获，并根据信号采取适当的操作。这些信号在 C++ 头文件 `<csignal>` 中定义。

| 信号 | 描述 |
| --- | --- |
| SIGABRT | 程序的异常终止，例如调用 `abort`。 |
| SIGFPE | 错误的算术运算，例如除以零或导致溢出的运算。 |
| SIGILL | 检测到非法指令。 |
| SIGINT | 接收到交互式注意信号。 |
| SIGSEGV | 对存储器的无效访问。 |
| SIGTERM | 发送给程序的终止请求。 |

### signal() 函数

C++ 信号处理库提供了 `signal` 函数来捕获意外事件。以下是 `signal()` 函数的语法：

```cpp
void (*signal (int sig, void (*func)(int)))(int);
```

简单来说，这个函数接收两个参数：第一个参数是一个整数，表示信号编号；第二个参数是指向信号处理函数的指针。

让我们编写一个简单的 C++ 程序，使用 `signal()` 函数捕获 `SIGINT` 信号。无论你想在程序中捕获什么信号，都必须使用 `signal` 函数注册该信号，并将其与信号处理器关联起来。请看下面的示例：

```cpp
#include <iostream>
```

![](img/7976f323fd1a5c8774f95fbf029a106f_281_0.png)

