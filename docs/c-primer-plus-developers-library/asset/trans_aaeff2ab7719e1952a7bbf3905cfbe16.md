

```cpp
return true;
else
    return false;
}
```

因为内置的 < 运算符已经返回 bool 类型的值，所以你可以进一步将代码简化如下：

```cpp
bool operator<(const String &st1, const String &st2)
{
    return (std::strcmp(st1.str, st2.str) < 0);
}
```

同样，你可以像下面这样编写另外两个比较函数：

```cpp
bool operator>(const String &st1, const String &st2)
{
    return st2 < st1;
}
bool operator==(const String &st1, const String &st2)
{
    return (std::strcmp(st1.str, st2.str) == 0);
}
```

第一个定义用 < 运算符来表达 > 运算符，对于内联函数来说会是一个不错的选择。

将比较函数声明为友元，便于在 String 对象和常规 C 字符串之间进行比较。例如，假设 answer 是一个 String 对象，并且你有如下代码：

```cpp
if ("love" == answer)
```

这会被转换为如下代码：

```cpp
if (operator==("love", answer))
```

然后编译器会使用某个构造函数将代码实际转换为：

```cpp
if (operator==(String("love"), answer))
```

这样就能与原型匹配。

## 使用方括号表示法访问字符

对于标准的 C 风格字符串，你可以使用方括号来访问单个字符：

```cpp
char city[40] = "Amsterdam";
cout << city[0] << endl; // display the letter A
```

在 C++ 中，两个方括号符号构成单个运算符，即方括号运算符，你可以通过名为 operator[]() 的方法重载这个运算符。通常，二元 C++ 运算符（有两个操作数的运算符）会把运算符放在两个操作数之间，例如 2 + 5。但方括号运算符会把一个操作数放在第一个方括号之前，把另一个操作数放在两个方括号之间。因此，在表达式 `city[0]` 中，city 是第一个操作数，`[]` 是运算符，0 是第二个操作数。

假设 opera 是一个 string 对象：

```cpp
String opera("The Magic Flute");
```

如果你使用表达式 `opera[4]`，C++ 会查找具有以下名称和签名的方法：

```cpp
String::operator[](int i)
```

如果找到匹配的原型，编译器会把表达式 `opera[4]` 替换为以下函数调用：

```cpp
opera.operator[](4)
```

opera 对象调用该方法，数组下标 4 成为函数实参。

下面是一个简单的实现：

```cpp
char & String::operator[](int i)
{
    return str[i];
}
```

根据这个定义，语句

```cpp
cout << opera[4];
```

会变成：

```cpp
cout << opera.operator[](4);
```

返回值是 `opera.str[4]`，也就是字符 'M'。因此，这个公有方法提供了对私有数据的访问。

将返回类型声明为 `char &` 类型，允许你为特定元素赋值。例如，你可以使用以下代码：

```cpp
String means("might");
means[0] = 'r';
```

第二条语句会被转换为重载运算符函数调用：

```cpp
means.operator[](0) = 'r';
```

这会把 'r' 赋给该方法的返回值。但该函数返回的是对 `means.str[0]` 的引用，因此这段代码等价于

```cpp
means.str[0] = 'r';
```

最后这行代码违反了私有访问规则，但由于 `operator[]()` 是类方法，因此允许修改数组内容。这段代码的最终效果是 "might" 变成 "right"。

假设你有一个常量对象：

```cpp
const String answer("futile");
```

那么，如果 operator[]() 唯一可用的定义就是你刚才看到的那个，以下代码会被标记为错误：

```cpp
cout << answer[1];  // compile-time error
```

原因是 answer 是 const 的，而该方法没有承诺不修改数据。（事实上，有时方法的工作就是修改数据，因此它不能承诺不修改。）

然而，C++ 在重载时会区分 const 和非 const 函数签名，因此你可以提供第二个版本的 operator[]()，仅供 const String 对象使用：

```cpp
// for use with const String objects
const char & String::operator[](int i) const
{
    return str[i];
}
```

有了这些定义，你就可以对常规 String 对象进行读/写访问，对 const String 数据进行只读访问：

```cpp
String text("Once upon a time");
const String answer("futile");
cout << text[1];      // ok, uses non-const version of operator[]()
cout << answer[1];    // ok, uses const version of operator[]()
cin >> text[1];       // ok, uses non-const version of operator[]()
cin >> answer[1];     // compile-time error
```

## 静态类成员函数

可以将成员函数声明为静态的。（如果函数定义是分开的，关键字 static 应出现在函数声明中，而不是函数定义中。）这有两个重要结果。

首先，静态成员函数不必由对象来调用；事实上，它甚至没有 this 指针可供使用。如果静态成员函数声明在公有部分，则可以使用类名和作用域解析运算符来调用它。例如，你可以给 String 类一个名为 HowMany() 的静态成员函数，并在类声明中使用以下原型/定义：

```cpp
static int HowMany() { return num_strings; }
```

它可以像这样调用：

```cpp
int count = String::HowMany();   // invoking a static member function
```

第二个结果是，由于静态成员函数不与特定对象关联，因此它只能使用静态数据成员。例如，`HowMany()` 静态方法可以访问 `num_strings` 静态成员，但不能访问 `str` 或 `len`。

同样，静态成员函数可用于设置一个类级标志，用来控制类接口某方面的行为。例如，它可以控制某个显示类内容的方法所使用的格式。

## 进一步重载赋值运算符

在查看 String 类示例的新清单之前，让我们先考虑另一个问题。假设你想把一个普通字符串复制到一个 String 对象中。例如，假设你使用 `getline()` 读取一个字符串，并想把它放入一个 String 对象。类方法已经允许你这样做：

```cpp
String name;
char temp[40];
cin.getline(temp, 40);
name = temp;  // use constructor to convert type
```

然而，如果你必须经常这样做，这可能不是一个令人满意的解决方案。为了了解原因，让我们回顾一下最后一条语句是如何工作的：

- 1. 程序使用 `String(const char *)` 构造函数构造一个临时 String 对象，其中包含 `temp` 中所存字符串的副本。请记住，在第 11 章“使用类”中，带单个实参的构造函数充当转换函数。
- 2. 在本章后面的清单 12.6 中，程序使用 `String & String::operator=(const String &)` 函数将信息从临时对象复制到 name 对象。
- 3. 程序调用 `~String()` 析构函数来删除临时对象。

使这个过程更高效的最简单方法是重载赋值运算符，使其直接处理普通字符串。这样就去掉了创建和销毁临时对象的额外步骤。下面是一种可能的实现：

```cpp
String & String::operator=(const char * s)
{
    delete [] str;
    len = std::strlen(s);
    str = new char[len + 1];
    std::strcpy(str, s);
    return *this;
}
```

像往常一样，你必须释放原先由 `str` 管理的内存，并为新字符串分配足够的内存。

清单 12.4 展示了修订后的类声明。除了已经提到的更改之外，它还定义了常量 `CINLIM`，该常量用于实现 `operator>>()`。

### 清单 12.4 **string1.h**

```cpp
// string1.h -- fixed and augmented string class definition

#ifndef STRING1_H
#define STRING1_H
#include <iostream>
using std::ostream;
using std::istream;

class String
{
private:
    char * str;             // pointer to string
    int len;                // length of string
    static int num_strings; // number of objects
    static const int CINLIM = 80; // cin input limit
public:
// constructors and other methods
    String(const char * s);       // constructor
    String();                     // default constructor
    String(const String &);       // copy constructor
    ~String();                   // destructor
    int length() const { return len; }
// overloaded operator methods
    String & operator=(const String &);
    String & operator=(const char *);
    char & operator[](int i);
    const char & operator[](int i) const;
// overloaded operator friends
    friend bool operator<(const String &st, const String &st2);
    friend bool operator>(const String &st, const String &st2);
    friend bool operator==(const String &st, const String &st2);
    friend ostream & operator<<(ostream & os, const String & st);
    friend istream & operator>>(istream & is, String & st);
// static function
    static int HowMany();
};
#endif
```

清单 12.5 给出了修订后的方法定义。

### 清单 12.5 **string1.cpp**

```cpp
// string1.cpp -- String class methods
#include <cstring>              // string.h for some
#include "string1.h"            // includes <iostream>
```

