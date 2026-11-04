
```
**pp += 100;

p = &j;
**pp += 100;
printf("%d\n", i+j);
return 0;
}
```

Answer: Since pp points to p and p points to i, **pp is equal to i. Therefore, the statement **pp += 100; is equivalent to i = i+100 = 10+100 = 110. The statement p = &j; makes p point to j, so **pp is equal to j. Therefore, the statement **pp += 100; is equivalent to j = j+100 = 20+100 = 120. As a result, the program displays 230.

## C.8.34 What are the values of a elements in the following program?

```
#include <stdio.h>
int main(void)
{
    int k = 0, b = 1, c = 2, d = 3, m, a[3];
    int *p[] = {&k, &b, &c, &d};
    for(m = 0; m < 3; m++)
        a[*p[m]] = **(p+m+1);
    return 0;
}
```

Answer: Since p[0] is equal to &k, p[1] equal to &b, p[2] equal to &c, and p[3] equal to &d, the values of *p[0], *p[1], *p[2], and *p[3] are 0, 1, 2, and 3, respectively. In the general case, p[m+1] is a pointer to the p[m+1] element. Let's trace the iterations:

First iteration (m=0): a[*p[0]] = **(p+1) = *p[1] = b, that is, a[0] = 1.

Second iteration (m=1): a[*p[1]] = **(p+2) = *p[2] = c, that is, a[1] = 2.

Third iteration (m=2): a[*p[2]] = **(p+3) = *p[3] = d, that is, a[2] = 3.

## C.8.35 Use p1 and complete the following program to read continuously an integer and output the word test a number of times equal to the absolute value of the input number. The program should use p2 to display the total number of the output words. If the user enters 0, the insertion of numbers should terminate. Use only for loops.

```
#include <stdio.h>
int main(void)
{
    int **p1, **p2, *p3, *p4, i, num, times;
    ...
}
```

Answer:

```
#include <stdio.h>
int main(void)
{
    int **p1, **p2, *p3, *p4, i, num, times;

    p3 = &num;
    p1 = &p3;

    p4 = &times;
    p2 = &p4;

    **p2 = 0;
    for(;;)
    {
        printf("Enter number: ");
        scanf("%d", *p1);
        if(**p1 == 0)
            break;
        if(**p1 < 0)
            **p1 = -**p1;
        for(i = 0; i < **p1; i++)
            printf("test\n");
        **p2 += **p1;
    }
    printf("Total number is = %d\n", **p2);
    return 0;
}
```

## Pointers and Two-Dimensional Arrays

Just as pointers are closely related to one-dimensional arrays, they are also related to multidimensional arrays. In this section, we'll focus on the most common case, that of two-dimensional arrays.

Recall from Chapter 7 that when a two-dimensional array is declared, its elements are stored in successive memory locations, starting with the elements of the first row, followed by the elements of the second row, and so on. For example, the following program declares a two-dimensional array and displays the memory addresses of its elements. Their distance is the size of the int type.

```
#include <stdio.h>
int main(void)
{
    int i, j, a[2][3];

    for(i = 0; i < 2; i++)
        for(j = 0; j < 3; j++)
            printf("Addr [%d][%d]:%p\n", i, j, &a[i][j]);

    return 0;
}
```

Also remember that C treats a two-dimensional array as a one-dimensional array, where each element is an array. For example, the elements of a are the a[0], a[1], and a[2], where each one is an array of three integers. In particular, C treats a[0] as an array and by subscripting its name we've got its elements, that is, a[0][0], a[0][1], and a[0][2]. Indeed, if we write sizeof(a[0]), the program outputs 12.

To process a two-dimensional array a[N][M] through pointer arithmetic, we use the name of each array a[0], a[1], ..., a[N-1] as a pointer to the first element of the respective row. For example, since a[0] can be used as a pointer to a[0][0], *a[0] is equal to a[0][0].

Since a[0] points to the first element, a[0]+1 can be used as a pointer to the second element, that is, a[0][1], and a[0]+2 as a pointer to the third element, that is, a[0][2]. In the general case, a[0]+j can be used as a pointer to the a[0][j] element of the first row. So, we have:

- a[0]+j is equivalent to &a[0][j].
- *(a[0]+j) is equivalent to a[0][j].

In a similar way, a[1]+j can be used as a pointer to the a[1][j] element of the second row. So, we have:

- a[1]+j is equivalent to &a[1][j].
- *(a[1]+j) is equivalent to a[1][j].

Therefore, in the general case, we have:

- a[i]+j is equivalent to &a[i][j].
- *(a[i]+j) is equivalent to a[i][j].

and because, as we know by now, a[i] is converted to *(a+i) we have:

- *(a+i)+j is equivalent to &a[i][j].
- *(*(a+i)+j) is equivalent to a[i][j].

An example of these equations is that a[0][0] is equivalent to *a[0] and **a. Essentially, when we write a[i][j] the compiler converts it to *(*(a+i)+j). To sum up, the following program uses three ways to display the elements of a two-dimensional array.

```
```c
#include <stdio.h>
int main(void)
{
    int i, j, a[2][3] = {10, 20, 30, 40, 50, 60};

    for(i = 0; i < 2; i++)
        for(j = 0; j < 3; j++)
        {
            printf("a[%d][%d]:%d ", i, j, a[i][j]);
            printf("a[%d][%d]:%d ", i, j, *(a[i]+j));
            printf("a[%d][%d]:%d\n", i, j, *(*(a+i)+j));
        }
    return 0;
}
```
```

We’d remove the outer loop and write: p = a+1; or equivalently p = &a[1];. The inner loop remains as is.

What about if we want to declare pointers to each row of the array? We could use an array of pointers. For example:

```
```c
#include <stdio.h>
int main(void)
{
    int i, a[4][2] = {10, 20, 30, 40, 50, 60, 70, 80}, *p[4] = {a[0],
a[1], a[2], a[3]};

    for(i = 0; i < 4; i++)
        printf("%d ", *(p[i]+1));
    return 0;
}
```
```

When initialized, each p element points to the first element of the respective row of a. For example, p[0] points to a[0][0] and p[0]+1 points to a[0][1]. Therefore, the program displays the values of the second column, that is, 20 40 60 80.

Before finishing a really tough section, the equivalent pointer expressions to access an element of up to a four-dimensional array are:

```
```c
arr[i] = *(arr+i)
arr[i][j] = *((arr+i)+j)
arr[i][j][k] = *(*((arr+i)+j)+k)
arr[i][j][k][l] = *(*(*(*(arr+i)+j)+k)+l)
```
```

## Exercises

### C.8.36 What does the following program do?

```
```c
#include <stdio.h>
int main(void)
{
    int i, arr[2][5] = {10, 20, 30, 40, 50, 60, 70, 80, 90, 100};

    for(i = 0; i < 2; i++)
        *(arr[i]+3) = 0;
    return 0;
}
```
```

**Answer:** In each iteration, arr[i] points to the first element of row i. The expression arr[i]+3 is a pointer to the fourth element of row i. Therefore, *(arr[i]+3) is equal to arr[i][3]. As a result, the program makes zero the elements of the fourth column, so, arr[0][3] and arr[1][3] become 0.

### C.8.37 What does the following program do?

```
```c
#include <stdio.h>
```

```
{
    int *p, arr[SIZE][SIZE] = {0};

    for(p = &arr[0][0]; p <= &arr[SIZE-1][SIZE-1]; p++)
    {
        if ((p-&arr[0][0])%(SIZE+1) == 0)
            *p = 1;
    }
    return 0;
}
```

Comments: Since the elements of the array are initialized with 0, it is sufficient to make the elements of the main diagonal equal to 1. The if condition checks if the element belongs to the diagonal. The form of that condition is based on the observation that the number of elements between two successive diagonal's elements is SIZE. For example, in the 5×5 array, the elements of the diagonal are in positions 0, 6, 12, 18, and 24.

Also, with this example, we want to show you that it is perfectly legal to treat one two-dimensional as if it were one-dimensional. We exploit the fact that the elements are stored in successive positions in memory.

## C.8.40 Write a program that assigns random integers to a 3×5 array and displays the minimum and the maximum value of each row and column. Use pointer arithmetic to process the array.

```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define ROWS 3
#define COLS 5

int main(void)
{
    int i, j, min, max, arr[ROWS][COLS];

    srand(time(NULL));
    for(i = 0; i < ROWS; i++)
    {
        min = max = *arr[i];
        for(j = 1; j < COLS; j++)
        {
            *(arr[i]+j) = rand();
            if(*(arr[i]+j) < min)
                min = *(arr[i]+j);
            if(*(arr[i]+j) > max)
                max = *(arr[i]+j);
        }
        printf("Row %d: Min=%d Max=%d\n", i+1, min, max);
    }
    for(i = 0; i < COLS; i++)
    {
        min = max = *(arr[0]+i);
        for(j = 1; j < ROWS; j++)
```
