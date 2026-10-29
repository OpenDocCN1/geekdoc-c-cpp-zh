

```
cout << "The date stored in oldDate is ";
oldDate.showDate();
cout << "\nThe date stored in newDate is ";
newDate.showDate();
cout << endl;

return 0;
}
```

正如程序11.5的输出所示，日期值已成功交换：

```
The date stored in oldDate is 04/03/99
The date stored in newDate is 12/18/12
```

```
After the swap:

The date stored in oldDate is 12/18/12
The date stored in newDate is 04/03/99
```

下面的swap()方法产生了相同的输出，该方法使用引用参数而不是指针：

```
void Date::swap(Date& temp) // method to swap two dates
{
    int tempstore;

    // swap the day member
    tempstore = temp.day;
    temp.day = day;
    day = tempstore;

    // swap the month member
    tempstore = temp.month;
    temp.month = month;
    month = tempstore;

    // swap the year member
    tempstore = temp.year;
    temp.year = year;
    year = tempstore;

    return;
}
```

显然，swap()的引用版本比指针版本更容易阅读。实际上，C++引入引用的主要原因之一就是用作函数参数。然而，在某些应用中，必须使用指针。

## 11.3 数据类型转换

```
day = pt->day;
month=pt->month;
year = pt->year;

return;
}
```

- b. 在程序11.5中包含练习6a中给出的`addSixMonths()`方法，并验证你对练习6a的回答。
- 
- 7. **(修改)** a. 修改练习6a中给出的`addSixMonths()`方法，使其使用引用参数而非指针。
  b. 在程序11.5中包含为练习7a编写的`addSixMonths()`方法，并验证该方法是否按预期工作。
- 
- 8. **(修改)** a. 修改练习6a中给出的`addSixMonths()`方法，使其不改变传递对象中的数据值。通过传递`oldDate`的副本（而不是指针或引用）来实现。
  b. 在程序11.5中包含为练习8a编写的`addSixMonths()`方法，并验证该方法是否按预期工作。

你已经了解了从一种内置数据类型到另一种内置数据类型的转换（参见第3.1节和第3.3节）。随着类的引入，现在有三种新的转换可能性：

- 从类类型到内置类型的转换
- 从内置类型到类类型的转换
- 从类类型到类类型的转换

显然，只有当数据类型之间存在有意义的关联时，转换才有意义。本节使用Date类来解释这些转换，因为在由日、月、年变量组成的Date对象与形如yyyymmdd的整数之间确实存在有用的关联。例如，像9/15/2012这样的日期可以用整数20120915表示。以这种形式表示为整数的日期，便于排序和比较。由于表示日期的整数可能超出普通整数的大小，因此使用长整数，如图11.5所示。

## 为你的类添加功能

![](img/202cface8244f523c2641baa2e00d7dd_539_0.png)

**图11.5** 两种日期表示

类与内置数据类型之间以及类与类之间的转换，可以使用与11.1节中展示的运算符函数形式几乎相同的方法来完成。从内置数据类型到类的转换通过构造函数方法实现。所有三种新的转换可能性都通过使用Date类和图11.5中所示的长整数关系来展示。为了完整性，也包含了从内置数据类型到内置数据类型的转换。

### 内置到内置转换

内置到内置的转换由C++的隐式转换规则或其显式强制转换运算符处理。简要回顾一下，这种转换是隐式或显式的。隐式转换可以通过赋值发生。例如，当一个浮点值赋给一个整型变量时，只存储该值的整数部分。隐式转换由编译器自动执行。

当使用强制转换时，会发生显式转换。在C++中，有两种强制转换表示法。较旧的C表示法形式为`(dataType) expression`，而较新的C++表示法具有类似函数的形式`dataType(expression)`。例如，表达式`(int)24.32`和`int(24.32)`都会使双精度值24.32截断为整数值24。

### 类到内置转换

从用户定义的数据类型到内置数据类型的转换通过使用**转换运算符函数**来完成。这些转换运算符也被称为“强制转换”。创建转换运算符或强制转换与创建运算符函数（在第11.1节讨论）完全相同，只有一个例外：在函数头中使用内置数据类型名称而不是内置符号。因此，用于将Date对象转换为长整数的转换运算符函数必须命名为`operator long()`。程序11.6定义了该函数并使用它将Date对象转换为长整数。该函数的原型、定义和调用在程序中以阴影标出。

## 为你的类添加功能

```cpp
int main()
{
    Date a(4,1,2012);   // declare and initialize one object of type Date
    long b;             // declare an object of type long

    b = long(a);        // call the conversion function

    cout << "a's date is ";
    a.showDate();
    cout << "\nThis date, as a long integer, is " << b << endl;

    return 0;
}
```

程序11.6产生以下输出：

```text
a's date is 04/01/12
This date, as a long integer, is 20120401
```

正如该输出所示，a的日期值到长整数的转换是由赋值表达式b = long(a)产生的。这个赋值也可以写成b = a。在这种情况下，转换为long是隐式的。由于程序11.6中的显式转换语句清楚地记录了正在进行的转换，因此使用它更可取。

注意，转换运算符声明时没有显式参数或返回类型，所有转换运算符都是如此。这是因为被转换对象的数据类型是一个隐含参数，必须是所声明类的对象，而返回类型由函数名提供。

### 内置到类转换

将内置类型转换为类类型的用户自定义函数是作为构造函数创建的。对于将长整数日期转换为以月、日、年存储的日期，以下是一个合适的构造函数：

```cpp
// constructor for converting from long to Date
Date::Date(long findate)
{
    year = int(findate/10000.0);
    month = int((findate - year * 10000.0)/100.0);
    day = int(findate - year * 10000.0 - month * 100.0);
}
```

程序11.7以两种方式使用这个构造函数。首先，它作为构造函数在声明Date对象时初始化该对象。其次，它用于将长整数显式转换为Date对象。所有与转换函数相关的语句在程序中都加了阴影。

## 程序11.7

```
#include <iostream>
#include <iomanip>
using namespace std;

// class declaration section
class Date
{
    private:
        int month, day, year;
    public:
        Date(int = 7, int = 4, int = 2012);  // constructor
        // constructor for converting from long to Date
        Date(long);
        void showDate();
};
// class implementation section
Date::Date(int mm, int dd, int yyyy)  // constructor
{
    month = mm;
    day = dd;
    year = yyyy;
}
```

```
// constructor for converting from long to Date
Date::Date(long findate)
{
    year = int(findate/10000.0);
    month = int((findate - year * 10000.0)/100.0);
    day = int(findate - year * 10000.0 - month * 100.0);
}
```

```
// member function to display a date
void Date::showDate()
{
    cout << setfill('0')
         << setw(2) << month << '/'
         << setw(2) << day << '/'
         << setw(2) << year % 100;
    return;
}
```

