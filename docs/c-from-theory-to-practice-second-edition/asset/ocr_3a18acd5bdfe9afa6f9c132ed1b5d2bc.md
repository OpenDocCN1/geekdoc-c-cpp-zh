However, as we'll see later, if the variable i is declared as static you can safely return its address because the memory allocated for a static variable is not released when the function terminates.

> Don't return the address of a local variable unless it is declared as static.

Somewhere later, there is an exercise to test if you digested this rule.

# Global Variables

A variable that is declared outside of any function is called global. Its scope extends from the point of its declaration to the end of the file in which it is declared. Therefore, it can be accessed by all functions that follow its declaration. Unlike an automatic variable, a global variable has a permanent lifetime and retains its last assigned value. To sum up, the default properties of a global variable is file scope, external linkage, and static storage duration; that is, it remains in existence permanently.

When the same variable is used in many functions, many programmers choose to declare it as global instead of passing it as an argument in function calls. In fact, a global variable can be used as an alternative for communicating data between functions.

Typically, we avoid the use of global variables because it may be more difficult to identify erroneous conditions. For example, if an undesired value is assigned to a global variable, it'd be harder to identify the guilty function. Excessive relying on global variables may have a bad effect on program structure and make its comprehension more difficult. For example, it'd be more difficult for the reader to correlate each global variable with the functions that use it. We prefer to use arguments instead, so when reading the function declarations, it is clear which functions need them and if these functions can change their values. For example, if a wrong value is assigned, the list of the guilty functions is narrowed to those which can change its value.

When naming a global variable, it is very important to choose a descriptive name; it helps the reader to understand its role. Don't use meaningless names that are often given in local variables, like i. By default, the value of an uninitialized global variable or the elements of an aggregate type (e.g., array, structure) are set to 0, however, our preference is to set it explicitly. The following program declares the global variable glob. Since it is declared before the definitions of the functions, all functions may access it.

```
#include <stdio.h>

void add(void);
void sub(void);

int glob = 10;

int main(void)
{
    add();
    printf("Val = %d\n", glob);
    sub();
```