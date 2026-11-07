
在下一节中，我们将讨论在编写派生类构造函数的定义时，如何指定对基类构造函数的调用。

## 派生类和基类的构造函数

派生类可以拥有自己的私有成员变量，因此派生类可以显式地包含自己的构造函数来初始化这些变量。当我们声明一个派生类对象时，该对象会继承基类的成员，但派生类对象不能直接访问基类的私有（数据）成员。派生类的成员函数也是如此。也就是说，派生类的成员函数不能直接访问基类的私有成员。

因此，派生类的构造函数只能（直接）初始化从派生类的基类继承来的（公有数据）成员。于是，当声明一个派生类对象时，还必须触发执行基类的某个构造函数。此外，这种对基类构造函数的触发是在派生类构造函数的*定义的首部*中指定的。

首先，让我们编写类 boxType 的默认构造函数的定义。回顾一下，如果一个类包含默认构造函数，并且在声明对象时没有指定任何值，那么默认构造函数会执行并初始化该对象。因为类 rectangleType 包含默认构造函数，所以在编写类 boxType 的默认构造函数的定义时，我们不指定基类的任何构造函数。

```cpp
boxType::boxType()
{
    height = 0.0;
}
```

要编写带参数的类 boxType 构造函数的定义，我们首先编写类 boxType 构造函数的首部，其中包含*基类构造函数和派生类构造函数所需的所有参数*；也就是说，包含 boxType 和 rectangleType 两者所需的所有参数。然后，为了触发带参数的基类构造函数执行，我们在派生类构造函数的定义首部中，在首部后添加一个冒号（:），后面跟上基类构造函数的名称及其参数。实际上，我们通过冒号将基类构造函数“附加”到派生类构造函数上。派生类构造函数获得它自身和基类构造函数所需的所有参数，然后将基类参数传递给基类构造函数。

考虑以下类 `boxType` 的带参数构造函数的定义：

```cpp
boxType::boxType (double l, double w, double h)
             : rectangleType(l, w)
{
    if (h >= 0)
        height = h;
    else
        height = 0;
}
```

在这个定义中，我们指定了 `rectangleType` 的带两个参数的构造函数。当 `boxType` 的这个构造函数执行时，它会触发类 `rectangleType` 的带两个 double 类型参数的构造函数执行。

考虑以下语句：

```cpp
rectangleType myRectangle(5.0, 3.0);    //Line 1
boxType myBox(6.0, 5.0, 4.0);            //Line 2
```

第 1 行中的语句创建了 `rectangleType` 对象 `myRectangle`。因此，对象 `myRectangle` 有两个成员变量：length 和 width。第 2 行中的语句创建了 `boxType` 对象 `myBox`。因此，对象 `myBox` 有三个成员变量：length、width 和 height（见图 11-4）。

![](img/d0be7fc6d804b63484835c6c8bc67a07_799_0.png)

**图 11-4** 对象 `myRectangle` 和 `myBox`

考虑以下语句：

```cpp
myRectangle.print();       //Line 3
cout << endl;              //Line 4
myBox.print();             //Line 5
cout << endl;              //Line 6
```

在第 3 行中的语句中，执行类 `rectangleType` 的成员函数 `print`。在第 5 行中的语句中，执行与类 `boxType` 关联的函数 `print`。回顾一下，如果派生类重写了基类的成员函数，那么重定义只适用于派生类的对象。因此，第 3 行中的语句输出为（如类 `rectangleType` 中所定义）：

```text
Length = 5.0; Width = 3.0
```

第 5 行中的语句输出为（如类 `boxType` 中所定义）：

Length = 6.0; Width = 5.0; Height = 4.0

当对象 `myBox` 进入其作用域时，类 `rectangleType` 和 `boxType` 的构造函数都会执行。注意，基类的构造函数不会被派生类继承。因此，如果基类包含 `private` 数据成员，那么只有基类构造函数才能构造基类，包括派生类的基类部分。在这种情况下，派生类构造函数只能构造其定义中指定的额外成员。这意味着，派生类构造函数的定义中必须包含对基类构造函数的调用。

当派生类构造函数执行时，首先执行基类的构造函数以初始化从基类继承的数据成员，然后执行派生类的构造函数以初始化派生类声明的数据成员。因此，首先执行类 `rectangleType` 的构造函数来初始化实例变量 length 和 width，然后执行类 `boxType` 的构造函数来初始化实例变量 height。

示例 11-2 中的程序展示了基类对象和派生类对象的行为。

### 示例 11-2

在本示例中，我们编写一个程序来解决以下问题：

- 1. Jim 的草坪护理店专门为小农场和家庭草坪围栅栏，并为农场和草坪施肥。为简单起见，我们假设庭院和农场都是矩形的。为了围栅栏，程序需要知道周长；为了施肥，程序需要知道面积。我们将编写一个程序，使用类 `rectangleType` 存储庭院或农场的尺寸。程序还会提示用户输入庭院或农场的尺寸（以英尺为单位）、围栅栏的成本（每英尺）以及施肥的成本（每平方英尺）。然后程序将输出围栅栏和施肥的成本。
- 2. Linda 的礼品店专门包装小包裹。为简单起见，我们假设包裹是一个具有特定长、宽、高的盒子形状。我们将编写一个程序，使用类 `boxType` 记录包裹的尺寸。程序会要求用户输入包裹的尺寸以及包装包裹的成本（每平方英尺）。然后程序将输出包装该包裹的成本。（程序假设包装一个包裹的最低成本为 1.00 美元。）

考虑以下 C++ 程序：

```cpp
#include <iostream>                                      //Line 1
#include <iomanip>                                       //Line 2
#include "rectangleType.h"                              //Line 3
#include "boxType.h"                                    //Line 4
using namespace std;                                         //Line 5

int main()                                                   //Line 6
{                                                            //Line 7
    rectangleType yard;                                      //Line 8
    double fenceCostPerFoot;                                 //Line 9
    double fertilizerCostPerSquareFoot;                      //Line 10
    double length, width;                                    //Line 11
    double billingAmount;                                    //Line 12

    cout << fixed << showpoint << setprecision(2);           //Line 13

    cout << "Line 14: Enter the length and width of the "    //Line 14
         << "yard (in feet): ";                              //Line 15
    cin >> length >> width;                                  //Line 16
    cout << endl;

    yard.setDimension(length, width);                        //Line 17

    cout << "Line 18: Enter the cost of fence "              //Line 18
         << "(per foot): $";                                 //Line 19
    cin >> fenceCostPerFoot;                                 //Line 20
    cout << endl;

    cout << "Line 21: Enter the cost of fertilizer "         //Line 21
         << "(per square foot): $";                          //Line 22
    cin >> fertilizerCostPerSquareFoot;                      //Line 23
    cout << endl;

    billingAmount = yard.perimeter() * fenceCostPerFoot
                  + yard.area() * fertilizerCostPerSquareFoot; //Line 24

    cout << "Line 25: Amount due: $" << billingAmount        //Line 25
         << endl;

    boxType package;                                         //Line 26
    double height;                                           //Line 27
    double wrappingCostPerSquareFeet;                        //Line 28

    cout << "Line 29: Enter the length, width, and height "  //Line 29
         << "of the package (in feet): ";                    //Line 30
    cin >> length >> width >> height;                        //Line 31
    cout << endl;

    package.setDimension(length, width, height);             //Line 32

    cout << "Line 33: Enter the cost (25 to 50 cents) of "   //Line 33
         << "wrapping per square foot: ";                    //Line 34
    cin >> wrappingCostPerSquareFeet;                        //Line 35
    cout << endl;

    billingAmount = wrappingCostPerSquareFeet
                  * package.area() / 100;                    //Line 36

    if (billingAmount < 1.00)                                //Line 37
        billingAmount = 1.00;                                //Line 38
```
