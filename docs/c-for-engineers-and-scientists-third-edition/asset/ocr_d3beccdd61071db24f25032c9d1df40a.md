# Chapter 5 279

# Program 5.18

```
#include <iostream>
using namespace std;

int main()
{
    const int NUMGRADES = 4;
    const int NUMSTUDENTS = 20;
    int i, j;
    double grade, total;

    for (i = 1; i <= NUMSTUDENTS; i++) // start of outer loop
    {
        total = 0; // clear the total for this student
        for (j = 1; j <= NUMSTUDENTS; j++) // start of inner loop
        {
            cout << "Enter an examination grade for student: ";
            cin >> grade;
            total = total + grade; // add the grade to the total
        } // end of the inner loop
        average = total / NUMGRADES; // calculate the average
        cout << "\nThe average for student " << i
             << " is " << average << "\n"
             // end of the outer loop
    } // end of the outer loop

    return 0;
}
```

In reviewing Program 5.18, pay particular attention to the initialization of total in the outer loop, before the inner loop is entered: total is initialized 20 times, once for each student. Also, notice that the average is calculated and displayed immediately after the inner loop is finished. Because the statements that compute and display the average are also in the outer loop, 20 averages are calculated and displayed. The entry and addition of each grade in the inner loop uses techniques you have seen before and should be familiar with now.

# EXERCISES 5.6

+   1. (Mise. Application) Four experiments are performed, and each experiment has six results. The results for each experiment are given in the following list. Write a program using a nested loop to compute and display the average of the test results for each experiment.