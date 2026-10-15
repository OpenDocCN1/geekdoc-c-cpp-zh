
```cpp
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

**Fig. 7.16** | Definition of class GradeBook using an array to store test grades. (Part 2 of 2.)

```cpp
// Fig. 7.17: GradeBook.cpp
// Member-function definitions for class GradeBook that
// uses an array to store test grades.
#include <iostream>
using std::cout;
using std::cin;
using std::endl;
using std::fixed;

#include <iomanip>
using std::setprecision;
using std::setw;

#include "GradeBook.h" // GradeBook class definition

// constructor initializes courseName and grades array
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
```

**Fig. 7.17** | GradeBook class member functions manipulating an array of grades. (Part 1 of 4.)

```cpp
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
    // output grades array
    outputGrades();

    // call function getAverage to calculate the average grade
    cout << "\nClass average is " << setprecision( 2 ) << fixed <<
        getAverage() << endl;

    // call functions getMinimum and getMaximum
    cout << "Lowest grade is " << getMinimum() << "\nHighest grade is "
        << getMaximum() << endl;

    // call function outputBarChart to print grade distribution chart
    outputBarChart();
} // end function processGrades

// find minimum grade
int GradeBook::getMinimum()
{
    int lowGrade = 100; // assume lowest grade is 100

    // loop through grades array
    for ( int grade = 0; grade < students; grade++ )
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
```

```cpp
  // loop through grades array
  for ( int grade = 0; grade < students; grade++ )
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
   for ( int grade = 0; grade < students; grade++ )
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

    // for each grade, increment the appropriate frequency
    for ( int grade = 0; grade < students; grade++ )
      frequency[ grades[ grade ] / 10 ]++;

    // for each grade frequency, print bar in chart
    for ( int count = 0; count < frequencySize; count++ )
    {
      // output bar labels ("0-9:", ..., "90-99:", "100:" )
      if ( count == 0 )
        cout << "   0-9: ";
      else if ( count == 10 )
        cout << "  100: ";
      else
        cout << count * 10 << "-" << ( count * 10 ) + 9 << ": ";

      // print bar of asterisks
      for ( int stars = 0; stars < frequency[ count ]; stars++ )
        cout << '*';
```

```cpp
    cout << endl; // start a new line of output
  } // end outer for
} // end function outputBarChart

// output the contents of the grades array
void GradeBook::outputGrades()
{
    cout << "\nThe grades are:\n\n";

    // output each student's grade
    for ( int student = 0; student < students; student++ )
        cout << "Student " << setw( 2 ) << student + 1 << ": " << setw( 3 )
            << grades[ student ] << endl;
} // end function outputGrades
```

Fig. 7.17 | GradeBook class member functions manipulating an array of grades. (Part 4 of 4.)

Note that the size of the array in line 29 of Fig. 7.16 is specified by public const static data member students (declared in line 13). This data member is public so that it is accessible to the clients of the class. We’ll soon see an example of a client program using this constant. Declaring students with the const qualifier indicates that this data member is constant—its value cannot be changed after being initialized. Keyword static in this variable declaration indicates that the data member is shared by all objects of the class—all GradeBook objects store grades for the same number of students. Recall from Section 3.6 that when each object of a class maintains its own copy of an attribute, the variable that represents the attribute is known as a data member—each object (instance) of the class has a separate copy of the variable in memory. There are variables for which each object of a class does not have a separate copy. That is the case with static data members, which are also known as class variables. When objects of a class containing static data members are created, all the objects share one copy of the class’s static data members. A static data member can be accessed within the class definition and the member-function definitions like any other data member. As you’ll soon see, a public static data member can also be accessed outside of the class, even when no objects of the class exist, using the class name followed by the binary scope resolution operator (::) and the name of the data member. You’ll learn more about static data members in Chapter 10.

The class’s constructor (declared in line 16 of Fig. 7.16 and defined in lines 17–24 of Fig. 7.17) has two parameters—the course name and an array of grades. When a program creates a GradeBook object (e.g., line 13 of fig07_18.cpp), the program passes an existing int array to the constructor, which copies the array’s values into the data member grades (lines 22–23 of Fig. 7.17). The grade values in the passed array could have been input from a user or read from a file on disk (as we discuss in Chapter 17, File Processing). In our test program, we simply initialize an array with a set of grade values (Fig. 7.18, lines 10–11). Once the grades are stored in data member grades of class GradeBook, all the class’s member functions can access the grades array as needed to perform various calculations.

Member function processGrades (declared in line 21 of Fig. 7.16 and defined in lines 48–63 of Fig. 7.17) contains a series of member function calls that output a report summarizing the grades. Line 51 calls member function outputGrades to print the contents of the array grades. Lines 148–150 in member function outputGrades use a for
