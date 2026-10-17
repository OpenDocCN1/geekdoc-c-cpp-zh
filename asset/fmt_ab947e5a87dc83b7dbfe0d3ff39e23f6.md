
| `main()` |  |
| :--- | :--- |
| 第 1 步: `Point` `p1` (2.3, -7.1) |  |
| 第 6 步: `cout` << `p1.getX()` << `endl`; |  |
| 第 8 步: `return` 0; |  |

| `Point::Point` (double `x`, double `y`) |  |
| :--- | :--- |
| 第 2 步: `cout` << "Constructing Point object, parameterized: \n"; |  |
| 第 3 步: `cout` << "input parameters: " << `x` << " " << `y` << `endl`; |  |
| 第 4 步: `XCoord` = `x`; 第 5 步: `yCoord` = `y`; |  |

| `Point::getX` () |  |
| :--- | :--- |
| 第 7 步: `return` `xCoord`; |  |

| 内存快照: `main`(my) |  |
| :--- | :--- |
| 第 1 步: `Point` `p1` | 2.3 `double` `xCoord` |
| | -7.1 `double` `yCoord` |

**图 6.6** 程序追踪和内存快照。

访问器方法 `getX()` 是公共的，程序现在可以编译且没有错误。追踪和内存快照所示。

### 变器方法

变器方法是带有一个或多个参数的 `void` 函数。变器方法的目的是更改属性的值。在 `setX()` 的实现中，我们看到输入参数 `newX` 的值赋值给属性 `xCoord`。同样，在变器方法 `setY()` 中，输入参数 `newY` 的值被赋值给属性 `yCoord`。目前的惯例是将这些方法命名为 `setAttribute()`。

| 示例： |  |
| :--- | :--- |
| `double` `Point::getX()` `const` | { `return` `xCoord`; } |
| `void` `Point::setX`(double `newX`) | { `xCoord` = `newX`; } |

## 第 6 章 使用函数的模块化编程

我们将编写一个小型的驱动程序来测试类中的修改器方法（mutator methods）。驱动程序生成的输出所示。图 6.7 提供了程序执行轨迹和内存快照。

```cpp
/*
 * 用于测试 Point 类的驱动程序
 * filename main.cpp
 */
#include "Point.h"
#include <iostream>
using namespace std;
main() {
Step 1: Point p1();
Step 6: p1.setX(2.3);
Step 8: p1.setY(1.5);
Step 10: cout << "p1.x is " << p1.getX() << endl;
Step 12: cout << "p1.y is " << p1.getY() << endl;
Step 14: return 0;
}
Point::Point() {
Step 2: cout << "Constructing \nPoint object, default: \n";
Step 3: cout << "initializing to zero\n" << endl;
Step 4: xCoord = 0;
Step 5: yCoord = 0;
}
Point::setX(double xVal) {
Step 7: xCoord = xVal;
}
Point::setY(double yVal) {
Step 9: yCoord = yVal;
}
Point::getX() {
Step 11: return xCoord;
}
Point::getY() {
Step 13: return yCoord;
}
```

内存快照：`main()`

| Step 1: | `Point` `p1` | 0.0 | `double` `xCoord` |
| :--- | :--- | :--- | :--- |
| | | 0.0 | `double` `yCoord` |
| Step 6: | `Point` `p1` | 2.3 | `double` `xCoord` |
| | | 0.0 | `double` `yCoord` |
| Step 8: | `Point` `p1` | 2.3 | `double` `xCoord` |
| | | 1.5 | `double` `yCoord` |

图 6.7 驱动程序的程序轨迹和内存快照。

### 6.7 节 定义类方法

```cpp
int main()
{
    Point pl1;
    pl1.setX(2.3);
    pl1.setY(1.5);
    cout << " pl1.x is " << pl1.getX() << endl;
    cout << " pl1.y is " << pl1.getY() << endl;
    return 0;
}
```

`Ingers-MacBook-Pro:Programs jainger$` `g++` `main.cpp` `Point.cpp`
`Ingers-MacBook-Pro:Programs jainger$` `./a`
Constructing Point object, default:
initializing to zero
pl1.x is 2.3
pl1.y is 1.5

### 练习！

以下问题涉及本节开发的 `Point` 类。考虑给出的程序：

```cpp
#include "Point.h"
#include <iostream>
using namespace std;
int main()
{
    Point pl1, p2; //line 1
    pl1.xCoord = 3; //line 2
    cout << pl1.getY(); //line 3
    cout << pl1 - p2 << endl; //line 4
    return 0;
}
```

1. 第 1 行是有效的语句吗？解释。
2. 第 2 行是有效的语句吗？解释。
3. 第 3 行是有效的语句吗？解释。
4. 第 4 行是有效的语句吗？解释。
5. 为 `Point` 类添加一个修改器方法，允许应用程序修改 x 和 y 坐标。其原型为：`void setXY(double xVal, double yVal);`

## 第 6 章 使用函数的模块化编程

## 6.8 应用问题解决：复合材料的设计

先进复合材料的设计是许多科学和工程领域的一个重要问题。作为其应用示例，封装材料目前正被设计用于保护电子组装中的关键部件，免受热冲击和机械冲击的影响。对于封装材料来说，外部具有足够的韧性以防止渗透，同时在靠近电子组件的内部提供振动阻尼可能是重要的。在本次模拟中，我们对两个圆柱之间的空间内悬浮氧化铝颗粒的熔融材料建模建模。当内圆柱旋转时，氧化铝颗粒从内圆柱均匀地迁移到外圆柱。氧化铝颗粒浓度越高，韧性越强；颗粒越少，振动阻尼越好。在本次练习中，我们感兴趣的是位于关键半径外的颗粒百分比，如图 6.8 所示。我们将使用模拟过程中创建名为 `compositeMaterialsSim1.dat` 的数据文件作为输入文件。

![](img/4456642232e4f4a18bd7dfe37e70176d_291_0.png)

**图 6.8** 悬浮在两个圆柱之间的颗粒。

### 1. 问题描述

名为 `compositeMaterialsSim1.dat` 的数据文件存储了模拟期间记录的颗粒 x、y 位置。编写一个 C++ 程序来确定位于用户指定的关键半径外的颗粒百分比。

### 2. 输入/输出描述

该程序的输入是名为 `compositeMaterialsSim1.dat` 的数据文件和关键半径。数据文件的第一行保存外圆柱的半径，随后是内圆柱的半径。剩余每行包含一个颗粒的 x 和 y 位置。关键半径可以由用户输入。

![](img/4456642232e4f4a18bd7dfe37e70176d_291.png)

### 3. 手动示例

我们将处理一个手动示例，如下所示：

![](img/4456642232e4f4a18bd7dfe3770176d_292_0.png)

我们示例的数据文件为：

```
10.0
5.0
2.0 3.0
1.0 4.0
8.0 9.0
```

```cpp
#include <iostream> // 用于 cin, cout
#include <fstream> // 用于文件输入
using namespace std;
// 函数原型
double distance(double x1, double y1, double x2, double y2);
int main()
{
    // 声明对象
    int pointCount(0), outside(0);
    double x,y,criticalRad;
    const double xORIGIN(0), yORIGIN(0);
    double dist, radiusOuter, radiusInner;
    // 打开输入文件
    ifstream fin("compositeMaterialsSim.dat");
    if(fin.fail()) {
        cout << "Could not open data file compositeMaterialsSim.dat" << endl;
        exit(1);
    }
    // 用户输入关键半径
    cout << "Enter critical radius ";
    cin >> criticalRad;
    // 输入外圆柱和内圆柱的半径
    fin >> radiusOuter >> radiusInner;
    // 在文件结束前，输入点数据
    fin >> x >> y;
    while(!fin.eof()) {
        ++pointCount; // 点数计数器加一
        dist = distance(x,y,xORIGIN, yORIGIN);
        if(dist > criticalRad) {
            ++outside; // 外部计数器加一
        }
        fin >> x >> y;
    }
    // 输出结果
    // 乘以 100.0 以强制进行浮点数运算
    cout << (100.0*outside/pointCount)
         << "% lie outside the critical radius" << endl;
    return 0;
}
#include <cmath> // 用于 sqrt 和 pow
double distance(double x1, double y1, double x2, double y2);
```

## 6.8 节 应用问题解决：复合材料设计

```cpp
double d1, d2, d;
d1 = x2-x1;
d2 = y2-y1;
d = sqrt(pow(d1,2) + pow(d2,2));
return d;
```
