```
```cpp
// Fig. 3.10: fig03_10.cpp
// Including class GradeBook from file GradeBook.h for use in main.
#include <iostream>
#include "GradeBook.h" // include definition of class GradeBook
using namespace std;

// function main begins program execution
int main()
{
    // create two GradeBook objects
    GradeBook gradeBook1( "CS101 Introduction to C++ Programming" );
    GradeBook gradeBook2( "CS102 Data Structures in C++" );

    // display initial value of courseName for each GradeBook
    cout << "gradeBook1 created for course: " << gradeBook1.getCourseName()
         << endl;
    cout << "gradeBook2 created for course: " << gradeBook2.getCourseName()
         << endl;
} // end main
```
```

```
gradeBook1 created for course: CS101 Introduction to C++ Programming
gradeBook2 created for course: CS102 Data Structures in C++
```

**Fig. 3.10**  |  Including class GradeBook from file GradeBook.h for use in main.

# Use std::: with Standard Library Components in Headers

Throughout the header (Fig. 3.9), we use std:: when referring to string (lines 11, 18, 24 and 37), and cout (line 33) and endl (line 34). For subtle reasons that we’ll explain in a later chapter, headers should never contain using directives or using declarations (Section 2.7).

# Including a Header That Contains a User-Defined Class

A header such as GradeBook.h (Fig. 3.9) cannot be used as a complete program, because it does not contain a main function. To test class GradeBook (defined in Fig. 3.9), you must write a separate source-code file containing a main function (such as Fig. 3.10) that instantiates and uses objects of the class.

The compiler doesn’t know what a GradeBook is because it’s a user-defined type. In fact, the compiler doesn’t even know the classes in the C++ Standard Library. To help it understand how to use a class, we must explicitly provide the compiler with the class’s definition—that’s why, for example, to use type string, a program must include the <string> header. This enables the compiler to determine the amount of memory that it must reserve for each string object and ensure that a program calls a string’s member functions correctly.

To create GradeBook objects gradeBook1 and gradeBook2 in lines 11–12 of Fig. 3.10, the compiler must know the size of a GradeBook object. While objects typically contain data members and member functions, C++ objects actually contain only data. The compiler creates only one copy of the class’s member functions and shares that copy among all the class’s objects. Each object, of course, needs its own data members, because their contents can vary among objects (such as two different BankAccount objects having two different balances). The member-function code, however, is not modifiable, so it can be shared among all objects of the class. Therefore, the size of an object depends on the