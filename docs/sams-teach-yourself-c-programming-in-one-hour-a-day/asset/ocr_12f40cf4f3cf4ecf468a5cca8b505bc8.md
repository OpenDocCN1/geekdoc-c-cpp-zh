# The Program’s Components

# The printf() Statement

The printf() statement (lines 12, 13, 19, and 20) is a library function that displays information onscreen. The printf() statement can display a simple text message (as in lines 12 and 13) or a message mixed with the value of one or more program variables (as in lines 19-20).

# The scanf() Statement

The scanf() statement (line 14) is another library function. It reads data from the keyboard and assigns data to one or more program variables.

The program statement on line 17 calls the function named calcYear(). In other words, it executes the program statements in the function calcYear(). It also sends the argument year to the function. After the statements calcYear() are completed, calcYear() returns a value to the program. This value is stored in the variable named year.

# The return Statement

Lines 22 and 28 contain return statements. The return statement on line 28 is part of the function calcYear(). It calculates the age person would be a specific age by adding the #define TARGET_AGE to the variable year and returns the result to the program that called calcYear(). The return statement on line 22 returns a value of 0 to the operating system just before the program ends.

# The Function Definition (Lines 26 Through 29)

When defining functions before presenting the program bigyear.c, two types of functions—library functions and user-defined functions—were mentioned. The printf() and scanf() statements are examples of the first category, and the function calcYear(), on line 29, is a user-defined function. As named, user-defined functions are written by the programmer during program development. This function adds the value of a created constant to a year and returns the answer (a different year) to the program that called it. In Lesson 5, “Packaging Code in Functions,” you learn that the proper use of functions is an important part of C programming practice.

Note that in a real C program, you probably wouldn’t use a function for a task as simple as adding two numbers. It has been done here for demonstration purposes only.

# Program Comments (Lines 1, 11, 16, and 25)

Any part of your program starts with /* and ends with */ or any single line begins with // is called a comment. The compiler ignores all comments, so they have absolutely no effect on how a program works. You can put anything you want

![](bbox=[0.938, 0.305, 0.976, 0.353])