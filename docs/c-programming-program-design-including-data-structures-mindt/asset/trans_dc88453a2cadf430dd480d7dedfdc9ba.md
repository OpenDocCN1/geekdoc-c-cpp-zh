
## 编程示例：复数

形如 $a + ib$ 的数称为复数，其中 $i^2 = -1$，且 $a$ 和 $b$ 是实数。我们称 $a$ 为 $a + ib$ 的实部，$b$ 为 $a + ib$ 的虚部。复数也可以表示为有序对 $(a, b)$。复数的加法和乘法由以下规则定义：

$(a + ib) + (c + id) = (a + c) + i(b + d)$

$(a + ib)(c + id) = (ac - bd) + i(ad + bc)$

使用有序对记号，这些规则可写为：

$(a, b) + (c, d) = ((a + c), (b + d))$

$(a, b) * (c, d) = ((ac - bd), (ad + bc))$

C++ 没有可用于操作复数的内置数据类型。在本示例中，我们将构造一个可用于处理复数的数据类型 `complexType`。我们将重载流插入和流提取运算符，以便于输入和输出。我们还将重载运算符 + 和 *，以执行复数的加法和乘法。如果 $x$ 和 $y$ 是复数，我们可以求值诸如 $x + y$ 和 $x * y$ 这样的表达式。

类 `complexType` 的定义为：

```cpp
#include <iostream>
using namespace std;

class complexType
{
    //Overload the stream insertion and extraction operators
    friend ostream& operator<<(ostream&, const complexType&);
    friend istream& operator>>(istream&, complexType&);

public:
    void setComplex(const double& real, const double& imag);
        //Function to set the complex numbers according to
        //the parameters.
        //Postcondition: realPart = real; imaginaryPart = imag;

    void getComplex(double& real, double& imag) const;
        //Function to retrieve the complex number.
        //Postcondition: real = realPart; imag = imaginaryPart;

    complexType(double real = 0, double imag = 0);
        //Constructor
        //Initializes the complex number according to
        //the parameters.
        //Postcondition: realPart = real; imaginaryPart = imag;

    complexType operator+
                (const complexType& otherComplex) const;
    //overload the operator +

    complexType operator*
                (const complexType& otherComplex) const;
    //overload the operator *

    bool operator== (const complexType& otherComplex) const;
    //overload the operator ==

private:
    double realPart;       //variable to store the real part
    double imaginaryPart;  //variable to store the
                           //imaginary part
};
```

图 13-2 展示了类 `complexType` 的 UML 类图。

![](img/b217c421655b51e7494cf3b89bb5432d_1009_0.png)

图 13-2 类 `complexType` 的 UML 类图

接下来，我们编写函数定义，以实现类 `complexType` 的各种操作。

这些函数中大多数函数的定义都很直接。我们将只讨论重载流插入运算符 `<<` 和流提取运算符 `>>` 的函数的定义。

要输出如下形式的复数：

`(a, b)`

```cpp
isObject >> complex.imaginaryPart;        //Step d
isObject >> ch;                            //Step e

}
return isObject;  //return the istream object
```

其他函数的定义如下：

```cpp
bool complexType::operator==
                    (const complexType& otherComplex) const
{
    return (realPart == otherComplex.realPart &&
            imaginaryPart == otherComplex.imaginaryPart);
}

//constructor
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

//overload the operator +
complexType complexType::operator+
                    (const complexType& otherComplex) const
{
    complexType temp;

    temp.realPart = realPart + otherComplex.realPart;
    temp.imaginaryPart = imaginaryPart
                       + otherComplex.imaginaryPart;

    return temp;
}

//overload the operator *
complexType complexType::operator*
                         (const complexType& otherComplex) const
{
    complexType temp;
    temp.realPart = (realPart * otherComplex.realPart)
                  - (imaginaryPart * otherComplex.imaginaryPart);
    temp.imaginaryPart = (realPart * otherComplex.imaginaryPart)
                       + (imaginaryPart * otherComplex.realPart);
    return temp;
}
```

以下程序演示了类 complexType 的使用：

```cpp
//**************************************************************
// Author: D.S. Malik
//
// This program shows how to use the class complexType.
//**************************************************************

#include <iostream>                                  //Line 1
#include "complexType.h"                             //Line 2

using namespace std;                                  //Line 3

int main()                                           //Line 4
{                                                    //Line 5
        complexType num1(21, 18);                    //Line 6
        complexType num2;                             //Line 7
        complexType num3;                             //Line 8

        cout << "Line 9: Num1 = " << num1 << endl;  //Line 9
        cout << "Line 10: Num2 = " << num2 << endl; //Line 10

        cout << "Line 11: Enter a complex number "  //Line 11
             << "in the form (a, b): ";             
        cin >> num2;                                 //Line 12
        cout << endl;                                 //Line 13

        cout << "Line 14: New value of num2 = "     
             << num2 << endl;                         //Line 14

        num3 = num1 + num2;                           //Line 15

        cout << "Line 16: Num3 = " << num3 << endl;  //Line 16
        cout << "Line 17: " << num1 << " + " << num2
             << " = " << num1 + num2 << endl;        //Line 17

        cout << "Line 18: " << num1 << " * " << num2
             << " = " << num1 * num2 << endl;        //Line 18

        return 0;                                     //Line 19
}                                                    //Line 20
```

示例运行：在此示例运行中，用户输入以阴影显示。

```text
Line 9: Num1 = (21, 18)
Line 10: Num2 = (0, 0)
Line 11: Enter a complex number in the form (a, b): (5, 9)

Line 14: New value of num2 = (5, 9)
Line 16: Num3 = (26, 27)
Line 17: (21, 18) + (5, 9) = (26, 27)
Line 18: (21, 18) * (5, 9) = (-57, 279)
```

你可以扩展这个数据类型，以对复数执行减法和除法。

接下来，我们将定义一个名为 `newString` 的类，并重载赋值运算符和关系运算符。也就是说，当我们声明一个 `newString` 类型的变量时，我们将能够使用赋值运算符将一个字符串复制到另一个字符串，并使用关系运算符比较这两个字符串。

不过，在讨论类 `newString` 之前，我们将研究运算符 `[]` 的重载。回想一下，我们已经使用运算符 `[]` 来访问数组的各个分量。为了访问 `newString` 类型字符串中的单个字符，我们必须为类 `newString` 重载运算符 `[]`。

### 重载数组索引（下标）运算符（[]）

回想一下，为类重载运算符 `[]` 的函数必须是该类的成员。此外，由于数组可以声明为常量或非常量，我们需要重载运算符 `[]` 以处理这两种情况。

将运算符函数 `operator[]` 声明为类的成员以处理非常量数组的语法是：

```cpp
Type& operator[](int index);
```

将运算符函数 `operator[]` 声明为类的成员以处理常量数组的语法是：

```cpp
const Type& operator[](int index) const;
```

其中 `Type` 是数组元素的数据类型。

假设 `classTest` 是一个具有数组成员变量的类。为类 `classTest` 重载运算符 `[]` 的定义如下：
