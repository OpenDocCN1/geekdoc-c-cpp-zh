# C.8.21

Use the ptr pointer and an iteration loop and complete the following program to decrement the arr elements by one. The program should display their sum, before it terminates. Use pointer arithmetic to process the array.

```
#include <stdio.h>
int main(void)
{
    int *ptr, sum, arr[5] = {11, 21, 31, 41, 51};
    ...
}
```

# Answer:

```
#include <stdio.h>
int main(void)
{
    int *ptr, sum, arr[5] = {11, 21, 31, 41, 51};

    sum = 0;
    for(ptr = arr; ptr < arr+5; ptr++)
    {
        --*ptr;
        sum += *ptr;
    }
    printf("Sum = %d\n", sum);
    return 0;
}
```

# Comments:

In the first iteration, the statement ptr = arr; makes ptr point to arr[0]. Therefore, *ptr is equal to arr[0], that is, 11. The statement --*ptr; is equivalent to --arr[0]; so arr[0] becomes 10. This value is added to sum.

In a similar way, the next iterations decrement the remaining elements by one and their values become 20, 30, 40, and 50, respectively. When the loop ends, sum is equal to the sum of the new values and the program outputs: Sum = 150

# C.8.22

Use the ptr pointer and complete the following program to read and store the grades of 50 students into arr and then display the array's values in reverse order. Use pointer arithmetic to process the array.

```
#include <stdio.h>

#define SIZE 50

int main(void)
{
    float *ptr, arr[SIZE];
    ...
}
```

# Answer:

```
#include <stdio.h>
```