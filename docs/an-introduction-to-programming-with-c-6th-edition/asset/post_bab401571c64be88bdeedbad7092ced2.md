
# CHAPTER 4 Completing the Problem-Solving Process

little or no modification. Your instructor will provide you with the appropriate instructions if you are not using Microsoft Visual C++ 2010 or Dev C++.

## DIRECTIONS

Follow the instructions for starting your C++ development tool. Depending on the development tool you are using, you may need to create a new project; if so, name the project Lab4-2 Project and save it in the Cpp:Chap04 folder. Follow the instructions shown in Figure 4-30 in a source file Lab4-2.cpp. (Do not enter the line numbers.) Save the file in the project folder or the Cpp:Chap04 folder. Now follow the instructions for running Lab4-2.cpp file. Run the program twice, using the data values of 9 and 11 for the hours enrolled. If necessary, correct any bugs (errors) in the program.

```cpp
// Lab4-2.cpp - displays the total owed
//Created by revised <your name> on <current date>
#include <iostream>
using namespace std;
int main(){
//declare variables and named constants
int hours = 0;
int totalowed = 0;
const int FEE_PER_HOUR = 100;
const int ROOM_BOARD = 2000;
//enter hours enrolled
cout << "Hours enrolled: ";
cin >> hours;
//calculate total owed
totalowed = hours * FEE_PER_HOUR + ROOM_BOARD;
//display total owed
cout << "Total owed: $" << totalowed << endl;
system("pause");
return 0;
}
```

Figure 4-30 Hoover College program

## LAB 4-3 Modify

If necessary, create a new project Lab4-3. Enter (or copy) Lab4-2.cpp instructions into a new source file Lab4-3.cpp. Hoover College now has courses that can be .5, 1, 2, or 3 semester hours. In addition, the fee per hour has been raised to $105. Modify the program instructions. Be sure to change Lab4-2.cpp in the first comment to Lab4-3.cpp. Test the program twice, using 9.5 and 11 as the number of hours enrolled should be $2997.5 and $3155. (Don't be concerned that the $2997.5 has only one decimal place. You will learn how to format numbers in Chapter 5.5).

103

## LAB 4-4 Desk-Check

Desk-check the three lines of code shown in Figure 4-31.

```cpp
int num = 75;
int answer = 0;
answer = num % 2;
```

Figure 4-31 Code for Lab 4-4

## LAB 4-5 Debug

Follow the instructions for starting C++ and opening the Lab4-5.cpp file. If necessary, make the system("pause"); statement comment, and save the program. Run and then debug the program.

## Summary

- The fourth step in the problem-solving process is to code the algorithm. You begin by declaring a memory location for each unique input, processing and output item from the IPO chart. You then translate each instruction in the algorithm into one or more C++ statements.
- In C++, perform standard input and output operations using stream objects. The standard input object is called cin. The standard output stream is called cout.
- You use cin along with the extraction operator (>>) to get either numeric or character input from the keyboard. You use cout along with the insertion operator (<<) to display information on the computer screen.
- The extraction operator stops removing characters from the cin object when it encounters a white-space character.
- The endl manipulator advances the cursor to the next line on the computer screen.
- A program should display (on the computer screen) a separate and meaningful prompt for each item of data the user should enter.
- You direct the computer to perform a calculation by writing an arithmetic expression that contains one or more arithmetic operators.
- Each arithmetic operator is associated with a precedence number, which controls the order in which the operation is performed in an expression. When an arithmetic expression contains more than one operator having the same priority, those operators are evaluated from left to right. You can use parentheses to enforce the normal order of precedence.
- When an arithmetic operation involves two values different data types, the computer implicitly promotes the value with the lower-ranking data type to the higher-ranking data type. The value returns to its original data type upon completion of the arithmetic operation.
- The quotient obtained by dividing one integer by another is always an integer in C++.
- You can use the static_cast operator to explicitly convert data from one data type to another.
- You can use an assignment statement to assign a value to a variable runtime. An assignment statement tells the computer to evaluate the expression on the right side of the assignment operator (=) and then store the result in the variable name appears on the left side of the assignment operator.
- The fifth step in the problem-solving process is to desk-check the program. You should use the same sample data used to desk-check the algorithm.
- The sixth (and final) step in the problem-solving process is to evaluate and modify (if necessary) the program.
- The errors in a program are called bugs and typically fall into one of two categories: syntax errors or logic errors.
- In order to enter your C++ instructions into the computer and to run the program, you need to access to a text editor and a C++ compiler.
- The C++ instructions entered in a program are called source code and are saved in a source file, which has a .cpp filename extension.
- The compiler translates source code into machine code, also called object code.
- The linker produces an executable file that contains all the machine code necessary to run a C++ program. The executable file has an .exe extension.
- Programmers use comments to document a program internally. This makes the program easier to understand by anyone viewing it. Comments are not statements and are ignored by the compiler.
- The #include <iostream> directive tells the computer to include the contents of the iostream in the current program.
- The using namespace std; directive tells the computer that the definitions of standard C++ keywords and classes are located in the std namespace. A namespace is a special area in the computer's internal memory.

The execution of a C++ program begins with the main function. Therefore, C++ program must have one (and only one) main function.

The first line in a function is called the function header. Following the function header is the function body, which must be enclosed in braces.

C++ provides arithmetic assignment operators to abbreviate an assignment statement as follows: variableName arithmeticAssignment; However, the original assignment statement must have the following format, in which variableName is the name of the same variable: variableName = variableName arithmeticOperator.

## Key Terms

- #include—directive that tells the computer to merge the source code from one file with the source code from another
- %modulus—divides two integers and returns the remainder as an integer
- <<—the insertion operator in C++
- >>—the extraction operator in C++
- Arithmetic assignment operators—operators comprised of an arithmetic operator and the assignment operator; allow you to abbreviate an assignment statement that follows a specific format
- Assignment operator—the = used to assign a value in a variable during
- Assignment statement—the errors in a program
- cin—the standard input stream in C++; tells the computer to parse program execution when the user enters one or more characters at the keyboard; temporarily stores the characters entered at the keyboard
- Comment—a message used to document a program initially; begins with two forward slashes (/) in C++
- cout—the standard output stream object in C++; used with the insertion operator to display information on the computer screen
- Debugging—the process of identifying and correcting any errors in a program
- endl—a string manipulator that can be used to advance the cursor to the next line on the computer
- Executable file—a file that contains all the machine code necessary to run a program; executable files have an .exe file extension
- Explicit type conversion—the explicit conversion of data from one data type to another; usually performed with the static_cast operator
- Extraction operator—two greater-than signs (>>); extracts (removes) characters from the cin object and sends "in" to the computer's internal memory
- Function—a block of code that performs a task

105
