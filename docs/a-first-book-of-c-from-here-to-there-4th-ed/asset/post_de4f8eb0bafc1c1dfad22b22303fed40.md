
```
for (num = 1; num <= MAXNUMS; num++)
    cout << setw(3) << num << " "
         << setw(3) << num * num << " "
         << setw(4) << num * num * num << endl;

return 0;
}
```

When Program 5.10 is run, this is the display produced:

| NUMBER | SQUARE | CUBE |
|---:|---:|---:|
| 1 | 1 | 1 |
| 2 | 4 | 8 |
| 3 | 9 | 27 |
| 4 | 16 | 64 |
| 5 | 25 | 125 |
| 6 | 36 | 216 |
| 7 | 49 | 343 |
| 8 | 64 | 512 |
| 9 | 81 | 729 |
| 10 | 100 | 1000 |

Simply changing the number 10 in the for statement of Program 5.10 to 1000 creates a loop that’s executed 1000 times and produces a table of numbers from 1 to 100. As with the while statement, this small change produces an immense increase in the program’s processing and output. Notice also that the expression num++ was used in the altering list in place of the equivalent num = num + 1.

## Interactive for Loops

Using the cin object inside a for loop creates an interactive for loop, much like using this object in a while loop. For example, in Program 5.11, a cin object is used to input a set of numbers. As each number is input, it’s added to a total. When the for loop is exited, the average is calculated and displayed.

## Program 5.11

```
#include <iostream>
using namespace std;

// This program calculates the average
// of MAXCOUNT user-entered numbers
int main()
{
const int MAXCOUNT = 5;
int count;
double num, total, average;

total = 0.0;

for (count = 0; count < MAXCOUNT; count++)
{
    cout << "Enter a number: ";
    cin >> num;
    total = total + num;
}

average = total / count;
cout << "The average of the data entered is " << average
    << endl;

return 0;
}
```

The for statement in Program 5.11 creates a loop that’s executed five times. The user is prompted to enter a number each time through the loop. After each number is entered, it’s added to the total immediately. Although total was initialized to 0 before the for statement, this initialization could have been included with the initialization of count, as follows:

```
for (total = 0.0, count = 0; count < MAXCOUNT; count++)
```

Additionally, the declarations for both total and count could have been included with their initializations inside the initializing list, as follows:

```
for (double total = 0.0, int count = 0; count < MAXCOUNT; count++)
```

Any of these for constructs is considered a good programming practice. Which one you choose is simply a matter of your own programming style.

## Nested Loops

In many situations, using a loop within another loop, called a nested loop, is convenient. Here’s a simple example of a nested loop:

```
for(i = 1; i <= 5; i++) // start of outer loop <----+
{
    cout << "\n i is now " << i << endl; //
    //
    for(j = 1; j <= 4; j++) // start of inner loop |
    cout << "  j = " << j; // end of inner loop |
} // end of outer loop <----+
```

```
for(i = 1; i <= 5; i++)    // start of outer loop <----+
{                         //
    cout << "\n i is now " << i << endl;  //
                          //
    for(j = 1;  j <= 4; j++)// start of inner loop   |
        cout << "  j = " << j; // end of inner loop     |
}                         // end of outer loop     <----+

return 0;
}
```

This is the output of a sample run of Program 5.12:

```
i is now 1
    j = 1  j = 2  j = 3  j = 4
i is now 2
    j = 1  j = 2  j = 3  j = 4
i is now 3
    j = 1  j = 2  j = 3  j = 4
i is now 4
    j = 1  j = 2  j = 3  j = 4
i is now 5
    j = 1  j = 2  j = 3  j = 4
```

To understand the usefulness of a nested loop, take a look at using one to compute the average grade for each student in a class of 20 students. Each student has taken four exams during the semester. The final grade is calculated as the average of these exam grades. An outer loop consisting of 20 passes is used to compute the average grade for each student. The inner loop consists of four passes, and one exam grade is entered in each inner loop pass. As each grade is entered, it's added to the total for the student, and at the end of the loop, the average is calculated and displayed. Because both the outer and inner loops are fixed-count loops of 20 and 4, respectively, for statements are used to create these loops. Program 5.13 uses a nested loop to make the required calculations.

## Program 5.13

```
#include <iostream>
using namespace std;

int main()
{
    const int NUMGRADES = 4;
    const int NUMSTUDENTS = 20;
    int i,j;
    double grade, total, average;

for (i = 1; i <= NUMSTUDENTS; i++)  // start of outer loop
{
    total = 0;                  // clear the total for this student
    for (j = 1; j <= NUMGRADES; j++)  // start of inner loop
    {
        cout << "Enter an examination grade for student: "
            << j << ":";
        cin >> grade;
        total = total + grade;      // add the grade to the total
    }                           // end of the inner for loop
    average = total / NUMGRADES;    // calculate the average
    cout << "\nThe average for student " << i
        << " is " << average << "\n\n";
}                               // end of the outer for loop

return 0;
}
```

In reviewing Program 5.13, pay particular attention to the initialization of total in the outer loop, before the inner loop is entered: total is initialized 20 times, once for each student. Also, notice that the average is calculated and displayed immediately after the inner loop is finished. Because the statements that compute and print the average are also in the outer loop, 20 averages are calculated and displayed. The entry and addition of each grade in the inner loop uses techniques you have seen before and should be familiar with now.

## EXERCISES 5.3

- 1. (Practice) Write a for statement for each of the following cases:
  - a. Use a counter named i that has an initial value of 1, a final value of 20, and an increment of 1.
  - b. Use a counter named icount that has an initial value of 1, a final value of 20, and an increment of 2.
  - c. Use a counter named j that has an initial value of 1, a final value of 100, and an increment of 5.
  - d. Use a counter named icount that has an initial value of 20, a final value of 1, and an increment of -1.
  - e. Use a counter named icount that has an initial value of 20, a final value of 1, and an increment of -2.
  - f. Use a counter named count that has an initial value of 1.0, a final value of 16.2, and an increment of 0.2.
  - g. Use a counter named xent that has an initial value of 20.0, a final value of 10.0, and an increment of -0.5.

## 2. (Desk check) Determine the number of times each for loop is executed for the for statements written in Exercise 1.

## 3. (Desk check) Determine the value in total after each of the following loops is executed:

- a. total = 0;
  for (i = 1; i <= 10; i = i + 1)
      total = total + i;

- b. total = 1;
  for (count = 1; count <= 10; count = count + 1)
      total = total * 2;

- c. total = 0;
  for (i = 10; i <= 15; i = i + 1)
      total = total + i;

- d. total = 50;
  for (i = 1; i <=10; i = i + 1)
      total = total - i;

- e. total = 1;
  for (icnt = 1; icnt <= 8; ++icnt)
      total = total * icnt;

- f. total = 1.0;
  for (j = 1; j <= 5; ++j)
      total = total / 2.0;

## 4. (Desk check) Determine the output of the following program:

```
#include <iostream>
using namespace std;

int main()
{
    int i;

    for (i = 20; i >= 0; i -= 4)
        cout << i;

    return 0;
}
```

## 5. (Modify) Modify Program 5.10 to produce a table of the numbers 0 through 20 in increments of 2, with their squares and cubes.

## 6. (Modify) Modify Program 5.10 to produce a table of numbers from 10 to 1, instead of 1 to 10, as it currently does.

## 7. (Program) a. Write, compile, and run a C++ program that displays a table of 20 temperature conversions from Fahrenheit to Celsius. The table should start with a Fahrenheit value of 20 degrees and be incremented in values of 4 degrees. Recall that Celsius = (5.0/9.0) × (Fahrenheit - 32.0).

- b. Modify the program written for Exercise 7a to request the number of conversions to be made.
