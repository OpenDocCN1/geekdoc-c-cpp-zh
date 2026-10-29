
## Repetition

```cpp
cout << "\nThis program will ask you to enter "
     << MAXNUMS << " numbers.\n";
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
cout << "\nThe average of the numbers is "
     << average << endl;

return 0;
}
```

Program 5.7 is almost identical to Program 5.6, except for the calculation of the average. The constant display of the total inside and after the while loop has also been removed. The loop in Program 5.7 is used to enter and add four numbers. Immediately after the loop is exited, the average is computed and displayed. A sample run of Program 5.7 follows:

```text
This program will ask you to enter 4 numbers.

Enter a number: 26.2
Enter a number: 5
Enter a number: 103.456
Enter a number: 1267.89

The average of the numbers is 350.637
```

## Sentinels

All the loops created so far have been examples of fixed-count loops, in which a counter is used to control the number of loop iterations. By means of a while statement, variable-condition loops can also be constructed. For example, when entering grades, you might not want to count the number of grades that will be entered. Instead, you prefer to enter grades continuously, and at the end, type a special data value to signal the end of data input.

In programming, data values used to signal the start or end of a data series are called sentinels. Sentinel values must, of course, be selected so as not to conflict with legitimate data values. For example, if you're constructing a program to process a student's grades, and assuming no extra credit is given that could produce a grade higher than 100, you could use any grade higher than 100 as a sentinel value. Program 5.8 illustrates this concept: Data is requested and accepted continuously until a number larger than 100 is entered. Entering a number higher than 100 alerts the program to exit the while loop and display the sum of the numbers entered.

### Program 5.8

![](img/202cface8244f523c2641baa2e00d7dd_214_0.png)

```cpp
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

### Point of Information

#### Loop Types

A loop that evaluates a condition before any statements in the loop are executed is referred to as a pretest loop or an entrance-controlled loop. In C++, these loops are created by using while or for statements.

A loop that evaluates a condition at the end of the repeating section of code is referred to as a posttest loop or an exit-controlled loop. These loops always execute the loop statements at least once before the condition is tested. The do-while statement is used to construct this type of loop.

In addition to where the condition is tested (pretest or posttest), repeating sections of code are classified by the type of condition being tested. In a fixed-count loop, the condition is used to keep track of how many repetitions have occurred. In this type of loop, a fixed number of calculations are performed or a fixed number of lines are printed, at which point the repeating section of code is exited. All of C++'s repetition statements can be used to create fixed-count loops.

In a variable-condition loop, the tested condition doesn't depend on a count being reached, but on a variable that can change interactively with each pass through the loop. When a specified value is encountered, regardless of how many iterations have occurred, repetitions stop. All of C++'s repetition statements can be used to create variable-condition loops.

The following lines show a sample run of Program 5.8. As long as grades less than or equal to 100 are entered, the program continues to request and accept additional data. When a number less than or equal to 100 is entered, the program adds this number to the total. When a number greater than 100 is entered, the loop is exited, and the sum of the grades that were entered is displayed.

```text
To stop entering grades, type in any number greater than 100.

Enter a grade: 95
Enter a grade: 100
Enter a grade: 82
Enter a grade: 101

The total of the grades is 277
```

## break and continue Statements

Two useful statements in connection with repetition statements are the break and continue statements. You encountered the break statement in Section 4.4 when learning about the switch statement. This is the format of the break statement:

```cpp
break;
```

A break statement, as its name implies, forces an immediate break, or exit, from the switch, while, for, and do-while statements (discussed in the next sections). For example, execution of the following while loop is terminated immediately if a number greater than 76 is entered:

```cpp
while(count <= 10)
{
    cout << "Enter a number: ";
    cin >> num;
    if (num > 76)
    {
        cout << "You lose!\n";
        break;      // break out of the loop
    }
    else
        cout << "Way to go!\n";
        count++;
}
// break jumps to here
```

The break statement violates structured programming principles because it provides a second, nonstandard exit from a loop. Nevertheless, the break statement is extremely useful for breaking out of loops when an unusual condition is detected. It's also used to exit from a switch statement, but it's because the matching case value has been detected and processed.

The continue statement is similar to the break statement but applies only to loops created with while, do-while, and for statements. This is the general format of a continue statement:

```cpp
continue;
```

When continue is encountered in a loop, the next iteration of the loop begins immediately. For while loops, this means execution is transferred automatically to the top of the loop, and reevaluation of the tested expression is initiated. Although the continue statement has no direct effect on a switch statement, it can be included in a switch statement, which is also contained in a loop. The effect of continue is the same: The next loop iteration begins.

As a general rule, the continue statement is less useful than the break statement, but it's convenient for skipping over data that shouldn't be processed while remaining in a loop. For example, invalid grades are simply ignored in the following section of code, and only valid grades are added to the total:

```cpp
while (count < 30)
{
cout << "Enter a grade: ";
cin >> grade;
if(grade < 0 || grade > 100)
    continue;
total = total + grade;
count++;
}
```

## The Null Statement

All statements must be terminated by a semicolon. A semicolon with nothing preceding it is also a valid statement, called the null statement, as shown:

```cpp
;
```

It's a do-nothing statement used where a statement is required syntactically, but no action is called for. Typically, null statements are used with while or for statements. Program 5.9c in Section 5.3 shows an example of a for statement using a null statement.

## EXERCISES 5.2

- 1. (Modify) Rewrite Program 5.6 to compute the total of eight numbers.

- 2. (Modify) Rewrite Program 5.6 to display this prompt:
  Please type in the total number of data values to be added:
  In response to this prompt, the program should accept a user-entered number, and then use it to control the number of times the while loop is executed. So if the user enters 5 in response to the prompt, the program should request the input of five numbers and display the total after five numbers have been entered.

- 3. (Modify) Rewrite Program 5.7 to compute the average of 10 numbers.

> 1 Although this section of code illustrates the flow of control the continue statement provides, it's not the preferred way of achieving the correct result. Instead of using an if statement and a continue statement to exclude invalid data, a better method is including valid data with these statements:
> if (grade >= 0 && grade <= 100)
> {
>     total = total + grade;
>     count++;
> }
