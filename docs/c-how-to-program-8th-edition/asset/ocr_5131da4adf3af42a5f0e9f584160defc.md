| Function | Description | Example |
|---|---|---|
| `pow(x, y)` | *x* raised to power *y* (*x*^*y*) | `pow(2, 7)` is 128<br>`pow(9, .5)` is 3 |
| `sin(x)` | trigonometric sine of *x*<br>(*x* in radians) | `sin(0.0)` is 0 |
| `sqrt(x)` | square root of *x* (where *x* is a nonnegative value) | `sqrt(9.0)` is 3.0 |
| `tan(x)` | trigonometric tangent of *x*<br>(*x* in radians) | `tan(0.0)` is 0 |

**Fig. 6.2**  |  Math library functions. (Part 2 of 2.)

# 6.4 Function Definitions with Multiple Parameters

Let’s consider functions with *multiple* parameters. Figures 6.3–6.5 modify class GradeBook by including a user-defined function called maximum that determines and returns the largest of three int grades. When the application executes, the main function (lines 5–13 of Fig. 6.5) creates one GradeBook object (line 8) and calls its inputGrades member function (line 11) to read three integer grades from the user. In class GradeBook’s implementation file (Fig. 6.4), lines 52–53 of member function inputGrades prompt the user to enter three integer values and read them from the user. Line 56 calls member function maximum (defined in lines 60–73). Function maximum determines the largest value, then the return statement (line 72) returns that value to the point at which function Grades invokes maximum (line 56). Member function inputGrades then stores maximum’s return value in data member maximumGrade. This value is then output by calling function displayGradeReport (line 12 of Fig. 6.5). [*Note:* We named this function displayGradeReport because subsequent versions of class GradeBook will use this function to display a complete grade report, including the maximum and minimum grades.] In Chapter 7, Arrays and Vectors, we’ll enhance class GradeBook to process an arbitrary number of grades.

```
```cpp
// Fig. 6.3: GradeBook.h
// Definition of class GradeBook that finds the maximum of three grades.
// Member functions are defined in GradeBook.cpp
#include <string> // program uses C++ standard string class
using namespace std;

// GradeBook class definition
class GradeBook
{
public:
    GradeBook( string ); // constructor initializes course name
    void setCourseName( string ); // function to set the course name
    string getCourseName(); // function to retrieve the course name
    void displayMessage(); // display a welcome message
    void inputGrades(); // input three grades from user
};
```
```

**Fig. 6.3**  |  GradeBook header. (Part 1 of 2.)