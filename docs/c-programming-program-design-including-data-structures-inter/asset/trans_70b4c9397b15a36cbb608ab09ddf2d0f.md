

```cpp
~newString();
//Destructor
char &operator[] (int);
const char &operator[](int) const;

//overload the relational operators
bool operator==(const newString&) const;
bool operator!=(const newString&) const;
bool operator<=(const newString&) const;
bool operator<(const newString&) const;
bool operator>=(const newString&) const;
bool operator>(const newString&) const;

private:
    char *strPtr;          //pointer to the char array
                           //that holds the string
    int strLength;         //variable to store the length
                           //of the string
};
#endif
```

类 newString 有两个私有成员变量：一个用于存储 C 字符串，另一个用于存储 C 字符串的长度。

接下来，我们给出实现 newString 操作的函数定义。实现文件包含头文件 cassert，因为我们使用了函数 assert。（关于函数 assert 的说明，参见第 4 章或附录中的头文件 cassert。）

```cpp
//Implementation file myStringImp.cpp
#include <iostream>
#include <iomanip>
#include <cstring>
#include <cassert>
#include "myString.h"

using namespace std;

//Constructor: conversion from the char string to newString
newString::newString(const char *str)
{
    strLength = strlen(str);
    strPtr = new char[strLength + 1]; //allocate memory to
                                     //store the char string
    strcpy(strPtr, str); //copy string into strPtr
}

//Default constructor to store the null string
newString::newString()
{
    strLength = 0;
    strPtr = new char[1];
    strcpy(strPtr, "");
}

newString::newString(const newString& rightStr) //copy constructor
{
    strLength = rightStr.strLength;
    strPtr = new char[strLength + 1];
    strcpy(strPtr, rightStr.strPtr);
}

newString::~newString() //destructor
{
    delete [] strPtr;
}

//overload the assignment operator
const newString& newString::operator=(const newString& rightStr)
{
    if (this != &rightStr) //avoid self-copy
    {
        delete [] strPtr;
        strLength = rightStr.strLength;
        strPtr = new char[strLength + 1];
        strcpy(strPtr, rightStr.strPtr);
    }

    return *this;
}

char& newString::operator[](int index)
{
    assert(0 <= index && index < strLength);
    return strPtr[index];
}

const char& newString::operator[](int index) const
{
    assert(0 <= index && index < strLength);
    return strPtr[index];
}

//Overload the relational operators.
bool newString::operator==(const newString& rightStr) const
{
    return (strcmp(strPtr, rightStr.strPtr) == 0);
}

bool newString::operator<(const newString& rightStr) const
{
    return (strcmp(strPtr, rightStr.strPtr) < 0);
}

bool newString::operator<=(const newString& rightStr) const
{
    return (strcmp(strPtr, rightStr.strPtr) <= 0);
}

bool newString::operator>(const newString& rightStr) const
{
    return (strcmp(strPtr, rightStr.strPtr) > 0);
}

bool newString::operator>=(const newString& rightStr) const
{
    return (strcmp(strPtr, rightStr.strPtr) >= 0);
}

bool newString::operator!=(const newString& rightStr) const
{
    return (strcmp(strPtr, rightStr.strPtr) != 0);
}

//Overload the stream insertion operator <<
ostream& operator << (ostream& osObject, const newString& str)
{
    osObject << str.strPtr;

    return osObject;
}

//Overload the stream extraction operator >>
istream& operator >> (istream& isObject, newString& str)
{
    char temp[81];

    isObject >> setw(81) >> temp;
    str = temp;
    return isObject;
}
```

考虑以下语句：

`isObject >> setw(81) >> temp;`

在函数 `operator>>` 的定义中，因为 `temp` 被声明为大小为 81 的数组，所以能存储到 `temp` 中的最大字符串长度为 80。此语句（即输入语句）中的操纵符 `setw` 确保读入 `temp` 的字符不超过 80 个。

这些函数大多相当直接。下面解释重载转换构造函数、赋值运算符和复制构造函数的函数。

**转换构造函数**是一个单参数函数，它将其参数转换为构造函数所属类的对象。在我们的例子中，转换构造函数将字符串转换为 newString 类型的对象。

注意，赋值运算符仅针对 newString 类型的对象进行了显式重载。然而，如果我们想把 C 字符串存储到 newString 对象中，重载的赋值运算符也可以工作。考虑以下声明：

```cpp
newString str;
```

以及以下语句：

```cpp
str = "Hello there";
```

编译器将此语句转换为：

```cpp
str.operator=("Hello there");
```

- 1. 首先，编译器自动调用转换构造函数，创建一个 newString 类型的对象，以临时存储字符串 "Hello there"。
- 2. 其次，编译器调用重载的赋值运算符，将临时 newString 对象赋给对象 str。

因此，不必显式重载赋值运算符就能将 C 字符串存储到 newString 类型的对象中。

接下来，我们编写一个 C++ 程序，测试类 newString 的一些操作。

```cpp
//***********************************************************
// Author: D.S. Malik
//
// This program shows how to use the class newString.
//***********************************************************

#include <iostream>
#include "myString.h"

using namespace std;

int main()
{
    newString str1 = "Sunny";       //initialize str1 using
                                    //the assignment operator
    const newString str2("Warm");   //initialize str2 using the
                                    //conversion constructor

    newString str3; //initialize str3 to the empty string
    newString str4; //initialize str4 to the empty string

    cout << "Line 1: " << str1 << "      " << str2
         << "  ***" << str3 << "###." << endl;       //Line 1

    if (str1 <= str2)                //compare str1 and str2; Line 2
        cout << "Line 3: " << str1 << " is less "
             << "than or equal to" << str2 << endl;  //Line 3
    else
        cout << "Line 5: " << str2 << " is less "
             << "than " << str1 << endl;             //Line 5

    cout << "Line 6: Enter a string with a length "
         << "of at least 7: ";                       //Line 6
    cin >> str1;               //input str1;          //Line 7
    cout << endl;                                    //Line 8

    cout << "Line 9: The new value of "
         << "str1 = " << str1 << endl;               //Line 9

    str4 = str3 = "Birth Day";                       //Line 10

    cout << "Line 11: str3 = " << str3
         << ", str4 = " << str4 << endl;             //Line 11

    str3 = str1;                                     //Line 12
    cout << "Line 13: The new value of str3 = "
         << str3 << endl;                            //Line 13

    str1 = "Bright Sky";                             //Line 14

    str3[1] = str1[5];                               //Line 15
    cout << "Line 16: After replacing the second "
         << "character of str3 = " << str3 << endl;  //Line 16

    str3[5] = str2[0];                               //Line 17
    cout << "Line 18: After replacing the sixth "
         << "character of str3 = " << str3 << endl;  //Line 18

    str3[5] = 'g';                                   //Line 19
    cout << "Line 20: After replacing the sixth "
         << "character of str3 = " << str3 << endl;  //Line 20

    return 0;
}
```

示例运行：在此示例运行中，用户输入以底纹显示。

```
Line 1: Sunny    Warm  ***###.
Line 3: Sunny is less than or equal to Warm
Line 6: Enter a string with a length of at least 7: 123456789
Line 9: The new value of str1 = 123456789
Line 11: str3 = Birth Day, str4 = Birth Day
Line 13: The new value of str3 = 123456789
Line 16: After replacing the second character of str3 = 1t3456789
Line 18: After replacing the sixth character of str3 = 1t345W789
```

前面的程序按如下方式工作。第 1 行的语句输出 str1、str2 和 str3 的值。注意，str3 的值将打印在 `***` 和 `###` 之间。因为 str3 为空，所以 `***` 和 `###` 之间没有打印任何内容；参见示例运行中的第 1 行。第 2 行到第 5 行的语句比较 str1 和 str2 并输出结果。第 7 行的语句向 str1 输入一个长度至少为 7 的字符串，第 9 行的语句输出 str1 的新值。注意以下语句（见第 10 行）：

```cpp
str4 = str3 = "Birth Day";
```

因为赋值运算符的结合性是从右到左，所以先执行语句 str3 = "Birth Day";，然后执行语句 str4 = str3;。第 11 行的语句输出 str3 和 str4 的值。第 15、17 和 19 行的语句使用数组下标运算符 [] 分别操作 str3 的字符。其余语句的含义很直接。

## 函数重载

上一节讨论了运算符重载。运算符重载为程序员提供了一种简洁的表示法，使用户定义的数据类型可以像内置类型一样使用运算符。与运算符一起使用的参数类型决定要执行的操作。与运算符重载类似，C++ 允许程序员重载函数名。第 6 章介绍了函数重载。为了便于在下面的讨论中参考，让我们回顾一下这个概念。

回想一下，一个类可以有多个构造函数，但一个类的所有构造函数都具有相同的名称，即该类的名称。这是重载函数的一个例子。进一步回想，重载函数是指具有多个同名但参数列表不同的函数。参数列表决定哪个函数将执行。

要使函数重载生效，我们必须给出每个函数的定义。下一节将教你如何用单个代码段重载函数，并把为各个函数生成代码的工作留给编译器。

