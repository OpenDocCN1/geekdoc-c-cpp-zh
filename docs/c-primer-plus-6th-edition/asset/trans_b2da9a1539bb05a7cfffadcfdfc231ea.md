

# 新改进的 String 类 653

Listing 12.4 string1.h

```
// string1.h // fixed and augmented string class definition

#ifndef STRING1_H_
#define STRING1_H_
#include <iostream>
using std::ostream;
using std::istream;

class String {
private:
    char * str; // pointer to string
    int len; // length of string
    static int num_strings; // number of objects
    static const int CINLIM = 80; // cin input limit
public:
    constructors and other methods
    String(const char * s); // constructor
    String();
    String(const String &); // copy constructor
    ~String(); // destructor
    int length() const { return len; }
    // overloaded operator methods
    String &operator=(const String &);
    String &operator=(const char *);
    char &operator[](int i);
    const char &operator[](int i) const;
    // overloaded operator friends
    friend bool operator==(const String &st, const String &st2);
    friend bool operator+(const String &st1, const String &st2);
    friend bool operator+=(const String &st, const String &st2);
    friend ostream &operator<<(ostream &os, const String &st);
    friend istream &operator>>(istream &is, const String &st);
    // static function
    static int HowMany();
};

#endif
```

Listing 12.5 展示了修订后的方法定义。

# Listing 12.5 string1.cpp

```
// string1.cpp -- Class methods
#include <cstring> // string.h for some
#include "string1.h" // includes <iostream>
```

using std::cin;
using std::cout;

// initializing static class member

```
int String::num_strings = 0;
```

// static method

```
int String::HowMany() {
    return num_strings;
}
```

// class methods

```
String::String(const char * s) // construct String from C string
{
    len = std::strlen(s); // set size
    str = new char[len + 1]; // allot storage
    std::strcpy(str, s); // initialize pointer
    num_strings++; // set object count
}
```

```
String::String() // default constructor
{
    len = 4;
    str = new char[1];
    str[0] = '\0'; // default string
    num_strings++;
}
```

```
String::String(const String & st)
{
    num_strings++; // handle static member update
    len = st.len; // same length
    str = new char[len + 1]; // allot space
    std::strcpy(str, st.str); // copy string to new location
}
```

```
String::~String() // necessary destructor
{
    --num_strings; // required
    delete [] str; // required
}
```

// overloaded operator methods

// assign String to a String

# 新改进的 String 类 655

```
String &String::operator=(const String &st)
{
    if (this == &st)
        return *this;
    delete [] str;
    len = st.len;
    str = new char[len + 1];
    std::strcpy(str, st.str);
    return *this;
}
```

```
// assign a C string to a String
String &String::operator=(const char * s)
{
    delete [] str;
    len = std::strlen(s);
    str = new char[len + 1];
    std::strcpy(str, s);
    return *this;
}
```

```
// read-write char access for non-const String
char &String::operator[](int i)
{
    return str[i];
}
```

```
// read-only char access for const String
const char &String::operator[](int i) const
{
    return str[i];
}
```

```
// overloaded operator friends
bool operator<(const String &st1, const String &st2)
{
    return (std::strcmp(st1.str, st2.str) < 0);
}
```

```
bool operator>(const String &st1, const String &st2)
{
    return st2 < st1;
}
```

```
bool operator==(const String &st1, const String &st2)
{
    return (std::strcmp(st1.str, st2.str) == 0);
}
```

// Simple String output

```
ostream &operator<<(ostream & os, const String & st)
{
    os << st.str;
    return os;
}
```

// quick and dirty String input

```
istream &operator>>(istream & is, String & st)
{
    char temp[String::CINLIM];
    is.get(temp, String::CINLIM);
    if (is) {
        st = temp;
        while (is && is.get() != '\n')
            continue;
    }
    return is;
}
```

重载的 >> 运算符提供了一种简单的方法将键盘输入的一行读入 String 对象。它假设输入为 String::CINLIM 或更少字符，并丢弃超出该限制的任何字符。请记住，如果 istream 对象因某种原因失败，例如遇到文件结束条件，或在 get(char *, int) 的情况下读取空行，则其值将计算为 false。

Listing 12.6 使用一个简短的程序练习 String 类，该程序允许您输入几条字符串。程序让用户输入谚语，将字符串放入 String 对象中，显示它们，并返回最短且按字母顺序最靠前的那条。

# Listing 12.6 sayings1.cpp

```
// sayings1.cpp -- using expanded String class
// compile with string1.cpp
#include <iostream>
#include "string1.h"
const int ArSize = 10;
const int Maxlen = 8;
int main()
{
    using std::cout;
    using std::cin;
    using std::endl;
    String name;

# 新改进的 String 类 657

cout << "Hi, what's your name?\n"; 
cin >> name;
cout << " ", please enter up to " << ArSize
<< " short sayings <empty line to quit>:\n";
// array of objects
String sayings[ArSize];
char temp[MaxLen];           // temporary string storage
int i;
for (i = 0; i < ArSize; i++)
{
    cout << i+1 << ": ";
    cin.get(temp, MaxLen);
    while (cin && cin.get() != '\n')
        continue;
    if (!cin || temp[0] == '\0') // empty line?
        break;                       // i not incremented
    else
        sayings[i] = temp; // overloaded assignment
}
int total = i; // total # of lines read

if ( total > 0)
{
    cout << "Here are your sayings:\n";
    for (i = 0; i < total; i++)
        cout << sayings[i][0] << " : " << sayings[i] << endl;

int shortest = 0;
int first = 0;
for (i = 1; i < total; i++)
{
    if (sayings[i].length() < sayings[shortest].length())
        shortest = i;
    if (sayings[i] < sayings[first])
        first = i;
}

cout << "Shortest:\n" << sayings[shortest] << endl;
cout << "First alphabetically:\n" << sayings[first] << endl;
cout << "This program used " << String::HowMany()
    << " String objects. Bye.\n";
}
else
    cout << "No input! Bye.\n";
return 0;
```

# 第 12 章 类与动态内存分配

Note

旧版本的 get(char *, int) 在读取空行时不会计算为 false。对于这些版本，如果输入空行，字符串中的第一个字符为 null 字符。此示例使用以下代码：

```
if (!cin || temp[0] == '\0')    // empty line:
    break;                        // i not incremented
```

实现遵循 C++ 标准，if 语句中的第一个测试检测空行，而第二个测试则针对旧实现进行检测。

List 12.6 中的程序允许用户输入最多 10 条谚语。每条谚语读入一个临时字符数组并复制到字符串对象中。如果用户输入空白行，break 语句将终止输入循环。在回显输入后，程序使用 length() 和 operator<() 成员函数定位最短和按字母顺序最早的字符串。程序还使用下标运算符 [] 为每条谚语加上其首字母前缀。以下是示例运行：

Hi, what's your name?

>> Misty Gutz please enter up to 10 short sayings <empty line to quit>:

+   1: fool and money are soon parted
2: penny wise, pound foolish
3: the love of money is the root of much evil
4: out of sight, out of mind
5: absence makes the heart grow fonder
6: absinthe makes the heart grow fonder
7:

Here are your sayings:

+   a: fool and his money are soon parted
p: penny wise, pound foolish
t: the love of money is the root of much evil
o: out of sight, out of mind
a: absence makes the heart grow fonder
a: absinthe makes the heart grow fonder

Shortest saying:
pennny wise, pound foolish

First alphabetically:
a: fool and his money are soon parted

This program used 11 String objects. Bye.

# 使用 new 时需要注意的事项 659

## 使用 new 时需要注意的事项

到目前为止，你已经注意到在使用 new 初始化对象的指针成员时必须格外小心。特别是，你应该执行以下操作：

- 如果你在构造函数中使用 new 初始化指针成员，你应该在析构函数中使用 delete。
- new 和 delete 的使用应保持兼容。你应该将 new 与 delete 配对，将 new[] 与 delete[] 配对。
- 如果有多个构造函数，所有构造函数都应以相同的方式使用 new——要么全部使用方括号，要么都不使用。只有一个析构函数，因此所有构造函数都必须与其兼容。但是，可以在一个构造函数中使用 new 初始化指针，而在另一个构造函数中使用空指针（0，或 C++11 中的 nullptr）进行初始化，对空指针应用 delete 操作（有或没有方括号）是可以的。

### NULL 或 nullptr？

历史上，空指针可以用 0 或 NULL 表示，NULL 是在多个头文件中定义为 0 的符号常量。C 程序员经常使用 NULL 而不是 0 作为视觉提醒，表示该值是指针值，就像他们使用 '\0' 而不是 0 表示 null 字符作为视觉提醒一样。然而，C++ 传统更倾向于使用简单的 0 而不是等价的 NULL。而且，正如前面提到的，C++11 提供了 nullptr 作为更好的替代方案。

- 你应该定义一个拷贝构造函数，通过深度拷贝将一个对象初始化为另一个对象。通常，构造函数应模拟以下内容

```
String::String(const String & st)
{
    num_strings++;              // handle static member update if necessary
    len = st.len;               // same as copied string
    str = new char[len + 1];   // allot space
    std::strcpy(str, st.str);      // copy string to new location
}
```

特别是，拷贝构造函数应分配空间来保存被拷贝的数据，并应拷贝数据，而不是仅仅拷贝数据的地址。它还应更新在该过程中值会受影响的任何静态成员。

- 你应该定义一个赋值运算符，通过深度拷贝将一个对象拷贝到另一个对象。通常，类方法应模拟以下示例：

