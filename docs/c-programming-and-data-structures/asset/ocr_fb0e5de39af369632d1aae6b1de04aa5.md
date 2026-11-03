# Pseudocode

```
BEGIN
DEFINE: Long Integer cp, sp
DISPLAY: "Enter the cost price and selling price of an item: "
READ: cp, sp
IF: sp>cp
    DISPLAY: "There is a profit of 'sp-cp'"
ELSE
    IF: cp>sp
        DISPLAY: "There is a loss of 'cp-sp'"
    ELSE
        DISPLAY: "No profit no loss!"
    END IF
END IF
END
```

# Program

```
#include <stdio.h>
#include <conio.h>

void main()
{
    long cp, sp;
    clrscr();
    printf("\nEnter the cost price and selling price of an item: ");
    scanf("%ld\n%ld", &cp, &sp);  /*Reading CP and SP*/
    if(sp>cp)  /*Checking condition of profit*/
        printf("\nThere is a profit of %ld units", sp-cp);
    else if(cp>sp)  /*Checking condition of loss*/
        printf("\nThere is a loss of %ld units", cp-sp);
    else
        printf("\n\nNo Profit No Loss!");
    getch();
}
Output
Enter the cost price and selling price of an item: 24
30

There is a profit of 6 units
```

Fig. 1.53 Solution for calculating profit and loss

# EXAMPLE 1.18 Design and develop the solution for finding the area of a circle.

# Solution

# Algorithm

+   Step 1 - Start
+   Step 2 - Accept the radius of the circle from the user (radius)
+   Step 3 - Calculate area of the circle using formula area = 3.14 * radius * radius
+   Step 4 - Display the computed area of the circle
+   Step 5 - Stop