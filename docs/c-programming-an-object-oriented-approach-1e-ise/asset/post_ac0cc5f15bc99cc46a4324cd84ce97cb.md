
integer day in the first run; the result is Tuesday. In the second run, we enter 5 for the integer day; the result is Thursday. When we enter 8 for the integer day, none of the cases match and nothing is printed. Note that the last break is not really needed, but good programmers add it to make the symmetry complete. Note also that we have added a second output in the first and last cases to demonstrate that multiple statements can also be executed in any case branch.

## Program 4.11 Printing the day of the week from a given day

```cpp
/****************************************************************
* Use a switch statement with break to print the name of the      *
* week day.                                                       *
****************************************************************/
#include <iostream>
using namespace std;

int main ()
{
    // Declaration
    int day;
    // Input
    cout << "Enter a number between 0 and 6: ";
    cin >> day;
    // Switch statement (Decision and output)
    switch (day)
    {
        case 0: cout << "Sunday" << endl;
                cout << "First day of the week " << endl;
                break;
        case 1: cout << "Monday" << endl;
                break;
        case 2: cout << "Tuesday" << endl;
                break;
        case 3: cout << "Wednesday" << endl;
                break;
        case 4: cout << "Thursday" << endl;
                break;
        case 5: cout << "Friday" << endl;
                break;
        case 6: cout << "Saturday" << endl;
                cout << "Last day of the week " << endl;
                break; // This is not needed, but added for parallelism
    } // End switch
    return 0;
} // End main
```

| Run: |
| :--- |
| Enter a number between 0 and 6: 0 |
| Sunday |
| First day of the week |
| Run: |
| Enter a number between 0 and 6: 4 |
| Thursday |
| Run: |
| Enter a number between 0 and 6: 6 |
| Saturday |
| Last day of the week |
| Run: |
| Enter a number between 0 and 6: 8 |

## Adding Default

Sometimes we have several cases that need to take the same action. In this case, if all of the cases are at the end of the switch statement, we can make the statement shorter by adding a **default** case. A *default* case is entered when none of the cases match.

The *default* case can also be used for error detection. It can be used to detect the error when none of the cases match the given value. However, we need to know that the *default* case can be used only once, as the last case.

> **The *default* case must be the last case in a *switch* statement.**

This means if we use the *default* to catch several case values, it cannot be used for error detection. We need to use other tools. The next example shows the use of a *default* case.

## EXAMPLE 4.13

Let us show how we can use the *switch* statement to change a test score to a letter grade. We have a problem that needs to be solved; the grade is based on a range of scores, not a single value. For example, if a score is in the range 90 to 100, the grade should be assigned the letter 'A'. However, we can solve the problem using a *switch* statement if we change the ranges to single values using the division operator. If we divide a score between 0 and 100 by 10, we get a value between 0 and 10. Program 4.12 shows how to solve the problem using this technique.

## Program 4.12 Printing a grade from a score

```cpp
1 /*********************************************************
2  * Use a switch statement to print a grade from a given score.       *
3  *********************************************************/
4 #include <iostream>
5 using namespace std;
6 
int main()
{
    // Declaration
    int score;
    char grade;
    // Input
    cout << "Enter a score between 0 and 100:";
    cin >> score;
    // Decision making using switch statement
    switch (score / 10)
    {
        case 10: grade = 'A';
                 break;
        case 9: grade = 'A';
                break;
        case 8: grade = 'B';
                break;
        case 7: grade = 'C';
                break;
        case 6: grade = 'D';
                break;
        default: grade = 'F';
    } // End switch
    // Output
    cout << "Score: " << score << endl;
    cout << "Grade: " << grade << endl;
    return 0;
}
```

```text
Run:
Enter a score between 0 and 100: 71
Score: 71
Grade: C

Run:
Enter a score between 0 and 100: 93
Score: 93
Grade: A

Run:
Enter a score between 0 and 100: 24
Score: 24
Grade: F
```

As you can see, we have used a *default* case to handle several cases (5, 4, 3, 2, 1, 0), which means all grades less than 60. However, we still have a problem. What if the user enters a score less than 0 or greater than 100? The program will give the grade F. To handle this problem, we need to test the validity of the input first. One way to do this is as follows.

```cpp
cout << "Enter a score between 0 and 100: ";
cin >> score;
if (score > 100)
{
    score = 100;
}
if (score < 0)
{
    score = 0;
}
```

We will see a better input validation strategy when we discuss repetition in the next chapter.

## Combining Cases

If the task performed by several cases is the same, we can combine the cases. This is possible because the *fall through* nature of the *switch* statement allows the program to go through the cases until a *break* statement is encountered. We show the idea in the next example.

## EXAMPLE 4.14

In Program 4.13 we read a letter grade and print a pass/no-pass grade. The default statement serves as the error detector.

## Program 4.13 Finding a pass/no-pass grade

```cpp
/*--------------------------------------------------------------*
 * Use a switch statement to find a pass/nonpass grade.          *
 *--------------------------------------------------------------*/
#include <iostream>
using namespace std;

int main()
{
    // Declaration
    char grade;
    // Input
    cout << "Enter a grade (A, B, C, D, F): ";
    cin >> grade;
    // Decision section using switch statement
    switch (grade)
    {
        case 'A':
18  case 'B':
19  case 'C': cout << "Grade is pass";
20          break;
21  case 'D':
22  case 'F': cout << "Grade is nopass";
23          break;
24  default: cout << "Error in the input. Try again.";
25  } // End switch
26  return 0;
27  } // End main
```

```text
Run:
Enter a grade (A, B, C, D, F): A
Grade is pass

Run:
Enter a grade (A, B, C, D, F): D
Grade is nopass

Run:
Enter a grade (A, B, C, D, F): F
Grade is nopass

Run:
Enter a grade (A, B, C, D, F): G
Error in the input. Try again.

Run:
Enter a grade (A, B, C, D, F): B
Grade is pass

Run:
Enter a grade (A, B, C, D, F): C
Grade is pass
```

## 4.4 CONDITIONAL EXPRESSIONS

Another construct that can be used for decision making is the **conditional expression**. It is the only *ternary* expression in C++. It uses two operators and three operands, as discussed next.

### 4.4.1 Structure of a Conditional Expression

The following shows the syntax of a conditional expression.

```cpp
condition ? expression1 : expression2
```

Table 4.3 shows the location of conditional expressions in the list of expressions in Appendix C.

| Group | Name | Operator | Expression | Prec | Assoc |
|---|---|---|---|---|---|
| Conditional | conditional | `?:` | `expr1 ? expr2 : expr3` | 4 | `←` |

The type *expr1* must be a Boolean expression with a *true* or *false* value. The types of *expr2* and *expr3* must be the same, but the common type can be any type discussed in previous chapters. The whole construct is also an expression with a value. The value of the whole expression is the value of *expr2* if *expr1* is *true*; otherwise, it is the value of *expr3*.

> **The conditional expression can be used anywhere an expression can be used.**

### 4.4.2 Comparison

Let us compare the conditional expression with the two-way *if-else* statement as shown in Figure 4.13.

- The two-way *if-else* statement is made of a Boolean expression with a true branch and a false branch. The conditional expression is made of a Boolean expression and two expressions, one for *true* and one for *false*.
- A two-way *if-else* statement is a statement; it can be used anywhere we can use a statement. The *conditional expression* is an expression; it can also be used anywhere we can use an expression. We can use it in one of the following ways:
  - a. We can use it as an expression in a statement.
  - b. We can add a semicolon at the end to change it to a stand-alone statement. This method is useful when both the second and third statements have a side effect.

## EXAMPLE 4.15

In Program 4.14 we print the larger of two integers using a *conditional expression*.

![](img/d68f6199646ca63591a6d8419e0ed4ba_161_0.png)

**Figure 4.13**  Comparing *if-else* statement and conditional expression
