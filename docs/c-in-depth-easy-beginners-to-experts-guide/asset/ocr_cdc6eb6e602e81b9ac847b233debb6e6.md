if this condition is valid (True). If the condition becomes invalid (false) then the loop will terminate.

Run every time command’ section will be performed in every loop cycle. We use this part to reach the final condition for terminating the loop.

For example we can increase or decrease loop variable’s value in a way that after specified number of cycles the loop condition becomes invalid and “for loop” can terminate.

At this step we rewrite example 3-1 with for loop. Just pay attention that we no more need I=I+1 for increasing loop variable. It is now included inside “for loop” condition phrase (i++).

# Example –

```
#include<stdio.h>
#include<conio.h>
    main()
    {
    int i=0;
    for(i=0;i<100;i++ )
    printf("ni=%d",i);
    system("pause");
    }
```

# Drill Note- Stdio.h – Standard Input Output.

# Drill Note- Conio.h – Console Input Output.

# Drill Note- Essentially all you need to remember the two semicolon characters that must separate the three parts of the construct.

# Example –

Write a program that gets temperatures of week days and calculate average temperature for that week.

```
#include<stdio.h>
```