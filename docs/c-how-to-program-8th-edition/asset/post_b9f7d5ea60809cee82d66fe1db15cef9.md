
There may be situations in your programs in which a function should not be allowed to modify array elements. The type qualifier `const` can be used to prevent modification of array values in the caller by code in a called function. When a function specifies an array parameter that’s preceded by the `const` qualifier, the elements of the array become constant in the function body, and any attempt to modify an element of the array in the function body results in a compilation error. This enables you to prevent accidental modification of array elements in the function’s body.

Figure 7.14 demonstrates the `const` qualifier applied to an array parameter. Function `tryToModifyArray` (lines 18–21) is defined with parameter `const int b[]`, which specifies that array `b` is constant and cannot be modified. The attempt by the function to modify array `b`’s element 0 (line 20) results in a compilation error. Some compilers, for example, produce an error like “Cannot modify a const object.” This message indicates that using a const object (`b[0]`) as an lvalue is an error—you cannot assign a new value to a const object.

![](img/bfd978e7e9b192bab46ec2a89e481263_319_0.png)

> **Software Engineering Observation 7.3**
> 
> *Applying the `const` type qualifier to an array parameter in a function definition to prevent the original array from being modified in the function body is another example of the principle of least privilege. Functions should not be given the capability to modify an array unless it’s absolutely necessary.*

```cpp
// Fig. 7.14: fig07_14.cpp
// Demonstrating the const type qualifier.
#include <iostream>
using namespace std;

void tryToModifyArray( const int b[] ); // function prototype

int main()
{
   int a[] = { 10, 20, 30 };

   tryToModifyArray( a );
   cout << a[ 0 ] << ' ' << a[ 1 ] << ' ' << a[ 2 ] << '\n';
} // end main

// In function tryToModifyArray, "b" cannot be used
// to modify the original array "a" in main.
void tryToModifyArray( const int b[] )
{
   b[ 0 ] /= 2; // compilation error
} // end function tryToModifyArray
```

*Microsoft Visual C++ compiler error message:*

```text
c:\cpphtp_examples\ch07\fig07_14\fig07_14.cpp(20) : error C3892: 'b' : you
cannot assign to a variable that is const
```

*GNU C++ compiler error message:*

```text
fig07_14.cpp:20: error: assignment of read-only location
```

**Fig. 7.14** | `const` type qualifier applied to an array parameter.

## 7.6 Case Study: Class GradeBook Using an Array to Store Grades

This section further evolves class GradeBook, introduced in Chapter 3 and expanded in Chapters 4–6. Recall that this class represents a grade book used by a professor to store and analyze student grades. Previous versions of the class process grades entered by the user, but do not maintain the individual grade values in the class’s data members. Thus, repeat calculations require the user to reenter the grades. One way to solve this problem would be to store each grade entered in an individual data member of the class. For example, we could create data members grade1, grade2, …, grade10 in class GradeBook to store 10 student grades. However, the code to total the grades and determine the class average would be cumbersome. In this section, we solve this problem by storing grades in an array.

### Storing Student Grades in an Array in Class GradeBook

The version of class GradeBook (Figs. 7.15–7.16) presented here uses an array of integers to store the grades of several students on a single exam. This eliminates the need to repeatedly input the same set of grades. Array `grades` is declared as a data member in line 28 of Fig. 7.15—therefore, each GradeBook object maintains its own set of grades.

```cpp
// Fig. 7.15: GradeBook.h
// Definition of class GradeBook that uses an array to store test grades.
// Member functions are defined in GradeBook.cpp
#include <string> // program uses C++ Standard Library string class
using namespace std;

// GradeBook class definition
class GradeBook
{
public:
   // constant -- number of students who took the test
   static const int students = 10; // note public data

   // constructor initializes course name and array of grades
   GradeBook( string, const int [] );

   void setCourseName( string ); // function to set the course name
   string getCourseName(); // function to retrieve the course name
   void displayMessage(); // display a welcome message
   void processGrades(); // perform various operations on the grade data
   int getMinimum(); // find the minimum grade for the test
   int getMaximum(); // find the maximum grade for the test
   double getAverage(); // determine the average grade for the test
   void outputBarChart(); // output bar chart of grade distribution
   void outputGrades(); // output the contents of the grades array
private:
   string courseName; // course name for this grade book
   int grades[ students ]; // array of student grades
}; // end class GradeBook
```

**Fig. 7.15** | Definition of class GradeBook that uses an array to store test grades.

```cpp
// Fig. 7.16: GradeBook.cpp
// Member-function definitions for class GradeBook that
// uses an array to store test grades.
#include <iostream>
#include <iomanip>
#include "GradeBook.h" // GradeBook class definition
using namespace std;

// constructor that initializes courseName and grades array
GradeBook::GradeBook( string name, const int gradesArray[] )
{
   setCourseName( name ); // initialize courseName

   // copy grades from gradesArray to grades data member
   for ( int grade = 0; grade < students; grade++ )
      grades[ grade ] = gradesArray[ grade ];
} // end GradeBook constructor

// function to set the course name
void GradeBook::setCourseName( string name )
{
   courseName = name; // store the course name
} // end function setCourseName

// function to retrieve the course name
string GradeBook::getCourseName()
{
   return courseName;
} // end function getCourseName

// display a welcome message to the GradeBook user
void GradeBook::displayMessage()
{
   // this statement calls getCourseName to get the
   // name of the course this GradeBook represents
   cout << "Welcome to the grade book for\n" << getCourseName() << "!"
        << endl;
} // end function displayMessage

// perform various operations on the data
void GradeBook::processGrades()
{
   outputGrades(); // output grades array

   // display average of all grades and minimum and maximum grades
   cout << "\nClass average is " << setprecision(2) << fixed <<
      getAverage() << "\nLowest grade is " << getMinimum() <<
      "\nHighest grade is " << getMaximum() << endl;

   outputBarChart(); // print grade distribution chart
} // end function processGrades

// find minimum grade
int GradeBook::getMinimum()
{
   int lowGrade = 100; // assume lowest grade is 100

   // loop through grades array
   for ( int grade = 0; grade < students; ++grade )
   {
      // if current grade lower than lowGrade, assign it to lowGrade
      if ( grades[ grade ] < lowGrade )
         lowGrade = grades[ grade ]; // new lowest grade
   } // end for

   return lowGrade; // return lowest grade
} // end function getMinimum

// find maximum grade
int GradeBook::getMaximum()
{
   int highGrade = 0; // assume highest grade is 0

   // loop through grades array
   for ( int grade = 0; grade < students; ++grade )
   {
      // if current grade higher than highGrade, assign it to highGrade
      if ( grades[ grade ] > highGrade )
         highGrade = grades[ grade ]; // new highest grade
   } // end for

   return highGrade; // return highest grade
} // end function getMaximum

// determine average grade for test
double GradeBook::getAverage()
{
   int total = 0; // initialize total

   // sum grades in array
   for ( int grade = 0; grade < students; ++grade )
      total += grades[ grade ];

   // return average of grades
   return static_cast< double >( total ) / students;
} // end function getAverage

// output bar chart displaying grade distribution
void GradeBook::outputBarChart()
{
   cout << "\nGrade distribution:" << endl;

   // stores frequency of grades in each range of 10 grades
   const int frequencySize = 11;
   int frequency[ frequencySize ] = {}; // initialize elements to 0
```

**Fig. 7.16** | GradeBook class member functions manipulating an array of grades.
