# Good Programming Practice 3.5

Although parameter names in function prototypes are optional (they are ignored by the compiler), many programmers use these names for documentation purposes.

# Error-Prevention Tip 3.4

Parameter names in a function prototype (which, again, are ignored by the compiler) can be misleading if wrong or confusing names are used. For this reason, many programmers create function prototypes by copying the first line of the corresponding function definitions (when the source code for the functions is available), then appending a semicolon to the end of each prototype.

# GradeBook.cpp: Defining Member Functions in a Separate Source-Code File

GradeBook.cpp (Fig. 3.12) defines class GradeBook’s member functions, which were declared in lines 12–15 of Fig. 3.11. The member-function definitions appear in lines 11–34 and are nearly identical to the member-function definitions in lines 15–38 of Fig. 3.9.

```
```cpp
// Fig. 3.12: GradeBook.cpp
// GradeBook member-function definitions. This file contains
// implementations of the member functions prototyped in GradeBook.h.
#include <iostream>
using std::cout;
using std::endl;

#include "GradeBook.h" // include definition of class GradeBook

// constructor initializes courseName with string supplied as argument
GradeBook::GradeBook( string name )
{
   setCourseName( name ); // call set function to initialize courseName
} // end GradeBook constructor

// function to set the course name
void GradeBook::setCourseName( string name )
{
   courseName = name; // store the course name in the object
} // end function setCourseName

// function to get the course name
string GradeBook::getCourseName()
{
   return courseName; // return object's courseName
} // end function getCourseName

// display a welcome message to the GradeBook user
void GradeBook::displayMessage()
{
   // call getCourseName to get the coursename
   cout << "Welcome to the grade book for\\n" << getCourseName()
        << "!" << endl;
} // end function displayMessage
```
```

**Fig. 3.12** | GradeBook member-function definitions represent the implementation of class GradeBook.