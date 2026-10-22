10. Consider the following declaration:

```
double mint[10];
```

+   a. What is the array name?
+   b. How many elements does the array have?
+   c. What kind of value can be stored in each element?
+   d. Which of the following is a correct usage of scanf() with this array?
+     i. scanf("%lf", mint[2])
+     ii. scanf("%lf", &mint[2])
+     iii. scanf("%lf", &mint)

11. Mr. Noah likes counting by twos, so he’s written the following program to create an array and to fill it with the integers 2, 4, 6, 8, and so on. What, if anything, is wrong with this program?

```
#include <stdio.h>
#define SIZE 8
int main(void)
{
    int by_twos[SIZE];
    int index;

    for (index = 1; index <= SIZE; index++)
        by_twos[index] = 2 * index;
    for (index = 1; index <= SIZE; index++)
        printf("%d ", by_twos[index]);
    printf("\n");
    return 0;
}
```

12. You want to write a function that returns a long value. What should your definition of the function include?

13. Define a function that takes an int argument and that returns, as a long, the square of that value.

14. What will the following program print?

```
#include <stdio.h>
int main(void)
{
    int k;
```