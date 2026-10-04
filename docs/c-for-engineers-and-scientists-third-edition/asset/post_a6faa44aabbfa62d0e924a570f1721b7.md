
# Chapter 4
## 199 Nested if Statements

### ### 4.3 Nested if Statements

As you have seen, an if-else statement can contain any valid C++ simple or compound statements, including another if-else statement. Therefore, one or more if-else statements can be included in either part of an if-else statement. Including one or more if statements inside an existing if statement is called a nested if statement. For example, substituting the one-way if statement

```
if (distance > 500)
cout << "snap";
```

for statement1 in the following if statement

```
if (hours < 9)
statement1;
else
cout << "pop";
```

results in this nested if statement:

```
if (hours < 9)
{
    if (distance > 500)
    cout << "snap";
}
else
cout << "pop";
```

The braces around the inner one-way if statement are essential because in their absence, C++ associates an else with the closest unpaired if. Therefore, without the braces, the preceding statement is equivalent to:

```cpp
if (hours < 9)
    if (distance > 500)
        cout << "snap";
else
    cout << "pop";
```

In this example, the else is paired with the inner if, which destroys the meaning of the original if-else statement. Also note that the indentation is irrelevant, as far as the compiler is concerned. The statement is compiled by associating the last else with the closest unpaired if, unless braces are used to alter the default pairing. The process of nesting if statements can be extended indefinitely, so the cout << "snap"; statement could be replaced by a complete if-else statement or another one-way if statement.

## 200 Selection Structures

Figures 4.4a and 4.4b illustrate the general form of a nested if-else statement when a second if-else statement is nested within a) the if part of an if-else statement and b) the else part of an if-else statement.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_219_0.png)

Figure 4.4a Nested within the if part

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_220_0.png)

Figure 4.4b Nested within the else part

### The if-else Chain

In general, the nested nesting in Figure 4.4a tends to be confusing and is avoided in practice. However, a useful construction for the nesting in Figure 4.4b has this form:

```cpp
if (expression_1)
    statement1;
else
    if (expression_2)
        statement2;
    else
        statement3;
```

As with all C++ programs, because white space is ignored, this indentation isn’t required. Typically, the preceding construction is written in the following arrangement:

```cpp
if (expression_1)
    statement1;
else if (expression_2)
    statement2;
else
    statement3;
```

### Selection Structures

This useful form of a nested if statement is called an if-else chain. Each condition is evaluated in order, and any condition is true, the corresponding statement is executed and the remainder of the chain is terminated. The statement associated with the final else is executed if no previous condition is satisfied. This final else serves as a default or catch-all case that's useful for detecting an error condition or processing a condition that's not handled specially by the previous conditions.

The chain can be continued indefinitely by repeating the last statement another if-else statement. Therefore, the general form of an if-else chain is as follows:

```cpp
if (expression_1)
   statement1;
else if (expression_2)
   statement2;
else if (expression_3)
   statement3;
.
.
else if (expression_n)
   statement_n;
else
   last_statement;
```

Each condition is evaluated in the order it appears in the statement. For the first condition that's true, the corresponding statement is executed, and the remainder of the statements in the chain are not executed. Therefore, if expression_1 is true, only statement1 is executed; otherwise, expression_2 is tested. If expression_2 is true, only statement2 is executed; otherwise, expression_3 is tested, and so on. The final else and its associated statement(s) in the chain are optional, and last_statement is executed only if no expressions are true.

To illustrate an if-else chain, Program 4.5 displays an item's status to letter input. The following input codes are used:

| Specification Status | Input Code |
|---|---|
| Space exploration | S |
| Military grade | M |
| Commercial grade | C |
| Toy grade | T |

### Program 4.5

```cpp
#include <iostream>
using namespace std;

int main() {
    char code;
    cout << "Enter a specification code: ";
    cin >> code;

    if (code == 'S') {
        cout << "The item is space grade.";
    } else if (code == 'M') {
        cout << "The item is military grade.";
    } else if (code == 'C') {
        cout << "The item is commercial grade.";
    } else if (code == 'T') {
        cout << "The item is toy grade.";
    } else {
        cout << "An invalid code was entered.";
    }

    cout << endl;
    return 0;
}
```

Another example of an if-else chain, take a look at determining the output of a converter using the following input/output relationship:

| Input Weight | Output |
|---|---|
| greater or equal to 90 lbs | 1111 |
| Less than 90 lbs but greater or equal to 80 lbs | 1110 |
| Less than 80 lbs but greater or equal to 70 lbs | 1101 |
| Less than 70 lbs but greater or equal to 60 lbs | 1100 |
| Less than 60 lbs | 1011 |

The following statements can be used to determine the correct output for variable inlbs:

```cpp
if (in >= 90)
    digout = 1111;
else if (in >= 80)
    digout = 1110;
else if (in >= 70)
    digout = 1101;
else if (in >= 60)
    digout = 1100;
else
    digout = 1011;
```

Notice that this example makes use of the chain stopping after a true condition is found by checking for the highest weight first. If the input value is less than 90, the if-else chain continues for the next highest weight, and so on, until the correct category is obtained. Program 4.6 uses an if-else chain to calculate and display the correct output corresponding to the weight input.

### Program 4.6

```cpp
#include <iostream>
using namespace std;

int main() {
    int digout;
    double inlbs;

    cout << "Enter the input weight: ";
    cin >> inlbs;

    if (inlbs >= 90)
        digout = 1111;
    else if (inlbs >= 80)
        digout = 1110;
    else if (inlbs >= 70)
        digout = 1101;
    else if (inlbs >= 60)
        digout = 1100;
    else
        digout = 1011;

    cout << "The digital output is " << digout << endl;

    return 0;
}
```

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_223_0.png)

## Chapter 4
## Nested if Statements

The following is a sample run of Program 4.6:

Enter the input weight: 72.5
The digital output is 1101

As with all C++ statements, each statement in an if-else chain can be replaced by a compound statement bounded by braces.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_224_0.png)

### EXERCISES 4.3

- 1. (Practice) Modify Program 4.5 to accept both lower and uppercase letters as codes. For example, if a user enters an m or an M, the program should display the message "The item is military grade."
- 2. (Practice) Write nested if statements corresponding to the conditions illustrated in the following flowcharts:

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_224_1.png)

## 206 Selection Structures

- 3. (Practice) An acute angle is less than 90 degrees, an obtuse angle is greater than 90 degrees, and a right angle is equal to 90 degrees. Using this information, write a C++ program that accepts an angle, in degrees, and displays the type of angle corresponding to the degrees entered.
- 4. (Data Processing) The grade level of undergraduate college students is typically determined by the following schedule:

| Number of Credits Completed | Grade Level |
|---|---|
| Less than 32 | Freshman |
| 32 to 63 | Sophomore |
| 64 to 95 | Junior |
| 96 or more | Senior |

Using this information, write a C++ program that accepts the number of credits a student has completed, determines the student's grade level, and displays the grade level.
- 5. (Data Processing) A student's letter grade is calculated according to the following schedule:

| Numerical Grade | Letter Grade |
|---|---|
| Greater than 90 but greater or equal to 90 | A |
| Less than 90 but greater or equal to 80 | B |
| Less than 80 but greater or equal to 70 | C |
| Less than 70 but greater or equal to 60 | D |
| Less than 60 | F |

Using this information, write a C++ program that accepts a student's numerical grade, converts the numerical grade to an equivalent letter grade, and displays the letter grade.
- 6. (Measurement) The tolerance of critical components in a system is determined according to the following schedule:

| Specification Status | Tolerance |
|---|---|
| Space exploration | Less than 0.1% |
| Military grade | Greater than or equal to 0.1% and less than 1% |
| Commercial grade | Greater than or equal to 1% and less than 10% |
| Toy grade | Greater than or equal to 10% |

Using this information, write a C++ program that accepts a component's tolerance reading and determines the specification that should be assigned to.
- 7. (General Math) Write a C++ program that accepts a number followed by one space and then a letter. If the letter following the number is f, the program is to treat the number entered as a temperature in degrees Fahrenheit, convert it to the equivalent degrees Celsius, and display a suitable message. If the letter following the number is c, the
