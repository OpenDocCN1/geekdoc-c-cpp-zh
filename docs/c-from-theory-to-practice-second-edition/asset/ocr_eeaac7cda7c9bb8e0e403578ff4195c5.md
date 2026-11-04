C.6.23 Write a program that reads an integer that corresponds to a number of lines. The program should display in each line a number of '*' equal to the line number. For example, if the user enters 5 the program should display:

```
```
*
* *
* * *
* * * *
* * * * *
```
```

```
```c
#include <stdio.h>
int main(void)
{
    int i, j, lines;

    printf("Enter lines: ");
    scanf("%d", &lines);

    for(i = 0; i < lines; i++)
    {
        for(j = 0; j <= i; j++)
            printf("* "); /* Add a space character after '*' . */
        printf("\n"); /* Change line to display the next group of
                         '*' . */
    }
    return 0;
}
```
```

Comments: Suppose that the user enters 5. Let’s explain the code by tracing the first two iterations of the outer loop.

+   - *First iteration of the outer loop (i=0):* Since the condition (i < 5) is true, the inner loop is executed.
+     - *First iteration of the inner loop (j=0):* Since the condition (j <= i) is true, the program displays *.
+     - *Second iteration of the inner loop (j=1):* Now, the condition is false; the loop terminates and printf() changes line.
+   - *Second iteration of the outer loop (i=1):* Since the condition (i < 5) is true, the inner loop is executed.
+     - *First iteration of the inner loop (j=0):* Since the condition (j <= i) is true, the program displays * and leaves a space.
+     - *Second iteration of the inner loop (j=1):* Another * is displayed.
+     - *Third iteration of the inner loop (j=2):* Now, the condition is false; the loop terminates and printf() changes line.

So far, the program has displayed:

```
```
*
* *
```
```

The following lines are produced in a similar way.