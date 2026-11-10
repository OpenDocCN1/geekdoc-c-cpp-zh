```
float add(float x, float y)
{
    return x + y;
}
```

Because the **add** function takes two float arguments and returns a float, the name of this function can now be assigned to fp2 in this manner:

```
fp2 = add;
```

Note that even though **add** uses two arguments, we don’t specify them in this assignment. These arguments are provided when the pointer is dereferenced. Whether you would like to use fp2 or (*fp2) for executing the assigned function is purely a matter of choice:

```
float result = (*fp2)(4.5, 5.5);
float result = fp2(4.5, 5.5);
```

result is 10.0
Ditto

Because fp2 has the return type float (same as **add**), the value returned by **add** has to be saved in a separate variable. For the same reason, fp2 can also be used as an expression, and this will be done in the next program.

The discussions involving fp1 and fp2 are merely conceptual. It’s unlikely that you’ll actually invoke functions in the ways just discussed. We have to learn to use function pointers as function arguments, but we’ll do that only after confirming what we have learned so far.

# 17.11.2　func_pointer.c: Using Function Pointers

The attributes of function pointers are demonstrated in Program 17.4, which makes two of them—fp1 and fp2—point to the functions **print_something** and **add**, respectively. The necessary explanations are adequately provided in the annotations.

```
/* func_pointer.c: Uses 2 function pointers to execute functions
                         with and without arguments and return value. */

#include <stdio.h>

void print_something(void);
float add(float x, float y);

int main(void)
{
    float result;

    /* Pointer for function using no arguments and returning nothing */
    void (*fp1)();                 /* Declares function pointer fp1 */
    fp1 = print_something;         /* Assigns function to function pointer */
    (*fp1)();                      /* Invokes dereferenced function pointer */
    fp1();                         /* Invokes function pointer directly */
```