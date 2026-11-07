
然而，类的用户应当了解某个特定函数的作用以及如何使用它。因此，在包含函数原型的规范文件中，我们会加入注释，简要描述该函数，并说明任何前置条件和/或后置条件。

**前置条件：** 一条说明在调用函数之前必须为真的条件的语句。

**后置条件：** 一条说明在函数调用完成后什么为真的语句。

以下是**类** `clockType` 的规范文件和实现文件：

```cpp
//clockType.h, the specification file for the class clockType

class clockType
{
public:
    void setTime(int hours, int minutes, int seconds);
        //Function to set the time.
        //The time is set according to the parameters.
        //Postcondition: hr = hours; min = minutes;
        //              sec = seconds;
        //              The function checks whether the
        //              values of hours, minutes, and seconds
        //              are valid. If a value is invalid, the
        //              default value 0 is assigned.

    void getTime(int& hours, int& minutes, int& seconds) const;
        //Function to return the time.
        //Postcondition: hours = hr; minutes = min;
        //              seconds = sec;

    void printTime() const;
        //Function to print the time.
        //Postcondition: The time is printed in the form
        //              hh:mm:ss.

    void incrementSeconds();
        //Function to increment the time by one second.
        //Postcondition: The time is incremented by one second.
        //              If the before-increment time is
        //              23:59:59, the time is reset to 00:00:00.

    void incrementMinutes();
        //Function to increment the time by one minute.
        //Postcondition: The time is incremented by one minute.
        //              If the before-increment time is
        //              23:59:53, the time is reset to 00:00:53.

    void incrementHours();
        //Function to increment the time by one hour.
        //Postcondition: The time is incremented by one hour.
```

```cpp
using namespace std;
.
.

//Place the definitions of the function main and the other
//user-defined functions here
.
.
```

> **注意**
>
> 为了节省篇幅，我们没有提供实现文件和包含用户程序的文件的完整细节。但是，你可以在本书配套的网站上找到这些文件以及规范（头）文件。

## 可执行代码

上一节讨论了如何隐藏类的实现细节。要在程序中使用对象，在执行期间，程序必须能够访问对象的实现细节（即实现对象操作的算法）。本节讨论客户程序如何获得对对象实现细节的访问。为便于说明，我们将使用类 clockType。

如前所述，要使用类 clockType，程序必须通过 include 语句包含头文件 clockType.h。例如，下面的程序段包含了头文件 clockType.h：

```cpp
//Program testClockClass.cpp

#include "clockType.h"
.
.
.
int main()
{
    .
    .
    .
}
```

程序 testClockClass.cpp 必须只包含头文件，而不是实现文件。要创建可执行代码来运行程序 testClockClass.cpp，需要以下步骤：

1. 我们单独编译文件 clockTypeImp.cpp 并创建目标代码文件 clockTypeImp.obj。目标代码文件包含机器语言代码，但该代码不是可执行形式。

   假设命令 `cc` 在计算机的系统命令行上调用 C++ 编译器或链接器，或二者兼有。命令：

   ```
   cc -c clockTypeImp.cpp
   ```

   会创建目标代码文件 `clockTypeImp.obj`。

2. 要为源代码文件 `testClockClass.cpp` 创建可执行代码，我们编译源代码文件 `testClockClass.cpp`，创建目标代码文件 `testClockClass.obj`，然后链接文件 `testClockClass.obj` 和 `clockTypeImp.obj` 以创建可执行文件 `testClockClass.exe`。系统命令行上的以下命令会创建可执行文件 `testClockClass.exe`：

   ```
   cc testClockClass.cpp clockTypeImp.obj
   ```

**注意**

1. 要为任何源代码文件创建目标代码文件，我们在系统命令行上使用命令行选项 `-c`。例如，要为名为 `exercise.cpp` 的源代码文件创建目标代码文件，我们在系统命令行上使用以下命令：

   ```
   cc -c exercise.cpp
   ```

2. 要将多个目标代码文件与一个源代码文件链接，我们在系统命令行上列出所有目标代码文件。例如，要将 `A.obj` 和 `B.obj` 与源代码文件 `test.cpp` 链接，我们使用以下命令：

   ```
   cc test.cpp A.obj B.obj
   ```

3. 如果源代码文件被修改，则必须重新编译。

4. 如果一个源文件中的修改影响其他文件，则其他文件必须重新编译并重新链接。

5. 用户必须能够访问头文件和目标代码文件。需要访问头文件以查看对象做什么以及如何使用它们。需要访问目标代码文件，以便用户可以将程序与目标代码链接以生成可执行代码。用户不需要访问包含实现细节的源代码文件。

如第1章所述，IDE（集成开发环境）Visual C++ 2012 Express、Visual Studio 2012 和 C++ Builder 将编辑器、编译器和链接器整合到一个包中。使用一条命令，程序便会与其他必要文件一起编译和链接。这些系统还以项目的形式管理多文件程序。因此，一个项目由若干文件组成，这些文件称为项目文件。这些系统通常有一条命令，称为 **build**、**rebuild** 或 **make**。（请查阅你系统的文档。）当 build、rebuild 或 make 命令应用于项目时，系统会自动编译并链接创建可执行代码所需的所有文件。当项目中的一个或多个文件发生变化时，你可以使用这些命令重新编译并重新链接这些文件。

## 更多类示例

在本节中，我们给出各种类以及如何在程序中使用它们的示例。

### 示例 10-8

以下语句定义了类 `circleType`，以实现圆的基本属性：

```cpp
class circleType
{
public:
    void setRadius(double r);
        //Function to set the radius.
        //Postcondition: if (r >= 0) radius = r;
        //                otherwise radius = 0;

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

下面演示如何在程序中使用类 `circleType`：

```cpp
//The user program that uses the class circleType

#include <iostream>
#include <iomanip>
#include "circleType.h"

using namespace std;

int main()                                      //Line 1
{                                               //Line 2
        circleType circle1(8);                 //Line 3
        circleType circle2;                    //Line 4

        double radius;                         //Line 5

        cout << fixed << showpoint << setprecision(2); //Line 6

        cout << "Line 7: circle1 = "
             << "radius: " << circle1.getRadius()
             << ", area: " << circle1.area()
             << ", circumference: " << circle1.circumference()
             << endl;                          //Line 7

        cout << "Line 8: circle2 = "
             << "radius: " << circle2.getRadius()
             << ", area: " << circle2.area()
             << ", circumference: " << circle2.circumference()
             << endl << endl;                  //Line 8

        cout << "Line 9: Enter the radius of a circle: "; //Line 9
        cin >> radius;                          //Line 10
        cout << endl;                            //Line 11
```
