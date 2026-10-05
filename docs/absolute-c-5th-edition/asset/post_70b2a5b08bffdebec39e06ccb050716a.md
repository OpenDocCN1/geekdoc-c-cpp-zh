
There are two differences between a *using* declaration, such as

```
using std::cout;
```

and a *using* *directive*, such as

```
using namespace std;
```

The differences are as follows:

- 1. A *using* declaration makes only one name in the namespace available to your code, while a *using* directive makes all the names in a namespace available.
- 2. A *using* declaration introduces a name (like *cout*) into your code so a *using* directive potentially introduces the name of the can. However, a *using* directive potentially introduces the names in the namespace.

Point 1 is pretty obvious. Point 2 has some subtleties. For example, suppose the namespaces NS1 and NS2 both provide definitions for *myFunction*, but have no other name conflicts. Then the following will produce no problems *provided that* (within the scope of these directives) the conflicting name *myFunction* is never used in your code.

```
using namespace NS1;
using namespace NS2;
```

On the other hand, the following is illegal, if the function *myFunction* is never used:

```cpp
using NS1::myFunction;
using NS2::myFunction;
```

Sometimes this point can be important, but it does not impinge on most routine code. So, we will often use the term *using directive* loosely to mean either a *using* directive or a *using* declaration.

## Qualifying Names

This section introduces how to qualify names that we have not discussed before. Suppose that you intend to use the name *fun1* as defined in the namespace NS1, but you only intend to use it one time (or a small number of times). You can name the function (or other item) using the name of the namespace and the scope resolution operator as follows:

```
NS1::fun1();
```

This form is often used when specifying a parameter type. For example, consider

```cpp
int getInput(std::istream inputStream)
```

# CHAPTER 11 Separate Compilation and Namespaces

In the function getInput, the parameter inputStream is of type istream, where istream is defined in the std namespace. If use of this name istream is the only name you need from the std namespace (or if all the names you need are similarly qualified with std::), then you do not need

```
using namespace std;
```

or

```
using std::istream;
```

Note that you can use std::istream even within the scope of a using directive for another namespace which also defines the name istream. In this case std::istream and istream will have different definitions. For example, consider

```cpp
using namespace MySpace;
void someFunction(istream p1, istream p2);
```

Assuming istream is a type defined in the namespace MySpace, then p1 will have the type istream as defined in MySpace and p2 will have the type istream as the std namespace.

## Self-Test Exercises

- 8. What is the output produced by the following program?

```cpp
#include <iostream>
using namespace std;
namespace Hello
{
void message( );
}
namespace Goodbye
{
void message( );
}
void message( );
int main( )
{
using Goodbye::message;
{
using Hello::message;
message( );
Goodbye::message( );
}
```

# Self-Test Exercises (continued)

```cpp
message( );

return 0;
}

void message( )
{
    cout << "Global message.\n"
}

namespace Hello
{
    void message( )
{
        cout << "Hello.\n"
    }
}

namespace Goodbye
{
    void message( )
{
        cout << "Good-Bye.\n"
    }
}
```

- 9. Write the declaration (prototype) for a void function named wow. The function wow has two parameters, the first of type speed as defined in the speedway namespace and the second of type speed as defined in the indy500 namespace.

> TIP: Choosing a Name for a Namespace

It is a good idea to include your last name or some other string in the names of your namespaces so to reduce the chance that somebody else will use the same namespace name as you do. With multiple programmers writing code for the same project, it is important that namespaces that are meant to be distinct really have distinct names. Otherwise, you can easily have multiple definitions of the same names in the same scope.

## EXAMPLE: A Class Definition in a Namespace

In Displays 11.6 and 11.7 we have rewritten both the header file dtime.h for the class and the implementation file for the class DigitalTime. This time (no pun intended), we have placed the definition in a namespace called DTimeitch. Note that the namespace DTimeitch spans the two files dtime.h and dtime.cpp. A namespace can span multiple files.

If you rewrite the definition of the class as shown in Displays 11.6 and 11.7, the application file in Display 11.3 needs to specify the namespace DTimeitch in some way, such as the following:

```cpp
using namespace DTimeitch;
```

or

```cpp
using DTimeitch::DigitalTime;
```

## Display 11.6 Placing a Class in a Namespace (Header File)

```cpp
//This is the header file dtime.h.
#ifndef DTIME_H
#define DTIME_H A better version of this class definition will be given in Displays 11.8 and 11.9.
```cpp
#include <iostream>
using std::istream;
using std::ostream;
namespace DTimeitch
{
    class DigitalTime
{
        <The definition of the class DigitalTime is the same as in Display 11.2>.
    };
} //DTimeitch
#endif //DTIME_H
```
Note that the namespace DTimeitch spans two files. The other is shown in Display 11.7.

## Namespaces

### Unnamed Namespaces

A compilation unit is a file, such as a class implementation file, with all the files included in the file, such as the interface header file for the class. Every compilation unit has an unnamed namespace. A grouping for the unnamed namespace is written in the same way as any other namespace, but no name is given, as in the following example:

```cpp
namespace
{
    void sampleFunction( )
} //unnamed namespace
```

## Display 11.7 Placing a Class in a Namespace (Implementation File)

```cpp
1 //This is the implementation file dtime.cpp.
2 #include <iostream>
3 #include <cctype>
4 #include <cstdlib>
5 using std::istream;
6 using std::ostream;
7 using std::cout;
8 using std::cin;
9 #include "dtime.h"
```

> You can use the single directive using namespace std; in place of these four-using declarations. However, the four-using declarations are a preferable style.

```cpp
10 namespace DTimeitch
11 {
12
14 All the function definitions from Display 11.2 go here.
15
16 //DTimeitch
```

All the names defined in the unnamed namespace are to the compilation unit, and the names can be reused for something else outside the compilation unit. Displays 11.8 and 11.9 show a rewritten (and final) version of the interface and implementation file for the class DigitalTime. Note that the helping functions readHour, readMinute, and digitToInt are all in the unnamed namespace; they are local to the compilation unit. As illustrated in Display 11.10, the names in the unnamed namespace can be reused for something else outside the compilation unit. Display 11.10, the name readHour is reused for a different function in the application program.

If you look again at the implementation file in Display 11.9, you will see that the helping functions digitToInt, readHour, and readMinute are used outside the unnamed namespace without any namespace qualifier. Any name defined in

![](img/f46fc3d28ec32a6e3350e2846de0d1_526_0.png)

the unnamed namespace can be used without qualification anywhere in the compilation unit. (Of course, this needed to be so, since the unnamed namespace has no name to use for qualifying its names.)

## Display 11.8 Hiding the Helping Functions in a Namespace (Interface File)

```cpp
//This is the header file dtime.h. This is the interface for the class
//DigitalTime. Values of this type are times of day. The values are
// input and output in 24-hour notation, as in 9:30 for 9:30 AM and
// 14:45 for 2:45 PM.
#ifndef DTIME_H
#define DTIME_H
#include <iostream>
using std::iostream;
using std::ostream;

namespace TimeSavitch {
    class DigitalTime {
        DigitalTime(int theHour, int theMinute);
        //Initial the value to 0:00 (which is midnight).

        getHour() const;
        getMinute() const;

        void advance(int minutesAdded);
        //Changes the time to minutesAdded minutes later.
        void advance(int hours, int minutesAdded);
        //Changes the time to hours plus minutesAdded minutes later.
        friend bool operator ==(const DigitalTime&t1, const DigitalTime&t2);
        friend istream& operator >>(istream& in, DigitalTime& theObject);
        friend ostream& operator <<(ostream& out, const DigitalTime& theObject);

    private:
        int hour;
        int minute;
    };
}
#endif DTIME_H
```
