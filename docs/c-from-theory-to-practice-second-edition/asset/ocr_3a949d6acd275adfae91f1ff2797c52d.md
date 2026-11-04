```
putchar(arr[ch-'A']); /* The output digit depends on the value of ch. For example, if the user enters 'I' the output would be arr[73-65] = 4. */
}
else if(ch >= '0' && ch <= '9')
{
    dig++;
    putchar(ch); /* A digit is displayed as is. */
}
else
{
    printf("Error: Not valid character\n");
    return 0;
}
if(dig == 10)
    break;
}
if(dig == 10)
    printf("\nNumber completed\n");
return 0;
}
```

# C.97

Write a program that reads the digits of a number as characters and displays its value. If the user enters a sign, it should be taken into account. Space characters are allowed only before the number, not between digits. Also, the program should check that the number of digits is up to 10.

```
#include <stdio.h>
int main(void)
{
    int ch, sign, val, dig;

    sign = '+';
    dig = 0;
    val = 0; /* val remains 0 until the user enters the first digit. Then, if the user enters a non-digit character the program terminates. */
    printf("Enter number: ");
    while ((ch = getchar()) != '\n' && ch != EOF)
    {
        if(ch == ' ' || ch == '\t')
        {
            if(val != 0)
            {
                printf("Error: No spaces between digits\n");
                return 0;
            }
        }
        else if(ch == '+' || ch == '-')
        {
            if(val != 0)
            {
                printf("Error: No signs between digits\n");
                return 0;
            }
        }
```