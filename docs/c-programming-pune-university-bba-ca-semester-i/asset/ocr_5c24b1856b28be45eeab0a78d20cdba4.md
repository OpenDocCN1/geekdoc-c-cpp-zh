# 7) Write a program on Sum of given N Numbers.

+   **Algorithm:**
+   
+   1. Initialize: `sum = 0`
+   2. Run a loop from `I = 1` to `N` and do following in loop.
+      - Read `M`
+      - `sum = sum + M`
+   3. Display `sum`
+   4. Stop

```
**Program:**

```c
#include<stdio.h>
#include<stdlib.h>
Int main()
{
        Int N, M, i , sum;
        sum = 0; /* read the number */
        Printf("Enter number to sum:");
        Scanf("%d", &N);
        for(i=1; i<=N; i++)
        {
                Printf("Enter number");
                Scanf("%d", &M);
                sum = sum + M;
        }
        printf("sum of given numbers is %d\n", sum);
        getch();
        return 0;
}
```
```

```
**Output:**

```text
Enter number to sum: 3
Enter number 10
Enter number 20
Enter number 30
sum of given numbers is 60
```
```