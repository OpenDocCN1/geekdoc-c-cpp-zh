

# 示例 10.1 以度数显示角度

```
/* Program demonstrating the use of a void function printDegrees() to display an angle in degrees.

    Input:  the radian measure of an angle and a user response to whether more angles are to be input
    Output: the angle measurement (displayed by printDegrees())
    ---------------------------------------------------------------*/

#include <iostream>      // cout, cin, <<, >>
using namespace std;

void printDegrees(double radians);   // prototype for printDegrees()
int main()
{
    cout << "This program converts radian measure of angles to\n" "degrees-minutes-seconds units.\n\n";
    char response;

    do
    {
        cout << "Enter the radian measure of an angle: ";
        double numRadians;
        cin >> numRadians;

        printDegrees(numRadians);

        cout << "\nMore angles (Y or N)? ";
        cin >> response;
    }
    while (response == 'y' || response == 'Y');
}

/* Function to convert radian measure of an angle to degrees-minutes-seconds format and output it.

    Receive: radians
    Output:  radians and equivalent degrees, minutes, seconds
    ---------------------------------------------------------------*/

void printDegrees(double radians)
{
    const double PI = 3.14159;
    double degreeMeasure = (180.0 / PI) * radians;

    int degrees = int(degreeMeasure);
    degreeMeasure -= degrees;
    degrees %= 360;
    degreeMeasure *= 60.0;
    
    int minutes = int(degreeMeasure);
    degreeMeasure -= minutes;
    degreeMeasure *= 60.0;
    int seconds = int(degreeMeasure);

    cout << radians << " radians is equivalent to\n"
         << degrees << " degrees, " << minutes << " minutes, "
         << seconds << " seconds" << endl;
}
```

# 示例运行：

```
This program converts radian measure of angles to the
degrees-minutes-seconds units.

Enter the radian measure of an angle: 0
0 radians is equivalent to
0 degrees, 0 minutes, 0 seconds

More angles (Y or N)? Y
Enter the radian measure of an angle: 3.14159
3.14159 radians is equivalent to
180 degrees, 0 minutes, 0 seconds

More angles (Y or N)? Y
Enter the radian measure of an angle: 1
1 radians is equivalent to
57 degrees, 17 minutes, 44 seconds

More angles (Y or N)? N
```

## 10.1.2 示例 2：转换坐标

前一示例中的函数接收一个值，但与前几章中的大多数函数不同，它不返回值。在本示例中，我们的函数将接收两个值，即平面上点 $P$ 的 **极坐标** $(r, \theta)$，但也必须返回两个值，即该点的 **直角坐标** $(x, y)$。

第一个极坐标 $r$ 是原点到 $P$ 的距离，第二个极坐标 $\theta$ 是从正 $x$ 轴到连接原点与 $P$ 的射线的角度。

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_369_0.png)

极坐标与点直角坐标之间的关系公式为

$$x = r\cos\theta$$

$$y = r\sin\theta$$

从技术上讲，C++ 函数不能返回两个值，因为执行 return 语句会立即终止函数的执行。因此，写成如下形式将不起作用

```
double polarToRectangular(double r, double theta)
{
    return r * cos(theta);
    return r * sin(theta);    // Execution won't get here!
}
```

因为第一个 return 语句会导致函数执行终止，所以第二个 return 语句永远不会被执行。而且，函数的 return 语句形式为

```
return expression;
```

因此，只能使用 return 语句向调用者返回单个值。

由于我们不能返回多个值，我们可能尝试通过一些额外的参数来向调用者传达信息。例如，我们可能尝试写成

```
double polarToRectangular(double r, double theta, double x, double y)
{
    x = r * cos(theta);
    y = r * sin(theta);
}
```

然后按如下方式调用函数：

```
double xCoord = 0,
    yCoord = 0;
polarToRectangular(1.5, 0.7854, xCoord, yCoord);
```

这是一个好主意，但不幸的是，它不会起作用，因为 C++ 参数默认是其对应实参的副本。也就是说，参数 x 包含其实参 xCoord 的副本，参数 y 包含其实参 yCoord 的副本。执行时，polarToRectangular() 修改这些副本，使实参 xCoord 和 yCoord 保持不变。

我们需要一种方法来“关闭”导致参数成为其实参副本的机制。为此目的，C++ 提供了引用参数，它不是参数的副本，而是将所有访问直接指回其实参。这是通过在参数的名称与其类型之间插入一个与号（&）来实现的。¹ 因此，我们函数的头部变为

```
void polarToRectangular(double r, double theta, double & x, double & y)
```

> ¹ 有些程序员更喜欢将与号附加到类型名上，如 double& x，而其他人更喜欢将其附加到参数名上——double &x。在本教材中，我们将简单地将其放在类型名和参数名之间。

普通参数（如 r 和 theta）是其实参的副本，因此只将值移入函数；引用参数（如 x 和 y）指回其实参，因此将值同时移入和移出函数。请注意，由于值仅通过引用参数传回调用者，因此使用 void 表示函数不通过 return 语句返回值。示例 10.2 显示了完整的函数以及测试它的驱动程序。

# 示例 10.2 转换坐标

```
/* This program computes the rectangular coordinates of points with given polar coordinates.

Input: polar coordinates of points in the plane
Output: the corresponding rectangular coordinates
--------------------------------------------------------------------------*/

#include <iostream>          // <<, >>, cout, cin
#include <iomanip>           // fixed, showpoint, setprecision()
#include <cmath>             // cos(), sin()
using namespace std;

void polarToRectangular(double r, double theta, double &x, double &y);

int main()
{
    cout << "This program converts polar coordinates to rectangular\n"
         << "coordinates using the void function polarToRectangular()\n\n";

    char response;
    do
    {
        cout << "Enter the polar coordinates of a point: ";
        double rCoord, tCoord,    // polar coordinates
               xCoord, yCoord;    // rectangular coordinates
        cin >> rCoord >> tCoord;

        polarToRectangular(rCoord, tCoord, xCoord, yCoord);
        cout << fixed << showpoint << setprecision(2)
             << "Rectangular coordinates are: "
             << xCoord << " " << yCoord << endl;

        cout << "\nMore conversions (Y or N)? ";
        cin >> response;
    }
    while (response == 'y' || response == 'Y');
}
```

```
/* Function to convert polar coordinates to rectangular coordinates.

Receive:  polar coordinates r and theta
Pass back: rectangular coordinates x and y
------------------------------------------------------------ */

void polarToRectangular(double r, double theta, double &x, double &y)
{
    x = r * cos(theta);
    y = r * sin(theta);
}
```

# 示例运行：

This program converts polar coordinates to rectangular coordinates using the void function polarToRectangular()

Enter the polar coordinates of a point: 1.414 0.783
Rectangular coordinates are: 1.00 1.00

More conversions (Y or N)? Y
Enter the polar coordinates of a point: 2.0 3.14159
Rectangular coordinates are: -2.00 -0.00

More conversions (Y or N)? Y
Enter the polar coordinates of a point: 1.23 4.56
Rectangular coordinates are: -0.19 -1.22

More conversions (Y or N)? N

# 10.2 参数深入

支配实参（调用函数时提供的值）与其对应参数（函数头中用于存储实参的变量）之间关系的规则称为参数传递机制。在本节中，我们将研究 C++ 中可用的各种传递机制。

## 10.2.1 值参数

最简单的参数传递机制是默认发生的机制。它被称为按值调用，其值通过此机制传递的参数称为值参数。支配它们的规则是：

