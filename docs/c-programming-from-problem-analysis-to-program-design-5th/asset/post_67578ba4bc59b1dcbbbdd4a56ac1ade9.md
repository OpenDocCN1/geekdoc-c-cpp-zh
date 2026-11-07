
centimeters is fixed, because 1 inch is always equal to 2.54 centimeters. When stored in memory, this type of data needs to be protected from accidental changes during program execution. In C++, you can use a **named constant** to instruct a program to mark those memory locations in which data is fixed throughout program execution.

**Named constant:** A memory location whose content is not allowed to change during program execution.

To allocate memory, we use C++’s declaration statements. The syntax to declare a named constant is:

```cpp
const dataType identifier = value;
```

In C++, **const** is a reserved word.

### EXAMPLE 2-11

Consider the following C++ statements:

```cpp
const double CONVERSION = 2.54;
const int NO_OF_STUDENTS = 20;
const char BLANK = ' ';
```

The first statement tells the compiler to allocate memory (eight bytes) to store a value of type **double**, call this memory space CONVERSION, and store the value 2.54 in it. Throughout a program that uses this statement, whenever the conversion factor is needed, the memory space CONVERSION can be accessed. The meaning of the other statements is similar.

Note that the identifier for a named constant is in uppercase letters. Even though there are no written rules, C++ programmers typically prefer to use uppercase letters to name a named constant. Moreover, if the name of a named constant is a combination of more than one word, called a *run-together word*, then the words are separated using an underscore. For example, in the preceding example, NO_OF_STUDENTS is a run-together word.

> **NOTE**
>
> As noted earlier, the default type of floating-point numbers is **double**. Therefore, if you declare a named constant of type **float**, then you must specify that the value is of type **float** as follows:
>
> ```cpp
> const float CONVERSION = 2.54f;
> ```
>
> Otherwise, the compiler will generate a warning message. Notice that 2.54f says that it is a **float** value. Recall that the memory size for **float** values is four bytes; for **double** values, eight bytes. Because memory size is of little concern these days, as indicated earlier, we will mostly use the type **double** to work with floating-point values.

Using a named constant to store fixed data, rather than using the data value itself, has one major advantage. If the fixed data changes, you do not need to edit the entire program and change the old value to the new value wherever the old value is used. Instead, you can make the change at just one place, recompile the program, and execute it using the new value throughout. In addition, by storing a value and referring to that memory location whenever the value is needed, you avoid typing the same value again and again and prevent accidental typos. If you misspell the name of the constant value's location, the computer will warn you through an error message, but it will not warn you if the value is mistyped.

In some programs, data needs to be modified during program execution. For example, after each test, the average test score and the number of tests taken changes. Similarly, after each pay increase, the employee's salary changes. This type of data must be stored in those memory cells whose contents can be modified during program execution. In C++, memory cells whose contents can be modified during program execution are called variables.

**Variable:** A memory location whose content may change during program execution.

The syntax for declaring one variable or multiple variables is:

```cpp
dataType identifier, identifier, . . .;
```

### EXAMPLE 2-12

Consider the following statements:

```cpp
double amountDue;
int counter;
char ch;
int x, y;
string name;
```

The first statement tells the compiler to allocate enough memory to store a value of the type `double` and call it amountDue. The second and third statements have similar conventions. The fourth statement tells the compiler to allocate two different memory spaces, each large enough to store a value of the type `int`; name the first memory space x; and name the second memory space y. The fifth statement tells the compiler to allocate memory space to store a string and call it name.

As in the case of naming named constants, there are no written rules for naming variables. However, C++ programmers typically use lowercase letters to declare variables. If a variable name is a combination of more than one word, then the first letter of each word, except the first word, is uppercase. (For example, see the variable amountDue in the preceding example.)

From now on, when we say “variable,” we mean a variable memory location.

> **NOTE** In C++, you must declare all identifiers before you can use them. If you refer to an identifier without declaring it, the compiler will generate an error message (syntax error), indicating that the identifier is not declared. Therefore, to use either a named constant or a variable, you must first declare it.

Now that data types, variables, and constants have been defined and discussed, it is possible to offer a formal definition of simple data types. A data type is called **simple** if the variable or named constant of that type can store only one value at a time. For example, if x is an **int** variable, at a given time, only one value can be stored in x.

## Putting Data into Variables

Now that you know how to declare variables, the next question is: How do you put data into those variables? In C++, you can place data into a variable in two ways:

- 1. Use C++’s assignment statement.
- 2. Use input (read) statements.

### Assignment Statement

The assignment statement takes the following form:

```cpp
variable = expression;
```

In an assignment statement, the value of the **expression** should match the data type of the variable. The expression on the right side is evaluated, and its value is assigned to the variable (and thus to a memory location) on the left side.

A variable is said to be **initialized** the first time a value is placed in the variable.

In C++, = is called the **assignment operator**.

### EXAMPLE 2-13

Suppose you have the following variable declarations:

```cpp
int num1, num2;
double sale;
char first;
string str;
```

Now consider the following assignment statements:

```cpp
num1 = 4;
num2 = 4 * 5 - 11;
sale = 0.02 * 1000;
first = 'D';
str = "It is a sunny day.";
```

For each of these statements, the computer first evaluates the expression on the right and then stores that value in a memory location named by the identifier on the left. The first statement stores the value 4 in num1, the second statement stores 9 in num2, the third statement stores 20.00 in sale, and the fourth statement stores the character D in first. The fifth statement stores the string "It is a sunny day." in the variable str.

The following C++ program shows the effect of the preceding statements:

```cpp
// This program illustrates how data in the variables are
// manipulated.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    int num1, num2;
    double sale;
    char first;
    string str;

    num1 = 4;
    cout << "num1 = " << num1 << endl;

    num2 = 4 * 5 - 11;
    cout << "num2 = " << num2 << endl;

    sale = 0.02 * 1000;
    cout << "sale = " << sale << endl;

    first = 'D';
    cout << "first = " << first << endl;

    str = "It is a sunny day.";
    cout << "str = " << str << endl;

    return 0;
}
```

### Sample Run:

```text
num1 = 4
num2 = 9
sale = 20
first = D
str = It is a sunny day.
```

For the most part, the preceding program is straightforward. Let us take a look at the output statement:

```cpp
cout << "num1 = " << num1 << endl;
```

This output statement consists of the string " num1 = ", the operator <<, and the variable num1. Here, first the value of the string " num1 = " is output, and then the value of the variable num1 is output. The meaning of the other output statements is similar.

A C++ statement such as:

```cpp
num = num + 2;
```

means “evaluate whatever is in num, add 2 to it, and assign the new value to the memory location num.” The expression on the right side must be evaluated first; that value is then assigned to the memory location specified by the variable on the left side. Thus, the sequence of C++ statements:

```cpp
num = 6;
num = num + 2;
```

and the statement:

```cpp
num = 8;
```

both assign 8 to num. Note that if num has not been initialized, the statement num = num + 2 might give unexpected results and/or the compiler might generate a warning message indicating that the variable has not been initialized.

The statement num = 5; is read as “num becomes 5” or “num gets 5” or “num is assigned the value 5.” Reading the statement as “num equals 5” is incorrect, especially for statements such as num = num + 2;. Each time a new value is assigned to num, the old value is overwritten.

### EXAMPLE 2-14

Suppose that num1, num2, and num3 are `int` variables and the following statements are executed in sequence.

- 1. `num1 = 18;`
- 2. `num1 = num1 + 27;`
- 3. `num2 = num1;`
- 4. `num3 = num2 / 5;`
- 5. `num3 = num3 / 4;`

The following table shows the values of the variables after the execution of each statement. (A ? indicates that the value is unknown. The orange color in a box shows that the value of that variable is changed.)
