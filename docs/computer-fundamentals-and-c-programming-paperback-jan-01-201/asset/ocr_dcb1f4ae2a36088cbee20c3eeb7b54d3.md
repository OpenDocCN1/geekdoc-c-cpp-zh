```
struct resolution {
    short horizontal;
    short vertical;
} res;
} p;
```

Next, write a program that assigns the values "Galaxy Note 9" and 8 for the first two members, and 1920 and 1080 for the inner structure. Print all values.

+   14.12 Modify the preceding program (C14.11) to include a pointer q that points to p and then print the same values using q with both * and -> notations.

+   14.13 Modify the function devised in C12.10 (Chapter 12) to return the downloaded time as a 3-member structure. How does this solution differ from the array-based technique?

+   14.14 Write a program that accepts three parameters of a hard disk (heads, cylinders and sectors/track) from user input and passes them as a structure to a function. The function must return the capacity as a 3-member structure (GB, MB and KB). Print the value as a single floating point number.

+   14.15 Write a program that accepts the details of five mutual fund schemes into an array of structures. Each structure comprises the fund name (30 characters), fund code (short) and the current Net Asset Value (NAV—a float). Using keyboard input, update the NAV of a specific fund using a function that accepts three arguments (fund code, pointer to the array and latest NAV).

+   14.16 Write a program that creates a union of a person’s name and age. Fill up both members using user input and then print the values. Does it matter if the input sequence is reversed?

+   14.17 Using a union, write a program that extracts each byte from an unsigned int and prints them as separate characters.

+   14.18 Point out the error in the following code:

```
struct any_struct {
    short s = 20;
    int i : 4;
}
```

+   14.19 Locate the errors in the following program so it prints X.x correctly. For X.x to have the value 300, what changes are required to be made in the program?

```
#include <stdio.h>
int main(void)
{
    struct x {
        short x : 4;
    } X;
    X.x = 8;
    printf("sizeof x = %hd\n", sizeof(x));
    printf("X.x = %hd\n", X.x);
    return 0;
}
```