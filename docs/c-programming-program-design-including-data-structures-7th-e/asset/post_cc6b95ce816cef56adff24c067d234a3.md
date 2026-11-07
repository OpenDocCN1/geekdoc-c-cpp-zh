
```cpp
int first = 13, second = 10;
char ch = ' ';
double x = 12.6;
```

The first C++ statement declares two **int** variables, *first* and *second*, and stores 13 in *first* and 10 in *second*. The meaning of the other statements is similar.

In reality, not all variables are initialized during declaration. It is the nature of the program or the programmer’s choice that dictates which variables should be initialized during declaration. The key point is that all variables must be initialized before they are used.

## Input (Read) Statement

Previously, you learned how to put data into variables using the assignment statement. In this section, you will learn how to put data into variables from the *standard input device*, using C++’s input (or read) statements.

**NOTE** In most cases, the standard input device is the keyboard.

When the computer gets the data from the keyboard, the user is said to be acting interactively.

Putting data into variables from the standard input device is accomplished via the use of **cin** and the operator **>>**. The syntax of cin together with >> is:

```cpp
cin >> variable >> variable ...;
```

This is called an **input (read) statement**. In C++, **>>** is called the **stream extraction operator**.

**NOTE** In a syntax, the shading indicates the part of the definition that is optional. Furthermore, throughout this book, the syntax is enclosed in yellow boxes.

### EXAMPLE 2-16

Suppose that *miles* is a variable of type **double**. Further suppose that the input is 73.65. Consider the following statement:

```cpp
cin >> miles;
```

This statement causes the computer to get the input, which is 73.65, from the standard input device and stores it in the variable *miles*. That is, after this statement executes, the value of the variable *miles* is 73.65.

Example 2–17 further explains how to input numeric data into a program.

### EXAMPLE 2-17

Suppose we have the following statements:

```
int feet;
int inches;
```

Suppose the input is:

```
23 7
```

Next, consider the following statement:

```
cin >> feet >> inches;
```

This statement first stores the number 23 into the variable feet and then the number 7 into the variable inches. Notice that when these numbers are entered via the keyboard, they are separated with a blank. In fact, they can be separated with one or more blanks or lines or even the tab character.

The following C++ program shows the effect of the preceding input statements:

```cpp
// This program illustrates how input statements work.

#include <iostream>

using namespace std;

int main()
{
    int feet;
    int inches;

    cout << "Enter two integers separated by one or more spaces: ";
    cin >> feet >> inches;
    cout << endl;

    cout << "Feet = " << feet << endl;
    cout << "Inches = " << inches << endl;

    return 0;
}
```

**Sample Run:** In this sample run, the user input is shaded.

```
Enter two integers separated by one or more spaces: 23 7
Feet = 23
Inches = 7
```

The C++ program in Example 2-18 illustrates how to read strings and numeric data.

### EXAMPLE 2-18

```cpp
// This program illustrates how to read strings and numeric data.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string firstName;                              //Line 1
    string lastName;                               //Line 2
    int age;                                       //Line 3
    double weight;                                 //Line 4

    cout << "Enter first name, last name, age, "
         << "and weight, separated by spaces."
         << endl;                                  //Line 5

    cin >> firstName >> lastName;                  //Line 6
    cin >> age >> weight;                          //Line 7

    cout << "Name: " << firstName << " "
         << lastName << endl;                     //Line 8

    cout << "Age: " << age << endl;               //Line 9
    cout << "Weight: " << weight << endl;         //Line 10

    return 0;                                      //Line 11
}
```

**Sample Run:** In this sample run, the user input is shaded.

```
Enter first name, last name, age, and weight, separated by spaces.
Sheila Mann 23 120.5
Name: Sheila Mann
Age: 23
Weight: 120.5
```

The preceding program works as follows: The statements in Lines 1 to 4 declare the variables firstName and lastName of type string, age of type int, and weight of type double. The statement in Line 5 is an output statement and tells the user what to do. (Such output statements are called prompt lines.) As shown in the sample run, the input to the program is:

```
Sheila Mann 23 120.5
```

The statement in Line 6 first reads and stores the string Sheila into the variable `firstName` and then skips the space after Sheila and reads and stores the string Mann into the variable `lastName`. Next, the statement in Line 7 first skips the blank after Mann and reads and stores 23 into the variable `age` and then skips the blank after 23 and reads and stores 120.5 into the variable `weight`.

The statements in Lines 8, 9, and 10 produce the third, fourth, and fifth lines of the sample run.

**NOTE** During program execution, if more than one value is entered in a line, these values must be separated by at least one blank or tab. Alternately, one value per line can be entered.

## Variable Initialization

Remember, there are two ways to initialize a variable: by using the assignment statement and by using a read statement. Consider the following declaration:

```cpp
int feet;
int inches;
```

Consider the following two sets of code:

```cpp
(a) feet = 35;
    inches = 6;
    cout << "Total inches = "
         << 12 * feet + inches;
```

```cpp
(b) cout << "Enter feet: ";
    cin >> feet;
    cout << endl;
    cout << "Enter inches: ";
    cin >> inches;
    cout << endl;
    cout << "Total inches = "
         << 12 * feet + inches;
```

In (a), feet and inches are initialized using assignment statements, and in (b), these variables are initialized using input statements. However, each time the code in (a) executes, feet and inches are initialized to the same value unless you edit the source code, change the value, recompile, and run. On the other hand, in (b), each time the program runs, you are prompted to enter values for feet and inches. Therefore, a read statement is much more versatile than an assignment statement.

Sometimes it is necessary to initialize a variable by using an assignment statement. This is especially true if the variable is used only for internal calculation and not for reading and storing data.

Recall that C++ does not automatically initialize variables when they are declared. Some variables can be initialized when they are declared, whereas others must be initialized using either an assignment statement or a read statement.

**NOTE** When the program is compiled, some of the newer IDEs might give warning messages if the program uses the value of a variable without first properly initializing that variable. In this case, if you ignore the warning and execute the program, the program might terminate abnormally with an error message.

**NOTE** Suppose you want to store a character into a `char` variable using an input statement. During program execution, when you enter the character, you do not include the single quotes. For example, suppose that `ch` is a `char` variable. Consider the following input statement:

```
cin >> ch;
```

If you want to store K into `ch` using this statement, during program execution, you only enter K. Similarly, if you want to store a string into a `string` variable using an input statement, during program execution, you enter only the string without the double quotes.

### EXAMPLE 2-19

This example further illustrates how assignment statements and input statements manipulate variables. Consider the following declarations:

```
int count, temp;
double length, width, area;
char ch;
string name;
```

Also, suppose that the following statements execute in the order given.

- 1. `count = 1;`
- 2. `count = count + 1;`
- 3. `cin >> length >> width;`
- 4. `area = length * width;`
- 5. `cin >> name;`
- 6. `length = length + 2;`
- 7. `width = 2 * length - 5 * width;`
- 8. `area = length * width;`
- 9. `cin >> ch;`
- 10. `temp = count + static_cast<int>(ch);`
