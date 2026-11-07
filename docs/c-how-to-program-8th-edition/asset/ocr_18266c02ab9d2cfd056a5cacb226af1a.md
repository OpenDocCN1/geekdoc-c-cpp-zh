```
```cpp
void setCourseName( string ); // function to set the course name
string getCourseName(); // function to retrieve the course name
void displayMessage(); // display a welcome message
void processGrades(); // perform various operations on the grade data
int getMinimum(); // find the minimum grade in the grade book
int getMaximum(); // find the maximum grade in the grade book
double getAverage( const int [], const int ); // get student's average
void outputBarChart(); // output bar chart of grade distribution
void outputGrades(); // output the contents of the grades array
private:
   string courseName; // course name for this grade book
   int grades[ students ][ tests ]; // two-dimensional array of grades
}; // end class GradeBook
```
```

**Fig. 7.22** | Definition of class GradeBook that uses a two-dimensional array to store test grades. (Part 2 of 2.)

```
```cpp
// Fig. 7.23: GradeBook.cpp
// Member-function definitions for class GradeBook that
// uses a two-dimensional array to store grades.
#include <iostream>
#include <iomanip> // parameterized stream manipulators
using namespace std;

// include definition of class GradeBook from GradeBook.h
#include "GradeBook.h"

// two-argument constructor initializes courseName and grades array
GradeBook::GradeBook( string name, const int gradesArray[][ tests ] )
{
   setCourseName( name ); // initialize courseName

   // copy grades from gradesArray to grades
   for ( int student = 0; student < students; ++student )
   {
      for ( int test = 0; test < tests; ++test )
         grades[ student ][ test ] = gradesArray[ student ][ test ];
   } // end for
} // end two-argument GradeBook constructor

// function to set the course name
void GradeBook::setCourseName( string name )
{
   courseName = name; // store the course name
} // end function setCourseName

// function to retrieve the course name
string GradeBook::getCourseName()
{
```
```

**Fig. 7.23** | Member-function definitions for class GradeBook that uses a two-dimensional array to store grades. (Part 1 of 4.)