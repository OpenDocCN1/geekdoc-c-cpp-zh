

只有当它们被激活——也就是被调用时——才会执行。C++ 提供了大量已经编写好的函数，这些函数称为**预定义函数**。在本节中，你将学习如何使用 C++ 系统提供的一些预定义函数。在本章后面，你将学习如何使用流函数来执行特定的输入/输出操作。

回顾第2章可知，预定义函数以库（称为头文件）的形式组织。一个特定的头文件可能包含多个函数。因此，要使用一个特定的函数，你需要知道该函数的名称以及其他一些内容，这些内容稍后将作说明。

一个非常有用的函数 pow（称为幂函数）可用于在程序中计算 x^y。也就是说，pow(x, y) = x^y。例如，pow(2.0, 3.0) = 2.0^3.0 = 8.0，pow(4.0, 0.5) = 4.0^0.5 = √4.0 = 2.0。在函数 pow 中使用的数字 2.0 和 3.0 称为函数 pow 的**实参**或**参数**。例如，在 pow(2.0, 3.0) 中，参数是 2.0 和 3.0。

像 pow(2.0, 3.0) 这样的表达式称为**函数调用**，它会导致附加到预定义函数 pow 的代码执行，并在这种情况下计算 2.0^3.0。头文件 cmath 包含函数 pow 的声明。

要在程序中使用预定义函数，你需要知道包含该函数声明的头文件的名称，并在程序中包含该头文件。此外，你需要知道函数名、函数所需的参数个数以及每个参数的类型。你还必须清楚该函数将执行什么操作。例如，要使用函数 pow，你必须包含头文件 cmath。函数 pow 有两个参数，它们是小数。该函数计算第一个参数的第二个参数次幂。（附录 F 描述了一些常用的头文件和预定义函数。）

以下示例中的程序说明了如何在程序中使用预定义函数。更具体地说，我们使用了来自头文件 cmath 的一些数学函数，以及来自头文件 string 的字符串函数 length。请注意，函数 length 用于确定字符串的长度。

### 示例 3-4

```cpp
//How to use predefined functions.
//This program uses the math functions pow and sqrt to determine
//and output the volume of a sphere, the distance between two
//points, respectively, and the string function length to find
//the number of characters in a string.
//If the radius of the sphere is r, then the volume of the sphere
//is (4/3)*PI*r^3. If (x1,y1) and (x2,y2) are the coordinates of two
//points in the x-y plane, then the distance between these points is
//sqrt((x2-x1)^2 + (y2-y1)^2).

#include <iostream>
#include <cmath>
#include <string>
using namespace std;

const double PI = 3.1416;

int main()
{
    double sphereRadius;                         //Line 1
    double sphereVolume;                         //Line 2
    double point1X, point1Y;                     //Line 3
    double point2X, point2Y;                     //Line 4
    double distance;                             //Line 5

    string str;                                  //Line 6

    cout << "Line 7: Enter the radius of the sphere: ";   //Line 7
    cin >> sphereRadius;                         //Line 8
    cout << endl;                                //Line 9

    sphereVolume = (4 / 3) * PI * pow(sphereRadius, 3);   //Line 10

    cout << "Line 11: The volume of the sphere is: "
         << sphereVolume << endl << endl;        //Line 11

    cout << "Line 12: Enter the coordinates of two "
         << "points in the X-Y plane: ";         //Line 12
    cin >> point1X >> point1Y >> point2X >> point2Y;      //Line 13
    cout << endl;                                //Line 14

    distance = sqrt(pow(point2X - point1X, 2)
                  + pow(point2Y - point1Y, 2));  //Line 15

    cout << "Line 16: The distance between the points "
         << "(" << point1X << ", " << point1Y << ") and "
         << "(" << point2X << ", " << point2Y << ") is: "
         << distance << endl << endl;            //Line 16

    str = "Programming with C++";                //Line 17

    cout << "Line 18: The number of characters, "
         << "including blanks, in \"" << str << "\" is: "
         << str.length() << endl;                //Line 18

    return 0;                                    //Line 19
}
```

示例运行：在此示例运行中，用户输入以阴影显示。

```
Line 7: Enter the radius of the sphere: 9
Line 11: The volume of the sphere is: 84.8232
Line 12: Enter the coordinates of two points in the X-Y plane: 4 7 9 -5
Line 16: The distance between the points (4, 7) and (9, -5) is: 13
Line 18: The number of characters, including blanks, in "Programming with C++" is: 20
```

逐行处理输入的数据。由于提取运算符 `>>` 会跳过换行符，除非程序捕获换行符，否则计算机无法知道一行在哪里结束以及下一行从哪里开始。

变量 cin 可以访问流函数 get，该函数用于读取字符数据。get 函数从输入流中读取下一个字符（包括空白字符），并将其存储在其参数指示的内存位置。get 函数有多种形式。接下来，我们讨论用于读取字符的一种形式。

cin 与 get 函数一起读取一个字符的语法如下：

```cpp
cin.get(varChar);
```

在 `cin.get` 语句中，`varChar` 是一个 char 变量。`varChar` 出现在函数名后的括号中，称为函数的**实参**或**参数**。前面语句的效果是将下一个输入字符存储在变量 `varChar` 中。

现在再次考虑以下输入：

```
A 25
```

要将 'A' 存储到 ch1，将空格存储到 ch2，将 25 存储到 num，你可以有效地使用 get 函数，如下所示：

```cpp
cin.get(ch1);
cin.get(ch2);
cin >> num;
```

由于这种形式的 get 函数只有一个参数并且只读取一个字符，而你需要从输入流中读取两个字符，因此你需要调用此函数两次。请注意，不能使用 get 函数将数据读入变量 num，因为 num 是 int 变量。上述形式的 get 函数只读取 char 数据类型的值。

前面的一组 cin.get 语句等价于以下语句：

```cpp
cin >> ch1;
cin.get(ch2);
cin >> num;
```

> 该函数还有其他形式，其中一种将在第8章学习。在接下来的几章中，你只需要这里介绍的 get 函数的形式。

## cin 与 ignore 函数

当你只想处理部分数据（例如，一行内的数据）时，可以使用流函数 ignore 来丢弃一部分输入。使用函数 ignore 的语法如下：

```cpp
cin.ignore(intExp, chExp);
```

这里，intExp 是一个产生整数值的整数表达式，chExp 是一个产生字符值的字符表达式。实际上，表达式 intExp 的值指定了一行中要忽略的最大字符数。

假设 intExp 产生的值为 100。这条语句表示忽略接下来的 100 个字符，或者忽略输入直到遇到 chExp 指定的字符，以先到者为准。具体来说，考虑以下语句：

```cpp
cin.ignore(100, '\n');
```

当此语句执行时，它忽略接下来的 100 个字符，或忽略所有字符直到找到换行符，以先到者为准。例如，如果接下来的 120 个字符不包含换行符，则只丢弃前 100 个字符，下一个输入数据是第 101 个字符。但是，如果第 75 个字符是换行符，则丢弃前 75 个字符，下一个输入数据是第 76 个字符。类似地，以下语句的确切操作：

```cpp
cin.ignore(100, 'A');
```

结果是忽略前 100 个字符，或忽略所有字符直到找到字符 'A'，以先到者为准。

### 示例 3-5

考虑以下声明：

```cpp
int a, b;
```

以及输入：

```
25 67 89 43 72
12 78 34
```

现在考虑以下语句：

```cpp
cin >> a;
cin.ignore(100, '\n');
cin >> b;
```

第一条语句 cin >> a; 将 25 存储到 a 中。第二条语句 cin.ignore(100, '\n'); 丢弃第一行中剩余的所有数字。第三条语句 cin >> b; 将（下一行的）12 存储到 b 中。

