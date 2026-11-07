
只有当它们被激活——也就是被调用时。C++ 附带了大量函数，称为**预定义函数**，这些函数已经编写好。本节中，你将学习如何使用 C++ 系统提供的一些预定义函数。本章后面，你将学习如何使用流函数来执行特定的 I/O 操作。

回想第 2 章，预定义函数组织为库的集合，称为头文件。一个特定的头文件可能包含多个函数。因此，要使用某个特定函数，你需要知道该函数的名称以及一些其他信息，这些内容很快就会介绍。

一个非常有用的函数 `pow`，称为幂函数，可用于在程序中计算 x^y。也就是说，`pow(x, y) = x^y`。例如，`pow(2.0, 3.0) = 2.0^3 = 8.0` 以及 `pow(4.0, 0.5) = 4.0^0.5 = 2.0`。你在函数 `pow` 中使用的数字 x 和 y 称为函数 `pow` 的**实参**或**形参**。例如，在 `pow(2.0, 3.0)` 中，参数是 2.0 和 3.0。

像 `pow(2.0, 3.0)` 这样的表达式称为**函数调用**，它会使附加到预定义函数 `pow` 的代码执行，在此例中计算 2.0^3.0。头文件 `cmath` 包含函数 `pow` 的规范。

要在程序中使用预定义函数，你需要知道包含该函数规范的头文件的名称，并在程序中包含该头文件。此外，你需要知道函数的名称、函数接受的参数个数以及每个参数的类型。你还必须了解该函数将要做什么。例如，要使用函数 `pow`，必须包含头文件 `cmath`。函数 `pow` 有两个参数，都是十进制数。该函数计算第一个参数的第二个参数次幂。（附录 F 介绍了一些常用的头文件和预定义函数。）

下面示例中的程序说明了如何在程序中使用预定义函数。更具体地说，我们使用来自头文件 `cmath` 的一些数学函数，以及来自头文件 `string` 的字符串函数 `length`。注意，函数 `length` 确定字符串的长度。

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
//sqrt((x1-x2)^2 + (y2-y1)^2)

#include <iostream>
#include <cmath>
#include <string>

using namespace std;

const double PI = 3.1416;

int main()
{
        double sphereRadius;                                      //Line 1
        double sphereVolume;                                      //Line 2
        double point1X, point1Y;                                  //Line 3
        double point2X, point2Y;                                  //Line 4
        double distance;                                          //Line 5

        string str;                                               //Line 6

        cout << "Line 7: Enter the radius of the sphere: ";      //Line 7
        cin >> sphereRadius;                                      //Line 8
        cout << endl;                                             //Line 9

        sphereVolume = (4.0 / 3) * PI * pow(sphereRadius, 3);     //Line 10

        cout << "Line 11: The volume of the sphere is: "
             << sphereVolume << endl << endl;                     //Line 11

        cout << "Line 12: Enter the coordinates of two "
             << "points in the X-Y plane: ";                      //Line 12
        cin >> point1X >> point1Y >> point2X >> point2Y;          //Line 13
        cout << endl;                                             //Line 14

        distance = sqrt(pow(point2X - point1X, 2)
                      + pow(point2Y - point1Y, 2));               //Line 15

        cout << "Line 16: The distance between the points "
             << "(" << point1X << ", " << point1Y << ") and "
             << "(" << point2X << ", " << point2Y << ") is: "
             << distance << endl << endl;                         //Line 16

        str = "Programming with C++";                             //Line 17

        cout << "Line 18: The number of characters, "
             << "including blanks, in \"" << str << "\" is:"
             << str.length() << endl;                             //Line 18

        return 0;                                                 //Line 19
}
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```
Line 7: Enter the radius of the sphere: 3

Line 11: The volume of the sphere is: 113.098

Line 12: Enter the coordinates of two points in the X-Y plane: 4 7 9 -5

Line 16: The distance between the points (4, 7) and (9, -5) is: 13

Line 18: The number of characters, including blanks, in "Programming with C++" is: 20
```

前面的程序工作如下。第 1 行到第 6 行的语句声明程序中使用的变量。第 7 行的语句提示用户输入球的半径，第 8 行的语句将半径存储在变量 `sphereRadius` 中。第 10 行的语句使用函数 `pow` 计算球的体积并将其存储在变量 `sphereVolume` 中。第 11 行的语句输出体积。第 12 行的语句提示用户输入 X-Y 平面中两个点的坐标，第 13 行的语句将这些坐标分别存储在变量 `point1X`、`point1Y`、`point2X` 和 `point2Y` 中。第 15 行的语句使用函数 `sqrt` 和 `pow` 确定两点之间的距离。第 16 行的语句输出两点之间的距离。第 17 行的语句将字符串 "Programming with C++" 存储在 `str` 中。第 18 行的语句使用字符串函数 `length` 确定并输出 `str` 的长度。注意函数 `length` 是如何使用的。本章后面我们将解释诸如 `str.length()` 这类表达式的含义。

因为 I/O 是任何编程语言的基础，而且编写执行特定 I/O 操作的指令并非人人都能胜任，所以每种编程语言都提供了一组有用的函数来执行特定的 I/O 操作。在本章剩余部分，你将学习如何在程序中使用其中一些函数。作为程序员，你必须密切关注这些函数的使用方式，以便充分利用它们。这里你将学习的第一个函数是函数 `get`。

### cin 与 get 函数

如你所见，提取运算符在扫描下一个输入值时跳过所有前导空白字符。考虑以下变量声明：

```
    char ch1, ch2;
    int num;
```

以及输入：

```
A 25
```

现在考虑以下语句：

```
    cin >> ch1 >> ch2 >> num;
```

当计算机执行此语句时，'A' 存储在 `ch1` 中，空白被提取运算符 `>>` 跳过，字符 '2' 存储在 `ch2` 中，而 5 存储在 `num` 中。然而，如果你原本打算将 'A' 存储在 `ch1` 中、将空白存储在 `ch2` 中、将 25 存储在 `num` 中，那该怎么办？很明显，你不能使用提取运算符 `>>` 来输入这些数据。

如前所述，有时你需要处理整个输入，包括空白字符，例如空格和换行符。例如，假设你想逐行处理输入的数据。因为提取运算符 `>>` 会跳过换行符，除非程序捕获换行符，否则计算机不知道一行在哪里结束、下一行从哪里开始。

变量 `cin` 可以访问流函数 `get`，该函数用于读取字符数据。`get` 函数从输入流中输入紧接着的下一个字符（包括空白字符），并将其存储在其参数所指示的内存位置。函数 `get` 有多种形式。接下来，我们讨论用于读取一个字符的那种形式。

`cin` 与用于读取一个字符的 `get` 函数一起使用的语法如下：

```
    cin.get(varChar);
```

在 `cin.get` 语句中，`varChar` 是一个 char 变量。`varChar` 出现在函数名后的圆括号中，称为该函数的实参或参数。前面语句的作用是将下一个输入字符存储在变量 `varChar` 中。

现在再次考虑以下输入：

```
A 25
```

要将 'A' 存储在 `ch1` 中、将空白存储在 `ch2` 中、将 25 存储在 `num` 中，你可以按如下方式有效使用 `get` 函数：

```
    cin.get(ch1);
    cin.get(ch2);
    cin >> num;
```

因为这种形式的 `get` 函数只有一个参数，并且只读取一个字符，而你需要从输入流中读取两个字符，所以需要调用此函数两次。注意，你不能使用 `get` 函数将数据读入变量 `num`，因为 `num` 是 int 变量。前面这种形式的 `get` 函数只读取 char 数据类型的值。

前面那组 `cin.get` 语句等价于以下语句：

```
    cin >> ch1;
    cin.get(ch2);
    cin >> num;
```

> 函数 `get` 还有其他形式，你将在第 8 章学习其中一种。在接下来的几章中，你只需要这里介绍的函数 `get` 的形式。

