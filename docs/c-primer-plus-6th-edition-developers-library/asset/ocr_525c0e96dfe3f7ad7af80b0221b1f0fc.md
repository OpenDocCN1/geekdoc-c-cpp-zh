Here, comp is the name of the comparison function. What should this function look like? Suppose you want to sort by last name, then by first name. You could write the function this way:

```
#include <string.h>
int comp(const void * p1, const void * p2)   /* mandatory form */
{
    /* get right type of pointer */
    const struct names *ps1 = (const struct names *) p1;
    const struct names *ps2 = (const struct names *) p2;
    int res;

    res = strcmp(ps1->last, ps2->last);   /* compare last names */
    if (res != 0)
        return res;
    else        /* last names identical, so compare first names */
        return strcmp(ps1->first, ps2->first);
}
```

This function uses the strcmp() function to do the comparison; its possible return values match the requirements for the comparison function. Note that you need a pointer to a structure to use the -> operator.

# The Assert Library

The assert library, supported by the assert.h header file, is a small one designed to help with debugging programs. It consists of a macro named assert(). It takes as its argument an integer expression. If the expression evaluates as false (nonzero), the assert() macro writes an error message to the standard error stream (stderr) and calls the abort() function, which terminates the program. (The abort() function is prototyped in the stdlib.h header file.) The idea is to identify critical locations in a program where certain conditions should be true and to use the assert() statement to terminate the program if one of the specified conditions is not true. Typically, the argument is a relational or logical expression. If assert() does abort the program, it first displays the test that failed, the name of the file containing the test, and a line number.

# Using assert

Listing 16.18 shows a short example using assert. It asserts that z is greater than or equal to 0 before attempting to take its square root. It also mistakenly subtracts a value instead of adding it, making it possible for z to obtain forbidden values.