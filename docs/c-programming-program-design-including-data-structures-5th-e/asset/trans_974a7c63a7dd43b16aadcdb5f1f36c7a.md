
函数 `setDimension` 的定义为：

```cpp
void boxType::setDimension(double l, double w, double h)
{
    rectangleType::setDimension(l, w);

    if (h >= 0)
        height = h;
    else
        height = 0;
}
```

请注意，在上述函数 `setDimension` 的定义中，对 `class` `rectangleType` 的成员函数 `setDimension` 的调用前面加上了类名和作用域解析运算符，尽管 `class` `boxType` 重载——而不是重写——函数 `setDimension`。

函数 `getHeight` 的定义为：

```cpp
double boxType::getHeight() const
{
    return height;
}
```

`class` `boxType` 的成员函数 area 确定盒子的表面积。要确定盒子的表面积，我们需要访问盒子的长度和宽度，它们被声明为 `class` `rectangleType` 的 `private` 成员。因此，我们使用 `class` `rectangleType` 的成员函数 `getLength` 和 `getWidth` 分别获取长度和宽度。由于 `class` `boxType` 不包含任何名为 `getLength` 或 `getWidth` 的成员函数，我们调用 `class` `rectangleType` 的这些成员函数时不使用基类名。

```cpp
double boxType::area() const
{
    return 2 * (getLength() * getWidth()
              + getLength() * height
              + getWidth() * height);
}
```

`class` `boxType` 的成员函数 volume 确定盒子的体积。要确定盒子的体积，可以将盒子的长度、宽度和高度相乘，或者将盒子底面积乘以其高度。我们用第二种方式编写成员函数 volume 的定义。为此，可以使用 `class` `rectangleType` 的成员函数 area 来确定底面积。因为 `class` `boxType` 重写了成员函数 area，为了指定调用 `class` `rectangleType` 的成员函数 area，我们使用基类名和作用域解析运算符，如下面的定义所示：

```cpp
double boxType::volume() const
{
    return rectangleType::area() * height;
}
```

考虑以下类 `boxType` 的带参数构造函数的定义：

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

在此定义中，我们指定了 `rectangleType` 的带两个参数的构造函数。当 `boxType` 的这个构造函数执行时，会触发类 `rectangleType` 中带两个 `double` 类型参数的构造函数执行。

考虑以下语句：

```cpp
rectangleType myRectangle(5.0, 3.0);    //Line 1
boxType myBox(6.0, 5.0, 4.0);             //Line 2
```

第 1 行的语句创建 rectangleType 对象 myRectangle。因此，对象 myRectangle 有两个成员变量：length 和 width。第 2 行的语句创建 boxType 对象 myBox。因此，对象 myBox 有三个成员变量：length、width 和 height（见图 12-4）。

![](img/f97f778697507bb6fdd80c5991210cba_728_0.png)

**图 12-4** 对象 *myRectangle* 和 *myBox*

考虑以下语句：

```cpp
myRectangle.print();      //Line 3
cout << endl;             //Line 4
myBox.print();            //Line 5
cout << endl;             //Line 6
```

第 3 行的语句中，执行类 `rectangleType` 的成员函数 `print`。第 5 行的语句中，执行与类 `boxType` 关联的函数 `print`。回想一下，如果派生类重写了基类的成员函数，则该重定义仅适用于派生类的对象。因此，第 3 行语句的输出为：

```text
Length = 5.0; Width = 3.0
```

第 5 行语句的输出为：

```text
Length = 6.0; Width = 5.0; Height = 4.0
```

当对象 myBox 进入其作用域时，类 rectangleType 和 boxType 的构造函数会执行。注意，基类的构造函数不会在派生类中继承。对基类构造函数的调用在派生类构造函数的定义中指定。当派生类构造函数执行时，首先执行基类的构造函数来初始化从基类继承的数据成员，然后执行派生类的构造函数来初始化派生类声明的数据成员。因此，首先执行类 rectangleType 的构造函数来初始化实例变量 length 和 width，然后执行类 boxType 的构造函数来初始化实例变量 height。

示例 12–2 中的程序展示了基类对象和派生类对象的行为方式。

## 示例 12-2

考虑以下 C++ 程序：

```cpp
#include <iostream>
#include <iomanip>
#include "rectangleType.h"
#include "boxType.h"

using namespace std;

int main()
{
    rectangleType myRectangle1;                         //Line 1
    rectangleType myRectangle2(8, 6);                   //Line 2

    boxType myBox1;                                     //Line 3
    boxType myBox2(10, 7, 3);                            //Line 4

    cout << fixed << showpoint << setprecision(2);      //Line 5

    cout << "Line 6: myRectangle1: ";                   //Line 6
    myRectangle1.print();                                //Line 7
    cout << endl;                                        //Line 8
    cout << "Line 9: Area of myRectangle1: "            //Line 9
         << myRectangle1.area() << endl;

    cout << "Line 10: myRectangle2: ";                  //Line 10
    myRectangle2.print();                                //Line 11
    cout << endl;                                        //Line 12
    cout << "Line 13: Area of myRectangle2: "
         << myRectangle2.area() << endl;                 //Line 13

    cout << "Line 14: myBox1: ";                 //Line 14
    myBox1.print();                              //Line 15
    cout << endl;                                //Line 16
    cout << "Line 17: Surface Area of myBox1: "
         << myBox1.area() << endl;               //Line 17
    cout << "Line 18: Volume of myBox1: "
         << myBox1.volume() << endl;             //Line 18

    cout << "Line 19: myBox2: ";                 //Line 19
    myBox2.print();                              //Line 20
    cout << endl;                                //Line 21
    cout << "Line 22: Surface Area of myBox2: "
         << myBox2.area() << endl;               //Line 22
    cout << "Line 23: Volume of myBox2: "
         << myBox2.volume() << endl;             //Line 23

    return 0;                                    //Line 24
}
```

### 运行示例：

```text
Line 6: myRectangle1: Length = 0.00; Width = 0.00
Line 9: Area of myRectangle1: 0.00
Line 10: myRectangle2: Length = 8.00; Width = 6.00
Line 13: Area of myRectangle2: 48.00
Line 14: myBox1: Length = 0.00; Width = 0.00; Height = 0.00
Line 17: Surface Area of myBox1: 0.00
Line 18: Volume of myBox1: 0.00
Line 19: myBox2: Length = 10.00; Width = 7.00; Height = 3.00
Line 22: Surface Area of myBox2: 242.00
Line 23: Volume of myBox2: 210.00
```

前面的程序按如下方式工作：第 1 行的语句创建 rectangleType 对象 myRectangle1，并将其成员变量初始化为 0。第 2 行的语句创建 rectangleType 对象 myRectangle2，并将其成员变量 length 和 width 分别初始化为 8.0 和 6.0。

第 3 行的语句创建 boxType 对象 myBox1，并将其成员变量初始化为 0。第 4 行的语句创建 boxType 对象 myBox2，并将其成员变量 length、width 和 height 分别初始化为 10.0、7.0 和 3.0。

第 5 行的语句将程序输出设置为固定小数格式，并保留小数点和尾随零，保留两位小数。

第 6 行到第 9 行的语句输出 myRectangle1 的长度、宽度和面积。因为默认构造函数将 myRectangle1 的成员变量初始化为 0，所以该矩形的面积为 0 平方单位。请参见运行示例中的第 9 行。

第 10 行到第 13 行的语句输出 myRectangle2 的长度、宽度和面积。因为带参数的构造函数将 myRectangle2 的成员变量 length 和 width 分别初始化为 8.0 和 6.0，所以该矩形的面积为 48.0 平方单位。请参见运行示例中的第 13 行。
