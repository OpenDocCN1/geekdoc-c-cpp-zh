# Substituting pointers for array notation

Array notation must be a myth because it can easily be replaced by pointer notation. In fact, internally to your programs, it probably is.

Consider Table 19-2, which compares array notation with pointer notation. Assume that pointer a is initialized to array alpha. The array and pointer are of the same variable type; notation doesn't differ between variable types. A char array and an int array would use the same references, as shown in both columns in Table 19-2.

# TABLE 19-2 Array Notation Replaced by Pointers

| Array alpha[] | Pointer a |
|---|---|
| alpha[0] | *a or *(a+0) |
| alpha[1] | *(a+1) |
| alpha[2] | *(a+2) |
| alpha[3] | *(a+3) |
| alpha[n] | *(a+n) |

You can test your knowledge of array-to-pointer notation by using a sample program, such as the one shown in Listing 19-5.

# LISTING 19-5: A Simple Array Program

```
```c
#include <stdio.h>

int main()
{
    enum weekdays { mon, tues, wed, thurs, fri };
    float temps[5] = { 18.7, 22.8, 25.0, 23.3, 23.2 };

    printf("The temperature on Tuesday was %.1f\n", temps[tues]);
    printf("The temperature on Friday was %.1f\n", temps[fri]);
    return(0);
}
```
```