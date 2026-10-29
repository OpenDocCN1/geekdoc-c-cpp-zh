
## Display 11.9  Hiding the Helping Functions in a Namespace (Implementation File) (part 1 of 3)

```
//This is the implementation file dtime.cpp of the class DigitalTime.
//The interface for the class DigitalTime is in the header file dtime.h.
#include <iostream>
#include <cctype>
#include <cstdlib>
using std::istream;
using std::ostream;
using std::cout;
using std::cin;
#include "dtime.h"

namespace
{
    int digitToInt(char c)
    {
        return (int(c) - int('0'));
    }

    //Uses iostream, cctype, and cstdlib:
    void readMinute(int& theMinute)
    {
        char c1, c2;
        cin >> c1 >> c2;
        if (!(isdigit(c1) && isdigit(c2)))
        {
            cout << "Error: illegal input to readMinute\n";
            exit(1);
        }

        theMinute = digitToInt(c1)*10 + digitToInt(c2);

        if (theMinute < 0 || theMinute > 59)
        {
            cout << "Error: illegal input to readMinute\n";
            exit(1);
        }
    }

    //Uses iostream, cctype, and cstdlib:
    void readHour(int& theHour)
    {
        char c1, c2;
        cin >> c1 >> c2;
```

> Specifies the unnamed namespace

> Names defined in the unnamed namespace are local to the compilation unit. So, these helping functions are local to the file dtime.cpp.

## Display 11.9 Hiding the Helping Functions in a Namespace (Implementation File) (part 2 of 3)

```
40  if ( ! ( isdigit(c1) && isdigit(c2) || c2 == ':' ) )
41  {
42      cout << "Error: illegal input to readHour\n";
43      exit(1);
44  }
45
46  if ( isdigit(c1) && c2 == ':' )
47  {
48      theHour = digitToInt(c1);
49  }
50  else // (isdigit(c1) && isdigit(c2))
51  {
52      theHour = digitToInt(c1)*10 + digitToInt(c2);
53      cin >> c2; // discard '
54      if (c2 != ':')
55      {
56          cout << "Error: illegal input to readHour\n";
57          exit(1);
58      }
59  }
60
59  if (theHour == 24)
60      theHour = 0; // Standardize midnight as 0:00.
61
62  if (theHour < 0 || theHour > 23)
63  {
64      cout << "Error: illegal input to readHour\n";
65      exit(1);
66  }
67  } // unnamed namespace
68
69  namespace DTimeSavitch
70  {
71
72      // Uses iostream:
73      istream& operator >> (istream& ins, DigitalTime& theObject)
74      {
75          readHour(theObject.hour);
76          readMinute(theObject.minute);
77          return ins;
78      }
79      ostream& operator << (ostream& outs, const DigitalTime& theObject)
80      <The body of the function definition is the same as in Display 11.2.>

Within the compilation unit (in this case dtime.cpp), you can use names in the unnamed namespace without qualification.
```

## Display 11.10 Hiding the Helping Functions in a Namespace (Application Program) (part 2 of 2)

```
14      DigitalTime clock(theHour, 0), oldClock;

16      oldClock = clock;
17      clock.advance(15);
18      if (clock == oldClock)
19          cout << "Something is wrong.";
20      cout << "You entered " << oldClock << endl;
21      cout << "15 minutes later the time will be "
22          << clock << endl;

24      clock.advance(2, 15);
25      cout << "2 hours and 15 minutes after that\n"
26          << "the time will be "
27          << clock << endl;

29      return 0;
30  }
31  
32  void readHour(int& theHour)
33  {
34      using std::cout;
35      using std::cin;

37      cout << "Let's play a time game.\n"
38          << "Let's pretend the hour has just changed.\n"
39          << "You may write midnight as either 0 or 24,\n"
40          << "but, I will always write it as 0.\n"
41          << "Enter the hour as a number (0 to 24): ";
42      cin >> theHour;
```

When we gave these using declarations before, they were in main, so their scope was main. Thus, we need to repeat them here in order to use cin and cout in readHour.

### Sample Dialogue

```
Let's play a time game.
Let's pretend the hour has just changed.
You may write midnight as either 0 or 24,
but, I will always write it as 0.
Enter the hour as a number (0 to 24): 11
You entered 11:00
15 minutes later the time will be 11:15
2 hours and 15 minutes after that
the time will be 13:30
```

## Unnamed Namespace

You can use the *unnamed namespace* to make a definition local to a compilation unit. Each compilation unit has one unnamed namespace. All the identifiers defined in the unnamed namespace are local to the compilation unit. You place a definition in the unnamed namespace by placing the definition in a namespace grouping with no namespace name, as shown next:

```
namespace
{
    Definition_1
    Definition_2
    .
    .
    .
    Definition_Last
}
```

You can use any name in the unnamed namespace without qualifiers anyplace in the compilation unit. See Displays 11.8, 11.9, and 11.10 for a complete example.

## PITFALL: Confusing the Global Namespace and the Unnamed Namespace

Do not confuse the global namespace with the unnamed namespace. If you do not put a name definition in a namespace grouping, then it is in the global namespace. To put a name definition in the unnamed namespace, you must put it in a namespace grouping that starts out as follows, without a name:

```
namespace
{

```

Names in the global namespace and names in the unnamed namespace may both be accessed without a qualifier. However, names in the global namespace have global scope (all the program files), whereas names in an unnamed namespace are local to a compilation unit.

This confusion between the global namespace and the unnamed namespace does not arise very much in writing code, since there is a tendency to think of names in the global namespace as being “in no namespace,” even though that is not technically correct. However, the confusion can easily arise when discussing code.

## TIP: Unnamed Namespaces Replace the static Qualifier

Earlier versions of C++ used the qualifier static to make a name local to a file. This use of static is being phased out, and you should instead use the unnamed namespace to make a name local to a compilation unit. Note that this use of static has nothing to do with the use of static to make class members shared by all objects of a class (as discussed in the subsection "Static Members" of Chapter 7). So, since static is used to mean more than one thing, it is probably good that one use of the word is being phased out.

## TIP: Hiding Helping Functions

There are two good ways to hide a helping function for a class. You can make the function a private member function of the class or you can place the helping function in the unnamed namespace for the implementation file of the class. If the function naturally takes a calling object, then it should be made a private member function. If it does not naturally take a calling object, you can make it a static member function (for example, DigitalTime::readHour in Displays 11.1 and 11.2) or you can place it in the unnamed namespace of the implementation file (for example, readHour in Displays 11.8 and Displays 11.9).

If the helping function does not need a calling object, then placing the helping function in the unnamed namespace of the implementation file makes for cleaner code because it better separates interface and implementation into separate files and it avoids the need for so much function name qualification. For example, note that in Display 11.9 we can use the function name readHour unqualified since it is in the unnamed namespace, while in the version in Display 11.2 we need to use DigitalTime::readHour.

It is interesting to note how unnamed namespaces interact with the C++ rule that you cannot have two definitions of a name in the same namespace. There is one unnamed namespace in each compilation unit. It is easily possible for compilation units to overlap. For example, both the implementation file for a class and an application program using the class would normally include the header file (interface file) for the class. Thus, the header file is in two compilation units and hence participates in two unnamed namespaces. As dangerous as this sounds, it will normally produce no problems as long as each compilation unit's namespace makes sense when considered by itself. For example, if a name is defined in the unnamed namespace in the header file, it cannot be defined again in the unnamed namespace in either the implementation file or the application file. Thus, a name conflict is avoided.
