
让你编译程序，但不足以让你运行程序。为了运行程序，你必须编写（并编译）成员函数和重载运算符的定义。我们将这些函数和运算符定义放在另一个文件中，该文件称为**实现文件**。虽然大多数编译器并不要求，但传统上会让接口文件和实现文件使用相同的名称。然而，这两个文件的后缀不同。我们将ADT类的接口放在名为`dtime.h`的文件中，将ADT类的实现放在名为`dtime.cpp`的文件中。实现文件使用的后缀取决于你的C++版本。实现文件应使用与你通常用于包含C++程序的文件相同的后缀。如果你的程序文件以`.cxx`结尾，那么你应该用`.cxx`代替`.cpp`。如果你的程序文件以`.CPP`结尾，那么你的实现文件将以`.CPP`而不是`.cpp`结尾。我们使用`.cpp`，因为大多数编译器接受`.cpp`作为C++源代码文件的后缀。我们的DigitalTime ADT类的实现文件在显示12.2中给出。在我们解释了ADT的各种文件如何相互交互之后，我们将回到显示12.2，讨论该实现文件中定义的细节。

为了在程序中使用ADT类`DigitalTime`，程序必须包含include指令

```
#include "dtime.h"
```

请注意，实现文件和程序文件都必须包含这个指定接口文件的include指令。包含程序的文件（即包含程序主要部分的文件）通常称为**应用程序文件**或**驱动程序文件**。显示12.3包含一个应用程序文件，其中有一个非常简单的程序，使用并演示了DigitalTime ADT类。

## 编译并运行程序

如何运行这个包含在三个文件中的完整程序的具体细节取决于你使用的系统。然而，基本细节对所有系统都是相同的。你必须编译实现文件，并且必须编译包含程序主要部分的应用程序文件。你不编译接口文件，在本例中即显示12.1中给出的`dtime.h`文件。你不需要编译接口文件，因为编译器认为该接口文件的内容已经包含在另外两个文件中。回想一下，实现文件和应用程序文件都包含指令

```
#include "dtime.h"
```

编译程序会自动调用预处理器，预处理器读取这条include指令，并用`dtime.h`文件中的文本替换它。因此，编译器会看到`dtime.h`的内容，所以`dtime.h`文件不需要单独编译。（实际上，编译器会看到`dtime.h`的内容两次：一次在编译实现文件时，一次在编译应用程序文件时。）这种对`dtime.h`文件的复制只是一种

概念上的复制。编译器表现得好像`dtime.h`的内容被复制到了每个包含该include指令的文件中。然而，如果你在编译后查看该文件，你只会找到include指令；你不会找到`dtime.h`文件的内容。

一旦实现文件和应用程序文件编译完成，你仍然需要连接这些文件，以便它们能够协同工作。这称为链接文件，由称为链接器的独立实用程序完成。如何调用链接器的细节取决于你使用的系统。在

## 显示12.2 DigitalTime的实现文件（第1部分，共3部分）

```
//Implementation file dtime.cpp (Your system may require some
//suffix other than .cpp): This is the IMPLEMENTATION of the ADT DigitalTime.
//The interface for the class DigitalTime is in the header file dtime.h.
#include <iostream>
#include <cctype>
#include <cstdlib>
#include "dtime.h"
using namespace std;

//These FUNCTION DECLARATIONS are for use in the definition of
//the overloaded input operator >>:

void readHour(istream& ins, int& theHour);
//Precondition: Next input in the stream ins is a time in 24-hour notation,
//like 9:45 or 14:45.
//Postcondition: theHour has been set to the hour part of the time.
//The colon has been discarded and the next input to be read is the minute.

void readMinute(istream& ins, int& theMinute);
//Reads the minute from the stream ins after readHour has read the hour.

int digitToInt(char c);
//Precondition: c is one of the digits '0' through '9'.
//Returns the integer for the digit; for example, digitToInt('3') returns 3.

bool operator ==(const DigitalTime& time1, const DigitalTime& time2)
{
    return (time1.hour == time2.hour && time1.minute == time2.minute);
}
//Uses iostream and cstdlib:
DigitalTime::DigitalTime(int theHour, int theMinute)
{
    if (theHour< 0 || theHour> 23 || theMinute< 0 || theMinute> 59)
    {
        cout<< "Illegal argument to DigitalTime constructor.";
        exit(1);
    }
    
    else
    {
        hour = theHour;
        minute = theMinute;
    }
}
DigitalTime::DigitalTime( ) : hour(0), minute(0)
{
    //Body intentionally empty.
}
```

## 显示12.2 DigitalTime的实现文件（第2部分，共3部分）

```
void DigitalTime::advance(int minutesAdded)
{
    int grossMinutes = minute + minutesAdded;
    minute = grossMinutes % 60;

    int hourAdjustment = grossMinutes / 60;
    hour = (hour + hourAdjustment) % 24;
}

void DigitalTime::advance(int hoursAdded, int minutesAdded)
{
    hour = (hour + hoursAdded) % 24;
    advance(minutesAdded);
}

//Uses iostream:
ostream& operator <<(ostream& outs, const DigitalTime& theObject)
{
    outs << theObject.hour<< ':';
    if (theObject.minute< 10)
        outs << '0';
    outs << theObject.minute;
    return outs;
}

//Uses iostream:
istream& operator >>(istream& ins, DigitalTime& theObject)
{
    readHour(ins, theObject.hour);
    readMinute(ins, theObject.minute);
    return ins;
}

int digitToInt(char c)
{
    return (static_cast<int>(c) - static_cast<int>('0'));
}

//Uses iostream, cctype, and cstdlib:
void readMinute(istream& ins, int& theMinute)
{
    char c1, c2;
    ins >> c1 >> c2;

    if (!(isdigit(c1) && isdigit(c2)))
```

## 显示12.2 DigitalTime的实现文件（第3部分，共3部分）

```
{
    cout<< "Error illegal input to readMinute\n";
    exit(1);
}

theMinute = (digitToInt(c1) * 10) + digitToInt(c2);

if (theMinute< 0 || theMinute> 59)
{
    cout<< "Error illegal input to readMinute\n";
   exit(1);
}
}

//Uses iostream, cctype, and cstdlib:
void readHour(istream& ins, int& theHour)
{
    char c1, c2;
    ins >> c1 >> c2;
    if ( ! ( isdigit(c1) && (isdigit(c2) || c2 == ':' ) ) )
    {
        cout<< "Error illegal input to readHour\n";
        exit(1);
    }

    if (isdigit(c1) && c2 == ':')
    {
        theHour = digitToInt(c1);
    }
    else//(isdigit(c1) && isdigit(c2))
    {
        theHour = (digitToInt(c1) * 10) + digitToInt(c2);
        ins >> c2;//discard ':'
        if (c2 != ':')
        {
            cout<< "Error illegal input to readHour\n";
            exit(1);
        }
    }
    if (theHour < 0 || theHour > 23)
    {
        cout<< "Error illegal input to readHour\n";
        exit(1);
    }
}
```

## 显示12.3 使用DigitalTime的应用程序文件

```
//Application file timedemo.cpp (your system may require some suffix
//other than .cpp): This program demonstrates use of the class DigitalTime.
#include <iostream>
#include "dtime.h"
using namespace std;

int main( )
{
    DigitalTime clock, oldClock;

    cout<< "Enter the time in 24-hour notation: ";
    cin >> clock;

    oldClock = clock;
    clock.advance(15);
    if (clock == oldClock)
        cout << "Something is wrong.";
    cout << "You entered " << oldClock << endl;
    cout << "15 minutes later the time will be "
        << clock << endl;

    clock.advance(2, 15);
    cout << "2 hours and 15 minutes after that\n"
        << "the time will be "
        << clock << endl;

    return 0;
}
```

## 示例对话

```
Enter the time in 24-hour notation: 11:15
You entered 11:15
15 minutes later the time will be 11:30
2 hours and 15 minutes after that
the time will be 13:45
```

