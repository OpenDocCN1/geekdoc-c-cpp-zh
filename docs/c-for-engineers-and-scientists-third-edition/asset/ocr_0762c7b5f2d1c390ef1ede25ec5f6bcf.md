# 278 Repetition Statements

# Program 5.17

```
#include <iostream>
using namespace std;

int main() {
    const int MAXI = 5;
    const int MAXJ = 4;
    int i, j;

    for(i = 1; i <= MAXI; i++) // start of outer loop
        cout << "\ni is now " << i << endl; // start of inner loop
        for(j = 1; j <= MAXJ; j++)
            cout << " j = " << j; // end of inner loop
    // end of outer loop
    cout << endl;
    return 0;
}
```

To understand the usefulness of a nested loop, take a look at using one to compute the average grade for each student in a class of 20 students. Each student has taken four exams during the semester. The final grade is calculated as the average of these exam grades. The pseudocode describing how to compute this average is as follows:

+   - for 20 times
- set the grade total to zero
- for 4 times
    - input a grade
    - add the grade to the total
    - endfor // end of inner loop
    - calculate student's average grade
    - print the student's average grade
- endfor // end of outer loop

As described by the pseudocode, an outer loop consisting of 20 passes is used to compute the average grade for each student. The inner loop consists of four passes, and one examination grade is entered in each loop pass. As each grade is entered, it's added to the total for the student, and at the end of the loop, the average is calculated and displayed. Because both the outer and inner loops are fixed-count loops of 20 and 4, respectively, for statements are used to create these loops. Program 5.18 shows the C++ code corresponding to the pseudocode.