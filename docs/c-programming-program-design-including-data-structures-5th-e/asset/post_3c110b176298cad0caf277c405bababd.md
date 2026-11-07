
The following example further elaborates on this.

### EXAMPLE 2-30

Consider the following C++ program:

```cpp
//An improperly formatted C++ program.

#include <iostream>
#include <string>
using namespace std;

int main()
{
int num; double height;
string name;
cout << "Enter an integer: "; cin >> num; cout <<
       "num: " <<num<<endl;
cout<<"Enter the first name: "; cin>>name;
       cout<<endl; cout << "Enter the height: ";
cin>>height; cout<<endl;

cout<<"Name: "<<name<<endl; cout<<"Height: "
<<height; cout <<endl;return 0;
}
```

This program is syntactically correct; the C++ compiler would have no difficulty reading and compiling this program. However, this program is very hard to read. The program that you write should be properly indented and formatted. Note the difference when the program is reformatted:

```cpp
//A properly formatted C++ program.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    int num;
    double height;
    string name;

    cout << "Enter an integer: ";
    cin >> num;
    cout << endl;
    cout << "num: " << num << endl;

    cout << "Enter the first name: ";
    cin >> name;
    cout << endl;
    cout << "Enter the height: ";
    cin >> height;
    cout << endl;

    cout << "Name: " << name << endl;
    cout << "Height: " << height << endl;

    return 0;
}
```

As you can see, this program is easier to read. Your programs should be properly indented and formatted. To document the variables, programmers typically declare one variable per line. Also, always put a space before and after an operator. When you type your program using an IDE, typically, your program is automatically indented.

## More on Assignment Statements

The assignment statements you have seen so far are called **simple assignment statements**. In certain cases, you can use special assignment statements called **compound assignment statements** to write simple assignment statements in a more concise notation.

Corresponding to the five arithmetic operators +, −, *, /, and %, C++ provides five compound operators: +=, -=, *=, /=, and %=, respectively. Consider the following simple assignment statement, in which x and y are int variables:

```cpp
x = x * y;
```

Using the compound operator *=, this statement can be written as:

```cpp
x *= y;
```

In general, using the compound operator *=, you can rewrite the simple assignment statement:

```cpp
variable = variable * (expression);
```

as:

```cpp
variable *= expression;
```

The other arithmetic compound operators have similar conventions. For example, using the compound operator **+**, you can rewrite the simple assignment statement:

```
variable = variable + (expression);
```

as:

```
variable += expression;
```

The compound assignment statement allows you to write simple assignment statements in a concise fashion by combining an arithmetic operator with the assignment operator.

### EXAMPLE 2-31

This example shows several compound assignment statements that are equivalent to simple assignment statements.

| Simple Assignment Statement | Compound Assignment Statement |
|---|---|
| `i = i + 5;` | `i += 5;` |
| `counter = counter + 1;` | `counter += 1;` |
| `sum = sum + number;` | `sum += number;` |
| `amount = amount * (interest + 1);` | `amount *= interest + 1;` |
| `x = x / (y + 5);` | `x /= y + 5;` |

> **NOTE**
>
> Any compound assignment statement can be converted into a simple assignment statement. However, a simple assignment statement may not be (easily) converted to a compound assignment statement. For example, consider the following simple assignment statement:
>
> ```cpp
> x = x * y + z − 5;
> ```
>
> To write this statement as a compound assignment statement, the variable x must be a common factor in the right side, which is not the case. Therefore, you cannot immediately convert this statement into a compound assignment statement. In fact, the equivalent compound assignment statement is:
>
> ```cpp
> x *= y + (z − 5)/x;
> ```
>
> which is more complicated than the simple assignment statement. Furthermore, in the preceding compound statement, x cannot be 0. We recommend avoiding such compound expressions.

> **NOTE**
>
> In programming code, this book typically uses only the compound operator +=. So statements such as `a = a + b;` are written as `a += b;`.

## PROGRAMMING EXAMPLE: Convert Length

Write a program that takes as input given lengths expressed in feet and inches. The program should then convert and output the lengths in centimeters. Assume that the given lengths in feet and inches are integers.

**Input** Length in feet and inches.

**Output** Equivalent length in centimeters.

### PROBLEM ANALYSIS AND ALGORITHM DESIGN

The lengths are given in feet and inches, and you need to find the equivalent length in centimeters. One inch is equal to 2.54 centimeters. The first thing the program needs to do is convert the length given in feet and inches to all inches. Then, you can use the conversion formula, 1 inch = 2.54 centimeters, to find the equivalent length in centimeters. To convert the length from feet and inches to inches, you multiply the number of feet by 12, as 1 foot is equal to 12 inches, and add the given inches.

For example, suppose the input is 5 feet and 7 inches. You then find the total inches as follows:

```
totalInches = (12 * feet) + inches
             = 12 * 5 + 7
             = 67
```

You can then apply the conversion formula, 1 inch = 2.54 centimeters, to find the length in centimeters.

```
centimeters = totalInches * 2.54
             = 67 * 2.54
             = 170.18
```

Based on this analysis of the problem, you can design an algorithm as follows:

- 1. Get the length in feet and inches.
- 2. Convert the length into total inches.
- 3. Convert total inches into centimeters.
- 4. Output the centimeters.

### Variables

The input for the program is two numbers: one for feet and one for inches. Thus, you need two variables: one to store feet and the other to store inches. Because the program will first convert the given length into inches, you need another variable to store the total inches. You also need a variable to store the equivalent length in centimeters. In summary, you need the following variables:

```cpp
int feet;             //variable to hold given feet
int inches;           //variable to hold given inches
int totalInches;      //variable to hold total inches
double centimeters;   //variable to hold length in centimeters
```

![](img/f97f778697507bb6fdd80c5991210cba_132_0.png)

used throughout the program, then it is typically placed before the function `main`. We will comment further on where to put named constants within a program in Chapter 7, when we discuss user-defined functions in general. Until then, usually, we will place named constants before the function `main` so that they can be used throughout the program.

This program has only one function, the function `main`, which will contain all of the programming instructions in its body. In addition, the program needs variables to manipulate data, and these variables will be declared in the body of the function `main`. The reasons for declaring variables in the body of the function `main` are explained in Chapter 7. The body of the function `main` will also contain the C++ statements that implement the algorithm. Therefore, the body of the function `main` has the following form:

```cpp
int main()
{
    declare variables

    statements

    return 0;
}
```

To write the complete length conversion program, follow these steps:

- 1. Begin the program with comments for documentation.
- 2. Include header files, if any are used in the program.
- 3. Declare named constants, if any.
- 4. Write the definition of the function `main`.

### COMPLETE PROGRAM LISTING

```cpp
/*******************************************************
// Author: D. S. Malik
//
// Program Convert Measurements: This program converts
// measurements in feet and inches into centimeters using
// the formula that 1 inch is equal to 2.54 centimeters.
//*******************************************************

        //Header file
#include <iostream>

using namespace std;

        //Named constants
const double CENTIMETERS_PER_INCH = 2.54;
const int INCHES_PER_FOOT = 12;
```
