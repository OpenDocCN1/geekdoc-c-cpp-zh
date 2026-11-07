
## A Composition Example: The Employee Class

There are many attributes that define an employee, such as his or her name, their age, their sex, their hiring date, etc. Some of these attributes can exist on their own as classes, such as the name and the hiring date. In this section we'll build an Employee class that is composed of objects of a Name class and a Date class.

We already defined a Name class so we can just use a simplified version of that class here. We'll list it again when we display all the code for the employee class. We don't have a Date class, however, so let's define it now.

The members of a Date class will definitely include the day, the month, and the year. There are many other possibilities but we'll limit our definition to those three members.

The methods of a Date class we'll define here include just one constructor and a method for displaying a date in mm/dd/yyyy format. There are also many other methods we could include, but these two will be enough to demonstrate how the class can be used in a class composition example.

Here is the code for the Date class:

```cpp
class Date
{
private:
    int month, day, year;

public:
    Date()
    {
        month = 0;
        day = 0;
        year = 0;
    }

    Date(int m, int d, int y)
    {
        month = m;
        day = d;
        year = y;
    }

    void setDate(int m, int d, int y)
    {
        month = m;
        day = d;
        year = y;
    }

    string getDate()
    {
        stringstream dt;
        dt << month << "/" << day << "/" << year;
        return dt.str();
    }
};
```

The getDate() method above requires some explanation. The C++ language does not do a good job combining strings and integers. The easy way to write the getDate() function is:

```cpp
return month + "/" + day + "/" + year;
```

But this method won’t compile. The easiest solution is to use a special data type, stringstream, which allows you to assign a stream of data to a variable just as you write a stream of data to the console. You can then write the stream containing the month, day, and year with slashes to the variable and then display the value of the stringstream variable as a string.

Now we’re ready to build the Employee class using the Date class and the Name class. Here is the code:

```cpp
class Employee
{
private:
    Name empName;
    Date hireDate;

public:
    Employee(string first, string middle,
             string last, int m, int d, int y)
    {
        empName.setName(first, middle, last);
        hireDate.setDate(m, d, y);
    }

    string getEmployee()
    {
        return empName.getName() + "\n" +
               hireDate.getDate() + "\n";
    }
};
```

The data members consist of two objects – a Name object and a Date object. The constructor has to call the setName and setDate methods respectively to put data into the two data members since there is no way to call the constructors at this point. The getEmployee() method simply calls the respective get methods for the Name and Date objects, along with newline characters to make the output easier to read.

Many of the problems you will run into in object-oriented programming can be solved more easily and more efficiently using composition instead of inheritance. Composition takes advantage of code reuse in much the same way inheritance does, but won’t lead to confusing, inefficient, and potentially incorrect code in the same way inheritance can. Many more problems also lend themselves to a compositional solution rather than a solution using inheritance.

## Exercises

- 1. Design a DateBook class that consists of the classes Name and Date. Write a program to test the class. Be sure to create a full set of constructors and get and set methods.
- 2. Create a DateTime class that combines a Date class and a Time class so that if the time moves from 23:59 to 00:00, the corresponding day increments by 1. Be sure to include constructor and get and set methods.

## Appendix A

### Errors and Error Messages

It is inevitable that you will have errors in your programs. It is especially true that beginning C++ programmers will have many errors in their programs, but it is equally true that expert C++ programmers experience errors in their code every day. Programming is just too complex for a programmer to not expect to have to deal with errors. In this appendix we discuss a few of the common errors you will come up against as you start learning C++. More importantly, we discuss how to interpret the error messages you will receive when the compiler finds errors in your code.

#### Syntax Errors

The most common errors you will make as you first start learning C++ programming are *syntax errors*. A syntax error means that you didn't form a C++ statement correctly. An example of a common syntax error is leaving a semicolon off the end of a statement. Here is a C++ program with a semicolon left off one of the statements:

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    cout << "Hello, World!" << endl
    Console::ReadKey();
    return 0;
}
```

When you run this program, you first get a pop-up box with this message: "There were build errors. Would you like to continue and run the last successful build?" You should answer "No" to this question.

Now look at the bottom of Visual C++ Express, in the Output window. You will see the following message:

```text
1>------ Build started: Project: ErrorHandling.cpp, Configuration: Debug Win32 ------
1>ErrorHandling.cpp
1>ErrorHandling.cpp(12): error C2143: Syntax error: missing ';' before System::Console::ReadKey
====== Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ======
```

The Output message tells you very clearly that you have a missing semicolon and it also gives you the line where the compiler finally decided an error had occurred. It couldn't tell you the error was on line 11 because it had to wait to spot the following code on line 12 to be sure that the semicolon really needed to be placed at the end of line 11. However, Console::ReadKey() can't follow cout << "Hello, World!" << endl without there being a semicolon after the endl, so the error was reported.

Another common syntax error is to mistype the name of a variable. The following program demonstrates what happens when you type a variable name incorrectly:

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number1, number2, number3;
    number1 = 12;
    number2 = 23;
    numbre3 = number1 + number2;
    cout << "The sum is: " << number3 << endl;
    Console::ReadKey();
    return 0;
}
```

You can see where the variable number3 was mistyped on line 14. The resulting error message is:

```text
1>------ Build started: Project: ErrorHandling, Configuration: Debug Win32 ------
1>ErrorHandling.cpp
1>ErrorHandling.cpp(14): error C2065: 'numbre3': undeclared identifier
1>------ Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ------
```

This error message is more user-friendly, as it reports exactly which line the typo occurred on and what the typo was. All you have to do is go back to the program and fix the mistake.

Another common syntax error is one of omission — leaving out a library from the preprocessor directives. The program below forgets to include the <iostream> library:

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

int main(array<System::String ^> ^args)
{
    cout << "Hello, World!" << endl;
    Console::ReadKey();
    return 0;
}
```

The error message you get when compiling this program is:

```text
1>----- Build started: Project: ErrorHandling, Configuration: Debug Win32 ------
1>ErrorHandling.cpp
1>ErrorHandling.cpp(8): error C2065: 'cout' : undeclared identifier
1>ErrorHandling.cpp(8): error C2065: 'endl' : undeclared identifier
=========== Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ===========
```

This error message is a little less useful than the previous one, since it doesn't tell you what you did, it just lets you know that it doesn't recognize cout and endl. Anytime you see this error message, though, and the identifiers mentioned in the error message are system objects, such as cout and endl, then you can be sure you forgot to include the library that contains those objects.

A similar error message occurs when you try to use a variable in a program that hasn't been declared:

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;
#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number1, number2;
    number1 = 12;
    number2 = 23;
```
