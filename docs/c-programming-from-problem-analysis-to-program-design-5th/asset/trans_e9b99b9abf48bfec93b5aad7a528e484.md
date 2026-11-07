
考虑以下 `class boxType` 带参数构造函数的定义：

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

在这个定义中，我们指定了 `rectangleType` 带有两个参数的构造函数。当 `boxType` 的这个构造函数执行时，它会触发类 `rectangleType` 中带有两个 `double` 类型参数的构造函数执行。

考虑以下语句：

```cpp
rectangleType myRectangle(5.0, 3.0);    //Line 1
boxType myBox(6.0, 5.0, 4.0);           //Line 2
```

第 1 行中的语句创建了 `rectangleType` 对象 `myRectangle`。因此，对象 `myRectangle` 有两个成员变量：length 和 width。第 2 行中的语句创建了 `boxType` 对象 `myBox`。因此，对象 `myBox` 有三个成员变量：length、width 和 height（见图 13–4）。

**图 13–4** 对象 `myRectangle` 和 `myBox`

![](img/1fbe55537254baeb2b5b7dbaf64956ae_775_0.png)

考虑以下语句：

```cpp
myRectangle.print();       //Line 3
cout << endl;              //Line 4
myBox.print();             //Line 5
cout << endl;              //Line 6
```

在第 3 行中的语句中，执行 `class rectangleType` 的成员函数 `print`。在第 5 行中的语句中，执行与 `class boxType` 关联的函数 `print`。回想一下，如果派生类重写了基类的成员函数，那么重定义只适用于派生类的对象。因此，第 3 行中语句的输出为：

Length = 5.0; Width = 3.0

第 5 行中语句的输出为：

Length = 6.0; Width = 5.0; Height = 4.0

当对象 myRectangle1 进入其作用域时，类 rectangleType 和 boxType 的构造函数会执行。注意，基类的构造函数不会在派生类中被继承。对基类构造函数的调用是在派生类构造函数的定义中指定的。当派生类构造函数执行时，首先执行基类的构造函数来初始化从基类继承的数据成员，然后执行派生类的构造函数来初始化派生类声明的数据成员。因此，首先执行类 rectangleType 的构造函数来初始化实例变量 length 和 width，然后执行类 boxType 的构造函数来初始化实例变量 height。

示例 13–2 中的程序展示了基类和派生类的对象的行为方式。

## 示例 13-2

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

    cout << "Line 6: myRectangle1: ";                  //Line 6
    myRectangle1.print();                               //Line 7
    cout << endl;                                       //Line 8
    cout << "Line 9: Area of myRectangle1: "            //Line 9
         << myRectangle1.area() << endl;

    cout << "Line 10: myRectangle2: ";                 //Line 10
    myRectangle2.print();                               //Line 11
    cout << endl;                                       //Line 12
    cout << "Line 13: Area of myRectangle2: "           //Line 13
         << myRectangle2.area() << endl;

    cout << "Line 14: myBox1: ";                    //Line 14
    myBox1.print();                              //Line 15
    cout << endl;                                //Line 16
    cout << "Line 17: Surface Area of myBox1: "  //Line 17
         << myBox1.area() << endl;
    cout << "Line 18: Volume of myBox1: "         //Line 18
         << myBox1.volume() << endl;

    cout << "Line 19: myBox2: ";                    //Line 19
    myBox2.print();                                //Line 20
    cout << endl;                                  //Line 21
    cout << "Line 22: Surface Area of myBox2: "    //Line 22
         << myBox2.area() << endl;
    cout << "Line 23: Volume of myBox2: "           //Line 23
         << myBox2.volume() << endl;

    return 0;                                      //Line 24
}
```

### 示例运行结果：

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

前面的程序按如下方式工作：第 1 行中的语句创建 rectangleType 对象 myRectangle1，并将其成员变量初始化为 0。第 2 行中的语句创建 rectangleType 对象 myRectangle2，并将其成员变量 length 和 width 分别初始化为 8.0 和 6.0。

第 3 行中的语句创建 boxType 对象 myBox1，并将其成员变量初始化为 0。第 4 行中的语句创建 boxType 对象 myBox2，并将其成员变量 length、width 和 height 分别初始化为 10.0、7.0 和 3.0。

第 5 行中的语句将小数输出设置为固定小数格式，保留两位小数，并显示小数点和尾随零。

第 6 行到第 9 行中的语句输出 myRectangle1 的长度、宽度和面积。由于 myRectangle1 的成员变量由默认构造函数初始化为 0，因此该矩形的面积为 0 平方单位。参见示例运行结果中的第 9 行。

第 10 行到第 13 行中的语句输出 myRectangle2 的长度、宽度和面积。由于 myRectangle2 的成员变量 length 和 width 由带参数的构造函数分别初始化为 8.0 和 6.0，因此该矩形的面积为 48.0 平方单位。参见示例运行结果中的第 13 行。

第 14 行到第 18 行中的语句输出 myBox1 的长度、宽度、高度、表面积和体积。由于 myBox1 的成员变量由默认构造函数初始化为 0，因此该盒子的表面积为 0.0 平方单位，体积为 0.0 立方单位。参见示例运行结果中的第 17 行和第 18 行。

第 19 行到第 23 行中的语句输出 myBox2 的长度、宽度、高度、表面积和体积。由于 myBox2 的成员变量 length、width 和 height 由带参数的构造函数分别初始化为 10.0、7.0 和 3.0，因此该盒子的表面积为 242.0 平方单位，体积为 210.0 立方单位。参见示例运行结果中的第 22 行和第 23 行。

从该程序的输出可以得出，类 boxType 中函数 print 和 area 的重定义只适用于 boxType 类型的对象。

> **（带默认参数的构造函数与继承层次结构）** 回想一下，类可以有带默认参数的构造函数。因此，派生类也可以有带默认参数的构造函数。例如，假设类 rectangleType 的定义如下所示。（为节省篇幅，这些定义没有文档说明。）

```cpp
class rectangleType
{
public:
    void setDimension(double l, double w);
    double getLength() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;
    void print() const;
    rectangleType(double l = 0, double w = 0);
    //Constructor with default parameters

private:
    double length;
    double width;
};
```

假设构造函数的定义如下：

```cpp
rectangleType::rectangleType(double l, double w)
{
    setDimension(l, w);
}
```
