
This code produces the following display:

```
The value of the first expression is 23
The value of the second expression is 30
The value of the third expression is 0
```

As this output shows, each expression has a value associated with it. The value of the first expression is the sum of the variable age plus 5, which is 23. The value of the second expression is 30, which is also assigned to the variable age. The value of the third expression is 0 because age is not equal to 40, and a false condition is represented in C++ with the value 0. If the value in age had been 40, the relational expression age == 40 would be true and have the value 1.

Say the relational expression age == 40 was intended to be used in the if statement

```
if (age == 40)
    cout << "Happy Birthday!";
```

but was mistyped as age = 40, resulting in the following:

```
if (age = 40)
    cout << "Happy Birthday!";
```

Because the mistake results in a valid C++ expression, and any C++ expression can be tested by an if statement, the resulting if statement is valid and causes the message Happy Birthday! to be displayed regardless of what value was previously assigned to age. Can you see why?

The condition tested by the if statement doesn't compare the value in age to the number 40. It assigns the number 40 to age. That is, the expression age = 40 isn't a relational expression at all; it's an assignment expression. At the completion of the assignment, the expression itself has a value of 40. Because C++ treats any non-zero value as true, the cout statement is executed. Another way of looking at it is to realize that the if statement is equivalent to the following statements:

```
age = 40;  // assign 40 to age
if (age)    // test the value of age
cout << "Happy Birthday!";
```

Because a C++ compiler has no means of knowing that the expression being tested isn't the one you want, you must be especially careful when writing conditions.

## Point of Information
### The Boolean Data Type

Before the current ANSI/ISO C++ standard, C++ didn’t have a built-in Boolean data type with its two Boolean values, true and false. Because this data type wasn’t originally part of the language, a tested expression could not evaluate to a Boolean value. Therefore, the syntax

```
if (Boolean expression is true)
    execute this statement;
```

also wasn’t built into C or C++. Instead, C++ uses the more encompassing syntax,

```
if (expression)
    execute this statement;
```

where expression is any expression that evaluates to a numeric value. If the value of the tested expression is a non-zero value, it’s considered true, and only a zero value is considered false.

As the ANSI/ISO C++ standard specifies, C++ has a built-in Boolean data type containing the values true and false. Boolean variables are declared with the bool keyword. As currently implemented, the actual values that the Boolean values true and false represent are the integer values 1 and 0. For example, examine the following program, which declares two Boolean variables:

```
#include <iostream>
using namespace std;
int main()
{
    bool t1, t2;

    t1 = true;
    t2 = false;
    cout << "The value of t1 is " << t1
         << "\nand the value of t2 is " << t2 << endl;

    return 0;
}
```

This program produces the following output:

```
The value of t1 is 1
and the value of t2 is 0
```

## Point of Information
### The Boolean Data Type (continued)

As shown by this output, the Boolean values true and false are represented by the integer values 1 and 0 and have the following relationships:

```
!true = is false
!false = is true
```

Additionally, applying a postfix or prefix ++ operator to a variable of type bool sets the Boolean value to true. The postfix and prefix -- operators can't be applied to Boolean variables.

Boolean values can also be compared, as shown in the following code:

```
if (t1 == t2)
    cout << "The values are equal" << endl;
else
    cout << "The values are not equal" << endl;
```

Last, assigning any non-zero value to a Boolean variable results in the variable being set to true (a value of 1), and assigning a zero value to a Boolean results in the variable being set to false (a value of 0).

## EXERCISES 4.2

- 1. (Practice) Write suitable if statements for the following conditions:
- a. If an angle is equal to 90 degrees, print the message "The angle is a right angle."; else, print the message "The angle is not a right angle."
- b. If the temperature is above 100 degrees, display the message "above the boiling point of water"; else, display the message "below the boiling point of water."
- c. If the number is positive, add the number to the variable positivesum; else, add the number to the variable negativesum.
- d. If the slope is less than 0.5, set the variable flag to 0; else, set flag to 1.
- e. If the difference between slope1 and slope2 is less than 0.001, set the variable approx to 0; else, calculate approx as the quantity (slope1 - slope2) / 2.0.
- f. If the frequency is above 60, display the message "The frequency is too high."
- g. If the difference between temp1 and temp2 exceeds 2.3, calculate the variable error as (temp1 - temp2) * factor.
- h. If x is greater than y and z is less than 20, request that the user input a value for the variable p.
- i. If distance is greater than 20 and less than 35, request that the user input a value for the variable time.

## The if-else Statement

2. (Practice) Write if statements corresponding to the conditions shown in the following flowcharts:

![](img/e9bf940282dfb289356f077151cc69dd_174_0.png)

![](img/e9bf940282dfb289356f077151cc69dd_174_1.png)

![](img/e9bf940282dfb289356f077151cc69dd_174_2.png)

![](img/e9bf940282dfb289356f077151cc69dd_174_3.png)

3. (Practice) Write a C++ program that asks the user to input two numbers.

If the first number entered is greater than the second number, the program should print the message “The first number is greater.”; else, it should print the message “The first number is smaller.” Test your program by entering the numbers 5 and 8 and then using the numbers 11 and 2. What do you think your program will display if the two numbers entered are equal? Test this case.

4. (Program) a. In a pass/fail course, a student passes if the grade is greater than or equal to 70 and fails if the grade is lower than 70.

Write a C++ program that accepts a grade and prints the message “A passing grade” or “A failing grade,” as appropriate.

b. How many runs should you make for the program written in Exercise 4a to verify that it’s operating correctly? What data should you input in each program run?

5. (Program) a. If money is left in a particular bank for more than 5 years, the bank pays interest at a rate of 4.5%; otherwise, the interest rate is 3.0%.

Write a C++ program that uses the cin object to accept the number of years in the variable numYears and display the correct interest rate, depending on the value input into numYears.

b. How many runs should you make for the program written in Exercise 5a to verify that it’s operating correctly? What data should you input in each program run?

6. (Practice) a. Write a C++ program to display the message “PROCEED WITH TAKEOFF” or “ABORT TAKEOFF” depending on the input.

If the character g is entered in the variable code, the first message should be displayed; otherwise, the second message should be displayed.

b. How many runs should you make for the program written in Exercise 6a to verify that it’s operating correctly? What data should you input in each program run?

7. (Program) Write, compile, and run a C++ program that accepts a user-input integer number and determines whether it’s even or odd.

The output should display the message “The entered number is even.” or “The entered number is odd.” corresponding to the number the user entered. (Hint: An even number has a 0 remainder when divided by 2.)

8. (Program) Write, compile, and run a C++ program that accepts a user-entered number and calculates the square root and the reciprocal.

Before calculating the square root, validate that the number isn’t negative, and before calculating the reciprocal, check that the number isn’t zero. If either condition occurs, display a message stating that the operation can’t be calculated.

9. (Program) Years that are evenly divisible by 400 or are evenly divisible by 4 but not by 100 are leap years.
