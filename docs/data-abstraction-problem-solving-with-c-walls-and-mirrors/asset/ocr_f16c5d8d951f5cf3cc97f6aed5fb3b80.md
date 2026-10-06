# Assertions 229

This version of findBox meets the basic requirements: It searches the array of boxes and returns the box containing the target string. We encounter a problem if a box containing the target string is not in the array. If the target is not found, the function's while loop ends when index is equal to size, which is the number of entries in the array. The function will return boxes[size], which is undefined. Problem will occur when the client tries to use this “box."

We can repair our code by testing found to make sure we found the target before returning a box from the array. Using a simple if statement is insufficient, as we would still have the problem of what to return when the target is not found. The next section gives one way to fix our code.

# C3.2 Assertions

Chapter 3 and Appendix B define what an assertion is a statement of truth about some aspect of your program's logic. You can express an assertion either as a comment or by using the C++ function assert. By using assert, you can make assertions about variables and objects in the program. Such assertions are in the form of a boolean expression that should be true at a specific point in the program. If the assertion is false, the assert function halts the execution of the program. Assertions can be used to validate methods before trying to execute the body of a function or method.

To use assert in a program, you must first include its header file:

```
#include <assert>
```

To call the assert function, you provide a boolean condition as its argument:

```
assert(someBooleanCondition);
```

When execution reaches this statement, the boolean condition—that is, the assertion—is tested. If the assertion is true, the program continues to execute normally. If the assertion is false, the program halts and an error message is displayed.

The assert statement is an easy way to verify a method's preconditions or postconditions. For example, when implementing the stack method peek, we could execute

```
assert(isEmpty());
```

before returning the top of the stack.

Our findBox function can test whether the box was found before returning boxes[index] by calling:

```
assert(found);
```

If the target is not found, the assertion is false and the program halts. This prevents the program from trying to use a box that does not exist. Listing C3-2 shows the revised findBox function using assertions.

LISTING C3-2 Revised findBox function with assertions
PlainBox<string> findBox(PlainBox<string> boxes[], int size, string target)
{
int index = 0;
bool found = false;
}
(continues)