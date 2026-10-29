
![](img/e9bf940282dfb289356f077151cc69dd_209_0.png)

![](img/e9bf940282dfb289356f077151cc69dd_210_0.png)

Figure 5.3 Accepting and adding a number to a total

![](img/e9bf940282dfb289356f077151cc69dd_210_1.png)

Figure 5.4 Accumulation flow of control

In reviewing Figure 5.4, observe that a provision has been made for initially setting the total to 0 before the while loop is entered. If you cleared the total inside the while loop, it would be set to 0 each time the loop was executed, and any value stored previously would be erased.

Program 5.6 incorporates the necessary modifications to Program 5.5 to total the numbers entered. As shown, the statement total = total + num; is placed immediately after the call to cin. Putting the accumulating statement at this point in the program ensures that the entered number is "captured" immediately into the total.

## Program 5.6

```
#include <iostream>
using namespace std;

int main()
{
const int MAXNUMS = 4;
int count;
double num, total;

cout << "\n\nThis program will ask you to enter "
<< MAXNUMS << " numbers.\n";
count = 1;
total = 0;

while (count <= MAXNUMS)
{
cout << "\nEnter a number: ";
cin >> num;
total = total + num;
cout << "The total is now " << total;
count++;
}

cout << "\n\nThe final total is " << total << endl;

return 0;
}
```

To make sure you understand, review Program 5.6. The variable total was created to store the total of the numbers entered. Before entering the while statement, the value of total is set to 0 to make sure any previous value in the storage location(s) assigned to this variable is erased. Inside the while loop, the statement total = total + num; is used to add the value of the entered number to total. As each value is entered, it's added to the existing total to create a new total. Therefore, total becomes a running subtotal of all the values

entered. Only after all numbers are entered does total contain the final sum of all the numbers. After the while loop is finished, a cout statement is used to display this sum.

Using the same data entered in the sample run for Program 5.5, the following sample run of Program 5.6 was made:

```
This program will ask you to enter 4 numbers.

Enter a number: 26.2
The total is now 26.2
Enter a number: 5
The total is now 31.2
Enter a number: 103.456
The total is now 134.656
Enter a number: 1267.89
The total is now 1402.546
```

The final total is 1402.546

Having used an accumulating assignment statement to add the numbers entered, you can go further and calculate the average of the numbers. Where do you calculate the average—inside the while loop or outside it? In the case at hand, calculating an average requires that both a final sum and the number of items in that sum be available. The average is then computed by dividing the final sum by the number of items. At this stage, you must ask, “At what point in the program is the correct sum available, and at what point is the number of items available?”

In reviewing Program 5.6, you can see that the correct sum needed for calculating the average is available after the while loop is finished. In fact, the whole purpose of the while loop is to ensure that the numbers are entered and added correctly to produce a correct sum. After the loop is finished, you also have a count of the number of items used in the sum. However, because of the way the while loop was constructed, the number in count (5) when the loop is finished is 1 more than the number of items (4) used to obtain the total. Knowing this, you simply subtract 1 from count before using it to determine the average. With this information as background, see whether you can read and understand Program 5.7.

![](img/e9bf940282dfb289356f077151cc69dd_212_0.png)

## Program 5.7

```
#include <iostream>
using namespace std;

int main()
{
const int MAXNUMS = 4;
int count;
double num, total, average;

cout << "\nThis program will ask you to enter " << MAXNUMS << " numbers.\n\n";
count = 1;
total = 0;

while (count <= MAXNUMS)
{
    cout << "Enter a number: ";
    cin >> num;
    total = total + num;
    count++;
}

count--;
average = total / count;
cout << "\nThe average of the numbers is " << average << endl;

return 0;
}
```

Program 5.7 is almost identical to Program 5.6, except for the calculation of the average. The constant display of the total inside and after the while loop has also been removed. The loop in Program 5.7 is used to enter and add four numbers. Immediately after the loop is exited, the average is computed and displayed. A sample run of Program 5.7 follows:

```
This program will ask you to enter 4 numbers.

Enter a number: 26.2
Enter a number: 5
Enter a number: 103.456
Enter a number: 1267.89

The average of the numbers is 350.637
```

## Sentinels

All the loops created so far have been examples of fixed-count loops, in which a counter is used to control the number of loop iterations. By means of a while statement, variable-condition loops can also be constructed. For example, when entering grades, you might not want to count the number of grades that will be entered. Instead, you prefer to enter grades continuously, and at the end, type a special data value to signal the end of data input.

In programming, data values used to signal the start or end of a data series are called sentinels. Sentinel values must, of course, be selected so as not to conflict with legitimate data values. For example, if you’re constructing a program to process a student’s grades, and assuming no extra credit is given that could produce a grade higher than 100, you could use any grade higher than 100 as a sentinel value. Program 5.8 illustrates this concept: Data is requested and accepted continuously until a number larger than 100 is entered. Entering a number higher than 100 alerts the program to exit the while loop and display the sum of the numbers entered.

## Program 5.8

```
#include <iostream>
using namespace std;

int main()
{
    const int HIGHGRADE = 100;
    double grade, total;

    grade = 0;
    total = 0;
    cout << "Info stop entering grades, type in any number";
    cout << "\n greater than 100.\n\n";
    cout << "Enter a grade: ";
    cin >> grade;

    while (grade <= HIGHGRADE)
    {
        total = total + grade;
        cout << "Enter a grade: ";
        cin >> grade;
    }

    cout << "\nThe total of the grades is " << total << endl;

    return 0;
}
```

## Point of Information

## Loop Types

A loop that evaluates a condition before any statements in the loop are executed is referred to as a pretest loop or an entrance-controlled loop. In C++, these loops are created by using while or for statements.

A loop that evaluates a condition at the end of the repeating section of code is referred to as a posttest loop or an exit-controlled loop. These loops always execute the loop statements at least once before the condition is tested. The do-while statement is used to construct this type of loop.

In addition to where the condition is tested (pretest or posttest), repeating sections of code are classified by the type of condition being tested. In a fixed-count loop, the condition is used to keep track of how many repetitions have occurred. In this type of loop, a fixed number of calculations are performed or a fixed number of lines are printed, at which point the repeating section of code is exited. All of C++'s repetition statements can be used to create fixed-count loops.

In a variable-condition loop, the tested condition doesn't depend on a count being reached, but on a variable that can change interactively with each pass through the loop. When a specified value is encountered, regardless of how many iterations have occurred, repetitions stop. All of C++'s repetition statements can be used to create variable-condition loops.

The following lines show a sample run of Program 5.8. As long as grades less than or equal to 100 are entered, the program continues to request and accept additional data. When a number less than or equal to 100 is entered, the program adds this number to the total. When a number greater than 100 is entered, the loop is exited, and the sum of the grades that were entered is displayed.

```
To stop entering grades, type in any number greater than 100.

Enter a grade: 95
Enter a grade: 100
Enter a grade: 82
Enter a grade: 101

The total of the grades is 277
```
