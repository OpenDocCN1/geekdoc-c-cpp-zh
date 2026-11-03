I read this statement as “for ever.” With no items in the parentheses, but still with the required two semicolons, the for loop repeats eternally — even after the cows come home. Here’s the while loop equivalent:

```
while(1)
```

The value in the parentheses doesn’t necessarily need to be 1; any true or non-zero value works. When the loop is endless on purpose, however, most programmers set the value to 1 simply to self-document that they know what’s up.

You can see an example of an endless loop on purpose in the next section.

# Breaking out of a loop

Any loop can be terminated instantly — including endless loops — by using a break statement within the loop’s repeating group of statements. When break is encountered, looping stops and program execution picks up with the next statement after the loop’s final curly bracket. Listing 9-9 demonstrates the process.

# LISTING 9-9: Get Me Outta Here!

```
#include <stdio.h>

int main()
{
    int count;

    count = 0;
    while(1)
    {
        printf("%d ",count);
        count = count+1;
        if( count > 50)
            break;
    }
    putchar('\n');
    return(0);
}
```

The while loop at Line 8 is configured to go on forever, but the if test at Line 12 can stop it: When the value of count is greater than 50, the break statement (refer to Line 13) is executed and the loop halts.