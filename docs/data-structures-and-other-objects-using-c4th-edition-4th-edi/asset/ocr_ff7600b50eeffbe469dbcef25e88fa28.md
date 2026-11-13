zero (because lower temperatures have no physical meaning). The programmer who uses the function is always responsible for ensuring that the precondition is valid. But, what if a programmer uses the function and the precondition is not valid? This is a programming error, similar to other errors, such as accidentally dividing by zero or attempting to use an array element beyond the array’s bounds.

In a perfect world, such programming errors would never occur: No program would ever attempt to divide by zero, or access an array beyond its bounds, or call a function with an invalid precondition. Of course, programmers aren’t perfect; both novice and experienced programmers make errors. During program development, functions should be designed to help programmers find errors as easily as possible. As part of this effort, the first action of a function should be to check that its precondition is valid. If the precondition fails, then the function prints a message and either halts the entire program, or performs some other error actions before returning.

At first glance, this approach may seem harsh. Why stop the whole program? It’s just a little invalid data! But think back to programs you have written. Did you ever make an error such as accessing an array beyond its bounds, perhaps writing x[42] when the last valid location was x[41]? When this happens, a program won’t always stop immediately; instead the program can continue computing with corrupted data, eventually producing a crash long after the actual error, or just silently producing a wrong answer. Difficult debugging work is sometimes needed to track down the actual location of the error. Testing and debugging is easier if a program produces an error message at the earliest detection of invalid data.

The assert facility is a good approach to detecting invalid data at an early point. To use assert, the program includes this directive:

```
#include <cassert>
```

(Older compilers may use <assert.h> instead.) The primary item in the cassert facility is called assert, which is used like a function with one argument. The argument is usually a true-false expression. The expression is evaluated. If the result is true, then no action is taken. But if the result is false, then an error message is printed, and the program is halted. These checks are called assertions. For example, the celsius_to_fahrenheit function uses this assertion:

```
assert(c >= MINIMUM_CELSIUS);
```

If the expression (c >= MINIMUM_CELSIUS) is true, then c is valid and the assertion takes no action. On the other hand, if the expression is false, then the precondition has been violated, so a message is printed and the program is halted.

After testing and debugging is complete, the programmer has the option of turning off all assertion checks to speed up the program. Assertions can be turned off by placing this statement immediately before the program’s include directives:

```
#define NDEBUG
```