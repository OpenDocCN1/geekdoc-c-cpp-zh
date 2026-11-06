
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
    string courseName; // course name for this GradeBook
    int grades[ students ]; // array of student grades
}; // end class GradeBook
```

*Fig. 7.15 | Definition of class GradeBook using an array to store test grades.*

```cpp
// Fig. 7.16: GradeBook.cpp
// Member-function definitions for class GradeBook that
// uses an array to store test grades.
#include <iostream>
#include <iomanip>
#include "GradeBook.h" // GradeBook class definition
using namespace std;

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
    cout << "\nClass average is " << setprecision( 2 ) << fixed <<
        getAverage() << "\nLowest grade is " << getMinimum() <<
        "\nHighest grade is " << getMaximum() << endl;

    outputBarChart(); // print grade distribution chart
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
    return static_cast<double>( total ) / students;
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
        ++frequency[ grades[ grade ] / 10 ];

    // for each grade frequency, print bar in chart
    for ( int count = 0; count < frequencySize; count++ )
    {
        // output bar labels ("0-9": ..., "90-99":, "100":)
        if ( count == 0 )
            cout << "  0-9: ";
        else if ( count == 10 )
            cout << "  100: ";
        else
            cout << count * 10 << "-" << ( count * 10 ) + 9 << ": ";

        // print bar of asterisks
        for ( int stars = 0; stars < frequency[ count ]; stars++ )
            cout << '*';
    }
```

*Fig. 7.16 | GradeBook class member functions manipulating an array of grades. (Part 1 of 4.)*

*Fig. 7.16 | GradeBook class member functions manipulating an array of grades. (Part 2 of 4.)*

*Fig. 7.16 | GradeBook class member functions manipulating an array of grades. (Part 3 of 4.)*

Member function `processGrades` (declared in line 20 of Fig. 7.15 and defined in lines 41–51 of Fig. 7.16) contains a series of member function calls that output a report summarizing the grades. Line 43 calls member function `outputGrades` to print the contents of the array `grades`. Lines 136–138 in member function `outputGrades` use a `for` statement to output each student's grade. Although array indices start at 0, a professor would typically number students starting at 1. Thus, lines 137–138 output `student + 1` as the student number to produce grade labels "Student 1: ", "Student 2: ", and so on.

Member function `processGrades` next calls member function `getAverage` (line 47) to obtain the average of the grades in the array. Member function `getAverage` (declared in line 23 of Fig. 7.15 and defined in lines 86–96 of Fig. 7.16) uses a `for` statement to total the values in array `grades` before calculating the average. The averaging calculation in line 95 uses `static const` data member `students` to determine the number of grades being averaged.

Lines 47–48 in member function `processGrades` call member functions `getMinimum` and `getMaximum` to determine the lowest and highest grades of any student on the exam, respectively. Let's examine how member function `getMinimum` finds the lower grade. Because the highest grade allowed is 100, we begin by assuming that 100 is the lowest grade (line 56). Then, we compare each of the elements in the array to the lowest grade, looking for smaller values. Lines 59–64 in member function `getMinimum` loop through the array, and line 62 compares each `grade` to `lowGrade`. If a `grade` is less than `lowGrade`, `lowGrade` is set to that grade. When line 66 executes, `lowGrade` contains the lowest grade in the array. Member function `getMaximum` (lines 70–83) works similarly to member function `getMinimum`.

Finally, line 50 in member function `processGrades` calls member function `outputBarChart` to print a distribution chart of the grade data using a technique similar to that in Fig. 7.9. In that example, we manually calculated the number of grades in each category (i.e., 0–9, 10–19, ..., 90–99 and 100) by simply looking at a set of grades. In this example, lines 108–109 use a technique similar to that in Fig. 7.10 and Fig. 7.11 to calculate the frequency of grades in each category. Line 105 declares and creates array `frequency` of 11 `int`s to store the frequency of grades in each grade category. For each grade in array `grades`, lines 108–109 increment the appropriate element of the `frequency` array. To determine which element to increment, line 109 divides the current grade by 10 using integer division. For example, if grade is 85, line 109 increments `frequency[8]` to update the count of grades in the range 80–89. Lines 112–127 next print the bar chart (see Fig. 7.17) based on the values in array `frequency`. Like lines 26–27 of Fig. 7.9, lines 123–124 of Fig. 7.16 use a value in array `frequency` to determine the number of asterisks to display in each bar.

## *Testing Class GradeBook*

The program of Fig. 7.17 creates an object of class `GradeBook` (Figs. 7.15–7.16) using the `int` array `gradesArray` (declared and initialized in lines 9–10). The binary scope resolution operator (::) is used in the expression "`GradeBook::students`" (line 9) to access class `GradeBook`'s `static const` data member `students`. We use this constant here to create an array that is the same size as array `grades` stored as a data member in class `GradeBook`. Lines 12–13 pass a course name and `gradesArray` to the `GradeBook` constructor. Line 14 displays a welcome message, and line 15 invokes the `GradeBook` object's `processGrades` member function. The output reveals the summary of the 10 grades in `myGradeBook`.
