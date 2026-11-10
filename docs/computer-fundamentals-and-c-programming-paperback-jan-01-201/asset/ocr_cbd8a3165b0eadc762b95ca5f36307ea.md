```
```c
/* all_about_char.c: Handling the char data type and escape sequences. */

#include <stdio.h>

int main(void)
{
    char schar = 250;
    unsigned char uchar = 250;
    char letter = 'A'; int numeral = '9';

    printf("schar = %d\n", schar);    /* Know char default on your system */
    printf("uchar = %d\n", uchar);

    /* Printing the entire alphabet in uppercase */
    while (letter <= 'Z') {             /* Using 'Z' instead of its ASCII value */
        printf("%c ", letter);          /* makes the code portable. */
        letter++;                        /* This is the letter + 1 */
    }

    printf("\n\t\tNext line starts after 16 spaces and also beeps\07\n");
    /* Printing all digits of the base-10 system in reverse */
    while (numeral >= '0') {             /* This code is also portable because */
        printf("%c ", numeral);          /* '0' is used instead of ASCII value. */
        numeral--;                       /* This is numeral = numeral - 1 */
    }
    return 0;
}
```
```

# PROGRAM 5.5: **all_about_char.c**

```
```text
schar = -6                                      Machine uses signed char by default
uchar = 250
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
             Next line starts after 16 spaces and also beeps
9 8 7 6 5 4 3 2 1 0
```
```

# PROGRAM OUTPUT: **all_about_char.c**

Between the two loops, a **printf** statement demonstrates the use of the \ and escape sequences. A \t shifts the cursor by eight spaces, so using two of them offsets the line by 16 spaces. If your terminal supports the beep sound, you’ll hear a beep as well (\07).

> **Note:** You must know the distinction between 'A', 'APE', "A" and "APE". 'A' is a character constant whose ASCII value (65) is stored as a binary number. 'APE' is not a valid character constant because only the last character ('E') is stored. "A" and "APE" are legal strings, occupying *two* and *four* characters in memory, respectively. Why an extra character for the strings? Read on.