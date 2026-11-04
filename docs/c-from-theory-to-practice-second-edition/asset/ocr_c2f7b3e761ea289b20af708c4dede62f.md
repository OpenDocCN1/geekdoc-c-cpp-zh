> *To save space, we won’t repeat its code in the programs that use it. We’ll just add its prototype to remind you how it is used.*

An unexpected behavior that makes many novice programmers wonder why their program does not work correctly arises when the program reads a string after having read a numerical value. In C.9, we saw a quite similar example. As another example, suppose that the user enters an integer and presses Enter. What does the program output?

```
```c
#include <stdio.h>
int main(void)
{
    char str[100];
    int num;

    printf("Enter number: ");
    scanf("%d", &num);

    printf("Enter text: ");
    fgets(str, sizeof(str), stdin);

    printf("%d %s\n", num, str);
    return 0;
}
```
```

scanf() reads the integer and stores it in num. The new line character generated when Enter is pressed is stored in stdin, and fgets() will read it and store it in str. Since fgets() terminates once the new line character is read, the user cannot enter more characters. Therefore, the program outputs only the input number. A solution is to use getchar() before fgets(), in order to read the new line character.

# Exercises

C.10.6 Write a program that reads a string of less than 100 characters and displays the number of its characters, the number of 'b' occurrences, and the input string after replacing the space character with the new line character and 'a' with 'p'. Don't use the return value of read_text().

```
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
```
```