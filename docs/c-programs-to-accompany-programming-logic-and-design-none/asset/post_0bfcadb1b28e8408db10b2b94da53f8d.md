
> **NOTE** Notice that a beginning curly brace (`{`) and an ending curly brace (`}`) are used in C++ to mark the beginning and end of code that executes as part of a loop.

According to the pseudocode, the body of the loop is made up of three sequential statements. The first statement calculates the `inputNumber` multiplied by 2; the second statement prints the `calculatedAnswer`; and the third statement retrieves the next `inputNumber` from the user. In C++, we actually need to add an additional statement between the curly braces that mark the body of the `while` loop. This additional statement prompts the user to enter the next number to be doubled.

In the following example, the code that makes up the body of the loop is in bold:

```cpp
int main()
{
    cout << "Enter a number to double or 0 to end: " << endl;
    cin >> inputNumber;
    while( inputNumber != 0)
    {
        calculatedAnswer = inputNumber * 2;
        cout << inputNumber << " doubled is " << calculatedAnswer << endl;
        cout << "Enter a number to double or 0 to end: " << endl;
        cin >> inputNumber;
    }
}
```

The last line of the pseudocode instructs you to end the program. In C++, the closing curly brace (`}`) for the `main` function signifies the end of the `main` function and therefore the end of the program. Note that the preceding code includes two closing curly braces. The last one is the one that ends the `main` function and the second to last one ends the `while` loop.

We are almost finished translating the pseudocode into C++ code. We just have a few housekeeping tasks to take care of. As you learned in Chapter 3 of *Programming Logic and Design, Fifth Edition*, declaring variables is one of these housekeeping tasks. The code that follows is the completed C++ program for doubling numbers. The code shown in bold is the code that declares the variables. The `#include` preprocessor directive and the `using` statement that you learned about in Chapter 1 of this book are also shown in bold. Additionally, you see the `return 0;` statement. This statement instructs the compiler to return the value 0 from the `main` function.

```cpp
#include <iostream>
using namespace std;
int main()
{
    int inputNumber;
    int calculatedAnswer;
    cout << "Enter a number to double or 0 to end: " << endl;
    cin >> inputNumber;
    while( inputNumber != 0)
    {
        calculatedAnswer = inputNumber * 2;
        cout << inputNumber << " doubled is " << calculatedAnswer << endl;
        cout << "Enter a number to double or 0 to end: " << endl;
        cin >> inputNumber;
    }
    return 0;
}
```

At this point, the program is ready to be compiled. Assuming there are no syntax errors, it should execute as planned. Although you have not learned everything you need to know to write this program yourself, you can see from this example that if you start with a well designed, functional, structured flowchart or pseudocode, writing the program in C++ is easier.

## LAB 3-1: USING FLOWCHARTS AND PSEUDOCODE TO WRITE A C++ PROGRAM

In this lab, you use the flowchart and pseudocode in Figure 3-2 to add code to a partially created C++ program. When completed, college admissions officers should be able to use the C++ program to determine whether to accept or reject a student, based on his or her class rank. You studied this flowchart and pseudocode in Chapter 2 of your book, *Programming Logic and Design, Fifth Edition*.

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_48_0.png)

## WRITING STRUCTURED C++ PROGRAMS

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_49_0.png)

```text
start
    read testScore, classRank
    if testScore >= 90 then
        if classRank >= 25 then
            print "Accept"
        else
            print "Reject"
        endif
    else
        if testScore >= 80 then
            if classRank >= 50 then
                print "Accept"
            else
                print "Reject"
            endif
        else
            if testScore >= 70 then
                if classRank >= 75 then
                    print "Accept"
                else
                    print "Reject"
                endif
            else
                print "Reject"
            endif
        endif
    endif
stop
```

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_49_1.png)

Figure 3-2 Flowchart and pseudocode of structured college admission program

- 1. Study the flowchart and pseudocode in Figure 3-2.
- 2. Open the source code file named `CollegeAdmission.cpp` using Notepad or the text editor of your choice.
- 3. Declare two integer variables named `testScore` and `classRank`.
- 4. Write the interactive input statements to retrieve a student’s test score and class rank from the user of the program. Don’t forget to prompt the user for the test score and class rank.
- 5. The rest of the program is written for you. Save this source code file in a directory of your choice, and then make that directory your working directory.
- 6. Compile the source code file `CollegeAdmission.cpp`.
- 7. Execute the program by entering 75 for the test score and 80 for the class rank. Record the output of this program.
  ____________________________________________________________
- 8. Execute the program by entering 80 for the test score and 40 for the class rank. Record the output of this program.
  ____________________________________________________________

## C++ COMMENTS

In Chapter 3 of your book, *Programming Logic and Design, Fifth Edition*, you learned about **program comments**, which are statements that do not execute. You use comments in C++ programs to explain your logic to people who read your source code. The C++ compiler ignores comments.

You can choose from two commenting styles in C++. In the first, you type two forward slash characters (`//`) at the beginning of each comment that you want the compiler to ignore. This style is useful when you only want to mark a single line or part of a line as a comment. In the second style, you enclose a block of lines with the characters `/*` and `*/`. This style is useful when you want to mark several lines as a comment. You may place comments anywhere in a C++ program except within a statement.

The following example shows both styles of comments added to the number-doubling program from the previous section. Note that the first eight lines of the program make up a multiline, block comment that explains some basic information about the program.

A second block comment follows this first one, introducing the code that creates the number-doubling program. Next, several single-line comments are included throughout to describe various parts of the program.

> **NOTE**
> It is a good programming practice to include header comments that provide basic information about a program.

```cpp
/*
    Program Name: NumberDouble.cpp
    Function: This program doubles a number that is input by
    a user and prints the calculated result on the user's
    screen.
    Input:  Interactive
    Output: The doubled number
*/
#include <iostream>
using namespace std;

/*
The following code creates the number-doubling program. It has a single
function named main.
*/
int main()
{
    // Declaration of variables
    int inputNumber;
    int calculatedAnswer;

    // Prompt user and get interactive user input
    cout << "Enter a number to double: " << endl;
    cin >> inputNumber;

    // Continue until user enters a 0 to end the program
    while( inputNumber != 0)
    {
        // Calculate the number doubled
        calculatedAnswer = inputNumber * 2;
        // Output the result
        cout << inputNumber << " doubled is " << calculatedAnswer << endl;
        // Prompt user and get interactive user input
        cout << "Enter a number to double: " << endl;
        cin >> inputNumber;
    } // End of while loop
    return 0;
} // End of main function
```

> **NOTE:** You are responsible for including well-written, meaningful comments in all of the programs that you write. In fact, some people think that commenting your source code is as important as the source code itself.

Next, you will see how to use a flowchart and pseudocode to write a modular program in C++.
