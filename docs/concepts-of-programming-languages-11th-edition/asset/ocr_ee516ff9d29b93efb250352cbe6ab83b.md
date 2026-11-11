# 14.2.5  An Example

The following example program illustrates some simple uses of exception handlers in C++. The program computes and prints a distribution of input grades by using an array of counters. The input is a sequence of grades, terminated by a negative number. The negative number raises a NegativeInputException exception because the grades must be non-negative integers. There are 10 categories of grades (0 – 9, 10 – 19, ..., 90 – 100). The grades themselves are used to compute indexes into an array of counters, one for each grade category. Invalid input grades are detected by trapping indexing errors in the counter array. A grade of 100 is special in the computation of the grade distribution because the categories all have 10 possible grade values, except the highest, which has 11 (90, 91, ..., 100). (The fact that there are more possible A grades than B’s or C’s is conclusive evidence of the generosity of teachers.) The grade of 100 is also handled in the same exception handler that is used for invalid input data.

It produces a distribution of input grades by using an array of counters for 10 categories. Illegal grades are detected by checking for invalid subscripts used in incrementing the selected counter.

```
```cpp
// Grade Distribution
// Input: A list of integer values that represent
//         grades, followed by a negative number
// Output: A distribution of grades, as a percentage for
//         each of the categories 0-9, 10-19, ..., 
//         90-100.
#include <iostream>
int main() {  // Any exception can be raised
    int new_grade,
        index,
        limit_1,
        limit_2,
        freq[10] = {0,0,0,0,0,0,0,0,0,0};
    // The exception definition to deal with the end of data
    class NegativeInputException {
      public:
        NegativeInputException() {  // Constructor
          cout << "End of input data reached" << endl;
        } // /** end of constructor
    }; // /** end of NegativeInputException class
    try {
      while (true) {
        cout << "Please input a grade" << endl;
        if ((cin >> new_grade) < 0)  // End of data
          throw NegativeInputException();
        index = new_grade / 10;
        try {
          if (index > 9)
            throw new_grade;
```
```