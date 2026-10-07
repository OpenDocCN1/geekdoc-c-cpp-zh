

# 新型改进型 String 类 653

Listing 12.4 string1.h

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
