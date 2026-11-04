
```c
    printf("\nSecond array\n");
    for(p2 = arr2; p2 < arr2+SIZE; p2++)
    {
        printf("Enter number: ");
        scanf("%d", p2);
    }
    for(p1 = arr1; p1 < arr1+SIZE; p1++)
    {
        for(p2 = arr2; p2 < arr2+SIZE; p2++)
        {
            if(*p1 == *p2)
                printf("Common element:%d found in positions %d and %d\n", *p1, p1-arr1+1, p2-arr2+1);
        }
    }
    return 0;
    }
```

### C.8.27 Use the p1 and p2 pointers and complete the following program to read the codes of 100 products and store them into arr. The program should store a code in the array only if it is not already stored. If the user enters -1, the insertion of codes should terminate. The program should display the codes of the stored products, before it terminates. Use pointer arithmetic to process the array.

```c
#include <stdio.h>

#define SIZE 100

int main(void)
{
    int *p1, *p2, arr[SIZE];
    ...
}
```

**Answer:**

```c
#include <stdio.h>

#define SIZE 100

int main(void)
{
    int *p1, *p2, arr[SIZE];

    p1 = arr;
    while(p1 < arr+SIZE)
    {
        printf("Enter code %d: ", p1-arr+1);
        scanf("%d", p1);
        if(*p1 == -1)
            break;

        for(p2 = arr; p2 < p1; p2++)  /* Traverse the array to check
if the input code is already stored. */
        {
            if(*p1 == *p2)
            {
                printf("Error: Code %d exists\n", *p1);
                break;
            }
        }
        /* If the code is not stored, increase the pointer. */
        if(p2 == p1)
            p1++;
    }
    /* Display the codes. */
    for(p2 = arr; p2 < p1; p2++)
        printf("C: %d\n", *p2);
    return 0;
}
```

### C.8.28 What are the values of arr elements in the following program?

```c
#include <stdio.h>
int main(void)
{
    int *ptr, arr[5] = {20};

    for(ptr = arr+1; ptr < arr+4; ptr++)
        *ptr = *(ptr-1) + *(ptr+1) + 1;
    return 0;
}
```

**Answer:** When arr is declared, arr[0] becomes 20 and the remaining elements are set to 0. The statement ptr = arr+1; makes ptr point to arr[1]. In each loop iteration, the statement ptr++ makes it point to the next element. The value of the current element becomes equal to the value of the previous element, plus the value of the next element, plus one. For example, in the first iteration, the statement is equivalent to: arr[1] = arr[0]+arr[2]+1 = 21; As a result, the values of arr[0] up to arr[3] will be 20 to 23, and arr[4] equal to 0.

### C.8.29 What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    int a[] = {0, 0, 1, 2, 3}, b[] = {0, 0, 4, 5, 6};
    int *ptr1 = a, *ptr2 = b;

    while(!*ptr1++ && !*ptr2++)
        ;
    printf("%d %d\n", *(b+(ptr1-a)), *(a+(ptr2-b)));
    return 0;
}
```

**Answer:** Yes, you need pen and paper to decipher it. It is a tough one, indeed; sorry to be pushing you. Let's trace the iterations:

```c
p[0] = &i;
p[1] = &j;
p[2] = &k;
printf("%d %d %d\n", *p[0], *p[1], *p[2]);
return 0;
}
```

The statement p[0] = &i; makes p[0] point to the address of i, so the value of *p[0] is equal to i. Similarly, *p[1] is equal to j and *p[2] equal to k. Therefore, the program outputs: 100 200 300.

Although we'll talk about strings in Chapter 10, an array of pointers is often used in place of a two-dimensional array to handle strings. One reason is to save memory. For example, the declaration:

```c
char names[][12] = {"First name", "Second name", "Third"};
```

allocates 12 bytes for each row, no matter what the length of the strings is. On the other hand, if we use an array of pointers:

```c
char *names[] = {"First name", "Second name", "Third"};
```

the allocated memory matches the length of each string. The elements of the array are pointers to the respective strings. Because of the diverse right-hand ends, this array is often called a *ragged* string array. Let's make a simple question, what is the size of this names array? Easy, count the characters and answer it. Please, read the answer at the next page only if you are absolutely sure; count carefully.

And because we told you to count the characters you did that? Lucky you are, we didn't choose lengthy strings... Here is the answer. Assuming that each pointer allocates 4 bytes, and the array contains three elements, its size is 12 bytes, no matter what the length of the strings is.

Besides saving memory, the use of an array of pointers to handle strings may improve the performance of the program. C.10.37 is such an example.

## Exercises

- C.8.30 What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    int *p[3], i, num;

    for(i = 0; i < 3; i++)
    {
        printf("Enter number: ");
        scanf("%d", &num);
        p[i] = &num;
    }
    for(i = 0; i < 3; i++)
        printf("Num: %d\n", *p[i]);
    return 0;
}
```

Answer: The statement p[i] = &num; makes each element of p to point to the address of num. Since all three pointers point to the same address, their content would be equal to the last value of num. Therefore, the second loop outputs three times the last input value.

- C.8.31 What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    int *p[3], i, arr[4] = {10, 20, 30, 40};

    for(i = 0; i < 3; i++)
    {
        p[i] = &arr[i]+1;
        printf("%d ", *p[i]);
    }
    return 0;
}
```

Answer: The statement p[i] = &arr[i]+1; makes each element of p point to the address of the next element after arr[i]. Therefore, when i is 0, p[0] points to arr[1], when it is 1, p[1] points to arr[2], and when it is 2, p[2] points to arr[3]. Therefore, the program displays: 20 30 40.

### C.8.32 The converse of the famous Pythagoras Theorem says that if a triangle has sides of length a, b and c, and if:

- $a^2 + b^2 = c^2$, the triangle is right
- $a^2 + b^2 > c^2$, the triangle is obtuse
- $a^2 + b^2 < c^2$, the triangle is acute

Write a program that uses an array of pointers to read the lengths of a, b, and c sides and determine the type of the triangle. The program should force the user to enter a value for c greater than the other two.

```c
#include <stdio.h>
int main(void)
{
    int *p[3], i, j, k;

    p[0] = &i;
    p[1] = &j;
    p[2] = &k;

    printf("Enter length_a and length_b: ");
    scanf("%d%d", p[0], p[1]);
    do
    {
        printf("Enter length_c: ");
        scanf("%d", p[2]);
    } while((*p[2] <= *p[0]) || (*p[2] <= *p[1]));

    if((*p[0])*(*p[0]) + (*p[1])*(*p[1]) == (*p[2])*(*p[2]))
        printf("Right triangle\n");
    else if((*p[0])*(*p[0]) + (*p[1])*(*p[1]) > (*p[2])*(*p[2]))
        printf("Acute triangle\n");
    else
        printf("Obtuse triangle\n");
    return 0;
}
```

## Pointer to Pointer

Just like an ordinary variable, when a pointer variable is declared, the compiler allocates memory to store its value. Therefore, we can declare another pointer variable to point to this memory address. To declare a pointer to a pointer variable, we use the * twice. For example, the statement:

```c
int **pp;
```

declares pp as a pointer to another pointer that points to `int`.

To use a pointer to a pointer variable, the single * provides access to the address of the second pointer, while the double ** provides access to the content of the address that the second pointer points to. For example:

```c
#include <stdio.h>
int main(void)
{
    int *p, **pp, i = 20;

    p = &i;
    pp = &p;
    printf("%d\n", **pp);
    return 0;
}
```

Since pp points to the address of p, *pp is equal to p. Since p points to the address of i, **pp is equal to i and the program displays 20.

The most usual application of a pointer to a pointer variable is when we want a function to be able to modify the value of a pointer argument. In Chapter 14, pay attention to the example in the comments of C.14.11. In general, you are allowed to declare a pointer to a pointer to another pointer variable and so on, such as ***pP, but in practice, it is rarely needed to exceed a depth of two. Let's see an example that combines all together an array, array of pointers, and pointer to a pointer.

```c
#include <stdio.h>
int main(void)
{
    int a[] = {10, 20, 30}, *p[] = {a, a+1, a+2}, **pp;

    for(pp = p; pp < p+3; pp++)
        printf("%d ", **pp);
    return 0;
}
```

Initially, pp points to p[0] which points to the address of a[0]. Therefore, **pp is equal to a[0]. When increased, pp points to p[1] which points to a[1]. As a result, the program displays: 10 20 30.

## Exercises

### C.8.33 What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    int *p, **pp, i = 10, j = 20;

    p = &i;
    pp = &p;
```
