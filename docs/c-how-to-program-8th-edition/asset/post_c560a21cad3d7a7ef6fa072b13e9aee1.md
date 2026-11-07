
```cpp
135    // print bar of asterisks
136    for ( int stars = 0; stars < frequency[ count ]; ++stars )
137       cout << '*';
138
139       cout << endl; // start a new line of output
140    } // end outer for
141 } // end function outputBarChart
142
143 // output the contents of the grades array
144 void GradeBook::outputGrades()
145 {
146    cout << "\nThe grades are:\n\n";
147    cout << setw( 8 ) << " "; // align column heads
148
149    // create a column heading for each of the tests
150    for ( int test = 0; test < tests; ++test )
151       cout << "Test " << test + 1 << "   ";
152
153    cout << "Average" << endl; // student average column heading
154
155    // create rows/columns of text representing array grades
156    for ( int student = 0; student < students; ++student )
157    {
158       cout << "Student " << setw( 2 ) << student + 1;
159
160       // output student's grades
161       for ( int test = 0; test < tests; ++test )
162          cout << setw( 8 ) << grades[ student ][ test ];
163
164       // call member function getAverage to calculate student's average;
165       // pass row of grades and the value of tests as the arguments
166       double average = getAverage( grades[ student ], tests );
167       cout << setw( 9 ) << setprecision( 2 ) << fixed << average << endl;
168    } // end outer for
169 } // end function outputGrades
```

**Fig. 7.23** Member-function definitions for class GradeBook that uses a two-dimensional array to store grades. (Part 4 of 4.)

Five member functions (declared in lines 23–27 of Fig. 7.22) perform array manipulations to process the grades. Each of these member functions is similar to its counterpart in the earlier one-dimensional array version of class GradeBook (Figs. 7.15–7.16). Member function getMinimum (defined in lines 57–74 of Fig. 7.23) determines the lowest grade of all students for the semester. Member function getMaximum (defined in lines 77–94 of Fig. 7.23) determines the highest grade of all students for the semester. Member function getAverage (lines 97–107 of Fig. 7.23) determines a particular student’s semester average. Member function outputBarChart (lines 110–141 of Fig. 7.23) outputs a bar chart of the distribution of all student grades for the semester. Member function outputGrades (lines 144–169 of Fig. 7.23) outputs the two-dimensional array in a tabular format, along with each student’s semester average.

Member functions getMinimum, getMaximum, outputBarChart and outputGrades each loop through array grades by using nested for statements. For example, consider the

```cpp
// Fig. 7.24: fig07_24.cpp
// Creates GradeBook object using a two-dimensional array of grades.

#include "GradeBook.h" // GradeBook class definition

// function main begins program execution
int main()
{
   // initialize two-dimensional array of student grades
   int gradesArray[ GradeBook::students ][ GradeBook::tests ] =
      { { 87, 96, 70 },
        { 68, 87, 90 },
        { 94, 100, 90 },
        { 100, 81, 82 },
        { 83, 65, 85 },
        { 78, 87, 65 },
        { 85, 75, 83 },
        { 91, 94, 100 },
        { 76, 72, 84 },
        { 87, 93, 73 } };

   GradeBook myGradeBook(
      "CS101 Introduction to C++ Programming", gradesArray );
   myGradeBook.displayMessage();
   myGradeBook.processGrades();
} // end main
```

![](img/bfd978e7e9b192bab46ec2a89e481263_339_0.png)

**Fig. 7.24** | Creates a GradeBook object using a two-dimensional array of grades, then invokes member function `processGrades` to analyze them. *(Part 1 of 2.)*

```
40–49:
50–59:
60–69: ***
70–79: *******
80–89: ***********
90–99: ***************
100: ***
```

**Fig. 7.24** | Creates a GradeBook object using a two-dimensional array of grades, then invokes member function processGrades to analyze them. (Part 2 of 2.)

## 7.11 Introduction to C++ Standard Library Class Template vector

We now introduce C++ Standard Library class template vector, which represents a more robust type of array featuring many additional capabilities. As you’ll see in later chapters, C-style pointer-based arrays (i.e., the type of arrays represented thus far) have great potential for errors. For example, as mentioned earlier, a program can easily “walk off” either end of an array, because C++ does not check whether subscripts fall outside the range of an array. Two arrays cannot be meaningfully compared with equality operators or relational operators. As you’ll learn in Chapter 8, pointer variables (known more commonly as pointers) contain memory addresses as their values. Array names are simply pointers to where the arrays begin in memory, and, of course, two arrays will always be at different memory locations. When an array is passed to a general-purpose function designed to handle arrays of any size, the size of the array must be passed as an additional argument. Furthermore, one array cannot be assigned to another with the assignment operator(s)—array names are const pointers, and, as you’ll learn in Chapter 8, a constant pointer cannot be used on the left side of an assignment operator. These and other capabilities certainly seem like “naturals” for dealing with arrays, but C++ does not provide such capabilities. However, the C++ Standard Library provides class template vector to allow you to create a more powerful and less error-prone alternative to arrays. In Chapter 11, we present the means to implement such array capabilities as those provided by vector. You’ll learn how to customize operators for use with your own classes (a technique known as operator overloading).

The vector class template is available to anyone building applications with C++. The notations that the vector example uses might be unfamiliar to you, because vector uses template notation. Recall that Section 6.18 discussed function templates. In Chapter 14, we discuss class templates. For now, you should feel comfortable using class template vector by mimicking the syntax in the example we show in this section. You’ll deepen your understanding as we study class templates in Chapter 14. Chapter 22 presents class template vector (and several other standard C++ container classes) in detail.

The program of Fig. 7.25 demonstrates capabilities provided by C++ Standard Library class template vector that are not available for C-style pointer-based arrays. Standard class template vector provides many of the same features as the Array class that we construct in Chapter 11. Standard class template vector is defined in header <vector> (line 5) and belongs to namespace std. Chapter 22 discusses the full functionality of vector. At the end of this section, we’ll demonstrate class vector’s bounds checking capabilities and introduce C++’s exception-handling mechanism, which can be used to detect and handle an out-of-bounds vector index.

```cpp
// Fig. 7.25: fig07_25.cpp
// Demonstrating C++ Standard Library class template vector.
#include <iostream>
#include <iomanip>
#include <vector>
using namespace std;

void outputVector( const vector< int > & ); // display the vector
void inputVector( vector< int > & ); // input values into the vector

int main()
{
   vector< int > integers1( 7 ); // 7-element vector< int >
   vector< int > integers2( 10 ); // 10-element vector< int >

   // print integers1 size and contents
   cout << "Size of vector integers1 is " << integers1.size()
        << "\nVector after initialization:" << endl;
   outputVector( integers1 );

   // print integers2 size and contents
   cout << "\nSize of vector integers2 is " << integers2.size()
        << "\nVector after initialization:" << endl;
   outputVector( integers2 );

   // input and print integers1 and integers2
   cout << "\nEnter 17 integers:" << endl;
   inputVector( integers1 );
   inputVector( integers2 );

   cout << "\nAfter input, the vectors contain:\n"
        << "integers1: " << endl;
   outputVector( integers1 );
   cout << "integers2: " << endl;
   outputVector( integers2 );

   // use inequality (!=) operator with vector objects
   cout << "\nEvaluating: integers1 != integers2" << endl;

   if ( integers1 != integers2 )
      cout << "integers1 and integers2 are not equal" << endl;

   // create vector integers3 using integers1 as an
   // initializer; print size and contents
   vector< int > integers3( integers1 ); // copy constructor

   cout << "\nSize of vector integers3 is " << integers3.size()
        << "\nVector after initialization:" << endl;
   outputVector( integers3 );
```

**Fig. 7.25** | Demonstrating C++ Standard Library class template vector. (Part 1 of 4.)
