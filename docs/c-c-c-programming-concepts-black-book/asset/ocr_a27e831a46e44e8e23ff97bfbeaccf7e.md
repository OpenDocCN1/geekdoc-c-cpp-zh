Output of the preceding program is as follows:

The result after shifting 5 bits to the right [-1]

We can notice in the output that even after shifting the number 5 bits to its right, the value stays as -1. This happens as the compiler fills the blank positions with 1 instead of 0. However, this handling may vary from compiler to compiler.

# Left Shift Operator

Left shift operator is similar to a right shift operator; however, the difference is that the bits are shifted to the left. For every bit being shifted, a 0 is added to the right of the number. The left shift operator is denoted by a << sign. Let’s consider the following expression:

abc << 5

Assume that abc contains a bit pattern, 10101110. If the number gets 5 places to its left, then the resultant value becomes 11000000. Figure 5.5 shows the working of left shift operation:

![](bbox=[0.169, 0.353, 0.718, 0.489])

Figure 5.5: Displaying the Left Shift Operation

Listing 5.37 shows the code for left shift in C:

# Listing 5.37: Showing the Code for Left Shift

```
```c
#include<stdio.h>
int main()
{
    int varA = 174;
    varA = varA << 5;
    printf("\n The result after shifting 5 bits to the left [%d] ",varA);
    getch();
    return 0;
}
```
```

Output of the preceding program is as follows:

The result after shifting 5 bits to the left [5568]

The decimal representation of 10101110 becomes 174. After shifting the number 5 places to its left, the result becomes 5568 in the 32-bit decimal representation.

Let’s take a look at the code that converts a given decimal number to its 16-bit binary notation, as shown in Listing 5.38:

# Listing 5.38: Showing the Binary Representation of Variables

```
```c
#include<stdio.h>
int main()
{
    int varA ,i,mask,bitPos;
    printf("\nEnter any decimal number -> ");
    scanf("%d",&varA);
```
```