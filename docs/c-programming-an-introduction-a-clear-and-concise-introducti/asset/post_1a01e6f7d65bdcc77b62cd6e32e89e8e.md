
```cpp
int temps[2][7] = {{87, 85, 89, 92, 94, 88, 90},
                   {79, 86, 85, 88, 93, 91}};
```

### Initializing a Two-Dimensional Array

To initialize a two-dimensional array, you have to write a nested for loop that traverses both the rows and the columns. Here is an example:

```cpp
const int rows = 2;
const int cols = 3;
int numbers[rows][cols];
    for(int r = 0; r < rows; ++r)
        for(int c = 0; c < cols; ++c)
            numbers[r][c] = 0;
```

In the code fragment above, the outer for loop is controlling the rows and the inner for loop is controlling the columns. So, the code starts with row 0 and populates columns 0, 1, and 2 with the value 0 and then moves to row 1, populating columns 0, 1, and 2 with the value 0 also.

### Displaying Two-Dimensional Array Elements

We can display the contents of the two-dimensional array above using the same nested for loop technique we used to initialize it. Here is our first try at it:

```cpp
for(int r = 0; r < rows; ++r)
    for (int c = 0; c < cols; ++c)
        cout << numbers[r][c] << " ";
```

The output from this code fragment is:

```text
0 0 0 0 0 0
```

This is the contents of the array but we'd like to see it in row/column order. To do this, we need to write a newline character after the first row. We can modify our code fragment to accommodate this by adding a cout statement after the outer for loop. Here is the new fragment:

```cpp
for(int r = 0; r < rows; ++r) {
    for (int c = 0; c < cols; ++c)
        cout << numbers[r][c] << " ";
    cout << endl;
}
```

Notice that we had to put the inner for loop inside a block since the body of the outer for loop now consists of two statements, the for loop and the cout statement.

The output from this code fragment is:

```text
0 0 0
0 0 0
```

### A Two-Dimensional Array Example

The following program demonstrates how a two-dimensional array can be used to compute individual student averages from a two-dimensional array storing the grades for five students. Let's look at the code before we discuss how it works:

```cpp
// Array2D.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    const int rows = 5;
    const int cols = 5;
    int total = 0;
    double average = 0.0;
    int grades[rows][cols] = {{75, 82, 84, 79, 91},
                              {85, 81, 94, 96, 89},
                              {92, 91, 94, 89, 90},
                              {74, 72, 81, 78, 80},
                              {84, 82, 82, 83, 81}};

    for(int r = 0; r < rows; ++r) {
        cout << "Student " << r+1 << ": ";
        for(int c = 0; c < cols; ++c) {
            cout << grades[r][c] << " ";
            total += grades[r][c];
        }
        average = total / cols;
        cout << "Average: " << average << endl;
        total = 0;
        average = 0.0;
    }
    Console::ReadKey();
    return 0;
}
```

The output from this program is:

```text
Student 1: 75 82 84 79 91 Average: 82
Student 2: 85 81 94 96 89 Average: 89
Student 3: 92 91 94 89 90 Average: 91
Student 4: 74 72 81 78 80 Average: 77
Student 5: 84 82 82 83 81 Average: 82
```

The two variables, total and average, are declared and initialized outside the nested for loops. Then we enter the outer loop, which places us in the first row of the grades (Student 1). As the inner loop moves from column to column, each grade is accessed, displayed, and added to the total. When the loop reaches the last column, control is transferred to the outer loop, where the average is computed and displayed. Finally, before beginning a new iteration of the outer loop and moving to the next student, the variables total and average are reset to 0. Not doing this would lead to the next total and average being miscalculated.

### Performing Column-Order Computation

Not every task involving a two-dimensional array involves processing the rows in the outer loop (this is called *row-order*). There are times when you want to process a two-dimensional array in column-order instead. One example of a column-order computation using the grades example above is if we want to compute the average for each test. To do this, we want to add together all the tests in the first column and then compute the average, followed by the tests in the second column, and so on. To do this, all we have to do is have the outer loop process the columns and the inner loop process the rows. The rest of the program looks just like it did when we were averaging the student's test grades.

Here is the program above modified to compute test averages also:

```cpp
// Array2D.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    const int rows = 5;
    const int cols = 5;
    int total = 0;
    double average = 0.0;
    int grades[rows][cols] = {{75, 82, 84, 79, 91},
                              {85, 81, 94, 96, 89},
                              {92, 91, 94, 89, 90},
                              {74, 72, 81, 78, 80},
                              {84, 82, 82, 83, 81}};
    for(int r = 0; r < rows; ++r) {
        cout << "Student " << r+1 << ": ";
        for(int c = 0; c < cols; c++) {
            cout << grades[r][c] << " ";
            total += grades[r][c];
        }
        average = total / cols;
        cout << "Average: " << average << endl;
        total = 0;
        average = 0.0;
    }
    cout << endl << "Test Averages: " << endl;
    total = 0;
    average = 0.0;
    for(int c = 0; c < cols; ++c) {
        cout << "Test " << c+1 << ": ";
        for(int r = 0; r < rows; ++r) {
            cout << grades[r][c] << " ";
            total += grades[r][c];
        }
        average = total / rows;
        cout << "Average: " << average << endl;
        total = 0;
        average = 0.0;
    }
    Console::ReadKey();
    return 0;
}
```

The output from the column-order portion of this program is:

```text
Test Averages:
Test 1: 75 85 92 74 84 Average: 82
Test 2: 82 81 91 72 82 Average: 81
Test 3: 84 94 94 81 82 Average: 87
Test 4: 79 96 89 78 83 Average: 85
Test 5: 91 89 90 80 81 Average: 86
```

### Exercises

- 1. Write a program that reads 10 words from a file, stores them in an array, and displays a histogram of the length of the words.
- 2. Write a program that stores a series of characters in an array. Determine if the characters make a palindrome, which is a word that is spelled the same forwards and backwards. For example, racecar and bob are palindromes.
- 3. Write a program that stores 10 random grades in an array. Display all the grades that are greater than 80.
- 4. Write a program that stores the months of the year in an array, prompts the user to enter a month number, and then displays the month that corresponds to that number. For example, 1-January, 2-February, 3-March, etc.
- 5. The table below lists the number of students enrolled in certain courses at different campuses. Write a program that places this data into a two-dimensional array and displays the total number of students enrolled at courses at each campus and displays the total number of students taking each course.

  |  | Course 1 | Course 2 | Course 3 |
  |---|---|---:|---:|---:|
  | Campus 1 | 23 | 34 | 15 |
  | Campus 2 | 12 | 21 | 19 |
  | Campus 3 | 14 | 19 | 23 |

## Chapter 11

### Classes and Object-Oriented Programming

The programs we write in C++ are simulations of our interactions with objects that exist in our world. A payroll program, for example, simulates how the company works and pays its employees for the work they do. Each of the pieces of a payroll program represent an object. For example, an employee has a time sheet, or time card, that stores the number of hours he or she works in a pay period. An employee also has a salary or hourly wage which represents the rate at which they get paid.

In object-oriented programming, we write programs that create objects that mirror the objects we are trying to simulate. In C++, an object is defined by a class. A class includes both a definition of an object's properties or attributes, and a description of the object's behaviors. For example, when describing an automobile, we describe what the automobile looks like and how it behaves or performs. We can do the same thing in C++ by creating and using classes and objects.

Besides defining attributes and behaviors of objects, classes also define how objects interact with each other. Generally, objects interact by sending messages to each other. Using the automobile analogy again, if a Person object wants an Automobile object to go, the Person sends the Automobile a “step on the gas pedal” message. The ability to send and receive messages is defined as part of an object's behaviors.

Another distinctive feature of classes is the ability to show or hide the attributes and behaviors that make up the class. Any attribute or behavior can be exposed to other objects or they can be hidden so that no other object has access to the attribute or behavior. This feature is called encapsulation and is one of the reasons object-oriented programming has proven to be so successful.

In practice, you can consider a class to be a user-defined type. Being able to extend the types a programming language can work with is a crucial feature of a programming language.
