
有了此定义，语句 `cout << opera[4];` 变为 `cout << opera.operator[][4];`

返回值是 `opera.str[4]`，即字符 'M'。因此，公共方法提供了访问私有数据的权限。

将返回类型声明为 `char &` 允许你为特定元素赋值。例如，你可以使用：

第二个语句转换为 `means.operator[](0] = 'r';`

返回值是 `opera.str[4]`，即字符 'M'。因此，公共方法提供了访问私有数据的权限。

将返回类型声明为 `char &` 允许你为特定元素赋值。例如，你可以使用：

第二个语句转换为 `means.operator[](0] = 'r';`

返回值是 `opera.str[4]`，即字符 'M'。因此，公共方法提供了访问私有数据的权限。

将返回类型声明为 `char &` 允许你为特定元素赋值。例如，你可以使用：

第二个语句转换为 `means.operator[](0] = 'r';`

返回值是 `opera.str[4]`，即字符 'M'。因此，公共方法提供了访问私有数据的权限。

将返回类型声明为 `char &` 允许你为特定元素赋值。例如，你可以使用：

第二个语句转换为 `means.operator[](0] = 'r';`

返回值是 `opera.str[4]`，即字符 'M'。因此，公共方法提供了访问私有数据的权限。

# 新型改进型 String 类 653

## Listing 12.4 string1.h

```cpp
// string1.h // 修复并增强的 String 类定义

#ifndef STRING1_H_

#define STRING1_H_

#include <iostream>

using std::ostream;

using std::istream;

class String {
private:
    char * str; // 字符串指针
    int len; // 字符串长度
    static int num strings; // 对象数量
    static const int CINLIM = 80; // cin 输入限制
public:
    // 构造函数和其他方法
    String(const char * s); // 构造函数
    String();
    String(const String &); // 拷贝构造
    ~String(); // 析构函数
    int length() const { return len; }
    // 重载运算符方法
    String &operator=(const String &);
    String &operator=(const char *);
    char &operator[](int i);
    const char &operator[](int i) const;
    // 重载运算符友
    friend bool operator==(const String &st, const String &st2);
    friend bool operator+(const String &st1, const String &st2);
    friend bool operator+=(const String &st, const String &st2);
    friend ostream &operator<<(ostream &os, const String &st);
    friend istream &operator>>(istream &is, const String &st);
    // 静态函数
    static int HowMany();
};
#endif
```

Listing 12.5 展示了修改后的方法定义。

# Listing 12.5 string1.cpp

```cpp
// string1.cpp -- 类方法
#include <cstring> // 部分功能需要的 string.h
#include "string1.h" // 包含 <iostream>
```

using std::cin;
using std::cout;

// 初始化静态类成员

```cpp
int String::num_strings = 0;
```

// 静态方法

```cpp
int String::HowMany() {
    return num_strings;
}
```

// 类方法

```cpp
String::String(const char * s) // 从 C 字符串构造 String
{
    len = std::strlen(s); // 设置大小
    str = new char[len + 1]; // 分配存储
    std::strcpy(str, s); // 初始化指针
    num_strings++; // 设置对象计数
}
```

```cpp
String::String() // 默认构造函数
{
    len = 4;
    str = new char[1];
    str[0] = '\0'; // 默认字符串
    num_strings++;
}
```

```cpp
String::String(const String & st)
{
    num_strings++; // 处理静态成员更新
    len = st.len; // 相同长度
    str = new char[len + 1]; // 分配空间
    std::strcpy(str, st.str); // 将字符串拷贝到新位置
}
```

```cpp
String::~String() // 必要的析构函数
{
    --num_strings; // 需要
    delete [] str; // 需要
}
```

// 重载运算符方法
// 将 String 赋值给 String

# 新型改进型 String 类 655

```cpp
String &String::operator=(const String &st)
{
    if (this == &st)
        return *this;
    delete [] str;
    len = len + 1;
    str = new char[len + 1];
    std::strcpy(str, st.str);
    return *this;
}
```

```cpp
// 将 C 字符串赋值给 String
String &String::operator=(const char * s)
{
    delete [] str;
    len = std::strlen(s);
    str = new char[len + 1];
    std::strcpy(str, s);
    return *this;
}
```

```cpp
// 非 const 类型 String 的读写字符访问
char &String::operator[](int i)
{
    return str[i];
}
```

```cpp
// const 类型 String 的只读字符访问
const char &String::operator[](int i) const
{
    return str[i];
}
```

```cpp
// 重载运算符友
bool operator<(const String &st1, const String &st2)
{
    return (std::strcmp(st1.str, st2.str) < 0);
}
```

```cpp
bool operator>(const String &st1, const String &st2)
{
    return st2 < st1;
}
```

```cpp
bool operator===(const String &st1, const String &st2)
{
    return (std::strcmp(st1.str, st2.str) == 0);
}
```

// 简单的 String 输出

```cpp
ostream &operator<<(ostream & os, const String &st)
{
    os << st.str;
    return os;
}
```

// 快速的 String 输入

```cpp
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

重载的 `>>` 运算符提供了一种将键盘输入读取到 String 对象的简单方法。它假设输入字符为 `String::CINLIM` 或少，并丢弃任何超出限制的字符。请记住，如果 `istream` 对象由于某种原因失败（例如遇到文件末尾条件，或者在 `get(char *, int)` 情况下读取到空行），则其值将求值为虚假。

Listing 12.6 通过一个短程序测试 String 类，该程序允许你输入几个字符串。程序让用户输入格言，将字符串放入 String 对象中，显示它们，并返回最短且按字母顺序最靠前的字符串。

# Listing 12.6 sayings1.cpp

```cpp
// sayings1.cpp -- 使用扩展的 String 类
// 使用 string1.cpp 编译
#include <iostream>
#include "string.h"
const int ArSize = 10;
const int Maxlen = 8;
int main()
{
    using std::cout;
    using std::cin;
    using std::endl;
    String name;
    cout << "Hi, what's your name?\n"; 
    cin >> name;
    String sayings[ArSize];
    int count = 0;
    for (int i = 0; i < ArSize; i++)
    {
        cout << "Enter saying " << i + 1 << ": ";
        if (cin >> sayings[i])
        {
            count++;
        }
        else
        {
            break;
        }
    }
    if (count > 0)
    {
        cout << "\nYou entered these sayings:\n";
        for (int i = 0; i < count; i++)
        {
            cout << sayings[i] << "\n";
        }
        int shortest = 0;
        for (int i = 1; i < count; i++)
        {
            if (sayings[i].length() < sayings[shortest].length())
            {
                shortest = i;
            }
            else if (sayings[i].length() == sayings[shortest].length())
            {
                if (sayings[i] < sayings[shortest])
                {
                    shortest = i;
                }
            }
        }
        cout << "\nThe shortest saying is: " << sayings[shortest] << "\n";
    }
    else
    {
        cout << "No sayings were entered.\n";
    }
    return 0;
}
```

# 第 12 章 类与动态内存分配

```cpp
String & String::operator=(const String & st)
{
    if (this == &st) // 对象赋值给自身
        return *this; // 全部完成
    delete [] str; // 释放旧字符串
    len = str.len;
    str = new char[len + 1]; // 为新字符串获取空间
    std::strcpy(str, st.str); // 拷贝字符串
    return *this; // 返回调用对象的引用
}
```

特别地，该方法应该检查自赋值；它应该释放成员指针指向的内存；它应该拷贝数据而不仅仅是数据的地址；并且它应该返回调用对象的引用。

# 准则与禁止（Don's and Dos）

以下摘录包含了两个错误做法的示例和一个良好构造函数的示例：

```cpp
String::String()
{
    str = "default string"; // 哎呀，没有使用 new []
    len = std::strlen(str);
}
```

```cpp
String::String(const char * s)
{
    len = std::strlen(s);
    str = new char; // 哎呀，没有 []
    std::strcpy(str, s); // 哎呀，没有空间
}
```

```cpp
String::String(const String & st)
{
    len = st.len;
    str = new char[len + 1]; // 好，分配了空间
    std::strcpy(str, st.str); // 好，拷贝值
}
```

第一个构造函数没有初始化 `str`。当为默认对象调用析构函数时，会对 `str` 执行 `delete`。对一个由 `str` 初始化的指针应用 `delete` 的结果是未定义的，而且可能很糟糕。以下任何一种做法都是正确的：

```cpp
String::String()
{
    len = 0;
    str = new char[1]; // 使用了带 [] 的 new
}
```

# 在构造函数中使用 new 的注意事项 第661 页

```cpp
String::String()
{
  len = 0; // 或者在 C++11 中，str = nullptr;
}
```

```cpp
String::String()
{
  static const char * s = "C++"; // 只初始化一次
  len = std::strlen(str);
  str = new char[len + 1]; // 使用了带 [] 的 new
  std::strcpy(str, s);
}
```

接下来，原始摘录中的第二个构造函数应用了 `new`，但它没有请求正确的内存量；因此 `new` 返回了一个仅包含一个字符空间的内存块。尝试向该位置拷贝更长的字符串是在制造内存问题。此外，不带括号的 `new` 使用与其他构造函数的正确形式不一致。

第三个构造函数很好。

最后，这是一个与之前的构造函数无法正常工作的析构函数：

```cpp
String::~String()
{
  delete str; // 哎呀，应该是 delete [] str;
}
```

析构函数错误地使用了 `delete`。由于构造函数请求的是字符数组，析构函数应该删除数组。

# 含有类成员的类的逐成员拷贝

假设你使用 `String` 类，或者为了方便，使用标准 `string` 类作为类成员类型：

```cpp
class Magazine
{
private:
  String title;
  string publisher;
};
```
