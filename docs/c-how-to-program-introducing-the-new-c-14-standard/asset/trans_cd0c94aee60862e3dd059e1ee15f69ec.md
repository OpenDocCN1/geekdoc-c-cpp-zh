
# 运算符

重载后缀增量运算符是一个挑战，因为编译器必须能够区分重载的前缀和后缀增量运算符函数的签名。所采用的约定是：当编译器看到后缀递增表达式 `d1++` 时，它会生成成员函数调用

```cpp
d1.operator++(0)
```

该运算符成员函数的原型为

```cpp
Date operator++(int)
```

参数 `0` 纯粹是一个*哑元*值，它使编译器能够区分前缀和后缀增量运算符函数。同样的语法也用于区分前缀和后缀递减运算符函数。

如果后缀增量被实现为*非成员函数*，那么当编译器看到表达式 `d1++` 时，会生成函数调用

```cpp
operator++(d1, 0)
```

该函数的原型将是

```cpp
Date operator++(Date&, int);
```

同样，`0` 参数被编译器用来区分以非成员函数实现的前缀和后缀增量运算符。注意，*后缀增量运算符*按值返回 `Date` 对象，而前缀增量运算符按引用返回 `Date` 对象——后缀增量运算符通常返回一个临时对象，其中包含对象在递增发生之前的原值。C++ 将此类对象视为*右值*，它们*不能用在赋值号左侧*。前缀增量运算符返回实际递增后的对象及其新值。这样的对象*可以用作左值*，出现在后续表达式中。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1355_0.png)

# 性能提示 10.1

*后缀增量（或减量）运算符创建了额外的对象，可能导致性能问题——尤其是当运算符在循环中使用时。因此，你应该优先使用重载的前缀增量和减量运算符。*

# 10.8 案例研究：Date 类

**图10.6–10.8** 的程序演示了一个 `Date` 类，该类使用重载的前缀和后缀增量运算符将 `Date` 对象中的天数加 1，并在必要时对月和年进行相应的递增。`Date` 头文件（**图10.6**）指定 `Date` 的 `public` 接口包括：重载的流插入运算符（第10行）、默认构造函数（第12行）、`setDate` 函数（第13行）、重载的前缀增量运算符（第14行）、重载的后缀增量运算符（第15行）、重载的 `+=` 加赋值运算符（第16行）、测试闰年的函数（第17行）、以及判断某天是否为该月最后一天的函数（第18行）。

```cpp
// Fig. 10.6: Date.h
// Date class definition with overloaded increment operators.
#ifndef DATE_H
#define DATE_H

#include <array>
#include <iostream>

class Date {
    friend std::ostream& operator<<(std::ostream&, const Date&);
public:
    Date(int m = 1, int d = 1, int y = 1900); // default constructor
    void setDate(int, int, int); // set month, day, year
    Date& operator++(); // prefix increment operator
    Date operator++(int); // postfix increment operator
    Date& operator+=(unsigned int); // add days, modify object
    static bool leapYear(int); // is year a leap year?
    bool endOfMonth(int) const; // is day at the end of month?
private:
    unsigned int month;
    unsigned int day;
    unsigned int year;

    static const std::array<unsigned int, 13> days; // days per month
    void helpIncrement(); // utility function for incrementing date
};

#endif
```

图10.6 带重载增量运算符的 `Date` 类定义。

```cpp
// Fig. 10.7: Date.cpp
// Date class member- and friend-function definitions.
#include <iostream>
#include <string>
#include "Date.h"
using namespace std;

// initialize static member; one classwide copy
const array<unsigned int, 13> Date::days{
   0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

// Date constructor
Date::Date(int month, int day, int year) {
   setDate(month, day, year);
}

// set month, day and year
void Date::setDate(int mm, int dd, int yy) {
   if (mm >= 1 && mm <= 12) {
      month = mm;
   }
   else {
      throw invalid_argument{"Month must be 1-12"};
   }

   if (yy >= 1900 && yy <= 2100) {
      year = yy;
   }
   else {
      throw invalid_argument{"Year must be >= 1900 and <= 2100"};
   }

   // test for a leap year
   if ((mm == 2 && leapYear(year) && dd >= 1 && dd <= 29) ||
       (dd >= 1 && dd <= days[mm])) {
      day = dd;
   }
   else {
      throw invalid_argument{
         "Day is out of range for current month and year"};
   }
}

// overloaded prefix increment operator
Date& Date::operator++() {
   helpIncrement(); // increment date
   return *this; // reference return to create an lvalue
}

// overloaded postfix increment operator; note that the
// dummy integer parameter does not have a parameter name
Date Date::operator++(int) {
   Date temp = *this; // hold current state of object
   helpIncrement();

   // return unincremented, saved, temporary object
   return temp; // value return; not a reference return
}

// add specified number of days to date
Date& Date::operator+=(unsigned int additionalDays) {
   for (unsigned int i = 0; i < additionalDays; ++i) {
      helpIncrement();
   }

   return *this; // enables cascading
}

// if the year is a leap year, return true; otherwise, return false
bool Date::leapYear(int testYear) {
   return (testYear % 400 == 0 ||
      (testYear % 100 != 0 && testYear % 4 == 0));
}

// determine whether the day is the last day of the month
bool Date::endOfMonth(int testDay) const {
   if (month == 2 && leapYear(year))
      return testDay == 29; // last day of Feb. in leap year
   else {
      return testDay == days[month];
   }
}

// function to help increment the date
void Date::helpIncrement() {
    // day is not end of month
    if (!endOfMonth(day)) {
        ++day; // increment day
    }
    else {
        if (month < 12) { // day is end of month and month < 12
            ++month; // increment month
            day = 1; // first day of new month
        }
        else { // last day of year
            ++year; // increment year
            month = 1; // first month of new year
            day = 1; // first day of new month
        }
    }
}

// overloaded output operator
ostream& operator<<(ostream& output, const Date& d) {
    static string monthName[13]{"", "January", "February",
        "March", "April", "May", "June", "July", "August",
        "September", "October", "November", "December"};
    output << monthName[d.month] << " " << d.day << ", " << d.year;
    return output; // enables cascading
}
```

**图10.7** `Date` 类的成员函数和 `friend` 函数定义。

```cpp
// Fig. 10.8: fig10_08.cpp
// Date class test program.
#include <iostream>
#include "Date.h" // Date class definition
using namespace std;

int main() {
   Date d1{12, 27, 2010}; // December 27, 2010
   Date d2; // defaults to January 1, 1900

   cout << "d1 is " << d1 << "\nd2 is " << d2;
   cout << "\n\nd1 += 7 is " << (d1 += 7);

   d2.setDate(2, 28, 2008);
   cout << "\n\nd2 is " << d2;
   cout << "\n++d2 is " << ++d2 << " (leap year allows 29th)";

   Date d3{7, 13, 2010};

   cout << "\n\nTesting the prefix increment operator:\n";
   cout << "   d3 is " << d3 << endl;
   cout << "++d3 is " << ++d3 << endl;
   cout << "   d3 is " << d3;

   cout << "\n\nTesting the postfix increment operator:\n";
   cout << "   d3 is " << d3 << endl;
   cout << "d3++ is " << d3++ << endl;
   cout << "   d3 is " << d3 << endl;
}
```

```text
d1 is December 27, 2010
d2 is January 1, 1900

d1 += 7 is January 3, 2011

   d2 is February 28, 2008
++d2 is February 29, 2008 (leap year allows 29th)

Testing the prefix increment operator:
   d3 is July 13, 2010
++d3 is July 14, 2010
   d3 is July 14, 2010

Testing the postfix increment operator:
   d3 is July 14, 2010
d3++ is July 14, 2010
   d3 is July 15, 2010
```

图10.8 Date 类测试程序。
