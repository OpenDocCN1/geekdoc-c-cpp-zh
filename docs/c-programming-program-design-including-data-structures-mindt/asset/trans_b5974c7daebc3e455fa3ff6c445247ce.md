

## 类的更多示例

在本节中，我们给出类的各种示例以及如何在程序中使用它们。

### 示例 10-8

以下语句定义了类 `circleType`，以实现圆的基本属性：

```cpp
class circleType
{
public:
    void setRadius(double r);
        //Function to set the radius.
        //Postcondition: if (r >= 0) radius = r;
        //               otherwise radius = 0;

    double getRadius();
        //Function to return the radius.
        //Postcondition: The value of radius is returned.

    double area();
        //Function to return the area of a circle.
        //Postcondition: Area is calculated and returned.

    double circumference();
        //Function to return the circumference of a circle.
        //Postcondition: Circumference is calculated and returned.

    circleType(double r = 0);
        //Constructor with a default parameter.
        //Radius is set according to the parameter.
        //The default value of the radius is 0.0;
        //Postcondition: radius = r;

private:
    double radius;
};
```

成员函数的定义如下：

```cpp
void circleType::setRadius(double r)
{
    if (r >= 0)
        radius = r;
    else
        radius = 0;
}

double circleType::getRadius()
{
    return radius;
}

double circleType::area()
{
    return 3.1416 * radius * radius;
}

double circleType::circumference()
{
    return 2 * 3.1416 * radius;
}

circleType::circleType(double r)
{
    setRadius(r);
}
```

以下说明如何在程序中使用 `class circleType`：

```cpp
//The user program that uses the class circleType
#include <iostream>                         //line 1
#include <iomanip>                          //line 2
#include "circleType.h"                    //line 3

using namespace std;                        //line 4

int main()                                   //line 5
{
    circleType circle1(8);                  //line 7
    circleType circle2;                     //line 8

    double radius;                          //line 9

    cout << fixed << showpoint << setprecision(2);   //line 10

    cout << "Line 11: circle1 - "
         << " radius: " << circle1.getRadius()
         << ", area: " << circle1.area()
         << ", circumference: "
         << circle1.circumference() << endl;         //line 11

    cout << "Line 12: circle2 - "
         << " radius: " << circle2.getRadius()
         << ", area: " << circle2.area()
         << ", circumference: "
         << circle2.circumference() << endl << endl; //line 12

    cout << "Line 13: Enter the radius: ";       //line 13
    cin >> radius;                              //line 14
                                                //line 15

    circle2.setRadius(radius);                         //Line 16

    cout << "Line 17: After setting the radius."
         << endl;                                      //Line 17

    cout << "Line 18: circle2 - "
         << "radius: " << circle2.getRadius()
         << ", area: " << circle2.area()
         << ", circumference: "
         << circle2.circumference() << endl;            //Line 18

    return 0;                                  //Line 19
} //end main                                      //Line 20
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```
Line 11: circle1 - radius: 8.00, area: 201.06, circumference: 50.27

Line 12: circle2 - radius: 0.00, area: 0.00, circumference: 0.00

Line 13: Enter the radius: 6.25

Line 17: After setting the radius.

Line 18: circle2 - radius: 6.25, area: 122.72, circumference: 39.27
```

前面的程序按如下方式工作。第 7 行和第 8 行的语句创建对象 circle1 和 circle2。circle1 的半径设置为 8；circle2 的半径通过构造函数使用默认值设置为 0。第 11 行和第 12 行的语句输出 circle1 和 circle2 的数据。第 13 行和第 14 行的语句提示用户输入一个圆的半径，并将该半径存储在变量 radius 中。第 16 行的语句使用成员函数 setRadius 和 radius 的值来设置 circle2 的半径。第 18 行的语句输出 circle2 的（新）数据。

### 示例 10-9

在第 6 章的示例 6-4 中，函数 rollDice 掷一对骰子，直到掷出的数字之和为给定数字。然后它返回为得到所需总和而掷骰子的次数。实际上，我们可以设计一个实现骰子基本属性的类。考虑以下类 die 的定义。

```cpp
class die
{
public:
    die();
        //Default constructor
        //Sets the default number rolled by a die to 1

    void roll();
        //Function to roll a die
        //This function uses a random number generator to randomly
        //generate a number between 1 and 6, and stores the number
        //in the instance variable num.

    int getNum() const;
        //Function to return the number on the top face of the die.
        //Returns the value of the instance variable num.

private:
    int num;
};
```

接下来给出成员函数的定义。

```cpp
die::die()
{
    num = 1;
    srand(time(0));
}

void die::roll()
{
    num = rand() % 6 + 1;
}

int die::getNum() const
{
    return num;
}
```

以下程序展示如何在程序中使用类 die：

```cpp
//The user program that uses the class die

#include <iostream>                     //Line 1
#include "die.h"                        //Line 2

using namespace std;                    //Line 3

int main()                              //Line 4
{                                       //Line 5
    die die1;                           //Line 6
    die die2;                           //Line 7

    cout << "Line 8: die1: " << die1.getNum()
         << endl;                       //Line 8
    cout << "Line 9: die2: " << die2.getNum()
         << endl;                       //Line 9

    die1.roll();                        //Line 10
    cout << "Line 11: After rolling die1: "
         << die1.getNum() << endl;      //Line 11

    die2.roll();                        //Line 12
    cout << "Line 13: After rolling die2: "
         << die2.getNum() << endl;      //Line 13

    cout << "Line 14: The sum of the numbers rolled"
         << " by the dice is: "
         << die1.getNum() + die2.getNum() << endl;  //Line 14

    die1.roll();                                      //Line 15
    die2.roll();                                      //Line 16

    cout << "Line 17: After again rolling, the sum of "
         << "the numbers rolled is: "
         << die1.getNum() + die2.getNum() << endl;  //Line 17

    return 0;                                         //Line 18
}                                                //Line 19
```

**示例运行：**

```
Line 8: die1: 1
Line 9: die2: 1
Line 11: After rolling die1: 4
Line 13: After rolling die2: 3
Line 14: The sum of the numbers rolled by the dice is: 7
Line 17: After again rolling, the sum of the numbers rolled is: 8
```

前面的程序按如下方式工作。第 6 行和第 7 行的语句创建对象 die1 和 die2，并使用默认构造函数将两个骰子都设置为 1。第 8 行和第 9 行的语句输出两个骰子的数字。第 10 行的语句掷 die1，第 11 行的语句输出掷出的数字。类似地，第 12 行的语句掷 die2，第 13 行的语句输出掷出的数字。第 14 行的语句输出 die1 和 die2 掷出的数字之和。第 15 行和第 16 行的语句再次掷两个骰子，第 17 行的语句输出掷出的数字之和。

示例 10-10 中设计的类 personType 非常有用；我们将在后续章节中使用这个类。

### 示例 10-10

一个人最常见的属性是其名和姓。对一个人姓名的典型操作是设置姓名和打印姓名。以下语句定义了一个具有这些属性的类。

```cpp
#include <string>

using namespace std;

class personType
{
public:
    void print() const;
        //Function to output the first name and last name
        //in the form firstName lastName
```

