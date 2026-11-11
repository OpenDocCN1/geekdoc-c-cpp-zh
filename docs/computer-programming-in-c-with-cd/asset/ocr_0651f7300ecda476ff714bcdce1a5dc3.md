Q10. What do you mean by the Jump statement? List the Jump statements supported by C++.

Ans. Jump statements are the statements that transfer control from one part of the program to another. The following are the jump statements supported by C++:

+   - break statement: Used to exit from loops and conditional statements
+   - continue statement: Used to quit iteration of the current loop and begin executing the next iteration
+   - goto statement: Used to perform an unconditional transfer of control to another statement in the code
+   - exit and abort statements: Used to end C++ programs

Q11. What is the difference between the break statement and the exit statement?

Ans. The break statement is used to exit from loops and conditional statements; whereas, the exit() function is used to end or terminate a C++ program. The exit() function also returns a value. If the return value is 0 or EXIT_SUCCESS, this indicates successful termination of the program, and if any other value or the constant EXIT_FAILURE is returned, this indicates an error.

Q12. What is the difference between the exit() function and abort() function?

Ans. The exit() and abort() functions are used to end C++ programs. The difference between exit() and abort() is that exit() allows the normal C++ runtime termination processing to take place, but abort() just stops the program immediately.

# Debugging Exercises

Q1. What is the output of the following program?

```
#include <stdio.h>

void main()
{
    float cel=0.0;
    float fh=0.0;
    printf("\n Enter the value of Fahrenheit:");
    scanf("%f",&fh);
    cel = ((fh-32)*5)/9;
    printf("\n The equivalent temperature in Celsius is: %f",cel);
}
```

Ans. Output of the preceding program is as follows:

```
Enter the value of Fahrenheit:98
The equivalent temperature in Celsius is :36.666668
```