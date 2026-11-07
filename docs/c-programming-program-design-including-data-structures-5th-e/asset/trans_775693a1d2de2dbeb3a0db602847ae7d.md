
要按以下形式输出一个复数：

`(a, b)`

其中 a 是实部，b 是虚部，显然算法是：

- a. 输出左圆括号 `(`。
- b. 输出实部。
- c. 输出逗号和一个空格。
- d. 输出虚部。
- e. 输出右圆括号 `)`。

因此，函数 `operator<<` 的定义为：

```cpp
ostream& operator<<(ostream& osObject,
                    const complexType& complex)
{
    osObject << "(";                 //Step a
    osObject << complex.realPart;     //Step b
    osObject << ", ";                //Step c
    osObject << complex.imaginaryPart; //Step d
    osObject << ")";                 //Step e

    return osObject;      //return the ostream object
}
```

接下来，我们讨论重载流提取运算符 `>>` 的函数的定义。

输入形式为：

`(3, 5)`

在此输入中，复数的实部是 3，虚部是 5。显然，读取这个复数的算法是：

- a. 读取并丢弃左圆括号。
- b. 读取并存储实部。
- c. 读取并丢弃逗号。
- d. 读取并存储虚部。
- e. 读取并丢弃右圆括号。

按照这些步骤，函数 `operator>>` 的定义为：

```cpp
istream& operator>> (istream& isObject, complexType& complex)
{
    char ch;

    isObject >> ch;                  //Step a
    isObject >> complex.realPart;    //Step b
    isObject >> ch;                  //Step c
    isObject >> complex.imaginaryPart; //Step d
    isObject >> ch;                  //Step e

    return isObject;      //return the istream object
}
```

其他函数的定义如下：

```cpp
bool complexType::operator==
                         (const complexType& otherComplex) const
{
    return (realPart == otherComplex.realPart &&
            imaginaryPart == otherComplex.imaginaryPart);
}

//Constructor
complexType::complexType(double real, double imag)
{
    realPart = real;
    imaginaryPart = imag;
}

//Function to set the complex number after the object
//has been declared
void complexType::setComplex(const double& real,
                             const double& imag)
{
    realPart = real;
    imaginaryPart = imag;
}

void complexType::getComplex(double& real, double& imag) const
{
    real = realPart;
    imag = imaginaryPart;
}

//Overload the operator +
complexType complexType::operator+
                         (const complexType& otherComplex) const
{
    complexType temp;

    temp.realPart = realPart + otherComplex.realPart;
    temp.imaginaryPart = imaginaryPart
                          + otherComplex.imaginaryPart;

    return temp;
}
```

```cpp
//overload the operator *
complexType complexType::operator*
                         (const complexType& otherComplex) const
{
    complexType temp;
    temp.realPart = (realPart * otherComplex.realPart)
                    + (imaginaryPart * otherComplex.imaginaryPart);
    temp.imaginaryPart = (realPart * otherComplex.imaginaryPart)
                       + (imaginaryPart * otherComplex.realPart);
    return temp;
}
```

以下程序演示了类 complexType 的用法：

```cpp
//************************************************************
// Author: D.S. Malik
//
// This program shows how to use the class complexType.
//************************************************************

#include <iostream>
#include "complexType.h"

using namespace std;

int main()
{
        complexType num1(23, 34);                         //Line 1
        complexType num2;                                 //Line 2
        complexType num3;                                 //Line 3

        cout << "Line 4: Num1 = " << num1 << endl;       //Line 4
        cout << "Line 5: Num2 = " << num2 << endl;       //Line 5

        cout << "Line 6: Enter the complex number "
             << "in the form (a, b) ";                  //Line 6
        cin >> num2;                                     //Line 7
        cout << endl;                                    //Line 8

        cout << "Line 9: New value of num2 = "
             << num2 << endl;                            //Line 9

        num3 = num1 + num2;                              //Line 10

        cout << "Line 11: Num3 = " << num3 << endl;      //Line 11

        cout << "Line 12: " << num1 << " + " << num2
             << " = " << num1 + num2 << endl;           //Line 12

        cout << "Line 13: " << num1 << " * " << num2
             << " = " << num1 * num2 << endl;           //Line 13

        return 0;
}
```

**示例运行：** 在此示例运行中，用户输入部分以阴影显示。

```cpp
Line 4: Num1 = (23, 34)
Line 5: Num2 = (0, 0)
Line 6: Enter the complex number in the form (a, b)  (3, 4)
Line 9: New value of num2 = (3, 4)
Line 11: Num3 = (26, 38)
Line 12: (23, 34) + (3, 4) = (26, 38)
Line 13: (23, 34) * (3, 4) = (-67, 194)
```

你可以扩展此数据类型，以对复数执行减法和除法运算。

接下来，我们将定义一个名为 `newString` 的类，并重载赋值运算符和关系运算符。也就是说，当我们声明一个 `newString` 类型的变量时，我们将能够使用赋值运算符将一个字符串复制到另一个字符串，并使用关系运算符比较这两个字符串。

然而，在讨论类 `newString` 之前，我们先考察运算符 `[]` 的重载。回想一下，我们已经使用运算符 `[]` 来访问数组的各个分量。要访问 `newString` 类型字符串中的单个字符，我们必须为类 `newString` 重载运算符 `[]`。

## 重载数组索引（下标）运算符（`[]`）

回想一下，为类重载运算符 `[]` 的函数必须是该类的成员。此外，由于数组可以声明为常量或非常量，我们需要重载运算符 `[]` 以处理这两种情况。

将运算符函数 `operator[]` 声明为类成员以用于非常量数组的语法是：

```cpp
Type& operator[](int index);
```

将运算符函数 `operator[]` 声明为类成员以用于常量数组的语法是：

```cpp
const Type& operator[](int index) const;
```

其中 Type 是数组元素的数据类型。

假设 `classTest` 是一个具有数组成员变量的类。为 `classTest` 重载运算符 `[]` 的定义是：

```cpp
class classTest
{
public:
    Type& operator[](int index);
        //Overload the operator[] for nonconstant arrays
    const Type& operator[](int index) const;
        //Overload the operator[] for constant arrays
    .
    .
private:
    Type *list; //pointer to the array
    int arraySize;
};
```

其中 Type 是数组元素的数据类型。

为 classTest 重载运算符 [] 的函数的定义如下：

```cpp
    //Overload the operator [] for nonconstant arrays
Type& classTest::operator[](int index)
{
    assert(0 <= index && index < arraySize);
    return list[index];    //return a pointer of the
                           //array component
}

    //Overload the operator [] for constant arrays
const Type& classTest::operator[](int index) const
{
    assert(0 <= index && index < arraySize);
    return list[index];    //return a pointer of the
                           //array component
}
```

> **注意**  前面的函数定义使用了 assert 语句。（关于 assert 语句的解释，参见第 4 章或附录。）

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

将执行用于非常量数组的运算符函数 operator[] 的函数体。对于以下语句：

```cpp
list1[2] = list3[5];
```

首先，将执行用于常量数组的运算符函数 operator[] 的函数体，因为 list3 是常量数组。接下来，将执行用于非常量数组的运算符函数 operator[] 的函数体，以完成赋值语句的执行。
