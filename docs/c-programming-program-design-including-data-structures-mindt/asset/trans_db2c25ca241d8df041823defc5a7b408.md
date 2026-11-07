

```cpp
class classTest
{
public:
    Type& operator[](int index);
        //Overload the operator for nonconstant arrays
    const Type& operator[](int index) const;
        //Overload the operator for constant arrays
    .
    .
    .
private:
    Type *list; //pointer to the array
    int arraySize;
};
```

其中，`Type` 是数组元素的数据类型。

用于为 `classTest` 重载运算符 `[]` 的函数定义如下：

```cpp
    //Overload the operator [] for nonconstant arrays
Type& classTest::operator[](int index)
{
    assert(0 <= index && index < arraySize);
    return list[index]; //return a reference to the
                        //array component
}
```

```cpp
    //Overload the operator [] for constant arrays
const Type& classTest::operator[](int index) const
{
    assert(0 <= index && index < arraySize);
    return list[index]; //return a reference to the
                        //array component
}
```

> **注意**
>
> 上述函数定义使用了 `assert` 语句。（有关 `assert` 语句的解释，请参阅第 4 章或附录。）

考虑以下语句：

```cpp
classTest list1;
classTest list2;
const classTest list3;
```

对于以下语句：

```cpp
list1[2] = list2[3];
```

会执行用于非 const 数组的运算符函数 `operator[]` 的函数体。对于以下语句：

```cpp
list1[2] = list3[5];
```

首先，由于 `list3` 是一个 const 数组，会执行用于 const 数组的运算符函数 `operator[]` 的函数体。接着，为完成对 `list1` 的赋值语句，会执行用于非 const 数组的运算符函数 `operator[]` 的函数体。

## 编程示例：newString

第 8 章讨论了 C 字符串。回顾如下：

1. C 字符串是一个或多个字符组成的序列。
2. C 字符串用双引号括起来。
3. C 字符串以空字符结尾。
4. C 字符串存储在字符数组中。

C 字符串允许执行的聚合操作只有输入和输出。若要使用其他操作，程序员需要包含头文件 `cstring`，该文件包含许多字符串处理函数的声明。

最初，C++ 没有提供任何用于处理 C 字符串的内置数据类型。不过，较新版本的 C++ 提供了一个字符串类，用于处理 C 字符串以及对 C 字符串执行的操作。

本示例的目标是定义一个用于 C 字符串处理的自定义类，同时进一步说明运算符重载。更具体地说，我们重载赋值运算符、关系运算符以及流插入和提取运算符，以便进行简单的输入和输出。我们将此类命名为 `newString`。首先，给出类 `newString` 的定义：

```cpp
#include <iostream>
using namespace std;

class newString
{
    //Overload the stream insertion and extraction operators.
    friend ostream& operator<< (ostream&, const newString&);
    friend istream& operator>> (istream&, newString&);

public:
    const newString& operator=(const newString&);
    //overload the assignment operator
    newString(const char *);
    //constructor; conversion from the char string
    newString();
    //Default constructor to initialize the string to nullptr
    newString(const newString&);
    //Copy constructor
    ~newString();
    //Destructor

    char& operator[](int);
    const char& operator[](int) const;

    //overload the relational operators
    bool operator==(const newString&) const;
    bool operator!=(const newString&) const;
    bool operator<=(const newString&) const;
    bool operator>=(const newString&) const;
    bool operator<(const newString&) const;
    bool operator>(const newString&) const;

private:
    char* strcopy(const char *str2);
    char* strcopy(char * str1, const char *str2);

    char* strPtr;      //pointer to the char array
                       //that holds the string
    int strLength;     //variable to store the length
                       //of the string
};
```

`newString` 类有两个私有成员变量：一个用于存储 C 字符串，另一个用于存储 C 字符串的长度。如第 8 章所述，在许多编译器中，用于将一个字符数组复制到另一个字符数组的函数 `strcpy` 已被弃用，而函数 `strncpy` 可能尚未实现。因此，我们包含了重载的私有成员函数 `strcopy`，用于将一个字符数组复制到 `strPtr` 中。

接下来，给出用于实现 `newString` 操作的函数定义。由于使用了函数 `assert`，实现文件包含头文件 `cassert`。（有关函数 `assert` 的解释，请参阅第 4 章或附录中的头文件 `cassert`。我们假设类 `newString` 的定义位于头文件 `myString.h` 中。）

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

    strcopy(str);
}

//Default constructor to store the null string
newString::newString()
{
    strLength = 0;
    strPtr = new char[1];
    strPtr[0] = '\0';
}

//copy constructor
newString::newString(const newString& rightStr)
{
    strLength = rightStr.strLength;
    strPtr = new char[strLength + 1];
    strcopy(rightStr.strPtr);
}

newString::~newString()  //destructor
{
    delete [] strPtr;
}

//overload the assignment operator
const newString& newString::operator=(const newString& rightStr)
{
    if (this != &rightStr)  //avoid self-copy
    {
        delete [] strPtr;
        strLength = rightStr.strLength;
        strPtr = new char[strLength + 1];
        strcopy(rightStr.strPtr);
    }
    return *this;
}

char& newString::operator[] (int index)
{
    assert(0 <= index && index < strLength);
    return strPtr[index];
}

const char& newString::operator[] (int index) const
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
ostream& operator<<(ostream& osObject, const newString& str)
{
    osObject << str.strPtr;

    return osObject;
}

//Overload the stream extraction operator >>
istream& operator>> (istream& isObject, newString& str)
{
    char temp[81];

    isObject >> setw(81) >> temp;
    str = temp;
    return isObject;
}

char* newString::strcopy(const char *str)
{
    for (int i = 0; i < strLength; i++)
        strPtr[i] = str[i];
    strPtr[strLength] = '\0';

    return strPtr;
}

char* newString::strcopy(char * str1, const char *str2)
{
    for (int i = 0; i < strlen(str2); i++)
        str1[i] = str2[i];
    str1[strlen(str2)] = '\0';

    return str1;
}
```

请注意函数 `operator>>` 定义中的语句：

```cpp
isObject >> setw(81) >> temp;
```

由于 `temp` 被声明为大小为 81 的数组，因此能够存储到 `temp` 中的最大字符串长度为 80。该语句（即输入语句）中的操纵器 `setw` 确保读入 `temp` 的字符数不会超过 80 个。

这些函数中的大多数都相当直观。下面解释用于重载转换构造函数、赋值运算符和复制构造函数的函数。

转换构造函数是一个单参数函数，用于将其参数转换为该构造函数所属类的对象。在本例中，转换构造函数将一个字符串转换为 `newString` 类型的对象。

请注意，赋值运算符只针对 `newString` 类型的对象进行了显式重载。但是，如果希望将 C 字符串存储到 `newString` 对象中，重载后的赋值运算符同样可以工作。考虑以下声明：

```cpp
newString str;
```

以及以下语句：

```cpp
str = "Hello there";
```

编译器会将此语句转换为：

```cpp
str.operator=("Hello there");
```

1. 首先，编译器自动调用转换构造函数，创建一个 `newString` 类型的对象，用于临时存储字符串 `"Hello there"`。
2. 其次，编译器调用重载后的赋值运算符，将临时的 `newString` 对象赋值给对象 `str`。

