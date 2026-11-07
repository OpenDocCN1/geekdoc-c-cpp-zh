

## 代码清单 12.1 **strngbad.h**

```cpp
// strngbad.h -- flawed string class definition
#include <iostream>
#ifndef STRNGBAD_H
#define STRNGBAD_H
class StringBad
{
private:
    char * str;             // pointer to string
    int len;                // length of string
    static int num_strings; // number of objects
public:
    StringBad(const char * s); // constructor
    StringBad();              // default constructor
    ~StringBad();             // destructor
// friend function
    friend std::ostream & operator<<(std::ostream & os,
                          const StringBad & st);
};
#endif
```

为什么要将这个类命名为 StringBad？这是为了提醒你：StringBad 是一个开发中的示例。它是使用动态内存分配开发类的第一阶段，并且它把显而易见的事情做对了；例如，它在构造函数和析构函数中正确地使用了 new 和 delete。它并没有真正做坏事，但该设计遗漏了一些必要且完全不明显的额外好做法。看到这个类存在的问题，应该有助于你理解并记住以后将它转换为功能更完整的 String 类时将要进行的不明显改动。

关于这个声明，你应注意两点。第一，它使用指向 char 的指针而不是 char 数组来表示名称。这意味着类声明不会为字符串本身分配存储空间。相反，它在构造函数中使用 new 为字符串分配空间。这种安排避免用预定义的字符串大小限制来束缚类声明。

第二，该定义将 num_strings 成员声明为属于静态存储类。静态类成员有一个特殊性质：无论创建多少个对象，程序都只创建静态类变量的一个副本。也就是说，静态成员在该类的所有对象之间共享，就像电话号码可能由家庭所有成员共享一样。例如，如果创建 10 个 StringBad 对象，就会有 10 个 str 成员和 10 个 len 成员，但只有一个共享的 num_strings 成员（见图 12.1）。对于应当对类私有、但对所有类对象都应具有相同值的数据来说，这很方便。例如，num_strings 成员旨在跟踪已创建对象的数量。

```cpp
// construct StringBad from C string
StringBad::StringBad(const char * s)
{
    len = std::strlen(s);              // set size
    str = new char[len + 1];           // allot storage
    std::strcpy(str, s);               // initialize pointer
    num_strings++;                     // set object count
    cout << num_strings << ": \"" << str
         << "\" object created\n";   // For Your Information
}

StringBad::StringBad()                 // default constructor
{
    len = 4;
    str = new char[4];
    std::strcpy(str, "C++");           // default string
    num_strings++;
    cout << num_strings << ": \"" << str
         << "\" object created\n";     // FYI
}

StringBad::~StringBad()                // necessary destructor
{
    cout << "\"" << str << "\" object deleted, "; // FYI
    --num_strings;                      // required
    cout << num_strings << " left\n";   // FYI
    delete [] str;                      // required
}

std::ostream & operator<<(std::ostream & os, const StringBad & st)
{
    os << st.str;
    return os;
}
```

首先，请注意代码清单 12.2 中的以下语句：

```cpp
int StringBad::num_strings = 0;
```

这条语句将静态成员 num_strings 初始化为 0。注意，不能在类声明内部初始化静态成员变量。这是因为类声明描述内存应如何分配，但并不分配内存。你通过使用该格式创建对象来分配并初始化内存。对于静态类成员，你要在类声明之外用一条单独的语句独立初始化该静态成员。这是因为静态类成员是单独存储的，而不是作为对象的一部分存储。注意，初始化语句给出了类型并使用作用域运算符，但没有使用 static 关键字。该初始化放在方法文件中，而不是类声明文件中。这是因为类声明位于头文件中，而一个程序可能在多个其他文件中包含同一个头文件。那样会导致初始化语句出现多个副本，而这是错误的。

类声明内不初始化静态数据成员这一规则的例外情况（见第 10 章“对象和类”）是：静态数据成员为整型或枚举类型的 const 时。

> **注意**
>
> 静态数据成员在类声明中声明，并在包含类方法的文件中初始化。初始化时使用作用域运算符来指明该静态成员属于哪个类。然而，如果静态成员是 const 整型或枚举类型，则可以在类声明本身中初始化。

接下来，注意每个构造函数都包含表达式 num_strings++。这确保每当程序创建新对象时，共享变量 num_strings 就增加 1，从而跟踪 String 对象的总数。此外，析构函数包含表达式 --num_strings。因此，String 类也会跟踪被删除的对象，使 num_strings 成员的值保持最新。

现在来看代码清单 12.2 中的第一个构造函数，它用常规 C 字符串初始化一个 String 对象：

```cpp
StringBad::StringBad(const char * s)
{
    len = std::strlen(s);          // set size
    str = new char[len + 1];       // allot storage
    std::strcpy(str, s);           // initialize pointer
    num_strings++;                 // set object count
    cout << num_strings << ": \"" << str
         << "\" object created\n"; // For Your Information
}
```

回想一下，类中的 str 成员只是一个指针，因此构造函数必须提供用于保存字符串的内存。初始化对象时，可以将字符串指针传递给构造函数：

```cpp
String boston("Boston");
```

然后，构造函数必须分配足够的内存来保存该字符串，并且必须将该字符串复制到那个位置。让我们一步一步地梳理这个过程。

首先，该函数初始化 len 成员，使用 strlen() 函数计算字符串的长度。接着，它使用 new 分配足够的空间来保存字符串，然后将新内存的地址赋给 str 成员。（回想一下，strlen() 返回字符串的长度，不计结尾空字符，因此构造函数给 len 加 1，以便为字符串（包括空字符）留出空间。）接下来，构造函数使用 `strcpy()` 将传入的字符串复制到新内存中。然后它更新对象计数。最后，为了帮助你监视正在发生的情况，构造函数显示当前对象数量以及对象中存储的字符串。这个特性在以后我们故意让 StringBad 类陷入麻烦时会派上用场。

要理解这种方法，你应认识到字符串并不存储在对象中。字符串单独存储在堆内存中，对象只存储告诉你在哪里找到该字符串的信息。

注意，不要使用下面这种写法：

```cpp
str = s;    // not the way to go
```

这只是存储地址，而没有复制字符串。

默认构造函数的行为类似，只是它提供默认字符串 "C++"。

析构函数包含了这个示例对类处理方式最重要的补充：

```cpp
StringBad::~StringBad()              // necessary destructor
{
    cout << "\"" << str << "\" object deleted, ";    // FYI
    --num_strings;                      // required
    cout << num_strings << " left\n";   // FYI
    delete [] str;                      // required
}
```

析构函数一开始会宣布析构函数何时被调用。这部分提供信息，但并非必需。然而，delete 语句至关重要。回想一下，str 成员指向用 new 分配的内存。当 StringBad 对象过期时，str 指针也会过期。但是，除非使用 delete 释放 str 所指向的内存，否则该内存仍保持已分配状态。删除对象会释放对象本身占用的内存，但不会自动释放曾作为对象成员的指针所指向的内存。为此，必须使用析构函数。通过将 delete 语句放在析构函数中，可以确保构造函数用 new 分配的内存在对象过期时被释放。

## 警告

每当在构造函数中使用 `new` 分配内存时，都应该在对应的析构函数中使用 `delete` 释放该内存。如果使用 `new []`（带方括号），则应使用 `delete []`（带方括号）。

代码清单 12.3 取自 *《每日蔬菜》* 正在开发的一个程序，它说明了 StringBad 构造函数和析构函数在何时以及如何工作。该程序将对象声明放在内层块中，因为当执行离开定义对象的块时，析构函数就会被调用。如果没有内层块，析构函数将在执行离开 `main()` 后被调用，这会在某些环境中导致你无法在执行窗口关闭前看到析构函数消息。请务必将代码清单 12.2 与代码清单 12.3 一起编译。

