# EXAMPLE A.1 Write a program for demonstrating the use of symbolic constants.

```
Program
```c
/*Program for demonstrating use of Symbolic Constants*/
#include <stdio.h>
#include <conio.h>
#define CP 50 /*Defining Symbolic Constant for Cost Price*/

void main() {
    int SP, profit;
    clrscr();
    printf("Enter the SELLING PRICE ");
    scanf("%d", &SP);
    profit=SP-CP; /*Using Symbolic Constant CP in an expression*/
    printf("\nThe profit earned is %d", profit);
    getch();
}
```
```

Output
Enter the SELLING PRICE 65

The profit earned is 15

# EXAMPLE A.2 Write a program that reads a date in the dd/mm/yyyy format and determines whether the entered date is correct or not.

```
Program
```c
/*Program for demonstrating the use of scanf function*/
#include <stdio.h>
#include <conio.h>
```
```