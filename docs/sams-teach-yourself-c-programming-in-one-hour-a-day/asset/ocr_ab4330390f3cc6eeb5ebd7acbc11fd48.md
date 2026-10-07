This header file also defines two symbolic constants for use as arguments to the exit() function:

#define EXIT_SUCCESS 0
#define EXIT_FAILURE 1

Thus, to exit with a return value of 0, call exit(EXIT_SUCCESS); for a return value of 1, call exit(EXIT_FAILURE).

| DO | DON'T |
|---|---|n|DO the exit() command to get out of the program if there's a problem. | |
|DO pass meaningful values to the exit() function. | |

# Summary

This lesson covers a variety of topics related to program control. You learned about the goto statement and why you should avoid it in your programs. You saw that the break and continue statements give additional control over the execution of loops and that you can use these statements with infinite loops to perform useful programming tasks. You also learned how to use the exit() function to control program termination.

# Q&A

+   - Is it better to use a switch statement or a nested loop?

+   - If you're checking a variable that can take more than two values, the switch statement is almost always better. The resulting code is easier to read, too. If you're checking a true/false condition, go with an if statement.

+   - Why should I avoid a goto statement?

+   - When you first see a goto statement, it's easy to believe that it fixes. However, goto can cause more problems than it fixes. A goto statement is an unstruct command that takes you to another point in a program. Many debuggers (software that helps you trace program problems) can't interrogate goto properly. goto statements also lead to spaghetti—code that goes all over the place.