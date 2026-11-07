
```
'R' > 'T' is false
'+' < '*' is false
'A' <= 'a' is true
```

Note that comparing values of different data types may produce unpredictable results. For example, the following expressions compare an integer and a character:

```
8 < '5'
```

In this expression, on a particular machine, 8 would be compared with the collating sequence of '5', which is 53. That is, 8 is compared with 53, which makes this particular expression evaluate to true.

Expressions 4 < 6 and 'R' > 'T' are logical (Boolean) expressions. When C++ evaluates a logical expression, it returns an integer value of 1 if the logical expression evaluates to true; it returns an integer value of 0 otherwise. In C++, any nonzero value is treated as true.

> **NOTE** Chapter 2 introduced the data type `bool`. Recall that the data type `bool` has two values: `true` and `false`. In C++, `true` and `false` are reserved words. The identifier `true` is set to 1, and the identifier `false` is set to 0. For readability, whenever logical expressions are used, the identifiers `true` and `false` will be used here as the value of the logical expression.

Now that we know how relational operators work, we can start learning how to implement decisions in a C++ program. Although there are only two logical values, `true` and `false`, they turn out to be extremely useful because they permit programs to incorporate decision making that alters the processing flow. The remainder of this chapter discusses ways to incorporate decisions into a program. In C++, there are two selections, or branch control structures: `if` statements and the `switch` structure. This section discusses how `if` and `if...else` statements can be used to create one-way selection, two-way selection, and multiple selections. The `switch` structure is discussed later in this chapter.

## One-Way Selection

A bank would like to send a notice to a customer if her or his checking account balance falls below the required minimum balance. That is, if the account balance is below the required minimum balance, it should send a notice to the customer; otherwise, it should do nothing. Similarly, if the policyholder of an insurance policy is a nonsmoker, the company would like to apply a 10% discount to the policy premium. Both of these

### EXAMPLE 4-3

```cpp
//Program to compute and output the penalty on an unpaid
//credit card balance. The program assumes that the interest
//rate on the unpaid balance is 1.5% per month.

#include <iostream>                         //Line 1
#include <iomanip>                          //Line 2

using namespace std;                        //Line 3

const double INTEREST_RATE = 0.015;         //Line 4

int main ()                                  //Line 5
{
    double creditCardBalance;               //Line 6
    double payment;                         //Line 7
    double penalty = 0.0;                   //Line 8

    cout << fixed << showpoint << setprecision(2);       //Line 11

    cout << "Line 12: Enter credit card balance: ";     //Line 12
    cin >> creditCardBalance;                            //Line 13
    cout << endl;                                        //Line 14

    cout << "Line 15: Enter the payment: ";             //Line 15
    cin >> payment;                                      //Line 16
    cout << endl;                                        //Line 17

    balance = creditCardBalance - payment;               //Line 18

    if (balance > 0)                                     //Line 19
        penalty = balance * INTEREST_RATE;               //Line 20

    cout << "Line 21: The balance is: $" << balance      //Line 21
         << endl;
    cout << "Line 22: The penalty to be added to your "   //Line 22
         << "next month bill is: $" << penalty << endl;

    return 0;                                            //Line 23
}                                                       //Line 24
```

**Sample Run:** In this sample run, the user input is shaded.

```
Line 12: Enter credit card balance: 2500.00

Line 15: Enter the payment: 275.00

Line 21: The balance is: $2225.00
Line 22: The penalty to be added to your next month bill is: $33.38
```

The statements in Lines 7 to 10 declare the variables used in the program. The statement in Line 12 prompts the user to enter the credit card billing amount. The statement in Line 13 inputs the amount into the variable `creditCardBalance`. The statement in Line 15 prompts the user to enter the payment. The statement in Line 16 inputs the payment into the variable payment. The statement in Line 18 computes the unpaid balance. The `if` statement in Line 19 determines if the unpaid balance is positive. If the unpaid balance is positive, the statement in Line 20 computes the penalty. The statements in Lines 21 and 22 output the results. This program assumes that the interest rate on the unpaid balance is 18% per year (that is, 1.5% per month). As you can see, the interest rate on the unpaid balance can quickly add up and ruin your credit ratings as well as put you in financial trouble.

### EXAMPLE 4-4

Consider the following statement:

```cpp
if score >= 60      //syntax error
    grade = 'F';
```

This statement illustrates an incorrect version of an `if` statement. The parentheses around the logical expression are missing, which is a syntax error.

Putting a semicolon after the parentheses following the expression in an `if` statement (that is, before the statement) is a semantic error. If the semicolon immediately follows the closing parenthesis, the `if` statement will operate on the empty statement.

### EXAMPLE 4-5

Consider the following C++ statements:

```cpp
if (score >= 60);      //Line 1
    grade = 'F';       //Line 2
```

Because there is a semicolon at the end of the expression (see Line 1), the `if` statement in Line 1 terminates. The action of this `if` statement is null, and the statement in Line 2 is not part of the `if` statement in Line 1. Hence, the statement in Line 2 executes regardless of how the `if` statement evaluates.

## Two-Way Selection

There are many programming situations in which you must choose between two alternatives. For example, if a part-time employee works overtime, the paycheck is calculated using the overtime payment formula; otherwise, the paycheck is calculated using the regular formula. This is an example of two-way selection. To choose between two alternatives—that is, to implement two-way selections—C++ provides the `if...else` statement. Two-way selection uses the following syntax:

### EXAMPLE 4-7

The following program determines an employee’s weekly wages. If the hours worked exceed 40, the wages include overtime payment.

```cpp
//Program: Weekly wages

#include <iostream>                                      //Line 1
#include <iomanip>                                       //Line 2

using namespace std;                                     //Line 3

int main()                                                //Line 4
{                                                         //Line 5
    double wages, rate, hours;                            //Line 6

    cout << fixed << showpoint << setprecision(2);        //Line 7
    cout << "Line 8: Enter working hours and rate: ";     //Line 8
    cin >> hours >> rate;                                  //Line 9

    if (hours > 40.0)                                      //Line 10
        wages = 40.0 * rate +                              //Line 11
                1.5 * rate * (hours - 40.0);               //Line 12
    else                                                  //Line 12
        wages = hours * rate;                              //Line 13

    cout << endl;                                          //Line 14
    cout << "Line 15: The wages are $" << wages << endl;  //Line 15

    return 0;                                              //Line 16
}                                                         //Line 17
```

**Sample Run:** In this sample run, the user input is shaded.

Line 8: Enter working hours and rate: 50.00 12.50

Line 15: The wages are $687.50

The statement in Line 6 declares the variables used in the program. The statement in Line 7 sets the output of the floating-point numbers in a fixed decimal format, with a decimal point, trailing zeros, and two decimal places. The statement in Line 8 prompts the user to input the number of hours worked and the pay rate. The statement in Line 9 inputs these values into the variables hours and rate, respectively. The statement in Line 10 checks whether the value of the variable hours is greater than 40.0. If hours is greater than 40.0, then the wages are calculated by the statement in Line 11, which includes overtime payment. Otherwise, the wages are calculated by the statement in Line 13. The statement in Line 15 outputs the wages.

In a two-way selection statement, putting a semicolon after the expression and before statement1 creates a syntax error. If the `if` statement ends with a semicolon,
