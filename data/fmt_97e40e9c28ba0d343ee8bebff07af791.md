
图 7.15 | 将 `const` 类型限定符应用于数组参数。（第 2 部分，共 2 部分。）

## 7.6 案例研究：使用数组存储成绩的 GradeBook 类

本节将进一步演化第 3 章引入并在第 4–6 章扩展的 `GradeBook` 类。回想一下，该类表示教授用来存储和分析学生成绩的成绩册。该类以前的版本处理用户输入的成绩，但不会在类的数据成员中保留各个成绩值。因此，重复计算需要用户重新输入成绩。解决此问题的一种方法是将输入的每个成绩存储在类的单独数据成员中。例如，我们可以在 `GradeBook` 类中创建数据成员 `grade1`、`grade2`、…、`grade10` 来存储 10 个学生的成绩。但是，对成绩求和并计算班级平均分的代码会十分繁琐。在本节中，我们通过将成绩存储在数组中来解决这个问题。

### 在 GradeBook 类中使用数组存储学生成绩

这里展示的 `GradeBook` 类版本（图 7.16–7.17）使用整数数组来存储若干学生一次考试的成绩。这就不必重复输入同一组成绩。数组 `grades` 在图 7.16 的第 29 行被声明为数据成员——因此，每个 `GradeBook` 对象都维护自己的一组成绩。

```
1 // Fig. 7.16: GradeBook.h
2 // Definition of class GradeBook that uses an array to store test grades.
3 // Member functions are defined in GradeBook.cpp
4
5 #include <string> // program uses C++ Standard Library string class
6 using std::string;
7
8 // GradeBook class definition
9 class GradeBook
10 {
11 public:
12     // constant -- number of students who took the test
13     const static int students = 10; // note public data
```

图 7.16 | 使用数组存储考试成绩的 `GradeBook` 类定义。（第 1 部分，共 2 部分。）

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

**图 7.16** | 使用数组存储考试成绩的 `GradeBook` 类定义。 （第 2 部分，共 2 部分。）

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

**图 7.17** | 操作成绩数组的 `GradeBook` 类成员函数。 （第 1 部分，共 4 部分。）

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
