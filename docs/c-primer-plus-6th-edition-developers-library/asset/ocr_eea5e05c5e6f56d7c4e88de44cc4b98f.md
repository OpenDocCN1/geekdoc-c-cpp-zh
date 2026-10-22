This is fine. You can have only one defining declaration of a variable. But the declaration with extern is a reference declaration, and you can have as many of those as you want.

The program using roll_n_dice() should also include this header file. Not only does this provide the prototype for roll_n_dice(), it also makes roll_count available to that program. Listing 12.13 illustrates these points.

# Listing 12.13 The manydice.c File

```
/* manydice.c -- multiple dice rolls */
/* compile with diceroll.c */
#include <stdio.h>
#include <stdlib.h>          /* for library srand() */
#include <time.h>            /* for time() */
#include "diceroll.h"        /* for roll_n_dice() */
/* and for roll_count */
int main(void)
{
    int dice,roll;
    int sides;

    srand((unsigned int) time(0)); /* randomize seed */
    printf("Enter the number of sides per die, 0 to stop.\n");
    while (scanf("%d", &sides) == 1 && sides > 0 )
    {
        printf("How many dice?\n");
        if ((status =scanf("%d", &dice)) != 1)
        {
            if (status == EOF)
                break;          /* exit loop */
            else
            {
                printf("You should have entered an integer.");
                printf(" Let's begin again.\n");
                while (getchar() != '\n')
                    continue;   /* dispose of bad input */
                printf("How many sides? Enter 0 to stop.\n");
                continue;       /* new loop cycle */
            }
        }
        roll = roll_n_dice(dice, sides);
        printf("You have rolled a %d using %d %d-sided dice.\n",
               roll, dice, sides);
        printf("How many sides? Enter 0 to stop.\n");
    }
    printf("The rollem() function was called %d times.\n",
           roll_count);       /* use extern variable */
```