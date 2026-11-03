The value of variable c is assigned the sum of variables a and b. This calculation is made when the program runs, and then the result — whatever weirdo value that could be — is displayed.

Exercise 6-11: Create a project using the source code in Listing 6-7. Can you guess the output?

Exercise 6-12: Create a new source code file using Listing 6-7 as a starting point. Declare three float variables and assign values to two of them. Assign a value to the third variable by dividing the first variable by the second variable. Output the result.

# Constants Always the Same

Computers and their electronic brethren enjoy doing repetitive tasks. In fact, anything you do on a computer that requires you to do something over and over demands that a faster, simpler solution be at hand. Often, it's your mission to simply find the right tool to accomplish that goal.

# Using the same value over and over

It may be too early in your C programming career to truly ponder a repetitive program; the topic of looping is covered in Chapter 9. But that doesn't mean you can't code programs that use values over and over.

Exercise 6-13: Create a new program using the source code shown in Listing 6-8. Save it, build it, run it.

# LISTING 6-8: It's a Magic Number

```
#include <stdio.h>

int main()
{
    printf("The value is %d\n",3);
    printf("And %d is the value\n",3);
    printf("It's not %d\n",3+1);
    printf("And it's not %d\n",3-1);
    printf("No, the value is %d\n",3);
    return(0);
}
```