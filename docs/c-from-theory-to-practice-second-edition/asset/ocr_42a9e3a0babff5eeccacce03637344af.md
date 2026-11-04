# C.10.18 What is the output of the following program?

```
#include <stdio.h>
#include <string.h>
int main(void)
{
    char str[] = "csfbl", *p = str;
    while(*p)
    {
        --*p; /* To make it harder, we could merge the two statements into --*p++; */
        p++;
    }
    printf("%s\n", p-strlen(str));
    return 0;
}
```

Answer: The statement --*p; decreases the content of the address that p points to. For example, in the first iteration, p points to the first character of the string, that is, 'c'. Therefore, *p is equal to 'c' and the statement --*p; changes the value of str[0] and makes it equal to the previous character in the ASCII set. Therefore, str[0] becomes 'b'. Next, p is increased and points to the next element of str. In the same way, the next iterations make str[1], str[2], str[3], and str[4] equal to 'r', 'e', 'a', and 'k', respectively.

The loop terminates once p becomes equal to str+5, that is, once the null character is met. Since strlen() returns the length of the string, the expression p-strlen(str) is equivalent to str+5-5 = str. Therefore, the program displays the new string stored into str, that is, break. Indeed, have a break before moving on to the next exercise.

# C.10.19 What is the output of the following program?

```
#include <stdio.h>
#include <string.h>
int main(void)
{
    char str[] = "Text", *p = str;
    int i;
    for(i = 0; i < strlen(str)-1; i++, p++)
        printf("%c", p[i]);
    return 0;
}
```

Answer: Since strlen() returns 4, the loop is executed three times. Let's trace the iterations:

First iteration (i = 0): The value of p[0] is displayed, that is, T.
Second iteration (i++ = 1): Since p is incremented by one, p points to the second character of the string, that is, 'e'. Since we handle p as an array, p[0] is 'e' and p[1] is 'x'. Therefore, the program outputs x.