

main()
步骤1: Point p1 (2.3, -7.1)
步骤6: cout << p1.getX() << endl;
步骤8: return 0;

Point::Point(double x, double y)
步骤2: cout << "Constructing Point object, parameterized: \n";
步骤3: cout << "Input parameters: " << x << ", " << y << endl;
步骤4: xCoord = x;
步骤5: yCoord = y;

Point::getX()
步骤7: return xCoord;

内存快照：main()
步骤 1: Point p1
2.3 double xCoord
-7.1 double yCoord

图 6.6 程序跟踪和内存快照。

methods. 我们在类实现中定义了修改器方法。扩展的类实现如下。

```
/********************************************************************************/
/* Point Class Chapter6_7 */
/* filename: Point.cpp */
/* #include "Point.h" //Required for Point */
/* #include <iostream> //Required for cout */
/* #include <cmath> //Required for sqrt() and pow() */
using namespace std;

//Parameterized constructor
Point::Point(double x, double y)
{
//input parameters x,y
cout << " Constructing Point object, parameterized: \n";
cout << " Input parameters: " << x << ", " << y << endl;
xCoord = x;
yCoord = y;
}

//Default constructor
Point::Point()
{
cout << " Constructing Point object, default: \n";
cout << " initializing to zero" << endl;
xCoord = 0.0;
yCoord = 0.0;
}
```

//Distance Formula
double Point::operator -(const Point& rhs) const
{
 double t1, t2, d;
 t1 = rhs.xCoord - xCoord; // (x2-x1)
 t2 = rhs.yCoord - yCoord; // (y2-y1)
 d = sqrt( pow(t1,2) + pow(t2,2) );
 return d;
}
bool Point::operator ==(const Point& rhs) const
{
 if(rhs.xCoord == xCoord &&
    rhs.yCoord == yCoord )
    return true;
 else
    return false;
}
void Point::setX(double xVal)
{
 xCoord = xVal;
}
void Point::setY(double yVal)
{
 yCoord = yVal;
}

类方法可以访问调用对象的所有数据成员。我们在修改器方法 setX() 的实现中看到，输入参数 xVal 的值被赋给私有属性 xCoord。同样，在修改器方法 setY() 中，输入参数 yVal 的值被赋给私有属性 yCoord。

**语句框 6.3**

**方法定义：** 方法是类的成员函数。方法的定义由一个头部和随后的语句块组成。头部必须包含类名，后跟作用域解析运算符和方法名。

**语法：**
```
return-type class-name::method-name([parameter list])[modifier]
{
 //Statement block
 }
```

示例：
```
double Point::getX() const
{
    return xCoord;
}
void Point::setX(double newX)
{
    xCoord = newX;
}
```

我们对平面上点的定义并不限制可以合理分配给 x 和 y 坐标的值集合。实数集中的任何值都是合理的，因此在修改器方法中不需要对输入参数进行验证。在定义新数据类型时，通常可能存在对可以分配给一个或多个数据成员的值的自然限制。如果我们定义一个表示圆的新数据类型，并将圆定义为平面上的一个点和一个半径，那么给半径分配负值是不合理的。为了避免创建无意义的对象，可以在每个修改器方法中在分配新值之前执行测试。如果输入数据不在允许值的范围内，可以在方法内处理错误。因此，修改器方法允许应用程序修改对象的值或状态，同时保持对对象状态的控制。这在减少因意外处理错误数据而可能发生的错误传播方面非常有益。在修改器方法中验证数据的示例在第 10 章中说明。

我们将编写一个小型驱动程序来测试 Point 类中的修改器方法。驱动程序生成的输出如下。图 6.7 提供了程序跟踪和内存快照。

```
/*
 * Driver program to test Point class
 *
 * filename main.cpp
 */
#include "Point.h"
#include <iostream>
using namespace std;

int main()
{
    Point p1;
    p1.setX(2.3);
    p1.setY(1.5);
    cout << " p1.x is " << p1.getX() << endl;
    cout << " p1.y is " << p1.getY() << endl;
    return 0;
}
```

```
Ingbers-MacBook-Pro: Programs jaingber$ g++ main.cpp Point.cpp
Ingbers-MacBook-Pro: Programs jaingber$ ./a.out
Constructing Point object, default:
initializing to zero
p1.x is 2.3
p1.y is 1.5
```

main()
步骤1: Point p1;
步骤6: p1.setX(2.3);
步骤8: p1.setY(1.5);
步骤10: cout << "p1.x is " << p1.getX() << endl;
步骤12: cout << "p1.y is " << p1.getY() << endl;
步骤14: return 0;

Point::Point()
步骤2: cout << "Constructing Point object, default: \n";
步骤3: cout << "Initializing to zero" << endl;
步骤4: xCoord = 0.0;
步骤5: yCoord = 0.0;

Point::setX(double xVal)
步骤7: xCoord = xVal;

Point::setY(double yVal)
步骤9: yCoord = yVal;

Point::getX()
步骤11: return xCoord;

Point::getY()
步骤13: return yCoord;

内存快照：main()

步骤 1:
| Point p1 | 0.0 | double xCoord |
|---|---|---|
| | 0.0 | double yCoord |

步骤 6:
| Point p1 | 2.3 | double xCoord |
|---|---|---|
| | 0.0 | double yCoord |

步骤 8:
| Point p1 | 2.3 | double xCoord |
|---|---|---|
| | 1.5 | double yCoord |

图 6.7 驱动程序的程序跟踪和内存快照。

## 练习 6.3

以下问题涉及本节开发的 Point 类。请考虑下面给出的程序：

```
#include "Point.h"
#include <iostream>
using namespace std;
```

### 练习 6.3 续

```
int main()
{
    Point p1, p2; //line 1
    p1.xCoord = 3; //line 2
    cout << p1.getY(); //line 3
    cout << p1 - p2 << endl; //line 4
    return 0;
}
```

- 1. 该程序能否编译？
- 2. 第 1 行是否是有效语句？解释。
- 3. 第 2 行是否是有效语句？解释。
- 4. 第 3 行是否是有效语句？解释。
- 5. 第 4 行是否是有效语句？解释。
- 6. 向 Point 类添加一个修改器方法，允许应用程序同时修改 x 和 y 坐标。原型是：void setXY(double xVal, double yVal);

## 6.8 应用问题求解：复合材料设计

先进复合材料的设计是科学和工程许多领域中的重要问题。作为其应用的示例，封装材料目前正在被工程化，以绝缘电子组件中的关键部件免受热和机械冲击。封装材料在外部具有抗渗透韧性，同时在靠近电子组件的内部提供振动阻尼可能很重要。在此模拟中，我们正在建模两个圆柱之间空间中包含悬浮氧化铝颗粒的熔融塑料材料。最初，氧化铝颗粒均匀分布。当内圆柱旋转时，氧化铝颗粒从内圆柱迁移到外圆柱。氧化铝颗粒浓度越高，韧性越好；颗粒越少，振动阻尼效果越好。在此练习中，我们有兴趣确定位于临界半径之外的颗粒百分比，如图 6.8 所示。我们将使用在模拟过程中创建的名为 compositeMaterialsSim1.dat 的数据文件作为输入文件。

![](img/0235a4ea835dc4575bd036e024a533b3_322_0.png)

图 6.8 两个圆柱之间悬浮的颗粒。

### 1. 问题描述

一个名为 compositeMaterialsSim1.dat 的数据文件保存了模拟过程中记录的颗粒的 x,y 位置。编写一个 C++ 程序，确定位于用户指定临界半径之外的颗粒百分比。

### 2. 输入/输出描述

该程序的输入是一个名为 compositeMaterialsSim1.dat 的数据文件和临界半径。数据文件的第一行保存外圆柱的半径，接着是内圆柱的半径。每一行其余行保存一个颗粒的 x 和 y 位置。临界半径可能会变化，并由用户从键盘输入。

![](img/0235a4ea835dc4575bd036e024a533b3_323_0.png)

### 3. 手算示例

我们将使用仅四个颗粒进行手算示例，如下图所示：

![](img/0235a4ea835dc4575bd036e024a533b3_323_1.png)

