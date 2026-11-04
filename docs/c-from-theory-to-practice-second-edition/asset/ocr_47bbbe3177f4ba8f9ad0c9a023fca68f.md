```
```c
i = j = a[0]+2; /* The values of i and j become equal to 4. */
a[i+j] = 300; /* Since i+j = 4+4 = 8, the value of the ninth element becomes 300. */
b[i+1] = a[j]; /* The value of the sixth element of array b becomes equal to the value of the fifth element of array a.*/
```
```

Avoid side effects in indexing. For example, don't write something like this: b[i] = a[i++]; It depends on the compiler when i is incremented.

![](bbox=[0.12, 0.38, 0.18, 0.46])

> A popular error made by novice programmers is to forget that index numbering starts from 0. Just remember, in an array of n elements, the first element is stored in position 0, and the last one in position n-1, not n.

Another common error occurs when we want to copy one array into another. For example, it looks pretty natural to write b = a; However, this plausible assignment is illegal. In Chapter 8 and when investigating the close relationship between arrays and pointers, you'll see why. The simplest way to make the copy is to use a loop and copy the elements one by one or use a copy function, such as memcpy().

The following program declares an array of five integers, assigns the values 10, 20, 30, 40, and 50 to its elements, and displays those greater than 20.

```
```c
#include <stdio.h>
int main(void)
{
    int i, arr[5];

    arr[0] = 10;
    arr[1] = 20;
    arr[2] = 30;
    arr[3] = 40;
    arr[4] = 50;
    for (i = 0; i < 5; i++)
    { /* The braces are not necessary; we use them to make the code clearer. */
        if(arr[i] > 20)
            printf("%d\n", arr[i]);
    }
    return 0;
}
```
```

![](bbox=[0.12, 0.88, 0.18, 0.96])

> C does not check if the index is out of the array bounds. It is the programmer's responsibility to ensure that this won't happen. If it does, the behavior of the program is unpredictable.

For example, in the previous program, the valid indexes are from 0 to 4. However, if you write arr[5] = 500; the compiler won't raise an error message; it allows the execution of the program. In fact, this statement changes the content of the memory address just after the end of the array. If this memory is used by another variable, overwriting its