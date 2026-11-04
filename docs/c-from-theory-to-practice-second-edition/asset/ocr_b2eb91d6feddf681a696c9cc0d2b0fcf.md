As a result, the purpose of this program is to calculate the product of the input numbers through the use of a recursive function.

# C.11.51

Write a recursive function that uses the strchr() function (see its description in Appendix C) to display the number of occurrences of a character inside a string. Write a program that reads a string of less than 100 characters and a character and calls the function. Don’t rush to see the answer, try it.

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);
void find(char *p, int ch, int cnt);

int main(void)
{
    char ch, str[100];

    printf("Enter text: ");
    read_text(str, sizeof(str), 1);

    printf("Enter character: ");
    ch = getchar();
    find(str, ch, 0);
    return 0;
}

void find(char *p, int ch, int cnt)
{
    p = strchr(p, ch);
    if(p == NULL)
        printf("%d\n", cnt);
    else
        find(p+1, ch, cnt+1);
}
```

# C.11.52

Sometimes, in math, it is very difficult to prove some problems that seem quite simple, like the one of the mathematician Lothar Collatz, who first proposed it. Think of a positive integer n and execute the following algorithm:

+   a. If it is even, divide it by two (n/2).
+   b. If it is odd, triple it and add one (3n+1).

Repeat the same process for each produced number and you’ll come to a surprising result: for any integer you choose, you’ll always end up with ...!!! For example, if we choose the number 53, the produced numbers are 53 -> 160 -> 80 -> 40 -> 20 -> 10 -> 5 -> 16 -> 8 -> 4 -> 2 -> 1

This math problem, well known as “Collatz conjecture,” remains unsolved, although the use of computing machines confirms that for any positive integer up to 2^60, we’ll eventually reach 1.