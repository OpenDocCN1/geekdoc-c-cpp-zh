```
printf("%4d\n",x);
printf("%4d\n",x);
```

c.

```
char ch = 's';

while (ch < 'w')
{
    printf("%c", ch);
    ch++;
}
printf("%c\n",ch);
```

# 11. What will the following program print?

```
#define MESG "COMPUTER BYTES DOG"
#include <stdio.h>
int main(void)
{
    int n = 0;

    while ( n < 5 )
        printf("%s\n", MESG);
        n++;
    printf("That's all.\n");
    return 0;
}
```

# 12. Construct statements that do the following (or, in other terms, have the following side effects):

+   a. Increase the variable x by 10.

+   b. Increase the variable x by 1.

+   c. Assign twice the sum of a and b to c.

+   d. Assign a plus twice b to c.

# 13. Construct statements that do the following:

+   a. Decrease the variable x by 1.

+   b. Assigns to m the remainder of n divided by k.