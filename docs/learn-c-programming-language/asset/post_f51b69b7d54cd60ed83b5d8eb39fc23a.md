
```cpp
vals[4] = 50
```

When returning a reference, be careful that the object being referred to does not go out of scope. So it is not legal to return a reference to a local var. But you can always return a reference on a static variable.

```cpp
int& func() {
    int q;

    //! return q; // Compile time error

    static int x;

    return x;    // Safe, x lives outside this scope
}
```

## 20. DATE AND TIME

The C++ standard library does not provide a proper date type. C++ inherits the structs and functions for date and time manipulation from C. To access date and time related functions and structures, you would need to include `<ctime>` header file in your C++ program.

There are four time-related types: **clock_t, time_t, size_t, and tm**. The types - clock_t, size_t and time_t are capable of representing the system time and date as some sort of integer.

The structure type **tm** holds the date and time in the form of a C structure having the following elements:

```cpp
struct tm {
  int tm_sec;   // seconds of minutes from 0 to 61
  int tm_min;   // minutes of hour from 0 to 59
  int tm_hour;  // hours of day from 0 to 24
  int tm_mday;  // day of month from 1 to 31
  int tm_mon;   // month of year from 0 to 11
  int tm_year;  // year since 1900
  int tm_wday;  // days since Sunday
  int tm_yday;  // days since January 1st
  int tm_isdst; // hours of daylight savings time
}
```

Following are the important functions, which we use while working with date and time in C or C++. All these functions are part of standard C and C++ library and you can check their detail using reference to C++ standard library given below.

| SN | Function & Purpose |
| --- | --- |
| 1 | **time_t time(time_t *time);**<br>This returns the current calendar time of the system in number of seconds elapsed since January 1, 1970. If the system has no time, -1 is returned. |
| 2 | **char *ctime(const time_t *time);**<br>This returns a pointer to a string of the form *day month year* |
| 3 | **struct tm *localtime(const time_t *time);**<br><br>This returns a pointer to the **tm** structure representing local time. |
| 4 | **clock_t clock(void);**<br><br>This returns a value that approximates the amount of time the calling program has been running. A value of -1 is returned if the time is not available. |
| 5 | **char * asctime ( const struct tm * time );**<br><br>This returns a pointer to a string that contains the information stored in the structure pointed to by time converted into the form: day month date hours:minutes:seconds year\n\0 |
| 6 | **struct tm *gmtime(const time_t *time);**<br><br>This returns a pointer to the time in the form of a tm structure. The time is represented in Coordinated Universal Time (UTC), which is essentially Greenwich Mean Time (GMT). |
| 7 | **time_t mktime(struct tm *time);**<br><br>This returns the calendar-time equivalent of the time found in the structure pointed to by time. |
| 8 | **double difftime ( time_t time2, time_t time1 );**<br><br>This function calculates the difference in seconds between time1 and time2. |
| 9 | **size_t strftime();**<br><br>This function can be used to format date and time in a specific format. |

### Current Date and Time

Suppose you want to retrieve the current system date and time, either as a local time or as a Coordinated Universal Time (UTC). Following is the example to achieve the same:

```cpp
#include <iostream>
#include <ctime>

using namespace std;

int main( )
{
    // current date/time based on current system
    time_t now = time(0);

    cout << "Number of sec since January 1, 1970:" << now << endl;

    tm *ltm = localtime(&now);

    // print various components of tm structure.
    cout << "Year: "<< 1900 + ltm->tm_year << endl;
    cout << "Month: "<< 1 + ltm->tm_mon<< endl;
    cout << "Day: "<<  ltm->tm_mday << endl;
    cout << "Time: "<< 1 + ltm->tm_hour << ":";
    cout << 1 + ltm->tm_min << ":";
    cout << 1 + ltm->tm_sec << endl;
}
```

When the above code is compiled and executed, it produces the following result:

```text
Number of sec since January 1, 1970:1294548238
Year: 2011
Month: 1
Day: 8
Time: 22:44:59
```

```cpp
using namespace std;

int main( )
{
    char str[] = "Hello C++";

    cout << "Value of str is : " << str << endl;
}
```

When the above code is compiled and executed, it produces the following result:

```text
Value of str is : Hello C++
```

The C++ compiler also determines the data type of variable to be output and selects the appropriate stream insertion operator to display the value. The << operator is overloaded to output data items of built-in types integer, float, double, strings and pointer values.

The insertion operator << may be used more than once in a single statement as shown above and **endl** is used to add a new-line at the end of the line.

### The Standard Input Stream (cin)

The predefined object **cin** is an instance of **istream** class. The cin object is said to be attached to the standard input device, which usually is the keyboard. The **cin** is used in conjunction with the stream extraction operator, which is written as >> which are two greater than signs as shown in the following example.

```cpp
#include <iostream>

using namespace std;

int main( )
{
    char name[50];

    cout << "Please enter your name: ";
    cin >> name;
    cout << "Your name is: " << name << endl;
}
```

When the above code is compiled and executed, it will prompt you to enter a name. You enter a value and then hit enter to see the following result:

```text
Please enter your name: cplusplus
Your name is: cplusplus
```

The C++ compiler also determines the data type of the entered value and selects the appropriate stream extraction operator to extract the value and store it in the given variables.

The stream extraction operator >> may be used more than once in a single statement. To request more than one datum you can use the following:

```cpp
cin >> name >> age;
```

This will be equivalent to the following two statements:

```cpp
cin >> name;
cin >> age;
```

### The Standard Error Stream (cerr)

The predefined object cerr is an instance of ostream class. The cerr object is said to be attached to the standard error device, which is also a display screen but the object cerr is un-buffered and each stream insertion to cerr causes its output to appear immediately.

The cerr is also used in conjunction with the stream insertion operator as shown in the following example.

```cpp
#include <iostream>

using namespace std;

int main( )
{
    char str[] = "Unable to read....";

    cerr << "Error message : " << str << endl;
}
```

When the above code is compiled and executed, it produces the following result:

```text
Error message : Unable to read....
```

### The Standard Log Stream (clog)

The predefined object **clog** is an instance of **ostream** class. The clog object is said to be attached to the standard error device, which is also a display screen but the object **clog** is buffered. This means that each insertion to clog could cause its output to be held in a buffer until the buffer is filled or until the buffer is flushed.

The **clog** is also used in conjunction with the stream insertion operator as shown in the following example.

```cpp
#include <iostream>

using namespace std;

int main( )
{
    char str[] = "Unable to read....";

    clog << "Error message : " << str << endl;
}
```

When the above code is compiled and executed, it produces the following result:

```text
Error message : Unable to read....
```

You would not be able to see any difference in cout, cerr and clog with these small examples, but while writing and executing big programs the difference becomes obvious. So it is good practice to display error messages using cerr stream and while displaying other log messages then clog should be used.
