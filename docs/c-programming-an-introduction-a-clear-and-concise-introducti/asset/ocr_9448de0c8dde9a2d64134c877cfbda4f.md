```
```cpp
#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int grade1, grade2, grade3, grade4, grade5,
        sumOfGrades, numOfGrades;
    double average = 0.0;
    grade1 = 84;
    grade2 = 89;
    grade3 = 77;
    grade4 = 94;
    grade5 = 88;
    numOfGrades = 5;
    sumOfGrades = grade1 + grade2 + grade3 + grade4
                + grade5;
    average = sumOfGrades / numOfGrades;
    cout << "The average is: " << average << endl;
    Console::ReadKey();
    return 0;
}
```
```

Let's examine this program line-by-line. The first line:

```
```cpp
int grade1, grade2, grade3, grade4, grade5,
    sumOfGrades, numOfGrades;
```
```

initializes the integer variables we need for this program, 5 variables for the grades, a variable to store the sum of the grades and a variable to store the number of grades, which we'll need to compute the average.

The next line:

```
```cpp
double average = 0.0;
```
```

declares and initializes the variable we'll use to store the average. The average will probably be a floating-point value so we need to use a floating-point data type.

These lines assign values to the grade variables and the variable storing the number of grades: