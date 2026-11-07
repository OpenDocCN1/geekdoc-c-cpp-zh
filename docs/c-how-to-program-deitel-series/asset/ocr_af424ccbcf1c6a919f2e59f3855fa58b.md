```
```cpp
// function main begins program execution
int main()
{
   // two-dimensional array of student grades
   array<array<int, GradeBook::tests>, GradeBook::students> grades =
      { { 87, 96, 70,
          68, 87, 90,
          94, 100, 90,
          100, 81, 82,
          83, 65, 85,
          78, 87, 65,
          85, 75, 83,
          91, 94, 100,
          76, 72, 84,
          87, 93, 73 } };

   GradeBook myGradeBook(
      "CS101 Introduction to C++ Programming", grades );
   myGradeBook.displayMessage();
   myGradeBook.processGrades();
} // end main
```
```

**Fig. 7.24** | Creates a GradeBook object using a two-dimensional array of grades, then invokes member function processGrades to analyze them. (Part 2 of 2.)

# 7.10 Introduction to C++ Standard Library Class Template vector

We now introduce C++ Standard Library class template **vector**, which is similar to class template array, but also supports dynamic resizing. Except for the features that modify a vector, the other features shown in Fig. 7.25 also work for arrays. Standard class template vector is defined in header <vector> (line 5) and belongs to namespace std. Chapter 15 discusses the full functionality of vector. At the end of this section, we’ll demonstrate class vector’s bounds checking capabilities and introduce C++’s exception-handling mechanism, which can be used to detect and handle an out-of-bounds vector index.

```
```cpp
// Fig. 7.25: fig07_25.cpp
// Demonstrating C++ Standard Library class template vector.
#include <iostream>
#include <iomanip>
#include <vector>
#include <stdexcept>
using namespace std;

void outputVector( const vector< int > & ); // display the vector
void inputVector( vector< int > & ); // input values into the vector

int main()
```
```

**Fig. 7.25** | Demonstrating C++ Standard Library class template vector. (Part 1 of 4.)