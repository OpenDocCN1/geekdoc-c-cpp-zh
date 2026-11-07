
execute the following statement.” Thus, for each iteration, identifier item represents one element in items. Lines 13–14 are equivalent to the following counter-controlled repetition:

```cpp
for ( int counter = 0; counter < items.size(); ++counter )
    cout << items[ counter ] << " ";
```

## Using the Range-Based for to Modify an Array’s Contents

Lines 17–18 use a range-based for statement to multiply each element of items by 2. In line 17, the rangeVariableDeclaration indicates that itemRef is an item reference (&). Recall that a reference is an alias for another variable in memory—in this case, one of the array’s elements. We use an int reference because items contains int values and we want to modify each element’s value—because itemRef is declared as a reference, any change you make to itemRef changes the corresponding element value in the array.

## Using an Element’s Subscript

The range-based for statement can be used in place of the counter-controlled for statement whenever code looping through an array does not require access to the element’s subscript. For example, totaling the integers in an array (as in Fig. 7.8) requires access only to the element values—the elements’ subscripts are irrelevant. However, if a program must use subscripts for some reason other than simply to loop through an array (e.g., to print a subscript number next to each array element value, as in the examples early in this chapter), you should use the counter-controlled for statement.

## 7.6 Case Study: Class GradeBook Using an array to Store Grades

This section further evolves class GradeBook, introduced in Chapter 3 and expanded in Chapters 4–6. Recall that this class represents a grade book used by a professor to store and analyze student grades. Previous versions of the class process grades entered by the user, but do not maintain the individual grade values in the class’s data members. Thus, repeat calculations require the user to reenter the grades. One way to solve this problem would be to store each grade entered in an individual data member of the class. For example, we could create data members grade1, grade2, …, grade10 in class GradeBook to store 10 student grades. However, the code to total the grades and determine the class average would be cumbersome. In this section, we solve this problem by storing grades in an array.

### Storing Student Grades in an array in Class GradeBook

Figure 7.14 shows the output that summarizes the 10 grades we store in an object of the next version of class GradeBook (Figs. 7.15–7.16), which uses an array of integers to store the grades of 10 students for a single exam. This eliminates the need to repeatedly input the same set of grades, array grades is declared as a data member in line 28 of Fig. 7.15—therefore, each GradeBook object maintains its own set of grades.

```text
Welcome to the grade book for
CS101 Introduction to C++ Programming!
```

**Fig. 7.14**  |  Output of the GradeBook example that stores grades in an array. (Part 1 of 2.)

```cpp
double getAverage() const; // determine the average grade for the test
void outputBarChart() const; // output bar chart of grade distribution
void outputGrades() const; // output the contents of the grades array
private:
std::string courseName; // course name for this grade book
std::array< int, students > grades; // array of student grades
}; // end class GradeBook
```

**Fig. 7.15** | Definition of class GradeBook that uses an array to store test grades. (Part 2 of 2.)

```cpp
// Fig. 7.16: GradeBook.cpp
// GradeBook class member functions manipulating
// an array of grades.
#include <iostream>
#include <iomanip>
#include "GradeBook.h" // GradeBook class definition
using namespace std;

// constructor initializes courseName and grades array
GradeBook::GradeBook( const string &name,
   const array< int, students > &gradesArray )
   : courseName( name ), grades( gradesArray )
{
} // end GradeBook constructor

// function to set the course name
void GradeBook::setCourseName( const string &name )
{
   courseName = name; // store the course name
} // end function setCourseName

// function to retrieve the course name
string GradeBook::getCourseName() const
{
   return courseName;
} // end function getCourseName

// display a welcome message to the GradeBook user
void GradeBook::displayMessage() const
{
   // this statement calls getCourseName to get the
   // name of the course this GradeBook represents
   cout << "Welcome to the grade book for\n" << getCourseName() << "!"
      << endl;
} // end function displayMessage

// perform various operations on the data
void GradeBook::processGrades() const
{
   // output grades array
   outputGrades();

   // call function getAverage to calculate the average grade
   cout << setprecision( 2 ) << fixed;
   cout << "\nClass average is " << getAverage() << endl;

   // call functions getMinimum and getMaximum
   cout << "Lowest grade is " << getMinimum() << "\nHighest grade is "
        << getMaximum() << endl;

   // call function outputBarChart to print grade distribution chart
   outputBarChart();
} // end function processGrades

// find minimum grade
int GradeBook::getMinimum() const
{
   int lowestGrade = 100; // assume lowest grade is 100

   // loop through grades array
   for ( int grade : grades )
   {
      // if current grade lower than lowestGrade, assign it to lowestGrade
      if ( grade < lowestGrade )
         lowestGrade = grade; // new lowest grade
   } // end for

   return lowestGrade; // return lowest grade
} // end function getMinimum

// find maximum grade
int GradeBook::getMaximum() const
{
   int highGrade = 0; // assume highest grade is 0

   // loop through grades array
   for ( int grade : grades )
   {
      // if current grade higher than highGrade, assign it to highGrade
      if ( grade > highGrade )
         highGrade = grade; // new highest grade
   } // end for

   return highGrade; // return highest grade
} // end function getMaximum

// determine average grade for test
double GradeBook::getAverage() const
{
   int total = 0; // initialize total

   // sum grades in array
   for ( int grade : grades )
      total += grade;
```

**Fig. 7.16** | GradeBook class member functions manipulating an array of grades. (Part 1 of 3.)

**Fig. 7.16** | GradeBook class member functions manipulating an array of grades. (Part 2 of 3.)

indicates that the data member is shared by all objects of the class—so in this particular implementation of class GradeBook, all GradeBook objects store grades for the same number of students. Recall from Section 3.4 that when each object of a class maintains its own copy of an attribute, the variable that represents the attribute is known as a data member—each object (instance) of the class has a separate copy of the variable in memory. There are variables for which each object of a class does not have a separate copy. That is the case with static data members, which are also known as class variables. When objects of a class containing static data members are created, all the objects share one copy of the class’s static data members. A static data member can be accessed within the class definition and the member-function definitions like any other class member. As you’ll soon see, a public static data member can also be accessed outside of the class, even when no objects of the class exist, using the class name followed by the scope resolution operator (::) and the name of the data member. You’ll learn more about static data members in Chapter 9.

### Constructor

The class’s constructor (declared in line 15 of Fig. 7.15 and defined in lines 10–14 of Fig. 7.16) has two parameters—the course name and a reference to an array of grades. When a program creates a GradeBook object (e.g., line 15 of Fig. 7.17), the program passes an existing int array to the constructor, which copies the array’s values into the data member grades (line 12 of Fig. 7.16). The grade values in the passed array could have been input from a user or read from a file on disk (as we discuss in Chapter 14, File Processing). In our test program, we simply initialize an array with a set of grade values (Fig. 7.17, lines 11–12). Once the grades are stored in data member grades of class GradeBook, all the class’s member functions can access the grades array as needed to perform various calculations. Note that the constructor receives both the string and the array by reference—this is more efficient than receiving copies of the original string and array. The constructor does not need to modify either the original string or array, so we also declared each parameter as const to ensure that the constructor does not accidentally modify the original data in the caller. We also modified function setCourseName to receive its string argument by reference.

### Member Function processGrades

Member function processGrades (declared in line 20 of Fig. 7.15 and defined in lines 38–53 of Fig. 7.16) contains a series of member function calls that output a report summarizing the grades. Line 41 calls member function outputGrades to print the contents of the array grades. Lines 138–140 in member function outputGrades use a for statement to output each student’s grade. Although array indices start at 0, a professor would typically number students starting at 1. Thus, lines 139–140 output student + 1 as the student number to produce grade labels “Student 1: ”, “Student 2: ”, and so on.

### Member Function getAverage

Member function processGrades next calls member function getAverage (line 45) to obtain the average of the grades. Member function getAverage (declared in line 23 of Fig. 7.15 and defined in lines 88–98 of Fig. 7.16) totals the values in array grades before calculating the average. The averaging calculation in line 97 uses grades.size() to determine the number of grades being averaged.
