Running Listing 6.2 produces the following output:

```
n = 5
Now n = 6
n = 6
Now n = 7
The loop has finished.
```

The variable n first acquires the value 7 on line 10 during the second cycle of the loop. However, the program doesn’t quit then. Instead, it completes the loop (line 11) and quits the loop only when the test condition on line 7 is evaluated for the third time. (The variable n was 5 for the first test and 6 for the second test.)

# while: An Entry-Condition Loop

The while loop is a conditional loop using an entry condition. It is called “conditional” because the execution of the statement portion depends on the condition described by the test expression, such as (index < 5). The expression is an entry condition because the condition must be met before the body of the loop is entered. In a situation such as the following, the body of the loop is never entered because the condition is false to begin with:

```
index = 10;
while (index++ < 5)
    printf("Have a fair day or better.\n");
```

Change the first line to

```
index = 3;
```

and the loop will execute.

# Syntax Points

When using while, keep in mind that only the single statement, simple or compound, following the test condition is part of the loop. Indentation is an aid to the reader, not the computer. Listing 6.3 shows what can happen if you forget this.

# Listing 6.3 The while1.c Program

```
/* while1.c -- watch your braces */
/* bad coding creates an infinite loop */
#include <stdio.h>
int main(void)
{
    int n = 0;
    while (n < 3)
```