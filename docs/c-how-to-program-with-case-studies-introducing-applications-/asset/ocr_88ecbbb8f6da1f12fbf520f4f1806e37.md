**Sample shuffled array**

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 19 | 40 | 27 | 25 | 36 | 46 | 10 | 34 | 35 | 41 | 18 | 2 | 44 |
| 1 | 13 | 28 | 14 | 16 | 21 | 30 | 8 | 11 | 31 | 17 | 24 | 7 | 1 |
| 2 | 12 | 33 | 15 | 42 | 43 | 23 | 45 | 3 | 29 | 32 | 4 | 47 | 26 |
| 3 | 50 | 38 | 52 | 39 | 48 | 51 | 9 | 5 | 37 | 49 | 22 | 6 | 20 |

You may want your program to call the shuffle function several times to ensure a satisfactory shuffle.

Although the approach in this problem improves the shuffling algorithm, the dealing algorithm still requires searching the deck array for card 1, then card 2, then card 3, and so on. Worse yet, even after the dealing algorithm locates and deals the card, the algorithm still searches through the remainder of the deck. Modify the program of Fig. 7.16 so that once a card is dealt, no further attempts are made to match that card number, and the program immediately proceeds with dealing the next card. In Chapter 10, we develop a dealing algorithm that requires only one operation per card.

**7.17** What does this program do, assuming the user enters two strings of the same length?

```
```c
// ex07_19.c
// What does this program do?
#include <stdio.h>
#define SIZE 80

void mystery1(char *s1, const char *s2); // prototype

int main(void) {
    char string1[SIZE]; // create char array
    char string2[SIZE]; // create char array

    puts("Enter two strings: ");
    scanf("%39s%39s", string1, string2);
    mystery1(string1, string2);
    printf("%s", string1);
}

// What does this function do?
void mystery1(char *s1, const char *s2) {
    while (*s1 != '\0') {
        ++s1;
    }

    for (; *s1 = *s2; ++s1, ++s2) {
        ; // empty statement
    }
}
```
```