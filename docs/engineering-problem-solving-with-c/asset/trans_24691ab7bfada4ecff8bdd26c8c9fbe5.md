

在声明Point对象时分配给其数据成员。在文本的其余部分中，我们将继续为Point类添加补充说明。

请回顾，类型声明语句定义新标识符、分配内存，并可为新内存位置赋予初始值。鉴于Point类声明中提供的构造函数，类型声明语句可用于声明Point类型的对象，如下所示。

```
Point p1; //Default constructor is called
Point p2(1.0, 1.0); //Parameterized constructor is called

memory snapshot:

Point p1 -> [?]double xCoord
            [?]double yCoord

Point p2 -> [1.0]double xCoord
            [1.0]double yCoord
```

## 类实现

要完成Point类的定义，我们需要编写类实现。类实现文件必须为类声明中声明的每个方法包含一段代码。每段代码必须以一个标题开头，该标题包括类名、作用域解析运算符(::)和方法名。下面给出了我们Point类的实现文件。请注意，实现文件包含编译器指令#include "Point.h"。由于Point.h不是C++标准库的一部分，因此使用引号括起来声明文件的名称。

```
/*-------------------------------------------*/
/* Class implementation for initial Point class declaration */
/* filename: Point.cpp */
#include "Point.h" //Required
#include <iostream> //Required for cout
using namespace std;

//Default constructor
Point::Point()
{
   cout << "Constructing Point object, default: \n";
   cout << "Initializing to zero" << endl;
   xCoord = 0.0;
   yCoord = 0.0;
}

//Parameterized constructor
Point::Point(double x, double y)
{
   //input parameters x,y
   cout << "Constructing Point object, parameterized: \n";
   cout << "Input parameters: " << x << ", " << y << endl;
   xCoord = x;
   yCoord = y;
}
```

默认构造函数以标题`Point::Point()`开头。在定义默认构造函数的代码块中，值0.0被赋给数据成员`xCoord`和`yCoord`。这确保了所有使用默认构造函数声明的`Point`对象都将具有初始值0.0。

参数化构造函数以标题`Point::Point(double x, double y)`开头。在定义参数化构造函数的代码块中，参数`x`被赋给数据成员`xCoord`，参数`y`被赋给数据成员`yCoord`。这确保了所有使用参数化构造函数声明的Point对象都将具有由类型声明语句中的值指定的初始值。

![](img/0235a4ea835dc4575bd036e024a533b3_71_0.png)

在我们`Point`类的实现中，我们在每个构造函数中都包含了`cout`语句。`cout`语句对于跟踪执行和调试很有用，并且在方法完全测试后可以被注释掉。

![](img/0235a4ea835dc4575bd036e024a533b3_71_1.png)

程序`chapter2_3`说明了程序员定义的数据类型`Point`的用法。请注意，编译器指令`#include "Point.h"`已包含在程序`chapter2_3`中。想要使用程序员定义类型的应用程序必须在其源代码中包含`class`声明文件。

```
/*-------------------------------- Program chapter2_3 ----------------------------------*/
/* Program 2.3 */
/* */
/* This program illustrates the use of the */
/* programmer-defined data type Point */
/* */

#include <iostream> //Required for cout
#include "Point.h" //Required for Point
using namespace std;

int main()
{
 //Declare and initialize objects.
 cout << "In main, declare p1..." << endl;
 Point p1;
 cout << "In main, declare p2..." << endl;
 Point p2(1.5, -4.7);
 cout << "In main, declare ORIGIN..." << endl;
 const Point ORIGIN(0.0, 0.0);

 return 0;
}
/*-----------------------------------------------------------*/

memory snapshot:
Point p1 -> | 0.0 | double xCoord
          | 0.0 | double yCoord
Point p2 -> [1.5] double xCoord
       [-4.7] double yCoord
const Point ORIGIN [0.0] double xCoord
             [0.0] double yCoord
```

程序chapter2_3的输出如下：

```
In main, declare p1...
Constructing Point object, default:
Initializing to zero
In main, declare p2...
Constructing Point object, parameterized:
Input parameters: 1.5, -4.7
In main, declare ORIGIN...
Constructing Point object, parameterized:
Input parameters: 0, 0
```

## 语句框 2.2

类定义：程序员定义的类的定义由两部分组成：类声明和类实现。

```
Syntax: Class Declaration
class ClassName
{
 access modifier:
 declaration of attributes
 access modifier:
 declaration of methods
};
```

```
Syntax: Class Implementation
#include "className.h"
definitions of class methods
```

```
Example: class Declaration
class Point
{
 private:
 double xCoord;
 double yCoord;
 public:
 Point(double x, double y);
};
Usage:
#include "Point.h"
int main()
{
 Point p1(1.5, 2.7);
```

```
Example: class Implementation
#include "Point.h"
Point::Point(double x, double y)
{
 xCoord = x;
 yCoord = y;
}
```

## 修改 2.2

这些问题与本节开发的程序chapter2_3有关。

- 1. 将以下cout语句添加到文件Point.cpp中每个构造函数的末尾。

  cout << "(" << xCoord << "," << yCoord << ")" << endl;

  编译并执行修改后的代码。此修改如何更改输出？

- 2. 在文件Point.cpp中，通过将分配给数据成员的值更改为-1.0来修改默认构造函数。编译并执行代码。此修改如何更改输出？

- 3. 在文件Point.cpp中，通过注释掉默认构造函数中的两个赋值语句来修改默认构造函数。编译并执行代码。此修改如何更改输出？

- 4. 在文件Point.h中，通过删除终止类声明体的分号来修改类声明。尝试编译或构建代码。报告了什么错误消息？

## 2.4 使用IDE构建C++解决方案：Xcode

### 集成开发环境（IDE）

### Xcode

我们已讨论了C++程序的一般结构，并编写了几个小程序来说明数据类型的用法。在本节中，我们将说明如何使用集成开发环境（IDE）开发C++解决方案。IDE是一套旨在促进软件解决方案开发的软件包。IDE包括编辑器、编译器、调试器以及许多其他工具，以帮助设计和开发大型软件解决方案。有多种平台可用的优秀IDE。在本节中，我们将使用IDE Xcode为程序chapter2_3开发C++解决方案。

## Xcode

Xcode IDE由Apple开发，用于开发运行在Mac、iPad和iPhone上的应用程序。Xcode可免费下载。您可以在https://developer.apple.com/上找到更多有关Xcode的信息。启动Xcode应用程序时，将出现如下所示的欢迎窗口。

![](img/0235a4ea835dc4575bd036e024a533b3_74_0.png)

## 欢迎窗口

来源：版权所有 © Apple Inc.

从欢迎窗口的左侧，我们将选择Create a new Xcode project。这将弹出如下所示的新建项目窗口。

![](img/0235a4ea835dc4575bd036e024a533b3_74_1.png)

## 新建项目窗口

我们将从新建项目窗口的左侧选择Application，从窗口右侧选择Command Line Tool，然后单击Next。将出现如下所示的选项窗口，用于指定项目选项。

![](img/0235a4ea835dc4575bd036e024a533b3_75_0.png)

## 选项窗口

请注意，我们选择了C++作为语言。单击Next后，将出现一个保存窗口，允许您选择保存项目的位置。

![](img/0235a4ea835dc4575bd036e024a533b3_75_1.png)

## 保存窗口

我们在Google Drive上选择了一个名为Chapter 2的文件夹。做出选择后，单击Create。将出现如下所示的新窗口。这是开发我们C++解决方案的主窗口。

