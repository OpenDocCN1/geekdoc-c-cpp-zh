

```cpp
void setName(string first, string last);
    //Function to set firstName and lastName according
    //to the parameters.
    //Postcondition: firstName = first; lastName = last

string getFirstName() const;
    //Function to return the first name.
    //Postcondition: The value of firstName is returned.

string getLastName() const;
    //Function to return the last name.
    //Postcondition: The value of lastName is returned.

personType(string first = "", string last = "");
    //Constructor
    //Sets firstName and lastName according to the parameters.
    //The default values of the parameters are null strings.
    //Postcondition: firstName = first; lastName = last

private:
    string firstName; //variable to store the first name
    string lastName;  //variable to store the last name
};
```

图 10-11 展示了类 personType 的 UML 类图。

![](img/b217c421655b51e7494cf3b89bb5432d_745_0.png)

图 10-11  类 personType 的 UML 类图

现在给出类 personType 的成员函数的定义。

```cpp
void personType::print() const
{
    cout << firstName << " " << lastName;
}

void personType::setName(string first, string last)
{
    firstName = first;
    lastName = last;
}
```

```cpp
string personType::getFirstName() const
{
    return firstName;
}

string personType::getLastName() const
{
    return lastName;
}

//constructor
personType::personType(string first, string last)
{
    firstName = first;
    lastName = last;
}
```

### 示例 10-11

在本例中，我们设计并实现一个用于操作整数的类。考虑整数 620385147907652638。可以对该整数执行的一些操作包括：统计偶数数字、奇数数字和零的个数；求各位数字之和；反转各位数字；将该数拆分为三位数块；以及求这些数字之和。下面的类定义了其中一些操作。

```cpp
class integerManipulation
{
public:
    void setNum(long long n);
        //Function to set num.
        //Postcondition: num = n;

    long long getNum();
        //Function to return num.
        //Postcondition: The value of num is returned.

    void reverseNum();
        //Function to reverse the digits of num.
        //Postcondition: revNum is set to num with digits in
        //               the reverse order.

    void classifyDigits();
        //Function to count the even, odd, and zero digits of num.
        //Postcondition: evensCount = the number of even digits
        //                           in num.
        //               oddsCount = the number of odd digits in num.

    int getEvensCount();
        //Function to return the number of even digits in num.
        //Postcondition: The value of evensCount is returned.

    int getOddsCount();
        //Function to return the number of odd digits in num.
        //Postcondition: The value of oddsCount is returned.

    int getZerosCount();
        //Function to return the number of zeros in num.
        //Postcondition: The value of zerosCount is returned.

    int sumDigits();
        //Function to return the sum of the digits of num.
        //Postcondition: The sum of the digits is returned.

    integerManipulation(long long n = 0);
        //Constructor with a default parameter.
        //The instance variable num is set according to the
        //parameter, and other instance variables are
        //set to zero.
        //The default value of num is 0;
        //Postcondition: num = n; revNum = 0; evensCount = 0;
        //              oddsCount = 0; zerosCount = 0;

private:
    long long num;
    long long revNum;
    int evensCount;
    int oddsCount;
    int zerosCount;
};
```

其中一些成员函数的定义如下：

```cpp
void integerManipulation::setNum(long long n)
{
    num = n;
}

long long integerManipulation::getNum()
{
    return num;
}

void integerManipulation::reverseNum()
{
    cout << "See Programming Exercise 9 in Chapter 6." << endl;
}

void integerManipulation::classifyDigits()
{
    long long temp;

    temp = abs(num);

    int digit;

    while (temp != 0)
    {
        digit = temp - (temp / 10) * 10;
        temp = temp / 10;

        if (digit % 2 == 0)
        {
            evensCount++;
            if (digit == 0)
                zerosCount++;
        }
        else
            oddsCount++;
    }
}

int integerManipulation::getEvensCount()
{
    return evensCount;
}

int integerManipulation::getOddsCount()
{
    return oddsCount;
}

int integerManipulation::getZerosCount()
{
    return zerosCount;
}

int integerManipulation::sumDigits()
{
    cout << "See Programming Exercise 1 in Chapter 5." << endl;

    return 0;
}

integerManipulation::integerManipulation(long long n)
{
    num = n;
    revNum = 0;
    evensCount = 0;
    oddsCount = 0;
    zerosCount = 0;
}
```

下面的程序展示了如何在程序中使用这个类。

```cpp
//The user program that uses the class integerManipulation

#include <iostream>                         //Line 1
#include "integerManipulation.h"            //Line 2

using namespace std;                        //Line 3

int main()                                  //Line 4
{                                           //Line 5
    integerManipulation number;             //Line 6

    long long num;                          //Line 7

    cout << "Enter an integer: ";           //Line 8
    cin >> num;                             //Line 9
    cout << endl;                           //Line 10

    number.setNum(num);                     //Line 11

    number.classifyDigits();                //Line 12

    cout << number.getNum() << endl
         << "The number of even digits: "
         << number.getEvensCount() << endl
         << "The number of zeros: "
         << number.getZerosCount() << endl
         << "The number of odd digits: "
         << number.getOddsCount() << endl;  //Line 13

    return 0;                               //Line 14
} //end main                                //Line 15
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```
Enter an integer: 6203851479017652638

6203851479017652638
The number of even digits: 10
The number of zeros: 2
The number of odd digits: 9
```

本章末尾的编程练习 24 要求你编写类 `integerManipulation` 中尚未给出的函数定义。

## 内联函数

类 `clockType` 的定义包含数据成员的声明和成员函数的函数原型。成员函数的定义放在实现文件中。不过，在类定义中，你可以给出成员函数的完整定义。这样的成员函数定义称为**内联函数定义**。假设你想加入一个返回时钟小时数的函数。可以按如下方式编写类 `clockType` 的定义：

```cpp
class clockType
{
public:
    void setTime(int hours, int minutes, int seconds);
    void getTime(int& hours, int& minutes, int& seconds) const;
    void printTime() const;

    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();

    bool equalTime(const clockType& otherClock) const;

    int getHours() const
    {
        return hr;
    }

    clockType(int hours = 0, int minutes = 0,
              int seconds = 0);

private:
    int hr;
    int min;
    int sec;
};
```

在这个类定义中，函数 `getHours` 是内联的。内联函数定义通常用于非常短的函数定义。编译器以特殊方式处理内联函数。它通常会在调用该函数的每个位置插入内联函数的代码。调用函数时，会为其参数和局部变量分配内存；函数退出时，这些内存会被释放。因此，调用函数会带来开销。对于内联函数，可以省去函数调用的开销。一般来说，非常短的定义应定义为内联函数。

## 类的静态成员

> **注意**  可以跳过本节，而不会影响后续内容。

在第 6 章中，我们介绍了两种类型的变量：自动变量和静态变量。回顾一下，如果函数中的局部变量是 `static`，那么它在函数调用之间仍然存在。与静态变量类似，类也可以有静态成员、函数或变量。关于类的静态成员，请注意以下几点：

- 如果类中的某个函数是 `static`，则在类定义中，其函数头使用关键字 `static` 声明。

