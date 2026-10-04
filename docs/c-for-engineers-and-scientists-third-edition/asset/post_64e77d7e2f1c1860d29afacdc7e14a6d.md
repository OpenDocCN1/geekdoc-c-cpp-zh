
# 192 Selection Structures

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_211_0.png)

**Figure 4.3** A-way if statement

This modified form of the if statement is called a **one-way if statement**. Program 4.3 uses this statement to display a message for cars that have been driven more than 3000.0 miles.
To see its one-way selection criteria in action, Program 4.3 was run twice, each time with different input data. Only the input data for the first run causes the message *Car 256 is over the limit* to be displayed.

```
Please type in car number and mileage: 256 3562.8
  Car 256 is over the limit.
  End of program output.
```

and

```
Please type in car number and mileage: 23 2562.3
  End of program output.
```

# Program 4.3

```cpp
#include <iostream>
using namespace std;

int main() {
    const double LIMIT = 3000.0;
    int idNum;
    double miles;

    cout << "Please type in car number and mileage: " <<;
    cin >> idNum >> miles;

    if(miles > LIMIT)
        cout << " Car " << idNum << " is over the limit.\n";

    cout << "End of program output.\n";

    return 0;
}
```

# Problems Associated with the if-else Statement

Two of the most common problems encountered in using C++ if-else statement are the following:

- Misunderstanding the full implications of what an expression is
- Using the assignment operator, =, in place of the relational operator ==

Recall that an expression is any combination of operands and operators that yields a result. This definition is much broader and more encompassing than is apparent at first. For example, all the following are valid C++ expressions:

```
age + 5
age = 30
age == 40
```

Assuming the variables are declared correctly, each of the preceding expressions yields a result. Program 4.4 uses cout statements to display the value of these expressions when age = 18.

# 194 Selection Structures

# Program 4.4

```cpp
#include <iostream>
using namespace std;

int main() {
    int age = 18;

    cout << "The value of the first expression is " << (age + 5) << endl;
    cout << "The value of the second expression is " << (age = 30) << endl;
    cout << "The value of the third expression is " << (age == 40) << endl;

    return 0;
}
```

The display Program 4.4 produces as follows:

| The value of the first expression is 23 |
| The value of the second expression is 30 |
| The value of the third expression is 0 |

As the output of Program 4.4 shows, each expression has a value associated with it. The value of the first expression is the sum of the variable age plus 5, which is 23. The value of the second expression is 30, which is assigned to the variable age. The value of the third expression is 0 because age is not equal to 40, and a false condition is represented in C++. If the age had been 40, the relational expression age == 40 would be true and have a value of 1.

Now assume the relational expression age == 40 was intended to be used in this statement,

```cpp
if (age == 40)
    cout << "Happy Birthday!";
```

but was mist as 40, resulting in the following:

```cpp
if (age = 40)
    cout << "Happy Birthday!";
```

Because the mistake results in a valid C++ expression, and any C++ expression can be tested by an if statement, the resulting if statement is valid and causes the message Happy Birthday! to be displayed regardless of what value was previously assigned to age. Can you see why?

The condition tested by the if statement doesn't compare the value in age to the number 40. It assigns the number 40 to age. That, the expression age = 40 is not a relational expression at all; it's an assignment expression. At the completion of the assignment, the expression itself has a value of 40. Because C++ treats any non-zero value as true, the cout statement is executed. Another way of looking at it is to realize that the if statement is equivalent to the following statements:

```cpp
age = 40; // assign 40 to age
if (age) // test the value of age
cout << "Happy Birthday!";
```

Because a C++ compiler has no means of knowing the expression being tested isn't the one you want, you must be especially careful when writing conditions.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_215_0.png)

# 196 Selection Structures

# Point of Information

# The Boolean Data Type (continued)

As shown by this output, the Boolean values true and false are represented by the integer values 1 and 0 and have the following relationships:

```
!true = false
!false is true
```

Additionally, applying a postfix or prefix ++ operator to a variable of type bool sets the Boolean value to true. The postfix and prefix -- operators can't be applied to Boolean variables.

Boolean values can also be compared, as shown in the code:

```cpp
if (t1 == t2)
cout << "The values are equal" << endl;
else
cout << "The values are not equal" << endl;
```

Last, assigning any non-zero value to a Boolean variable results in the variable set to true (a value of 1), and assigning a zero value to a Boolean results in the variable being set to false (a value of 0).

# EXERCISES 4.2

- 1. (Practice) Write appropriate if statements for the following conditions:
   a. If an angle is equal to 90 degrees, print the message "The angle is a right angle";
      else, print the message "The angle is not a right angle."
   b. If the temperature is above 100 degrees, display the message "above the boiling point";
   c. If the number is positive, add the number to positivesum;
   d. If the slope is less than 0.5, set flag to zero.

# Chapter 4

# 197 The if-else Statement

- e. If the difference between volts1 and volts2 is less than 0.001, set approx to zero; else, calculate approx as (volts1 - volts2)/2.
- f. If the frequency is above 60, display the message.
- g. If the difference between temp1 and temp2 exceeds 3, calculate error.
- h. If x is greater than y and z is less than 20, request the user.

- 2. (Practice) Write if statements corresponding to the following flowcharts:
   a. ![](img/e2a849fc7bc04aa2e6669ad865e0c22b_216_0)
   b. ![](img/e2a849fc7bc04aa2e6669ad865e0c22b_216_1)
   c. ![](img/e2a849fc7bc04aa2e6669ad865e0c22b_216_2)
   d. ![](img/e2a849fc7bc04aa2e6669ad865e0c22b_216_3)

# Selection Structures

- 3. (Practice) Write a C++ program that asks the user to input two numbers. If the first number is greater than the second, the program should print "the first is greater"; else, it should print "the second is smaller." What do you think your program will display if the numbers are equal?

- 4. (Practice) A certain waveform is 0 for time less than 2 seconds, and 3 for time greater than 2 seconds. Write a C++ program that accepts time and displays the appropriate value, depending on the input.
   b. How many rounds should you make for the program in 4a to verify that it's correct? What data should you input in each run?

- 5. (Instance) An insulation test requires at least 600 volts. Write a C++ program that accepts test voltage and displays "PASSED VOLTAGE" or "FAILED VOLTAGE," as appropriate.

- 6. (Practice) a. Write a C++ program to compute the value of pressure in pounds per square inch (psi) as follows: For time, equal or less than 35 seconds, the pressure is 0.46psi + 9.45. The program should request time and display output.
   b. How many rounds should you make for the program in 6a to verify that it's correct? What data should you input in each run?

- 7. (Practice) a Write a C++ program to display "PROCEED WITH TAKEOFF" or "ABORT TAKEOFF" depending on the input. If the character g is entered into the variable, the first message should be displayed; otherwise, the second message should be displayed.
