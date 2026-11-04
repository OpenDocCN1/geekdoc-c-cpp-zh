# C.4.3 What is the output of the following program?

```
#include <stdio.h>
int main(void)
{
    int a = 4, b = 3, c = 5;

    printf("%d\n", (a < b) == !(c > b));
    return 0;
}
```

Answer: The value of the expression (a < b) is 0 because a is 4 and b is 3. Since the value of (c > b) is 1, the value of !(c > b) is 0. Since both expressions have the same value, the program displays 1.

# C.4.4 What is the output of the following program?

```
#include <stdio.h>
int main(void)
{
    int a = 10, b = -10;

    if(a > 0 && b < -10)
        printf("One ");
    else
        printf("Two ");

    if(a > 10 || b == -10)
        printf("One ");
    else
        printf("Two ");
    return 0;
}
```

Answer: Since b is -10, the second operand is false and the program outputs Two. Since the second operand in the second if statement is true, the program outputs One.

# C.4.5 What is the output of the following program?

```
#include <stdio.h>
int main(void)
{
    int a = 1, b = 4, c = 4;

    printf("%d\n", (a-1) || (b-- == c));
    printf("%d", (a > b) && (a-1 == b-3) && (c%2 || (a+b-c)));
    return 0;
}
```