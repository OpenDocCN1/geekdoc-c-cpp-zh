
# Program 2.8

```cpp
#include <iostream>
using namespace std;

int main() {
    char ch;    // this declares a character variable

    ch = 'a';    // store the letter a in ch
    cout << "The character stored in ch is " << ch << endl;
    ch = 'm';    // now store the letter m in ch
    cout << "The character now stored in ch is " << ch << endl;

    return 0;
}
```

When Program 2.8 runs, this output is produced:

The character stored in ch is a
The character now stored in ch is m

Notice in Program 2.8 that the first letter stored in the variable ch is a and the second letter stored is m. Because a variable is used to store only one value at a time, assigning m to the variable overwrites the value automatically.

# Multiple Declarations

Variables of the same data type can always be grouped together and declared by using a single declaration statement, which has this common form:

```
dataType variableList;
```

For example, the four declarations used in Program 2.7

```
double grade1;
double grade2;
double total;
double average;
```

can be replaced with this single declaration statement:

```cpp
double grade1, grade2, total, average;
```

Similarly, the two character declarations

```
char ch;
char key;
```

# 82 Problem Solving Using C++

can be replaced with this single declaration statement:

char ch, key;

Declaring multiple variables in a single declaration statement requires giving the data type of variables only once, separating all variable names by commas, and using only one semicolon to terminate the declaration. The space after each comma is inserted for readability and isn't required.

Declaration statements can also be used to store a value in declared variables. For example, the declaration statement

```
int num1 = 15;
```

both declare the variable num1 as an integer and sets the value of 15 in the variable. When a declaration statement is used to store a value in a variable, the variable is said to be initialized. Therefore, in this example, it is correct to say the variable num1 has been initialized to 15. Similarly, the declaration statements

```cpp
double grade1 = 87.0;
double grade2 = 93.5;
double total;
```

declare three double-precision variables and initialize two of them. When initializations are used, good programming practice declares each initialized variable on a line by itself. Constants, expressions using only constants (such as 87.0 + 12 - 2), and expressions using constants and previously initialized variables can be used as initializers for variables declared within a function. For example, Program 2.7 with declaration initialization becomes Program 2.7a.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_101_0.png)

# Program 2.7a

```cpp
#include <iostream>
using namespace std;

int main()
{
    double grade1 = 85.5;
    double grade2 = 97.0;
    double total, average;

    total = grade1 + grade2;
    average = total/2.0; // divide the total by 2.0
    cout << "The average grade is " << average << endl;

    return 0;
}
```

# Chapter 2 Variables and Declaration Statements

Notice the blank line after the last declaration statement. Inserting a blank line after variable declarations placed at the top of a C++ function is a good programming practice. It improves a program's appearance and readability.

An interesting feature of C++ is that variable declarations can be intermixed and even contained in other statements; the only requirement is that a variable must be declared before its use. For example, the variable total in Program 2.7a could have been declared when it was first used with the statement `double total = grade1 + grade2;`. In restricted situations (such as debugging, described in Section 3.7, or for a loop, declaring a variable at its first use can be helpful. In general, it's preferable not to spread out declarations; instead, group them as concisely and clearly as possible at the top of each function.

# Memory Allocation

The declaration statements you have seen so far performed both hardware and software tasks. From a software perspective, declaration statements provide a list of variables and their data types. In this software role, variable declarations also help control otherwise common and troublesome error caused by misspelling a variable's name in a program. For example, a variable distance is declared and initialized by this statement:

```cpp
int distance = 26;
```

Later in the program, the variable is invariantly misspelled in this statement:

```
mpg = distance / gallons;
```

In languages that do not require variable declarations, the program treats distnce as a new variable and assigns it an initial value of 0 or whatever value happens to be in the variable's storage area. In either case, a value is calculated and assigned to mpg, and finding the error or even knowing an error occurred would be difficult. These errors are impossible in C++, however, because the compiler flags distance as an undefined variable. The compiler can't, of course, detect when one declared variable is mistakenly typed in place of another declared variable.

In addition to their software role, declaration statements also perform a hardware task. Each data type has its own storage requirements, the compiler can allocate enough storage for the variable data type. Variable declarations provide this information, which can be used to tell the compiler to reserve physical memory for each variable. Declaration statements used for this hardware are also called **definition statements** because they define or tell the compiler how much memory is needed for data storage.

All the declaration statements you've encountered so far are definition statements that do not allocate storage and simply alert the data types of variables created elsewhere in the program.

Figures 2.10 show the operations set in motion by definition statements. The figures show that definition statements (or declaration statements that also allocate memory) ("tag") the first byte of each set of reserved bytes with a name. This is, of course, the variable's name, and the computer uses it to locate the starting point of a variable's memory area.

After a variable has been declared in a program, typically a programmer uses it to refer to the variable's contents (its value). The value's memory location is generally of little concern to programmers. The compiler, however, must know where each value is stored and

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_102_0.png)

# Problem Solving Using C++

Tells the computer to

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_103_0.png)

Tells the computer to

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_103_1.png)

Tells the computer to

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_103_2.png)

locate each variable correctly. For this task, the compiler uses the variable name to locate the first byte of storage previously allocated to the variable. Knowing the variable's data type then allows the compiler to store or retrieve the correct number of bytes.

# Chapter 2 85

Variables and Declaration Statements

Tells the computer to

```
char key; Reserve enough room for a character 1 byte "Tag" the first byte of reserved storage with the name key Tells the computer
```

Figure 2.10 Defining the character variable key

# Displaying a Variable's Address¹¹¹

Every variable has three major items associated with it: its data type, the value stored in it, and its address. The value stored in the variable is referred to as the variable's contents, and the address of the first memory location used for the variable constitutes its address. The number of locations actually used for the variable, as you have just seen, depends on the variable's data type. Figure 2.11 illustrates the relationship between these three items (type, contents, and location).

One or more bytes in memory

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_104_0.png)

Figure 2.11 A typical variable

Programmers are usually concerned only with the value assigned to a variable (its contents) and give little attention to where the value is stored (its address). For example, take a look at Program 2.9.

> ¹¹¹This topic can be omitted on first reading without loss of subject continuity.
