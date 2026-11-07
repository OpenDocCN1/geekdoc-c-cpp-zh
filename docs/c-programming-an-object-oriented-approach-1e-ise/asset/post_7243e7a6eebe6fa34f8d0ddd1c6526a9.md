
## Program 2.2 The second simple program

```cpp
/**************************************************************
 * This program shows how we can print a square of asterisks. *
 **************************************************************/
#include <iostream>
using namespace std;

int main()
{
    // Printing a square of asterisks
    cout << "******" << endl;
    cout << "******" << endl;
    cout << "******" << endl;
    cout << "******" << endl;
    cout << "******" << endl;
    cout << "******" << endl;
    return 0;
}
```

**Run:**
```text
******
******
******
******
******
******
```

## Analysis

We briefly analyze the lines in Program 2.2 that are different from the corresponding lines in the first program.

**Lines 1 to 3: Block Comment** Lines 1 to 3 in the second program are different from the first program. They are what we call a **block comment**. A block comment is one or more lines that are considered comments for the user or reviewer of the code and are totally ignored by the compiler (block comments are erased before the program is compiled). The format is shown below:

```text
/* Text to be ignored
Text to be ignored
Text to be ignored */
```

The comment has a starting section and ending section. The starting section is made of two characters (/*), and the ending section is made of the same two characters but in the reverse order (*/). Everything in between is considered a comment and is ignored. Note that we can have any character between the starting section and the ending section (including * and /) but not in combination to create a starting section or an ending section. Inside the program we use colored text for the whole comment. Note that in lines 1 to 3, we have used some asterisks as text to create a frame for our comment, but this is a personal choice.

**Line 5** This line is also new in this program, as shown below:

```cpp
using namespace std;
```

Line 5 tells the compiler that when it cannot see the last name of an object, insert `std::` in front of it to make the name complete. In other words, it tells the compiler that some names that we use in the program belong to the namespace std. With this single line, we can use the cout and endl objects without qualifying them with the std namespace.

**Line 9** This line is also a comment, but a **line comment** (instead of a block comment). This type of comment starts with two slashes and continues with text as a comment (up to the end of the line). The whole line is ignored by the compiler.

```cpp
// Printing a square of asterisks
```

This type of comment can span only a single line. If we need two lines of comments, we must start another line comment or use a block comment.

**Lines 10 to 15** These lines do the same thing as similar ones in the first program, but we can use cout and endl without `std::`. Each line prints a line of six asterisks on the monitor to create a square of asterisks. In Program 2.2 we have used a yellow background to highlight the body of the function here. This is not needed; it is only used for readability.

## 2.2 VARIABLE, VALUE, AND CONSTANT

Before we can write more programs, we need to understand three concepts: *variables, values,* and *constants*.

### 2.2.1 Variables

Programs written in the C++ language receive input data, manipulate them, and create output data. Since the input and output data may change, we must be able to store the input data, store the intermediate data, and store the output data in memory. For this reason, C++, like most programming languages, uses the concept of variables. A **variable** in computer language parlance is a memory location that needs to have a *name* and a *type*. It is called a variable because its contents may change during the execution of the program. Its purpose is to store and retrieve data. It must have a *type* because we use different data types for different purposes.

> **A variable is a memory location, with a name and a type, that stores different values in each moment of a program’s execution.**

Before we use a variable, we must define it. We must tell the compiler that we want to use a memory location with the given name and the given type. The name is used to refer to the variable; the type is used to tell what type of data is stored in the variable.

![](img/d68f6199646ca63591a6d8419e0ed4ba_45_0.png)

**Figure 2.5** Variables in memory and their definition in a program

### EXAMPLE 2.1

Figure 2.5 shows three variables with their types and names. The figure also shows how we define them to ensure that the compiler will know the variable to which we are referring.

We have not discussed data types yet, but we specify that all three data types are integer types (which can represent a whole number without fractions), such as 17, 35, 100, and so on, but not 23.67.

### 2.2.2 Values

The contents of a variable are referred to as its **value**. For example, if `num1` at this moment holds the integer 17, its value is 17. When we use the name of a variable in a program, sometimes we mean the variable itself, sometimes the value it holds. The next example shows the difference.

### EXAMPLE 2.2

Assume we want to write a program that accepts any two whole numbers, adds them together, and displays the result. While we have not studied data types yet, we understand that the two numbers and the result are integer types (int in C++). To store the two numbers and the result of the addition, we need to give them names. We call them **num1**, **num2**, and **sum**, respectively. We then write a program that, each time it runs, finds the sum of two numbers entered at the keyboard and prints them (Program 2.3).

## Program 2.3 A program that adds two values

```cpp
/**************************************************************
 * This program gets the values for two numbers from the keyboard, *
 * adds them together and prints the result on the monitor.       *
 **************************************************************/
#include <iostream>
using namespace std;

int main()
{
    // Definition
    int num1;
    int num2;
    int sum;
    // Getting inputs
    cout << "Enter the first number: ";
16    cin >> num1;
17    cout << "Enter the second number: ";
18    cin >> num2;
19    // Calculation and storing result
20    sum = num1 + num2;
21    // Display output
22    cout << "The sum is: " << sum;
23    return 0;
24 }
```

```text
Run:
Enter the first number: 23
Enter the second number: 35
The sum is: 58

Run:
Enter the first number: 7
Enter the second number: 110
The sum is: 117
```

We examine the contents of lines 11 to 13 as shown below:

```cpp
int num1;
int num2;
int sum;
```

These three lines declare variables. Declaration of a variable means reservation of memory with a corresponding name. In the case of the above three declarations, we have the situation shown previously in Figure 2.5. Note that no values are stored in the program at this moment.

Now we examine lines 15 to 18 as shown below:

```cpp
cout << "Enter the first number: ";
cin >> num1;
cout << "Enter the second number: ";
cin >> num2;
```

We are familiar with the first line. The first line prints a message, which is referred to as *prompt*, on the screen. It tells the user what to do next. The second line is new for us. It uses a target object, `cin` (for console in) and a command (`>>`), which means *read*. This command waits for the user of the program to enter a value (an integer in this case) on the keyboard and hit the enter key. The program then stores the value entered in variable `num1`. The third line is the same as the first one. The fourth line is the same as the second line, but it stores the value entered by the user in variable `num2`. After these four lines, two values are stored
