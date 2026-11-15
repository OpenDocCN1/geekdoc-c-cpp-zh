

| 方向 | 代码 |
|---|---|
| 北 (N) | 1 |
| 东北 (NE) | 2 |
| 东 (E) | 3 |
| 东南 (SE) | 4 |
| 南 (S) | 5 |
| 西南 (SW) | 6 |
| 西 (W) | 7 |
| 西北 (NW) | 8 |

## 1. 问题描述

读取海洋网格的一组风向。确定并打印风的主导方向以及从该方向吹来的点数。

## 2. 输入/输出描述

I/O 图显示数据文件作为输入，报告信息作为输出。

![](img/02c4582f051c5b51776411c92b079035_408_0.png)

## 3. 手算示例

假设网格包含以下信息：

```
4   4   5   5   4
3   4   4   4   5
4   5   4   4   4
4   4   4   4   4
4   4   4   4   5
```

值 4 在 25 次中出现 19 次，即 76% 的时间。因此，程序的输出应如下所示：

风有 76% 的时间来自东南方向。

## 4. 算法开发

首先，我们开发分解大纲，因为它将解决方案分解为一组顺序步骤。

### 分解大纲

- 1. 将风向数据读入数组，并确定具有最大值的方向。
- 2. 计算并打印风从该方向吹来的时间百分比。

### 伪代码细化

```
main: if file cannot be opened
    print error message
else
    read data and determine grid points for each direction
    determine the direction with maximum points
    compute and print the direction with maximum points
```

伪代码中的步骤现在足够详细，可以转换为 C++：

```cpp
// Program chapter8_6
//
// This program reads wind direction information from a data
// file and then determines the direction with the most points.
// The percentage of points with the maximum direction is computed
// and printed.

#include <iostream>
#include <fstream>
using namespace std;

int main(void)
{
    /* Declare variables. */
    int r, c, k, maxk=0;
    int grid[5][5], category[8]={0,0,0,0,0,0,0,0};
    double perc;
    char* direction[8]={"N", "NE", "E", "SE", "S ",
    "SW", "W ", "NW"};

    ifstream winds;
    /* Read and print information from the file. */
    winds.open("winds1.txt");
    if (winds.fail())
    cout << "Error opening input file." << endl;
    else
    {
    for (r=0; r<4; r++)
    winds >> grid[r][0] >> grid[r][1] >> grid[r][2]
    >> grid[r][3] >> grid[r][4];

    // Determine sums for the direction categories.
    for (r=0; r<=4; r++)
       for (c=0; c<=4; c++)
       {
          k = grid[r][c];
          category[k]++;
       }

    // Determine category with maximum sum.
    for (k=0; k<=7; k++)
       if (category[k] > category[maxk])
          maxk = k;

    // Print report.
    cout.setf(ios::fixed);
    cout.precision(1);
    perc = (double)category[maxk]/25*100;
    cout << "The wind is blowing from the "
         << direction[maxk-1]
         << perc << "% of the time." << endl;

    // Close file.
    winds.close();
}

// Exit program.
return 0;
}
//-----------------------------------------------
```

## 5. 测试

使用手算示例中的数据，程序的输出应如下所示：

风有 76% 的时间来自东南方向。

## 修改！

这些问题与本节开发的确定主导风向的程序有关。

- 1. 修改程序以打印每个类别中的值的数量，使用方向表示法（例如 SE）。
- 2. 修改程序，如果存在多个具有相同最大值数量的方向，则打印多个输出行。
- 3. 修改程序，如果罗盘的四个象限都有风，则打印消息“可能的气旋或飓风”。
- 4. 修改程序，以便打印一个网格来展示风向。例如，如果风来自西，则可以打印字符 '>'，如果风来自东，则打印 '<'。为所有八个风向选择字符。
- 5. 修改程序，以便从数据文件的第一行读取网格大小（行数和列数）。假设最大为 100 行乘 100 列。

## 8.7 类

在 C++ 中，类是面向对象编程的基础构建块。类与结构类似，不同之处在于类设计为包含函数成员以及数据成员。设计良好的类可以像预定义数据类型一样易于使用。类的实例称为对象。我们在本章的前面部分已经使用过预定义的类和对象。例如，我们使用 cin 对象和 cout 对象执行标准输入和输出操作。这些对象也被称为函数，包括 precision 和 setf。在本节中，我们将讨论程序员定义的类。

### 定义类数据类型

- 类声明
- 类实现
- 数据成员

类定义包含两部分：类声明和类实现。我们将分别讨论每个部分。

在类声明中，使用关键字 class 指定类的名称。类声明的主体由数据成员的类型声明语句和函数成员的函数原型组成。假设我们想要定义一个数据类型来表示用直角坐标表示的数据点；因此，该数据类型由 x 坐标和 y 坐标表示，如图 8.2 所示。在设计类类型时，我们需要考虑表示新数据类型所需的数据成员，以及我们希望为该数据类型定义的操作。

类设计也在类声明中描述。类设计包括用于实现所需操作的函数成员。考虑我们为 xy_coordinate 类提供的类声明，它由两个数据成员组成以定义点，以及两个成员函数来操作坐标以确定半径 r 和角度 theta，如图 8.2 所示。我们将在本节稍后向 xy_coordinate 类的设计添加更多成员函数。类声明通常存储在头文件中，如以下代码所示：

```cpp
//-----------------------------------------------
// Class declaration (version 1)
//
// These statements define a class for xy-coordinates.
// This declaration is stored in xy_coordinate.h.
#include <iostream>
#include <cmath>
class xy_coordinate
{
   // Declare function prototypes for public members.
   public:
      void input();
      void print();
      double radius();
      double angle();
   private:
      // Declare private data members.
      double x, y;
};
//-----------------------------------------------
```

- 公共成员
- 私有成员
- 作用域解析运算符

![](img/02c4582f051c5b51776411c92b079035_412_0.png)

xy_coordinate 类有两个数据成员和四个函数成员。关键字 public 和 private 用于控制对类成员的访问。指定为公共成员的成员可以在用户程序的任何位置引用。指定为私有成员的成员只能由 xy_coordinate 类的成员函数引用。我们建议将所有数据成员指定为私有，以遵循面向对象设计原则。这种受限访问称为信息隐藏。如果对类的数据表示进行修改，只需修改成员函数；无需更改用户程序。任何私有成员函数只能由其他成员函数调用。这些私有成员函数通常称为辅助函数，因为它们旨在帮助其他成员函数。

类实现包含所有类函数定义。在定义成员函数时，函数定义中使用作用域解析运算符 (::)。该运算符放置在类名和函数名之间，以指定该函数是类的成员。在编写成员函数定义时，首先指定函数返回的值的类型。类名、作用域解析运算符、函数名和参数列表将随之而来。回想一下，所有成员函数都可以直接访问数据成员，因此数据成员不出现在参数列表中。辅助函数也可以直接由成员函数调用。类实现也可以存储在单独的文件中。现在介绍 xy_coordinate 类的实现。请注意，函数 angle 是用于计算四象限角度编写的。

