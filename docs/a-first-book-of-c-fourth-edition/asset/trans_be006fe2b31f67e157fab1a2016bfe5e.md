

## 构造函数

## 知识要点

## 访问器方法

访问器方法是指任何访问类私有数据成员的非构造函数成员方法。例如，Date 类中的 showDate() 方法就是一个访问器方法。这些方法极其重要，因为它们提供了一种显示私有数据成员所存储值的方式。

在构造类时，请确保提供一套完整的访问器方法。每个访问器方法不一定非要返回数据成员的精确值，但应返回该值的一个有用表示形式。例如，如果日期 12/25/2012 以长整数成员变量的形式存储为 20122512，访问器方法可以显示该值。然而，更有用的表示形式是 12/25/12 或 2012 年 12 月 25 日。

析构函数在对象销毁时被自动调用，旨在“清理”对象可能留下的任何不良影响。通常，这些影响仅在对象包含指针成员时才会发生。

## 对象数组¹⁰

在创建对象数组时，默认构造函数的重要性变得显而易见。因为每次创建对象时都会调用构造函数，所以默认构造函数提供了一种将所有对象初始化为相同状态的高效方式。

声明对象数组与声明任何内置类型的数组相同。例如，以下声明创建了五个对象，名为 theDate[0] 到 theDate[4]：

```
Date theDate[5];
```

通过列出对象名称后跟一个点 (.) 和方法名来调用每个对象的成员方法。程序 10.4 演示了对象数组的使用，其中构造函数和析构函数中都包含 cout 语句。如该程序的输出所示，为每个声明的对象调用构造函数，然后五次调用 showDate() 成员方法，最后五次调用析构函数。当对象超出作用域时调用析构函数。在这种情况下，当 main() 函数停止执行时调用析构函数。

## 知识要点

## 修改器方法

修改器方法（更常称为“修改器”）是任何更改对象数据值的非构造函数类方法。修改器用于在构造函数方法自动创建并初始化对象之后更改对象的数据值。只要每个修改器具有唯一的名称或参数列表，一个类就可以包含多个修改器。例如，在 Date 类中，可以有一个修改器来更改 Date 对象的月、日和年的值。构造函数的主要目的是在创建对象时初始化对象的成员变量，因此不被视为修改器。

![](img/202cface8244f523c2641baa2e00d7dd_479_0.png)

## 程序 10.4

```
#include <iostream>
#include <iomanip>
using namespace std;

// class declaration section
class Date
{
private:
    int month;
    int day;
    int year;
public:
    Date();  // constructor
    ~Date(); // destructor
    void showDate();
};
// class implementation section
Date::Date()  // user-defined default constructor
{
    cout << "*** A Date object is being initialized ***\n";
    month = 1;
    day = 1;
    year = 2015;
}
Date::~Date()  // user-defined default destructor
{
    cout << "*** A Date object is going out of existence ***\n";
}
```

```
void Date::showDate()
{
    cout << "      The date is " << setfill('0')
         << setw(2) << month << '/'
         << setw(2) << day << '/'
         << setw(2) << year % 100; // extract the last 2 year digits
    return;
}
```

```
int main()
{
    const int NUMDATES = 5;
    Date thedate[NUMDATES];
    for(int i = 0; i < NUMDATES; i++)
    {
        thedate[i].showDate();
        cout << endl;
    }
    return 0;
}
```

程序 10.4 产生以下输出：

```
*** A Date object is being initialized ***
*** A Date object is being initialized ***
*** A Date object is being initialized ***
*** A Date object is being initialized ***
*** A Date object is being initialized ***
    The date is 01/01/2015
    The date is 01/01/2015
    The date is 01/01/2015
    The date is 01/01/2015
    The date is 01/01/2015
*** A Date object is going out of existence ***
*** A Date object is going out of existence ***
*** A Date object is going out of existence ***
*** A Date object is going out of existence ***
*** A Date object is going out of existence ***
```

## 练习 10.3

- 1.（复习）判断以下陈述是否正确：
  - a. 构造函数方法必须与其类同名。
  - b. 一个类只能有一个构造函数方法。
  - c. 一个类只能有一个默认构造函数方法。
  - d. 默认构造函数只能由编译器提供。
  - e. 默认构造函数可以没有参数，或者所有参数都必须有默认值。
  - f. 每个类都必须声明构造函数。
  - g. 构造函数必须声明返回类型。
  - h. 每次创建对象时都会自动调用构造函数。
  - i. 一个类只能有一个析构函数方法。
  - j. 析构函数必须与其类同名，并以波浪号 (~) 开头。
  - k. 析构函数可以有默认参数。
  - l. 每个类都必须声明析构函数。
  - m. 析构函数必须声明返回类型。
  - n. 每次对象销毁时都会自动调用析构函数。
  - o. 当类包含指针数据成员时，析构函数没有用处。

2.（桌面检查）对于程序 10.3，如果使用声明 Date c(15); 而不是 Date c(20090515L);，对象 c 初始化为什么日期？

3.（修改）修改程序 10.3，使类中唯一的数据成员是一个名为 yyyymmdd 的长整数。具体做法是用声明 long yyyymmdd; 替换以下现有声明：

```
int month;
int day;
int year;
```

使用类声明部分中当前声明的相同构造函数原型，重写它们，使 Date(long) 方法成为默认构造函数，而 Date(int, int, int) 方法将月、日和年转换为类数据成员的正确形式。

4.（编程）a. 构造一个 Time 类，包含整数数据成员 seconds、minutes 和 hours。该类包含两个构造函数：第一个应该是原型为 Time(int, int, int) 的默认构造函数，每个数据成员使用默认值 0。第二个构造函数应接受一个表示总秒数的长整数，并将该长整数分解为小时、分钟和秒。最后一个成员方法应显示类的数据成员。

b. 将练习 4a 中编写的类包含在完整程序中。

5.（编程）a. 构造一个名为 Student 的类，包含一个整数学生 ID 号、一个包含五个双精度成绩的数组，以及一个表示已输入成绩总数的整数。该类的构造函数应将所有 Student 数据成员初始化为 0。类中应包含以下成员方法：1) 输入学生 ID 号；2) 输入单个测试成绩并更新已输入的成绩总数；3) 计算平均成绩并显示学生 ID 及平均成绩。

b. 将练习 5a 中构造的类包含在完整程序中。程序应声明两个 Student 类型的对象，并接受和显示这两个对象的数据，以验证成员方法的运行。

## 6.（修改）a. 在练习 4 中，要求你构造一个 Time 类。为此类添加一个 tick() 方法，使时间增加一秒。测试你的方法，确保它能正确地将时间递增到新的一分钟和新的一小时。b. 修改为练习 6a 编写的 Time 类，添加一个 detick() 方法，使时间减少一秒。测试你的方法，确保它能正确地将时间递减到前一小时和前一分钟。

## 7.（编程）a. 构造一个名为 Coord 的类，包含两个名为 xval 和 yval 的双精度数据成员，用于存储点在笛卡尔坐标系中的 x 和 y 值。成员方法应包括构造函数和显示方法，以及一个名为 convToCartesian() 的方法。convToCartesian() 方法应接受两个名为 r 和 theta 的双精度数，表示极坐标中的一个点，并将其转换为笛卡尔坐标。从极坐标转换为笛卡尔坐标时，使用以下公式：x = r cos (theta) y = r sin (theta) b. 将练习 7a 中编写的程序包含在可运行的 C++ 程序中。

## 10.4 示例

既然你已经了解了类的构造方式以及描述它们的术语，就可以运用这些知识，以面向对象的方式创建两个示例。在第一个示例中，你开发一个用于计算矩形房间地板面积的类。在第二个示例中，你构造一个电梯对象。假设电梯可以在建筑物的第 1 层到第 15 层之间运行，并且必须始终知道电梯的位置。

## 示例 1：构造 Room 对象

在此示例中，你创建一个类，从中可以构造房间对象并计算其地板面积。出于建模目的，假设每个房间都是矩形的，因此地板面积可以按房间的长度乘以宽度来计算。

## 解决方案

在此应用程序中，你有一种类型的对象，即矩形房间，因此其地面面积可以通过房间的长度和宽度来确定。将这些值分配给房间后，就可以轻松地将房间的地板面积计算为房间的长度乘以宽度。因此，房间可以用名为 length 和 width 的双精度变量来表示。此外，你需要一个构造函数，以便在实例化房间对象时能够指定 length 和 width 的值。

