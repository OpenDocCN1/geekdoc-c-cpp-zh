

在下一节中，我们将讨论在编写派生类构造函数的定义时，如何指定对基类构造函数的调用。

## 派生类和基类的构造函数

派生类可以有自己的私有成员变量，因此派生类可以显式包含自己的构造函数。构造函数通常用于初始化成员变量。当我们声明一个派生类对象时，该对象继承了基类的成员，但派生类对象不能直接访问基类的私有（数据）成员。派生类的成员函数也是如此。也就是说，派生类的成员函数不能直接访问基类的私有成员。

因此，派生类的构造函数只能（直接）初始化从基类继承的（公有数据）成员。所以，当声明一个派生类对象时，它还必须自动执行基类的一个构造函数。由于构造函数不能像其他函数那样被调用，派生类构造函数的执行必须触发基类某个构造函数的执行。事实上，情况正是如此。此外，对基类构造函数的调用在派生类构造函数的定义头部指定。

在上一节中，我们定义了rectangleType类，并从中派生出boxType类。此外，我们还说明了如何覆盖rectangleType类的成员函数。现在让我们讨论如何编写boxType类构造函数的定义。

rectangleType类有两个构造函数和两个成员变量。boxType类有三个成员变量：length、width和height。其中成员变量length和width继承自rectangleType类。

首先，让我们编写boxType类默认构造函数的定义。回顾一下，如果一个类包含默认构造函数，且在声明对象时没有指定任何值，则默认构造函数会执行并初始化该对象。由于rectangleType类包含默认构造函数，因此在编写boxType类的默认构造函数定义时，我们不需要指定基类的任何构造函数。

```cpp
boxType::boxType()
{
    height = 0.0;
}
```

接下来，我们讨论如何编写带参数的构造函数的定义。为了触发基类的（带参数的）构造函数执行，你需要在派生类构造函数的定义头部指定基类构造函数的名称及参数。

考虑下面boxType类带参数的构造函数的定义：

```cpp
boxType::boxType(double l, double w, double h)
    : rectangleType(l, w)
{
    if (h >= 0)
        height = h;
    else
        height = 0;
}
```

在这个定义中，我们指定了带两个参数的rectangleType构造函数。当这个boxType构造函数执行时，它会触发rectangleType类带两个double类型参数的构造函数执行。

考虑下面的语句：

```cpp
rectangleType myRectangle(5.0, 3.0);  //Line 1
boxType myBox(6.0, 5.0, 4.0);         //Line 2
```

第1行中的语句创建了rectangleType对象myRectangle。因此，对象myRectangle有两个成员变量：length和width。第2行中的语句创建了boxType对象myBox。因此，对象myBox有三个成员变量：length、width和height（见图11-4）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_764_0.png)

**图11-4** 对象myRectangle和myBox

考虑下面的语句：

```cpp
myRectangle.print();     //Line 3
cout << endl;            //Line 4
myBox.print();           //Line 5
cout << endl;            //Line 6
```

在第3行的语句中，执行了rectangleType类的成员函数print。在第5行的语句中，执行了与boxType类相关联的print函数。回顾一下，如果派生类覆盖了基类的成员函数，则重定义仅适用于派生类的对象。因此，第3行语句的输出是：

```cpp
Length = 5.0; Width = 3.0
```

第5行语句的输出是：

Length = 6.0; Width = 5.0; Height = 4.0

当对象myBox进入其作用域时，rectangleType类和boxType类的构造函数都会执行。注意，基类的构造函数不会被派生类继承。对基类构造函数的调用是在派生类构造函数的定义中指定的。当派生类构造函数执行时，首先执行基类的一个构造函数，以初始化从基类继承的数据成员，然后执行派生类的构造函数，以初始化由派生类声明的数据成员。因此，首先执行rectangleType类的构造函数来初始化实例变量length和width，然后执行boxType类的构造函数来初始化实例变量height。

示例11-2中的程序演示了基类对象和派生类对象的行为方式。

### 示例 11-2

在这个示例中，我们编写一个程序来解决以下问题：

- 1. 吉姆的草坪护理店专门为小农场和家庭草坪围栅栏，并为农场和草坪施肥。为简单起见，我们假设庭院和农场都是矩形。为了围栅栏，程序需要知道周长；为了施肥，程序需要知道面积。我们将编写一个程序，使用rectangleType类来存储庭院或农场的尺寸。程序还会提示用户输入庭院或农场的尺寸（以英尺为单位）、围栅栏的成本（每英尺）以及施肥的成本（每平方英尺）。然后，程序将输出围栅栏和施肥的费用。
- 2. 琳达的礼品店专门包装小包裹。为简单起见，我们假设包裹是带有特定长度、宽度和高度的长方体形状。我们将编写一个程序，使用boxType类来存储包裹的尺寸。程序将要求用户输入包裹的尺寸以及包装包裹的成本（每平方英尺）。然后，程序将输出包装包裹的费用。（程序假设包装包裹的最低费用为$1.00。）

考虑以下C++程序：

```cpp
#include <iostream>                 //Line 1
#include <iomanip>                  //Line 2
#include "rectangleType.h"          //Line 3
#include "boxType.h"                //Line 4
using namespace std;                                                       //Line 5

int main()
{                                                                          //Line 7
    rectangleType yard;                                                    //Line 8
    double fenceCostPerFoot;                                               //Line 9
    double fertilizerCostPerSquareFoot;                                    //Line 10
    double length, width;                                                  //Line 11
    double billingAmount;                                                  //Line 12

    cout << fixed << showpoint << setprecision(2);                         //Line 13

    cout << "Line 14: Enter the length and width of the "                  //Line 14
         << "yard (in feet): ";                                            //Line 15
    cin >> length >> width;                                                //Line 16
    cout << endl;

    yard.setDimension(length, width);                                      //Line 17

    cout << "Line 18: Enter the cost of fence "                            //Line 18
         << "(per foot): $";                                               //Line 19
    cin >> fenceCostPerFoot;                                               //Line 20
    cout << endl;

    cout << "Line 21: Enter the cost of fertilizer "                       //Line 21
         << "(per square foot): $";                                        //Line 22
    cin >> fertilizerCostPerSquareFoot;                                    //Line 23
    cout << endl;

    billingAmount = yard.perimeter() * fenceCostPerFoot                    //Line 24
                  + yard.area() * fertilizerCostPerSquareFoot;

    cout << "Line 25: Amount due: $" << billingAmount                      //Line 25
         << endl;

    boxType package;                                                       //Line 26
    double height;                                                         //Line 27
    double wrappingCostPerSquareFeet;                                      //Line 28

    cout << "Line 29: Enter the length, width, and height "                //Line 29
         << "of the package (in feet): ";                                  //Line 30
    cin >> length >> width >> height;                                      //Line 31
    cout << endl;

    package.setDimension(length, width, height);                           //Line 32

    cout << "Line 33: Enter the cost (25 to 50 cents) of "                 //Line 33
         << "wrapping per square foot: ";                                  //Line 34
    cin >> wrappingCostPerSquareFeet;                                      //Line 35
    cout << endl;

    billingAmount = wrappingCostPerSquareFeet                              //Line 36
                  * package.area() / 100;

    if (billingAmount < 1.00)                                              //Line 37
        billingAmount = 1.00;                                              //Line 38
```

