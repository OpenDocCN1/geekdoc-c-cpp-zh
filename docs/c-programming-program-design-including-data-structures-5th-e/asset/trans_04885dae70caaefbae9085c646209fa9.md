
## 编程示例：`newString`

第9章讨论了C字符串。回想一下：

- 1. C字符串是一个或多个字符的序列。
- 2. C字符串用双引号括起来。
- 3. C字符串以空字符结尾。
- 4. C字符串存储在字符数组中。

允许对C字符串进行的唯一聚合操作是输入和输出。要使用其他操作，程序员需要包含头文件 cstring，其中包含许多用于字符串操作的函数的规范。

最初，C++没有提供任何内置数据类型来处理C字符串。然而，较新版本的C++提供了一个 string 类来处理C字符串以及对C字符串的操作。

本示例的目标是定义我们自己的类来进行C字符串操作，同时进一步说明运算符重载。更具体地说，我们重载赋值运算符、关系运算符以及流插入和提取运算符，以便于输入和输出。我们将这个类称为 `newString`。首先，我们给出类 `newString` 的定义：

```cpp
    //Header file myString.h
    #ifndef H_myString
    #define H_myString

    #include <iostream>

    using namespace std;

    class newString
    {
        //Overload the stream insertion and extraction operators.
        friend ostream& operator << (ostream&, const newString&);
        friend istream& operator >> (istream&, newString&);

    public:
        const newString& operator=(const newString&);
        //Overload the assignment operator
        newString(const char *);
        //constructor: conversion from the char string
        newString();
        //Default constructor to initialize the string to null
        //Copy constructor
        ~newString();
        //Destructor
        char & operator[] (int);
        const char &operator[](int) const;

        //Overload the relational operators
        bool operator==(const newString&) const;
        bool operator!=(const newString&) const;
        bool operator<(const newString&) const;
        bool operator<=(const newString&) const;
        bool operator>(const newString&) const;
        bool operator>=(const newString&) const;

    private:
        char *strPtr;      //pointer to the char array
                           //that holds the string
        int strLength;     //variable to store the length
                           //of the string
    };

    #endif
```

**类** newString 有两个私有成员变量：一个存储C字符串，一个存储C字符串的长度。

接下来，我们给出实现 newString 操作的函数定义。实现文件包含头文件 `cassert`，因为我们使用了函数 assert。（有关函数 assert 的说明，请参见第4章或附录中的头文件 `cassert`。）

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
    strcpy(strPtr, str);              //copy string into strPtr
}

//Default constructor to store the null string
newString::newString()
{
    strLength = 0;
    strPtr = new char[1];
    strcpy(strPtr, "");
}

newString::newString(const newString& rightStr)  //copy constructor
{
    strLength = rightStr.strLength;
    strPtr = new char[strLength + 1];
    strcpy(strPtr, rightStr.strPtr);
}

newString::~newString()  //destructor
{
    delete [] strPtr;
}

//overload the assignment operator
const newString& newString::operator=(const newString& rightStr)
{
    if (this != & rightStr)  //avoid self-copy
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
ostream& operator<< (ostream& osObject, const newString& str)
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
```

考虑函数 `operator>>` 定义中的语句：

`isObject >> setw(81) >> temp;`

因为 temp 被声明为大小为81的数组，所以能存入 temp 的最大字符串长度为80。这条语句（也就是输入语句）中的操纵符 setw 确保读入 temp 的字符不超过80个。

这些函数大多非常直接。让我们解释一下重载转换构造函数、赋值运算符和复制构造函数的函数。

**转换构造函数**是一个单参数函数，它将其参数转换为构造函数所属类的对象。在我们的例子中，转换构造函数将一个字符串转换为 `newString` 类型的对象。

注意，赋值运算符仅针对 `newString` 类型的对象显式重载。然而，如果我们想把一个C字符串存入 `newString` 对象，重载的赋值运算符也可以工作。考虑以下声明：

```cpp
newString str;
```

以及以下语句：

```cpp
str = "Hello there";
```

编译器将该语句转换为：

```cpp
str.operator=("Hello there");
```

- 1. 首先，编译器自动调用转换构造函数，创建一个 `newString` 类型的对象，以临时存储字符串 "Hello there"。
- 2. 其次，编译器调用重载的赋值运算符，将临时的 `newString` 对象赋给对象 `str`。

因此，不必为了将C字符串存入 `newString` 类型的对象而显式重载赋值运算符。

接下来，我们编写一个C++程序，测试类 `newString` 的一些操作。

```cpp
/////////////////////////////////////////////////////////////////////
// Author: D.S. Malik
//
// This program shows how to use the class newString.
/////////////////////////////////////////////////////////////////////

#include <iostream>
#include "myString.h"

using namespace std;

int main()
{
    newString str1 = "Sunny";      //initialize str1 using
                                    //the assignment operator
    const newString str2("Warm");   //initialize str2 using the
                                    //conversion constructor
    newString str3;  //initialize str3 to the empty string
    newString str4;  //initialize str4 to the empty string

    cout << "Line 1: " << str1 << " " << str2
         << " ** " << str1 << "####" << endl;       //Line 1

    if (str1 <= str2)                    //compare str1 and str2; Line 2
        cout << "Line 3: " << str1 << " is less "
             << "than or equal to " << str2 << endl; //Line 3
    else                                 //Line 4
        cout << "Line 5: " << str2 << " is less "
             << "than " << str1 << endl;             //Line 5

    cout << "Line 6: Enter a string with a length "
         << "of at least 7: ";                         //Line 6
    cin >> str1;                                        //input str1;       Line 7
    cout << endl;                                       //Line 8

    cout << "Line 9: The new value of "
         << "str1 = " << str1 << endl;                 //Line 9

    str4 = str3 = "Birth Day";                         //Line 10

    cout << "Line 11: str3 = " << str3
         << ", str4 = " << str4 << endl;              //Line 11

    str3 = str1;                                        //Line 12
    cout << "Line 13: The new value of str3 = "
         << str3 << endl;                               //Line 13

    str1 = "Bright Sky";                               //Line 14

    str3[1] = str1[5];                                  //Line 15
    cout << "Line 16: After replacing the second "
         << "character of str3 = " << str3 << endl;    //Line 16

    str3[2] = str2[0];                                  //Line 17
    cout << "Line 18: After replacing the third "
         << "character of str3 = " << str3 << endl;    //Line 18

    str3[5] = 'g';                                      //Line 19
    cout << "Line 20: After replacing the sixth "
         << "character of str3 = " << str3 << endl;    //Line 20

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```
Line 1: Sunny    Warm  ****
Line 3: Sunny is less than or equal to Warm
```

