# LESSON 7: Fundamentals of Reading and Writing Information

Table 7.1 lists C's most commonly used escape sequences. Listing 7.1 demonstrates some of the frequently used escape sequences.

# Input

LISTING 7.1 escape.c: Using printf() Escape Sequences

```
/* Demonstration of frequently used escape sequences */
#include <stdio.h>
#define QUIT 3

int get_menu_choice( void );
void print_report( void );

int main( void ) {
    int choice = 0;

    printf("\nW'd like to welcome you to the menu program\\n");
    printf("\Are you ready to make a choice?\n");
    while (choice != QUIT) {
        choice = get_menu_choice();
        if (choice == 1) {
            printf("\nbeeping the computer\a\a\a");
        } else {
            if (choice == 2) {
                print_report();
            }
            printf("nYou choose to quit!\n");
        }
        return 0;
    }
}

int get_menu_choice( void ) {
    int selection = 0;
    do {
        printf("\n");
        printf("\n1 - Beep Computer");
        printf("\n2 - Display Report");
        printf("\n3 - Quit");
        printf("\n");
```