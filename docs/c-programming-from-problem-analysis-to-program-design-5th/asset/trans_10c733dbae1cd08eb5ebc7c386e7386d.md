
然而，类的用户应当了解某个特定函数的作用以及如何使用它。因此，在包含函数原型的规范文件中，我们会加入注释，简要描述该函数，并说明任何前置条件和/或后置条件。

**前置条件：** 一条说明在调用函数之前必须为真的条件的语句。

**后置条件：** 一条说明在函数调用完成后为真的内容的语句。

以下是类 clockType 的规范文件和实现文件：

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
        //              If the before-increment time is
        //              23:45:53, the time is reset to 00:45:53.

    bool equalTime(const clockType& otherClock) const;
        //Function to compare the two times.
        //Postcondition: Returns true if this time is equal to
        //               otherClock; otherwise, returns false.

    clockType(int hours, int minutes, int seconds);
        //Constructor with parameters.
        //The time is set according to the parameters.
        //Postcondition: hr = hours; min = minutes;
        //               sec = seconds;
        //               The constructor checks whether the
        //               values of hours, minutes, and seconds
        //               are valid. If a value is invalid, the
        //               default value 0 is assigned.

    clockType();
        //Default constructor
        //The time is set to 00:00:00.
        //Postcondition: hr = 0; min = 0; sec = 0;

private:
    int hr;  //variable to store the hours
    int min; //variable to store the minutes
    int sec; //variable to store the seconds
};
```

```cpp
//clockTypeImp.cpp, the implementation file

#include <iostream>
#include "clockType.h"

using namespace std;
.
.
.

//Place the definitions of the member functions of the class
//clockType here.
.
.
.
```

```cpp
//The user program that uses the class clockType

#include <iostream>
#include "clockType.h"

using namespace std;
.
.
.
//Place the definitions of the function main and the other
//user-defined functions here
.
.
```

> **注意** 为节省篇幅，我们没有提供实现文件以及包含用户程序的文件完整细节。不过，你可以在本书配套网站上找到这些文件以及规范（头）文件。

## 可执行代码

上一节讨论了如何隐藏类的实现细节。要在程序中使用对象，在执行期间，程序必须能够访问该对象的实现细节（即实现对该对象操作的算法）。本节讨论客户端程序如何获得对某个对象实现细节的访问权限。为便于说明，我们将使用类 clockType。

如前所述，要使用类 clockType，程序必须通过 include 语句包含头文件 clockType.h。例如，以下程序段包含了头文件 clockType.h：

```cpp
//Program test.cpp

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

程序 test.cpp 必须只包含头文件，而不是实现文件。要创建用于运行程序 test.cpp 的可执行代码，需要以下步骤：

- 1. 我们单独编译文件 clockTypeImp.cpp，并创建目标代码文件 clockTypeImp.obj。目标代码文件包含机器语言代码，但该代码不是可执行形式。

  假设命令 cc 在计算机的系统命令行上调用 C++ 编译器或链接器，或两者兼有。命令：

  ```
  cc -c clockTypeImp.cpp
  ```

  会创建目标代码文件 clockTypeImp.obj。

- 2. 要为源代码文件 test.cpp 创建可执行代码，我们编译源代码文件 test.cpp，创建目标代码文件 test.obj，然后链接文件 test.obj 和 clockTypeImp.obj 以创建可执行文件 test.exe。系统命令行上的以下命令会创建可执行文件 test.exe：

  ```
  cc test.cpp clockTypeImp.obj
  ```

**注意**

- 1. 要为任何源代码文件创建目标代码文件，我们在系统命令行上使用命令行选项 -c。例如，要为名为 exercise.cpp 的源代码文件创建目标代码文件，我们在系统命令行上使用以下命令：

  ```
  cc -c exercise.cpp
  ```

- 2. 要将多个目标代码文件与一个源代码文件链接，我们在系统命令行上列出所有目标代码文件。例如，要将 A.obj 和 B.obj 与源代码文件 test.cpp 链接，我们使用命令：

  ```
  cc test.cpp A.obj B.obj
  ```

- 3. 如果源代码文件被修改，则必须重新编译。

- 4. 如果一个源文件中的修改影响其他文件，则其他文件必须重新编译并重新链接。

- 5. 用户必须能够访问头文件和目标代码文件。需要访问头文件，以了解对象的作用以及如何使用它们。需要访问目标代码文件，以便用户可以将程序与目标代码链接，生成可执行代码。用户不需要访问包含实现细节的源代码文件。

如第 1 章所述，IDE Visual C++ 2008 Express、Visual Studio .NET、C++ Builder 和 CodeWarrior 将编辑器、编译器和链接器全部集成在一个包中。使用一条命令，程序就会与其他必要文件一起被编译和链接。这些系统还以项目的形式管理多文件程序。因此，一个项目由若干文件组成，这些文件称为项目文件。这些系统通常有一条命令，称为 build、rebuild 或 make。（请查阅你的系统文档。）当对项目应用 build、rebuild 或 make 命令时，系统会自动编译并链接创建可执行代码所需的所有文件。

当项目中的一个或多个文件发生更改时，你可以使用这些命令重新编译并重新链接这些文件。

### 示例 12-8

在示例 6-4 中，函数 rollDice 掷一对骰子，直到掷出的数字之和为给定数字，并返回为得到所需和而掷骰子的次数。事实上，我们可以设计一个类来实现骰子的基本属性。考虑以下类 die 的定义。

```cpp
class die
{
public:
    die();
        //Default constructor
        //Sets the default number rolled by a die to 1

    int roll();
        //Function to roll a die.
        //This function uses a random number generator to randomly
        //generate a number between 1 and 6, and stores the number
        //in the instance variable num and returns the number.

    int getNum() const;
        //Function to return the number on the top face of the die.
        //Returns the value of the instance variable num.

private:
    int num;
};
```

成员函数的定义如下。

```cpp
die::die()
{
    num = 1;
    srand(time(0));
}

int die::roll()
{
    num = rand() % 6 + 1;

    return num;
}

int die::getNum() const
{
    return num;
}
```
