
Notice that free() is used to release dynamically allocated memory, not static. For example, if we declare ptr as an array (i.e., int ptr[100]), the program would fail again. Also, don't attempt to release an already released memory. In the following example, the second call to free() is wrong because the memory is already released:

```c
int *ptr = (int*) malloc(100*sizeof(int));
if(ptr != NULL)
{
    free(ptr);
    free(ptr);
}
```

![](img/b8da5dcf9ba7f1fad5213c453d095246_476_0.png)

Don't forget to call free() to release a dynamically allocated memory when no longer needed, in order to avoid memory leaks.

For example, is the following code well written?

```c
char *ptr = (char*) malloc(10);
strcpy(ptr, "test");
ptr = (char*) malloc(20);
printf("%c\n", *ptr);
free(ptr);
```

Since the first memory block was not released before ptr points to the second block, a memory leak is created; this memory remains unusable. The code outputs the value of the first character in that new memory. Be careful with memory leaks, otherwise you may end up with a program crash due to an out-of-memory error. Find the errors in the following program:

```c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    char *p1, *p2;

    p1 = (char*) malloc(10);
    p2 = (char*) malloc(10);
    if(p1 != NULL && p2 != NULL)
    {
        p1 = p2;
        free(p1);
        p2[0] = 'a';
        free(p2);
    }
    return 0;
}
```

- a. The statement p1 = p2; makes p1 and p2 point to the same memory. The statement free(p1); releases this memory, so the next statement assigns a value to a nonallocated memory.
- b. The statement free(p2); releases memory already released.
- c. The first block of memory pointed to by p1 was never released.

Need more practice? Find the errors in the following program:

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct
{
    int *i;
    char *c;
} test;

int main(void)
{
    test *t;
    int i;

    t = (test*) malloc(sizeof(test));
    t->i = (int*) malloc(10*sizeof(int));
    t->c = (char*) malloc(10);
    t->i[0] = 'a';
    t->c[5] = 50;
    for(i = 0; i < 10; i++)
        printf("%d %d\n", t->i[i], t->c[i]);
    free(t);
    free(t->i);
    free(t->c);
    return 0;
}
```

Are t->i[0] = 'a' or t->c[5] = 50 wrong? Certainly not, we just assign two integers. What about the loop? Nothing wrong with that; it uses array subscripting to display the existing values. What about the memory release? Well, here is the bug. First we have to release the memory allocated for the members of the structure and then the memory for the entire structure, not the other way around. Therefore, we must move free(t) to the end.

In large programs, where the same pointer may be used in different parts of the program, our advice is to make it NULL each time you free it for more safety. This practice helped us a lot when debugging programs with memory problems. See what happened to me once. One time, I used an array of some thousands of pointers to structures. I initialized them with NULL and memory was allocated for some of them during program execution. So far, so good. Once in a while, memory was released in random order. After that, the program was crashing. And the worst part was that the program was crashing occasionally, not always. It was really a nightmare. After days of stress and hard debugging, we concluded that the crash was due to some pointer misuse (... what else?). Here is the buggy code:

```c
if(arr[i] != NULL)
    x = arr[i]->member;
```

The if condition didn't let a null pointer access the member. That's fine, but what about a pointer that used to point to a memory and that memory is later released? For example, suppose that the memory pointed to by some arr[i] is released. The condition is still true, because the fact that the memory is released does not mean that the value of arr[i] becomes NULL. Therefore, when using arr[i] to access the member, the program was crashing. The NULL value must be explicitly assigned, so when I added the statement arr[i] = NULL after releasing the memory, the problem was solved and we went straight for beers. Cheers!!!

## Memory Management Functions

This section discusses briefly the memcpy(), memmove(), and memcmp() functions that are often used for memory management. memcpy() is used to copy any type of data from one memory region to another. It is declared in string.h:

```c
void *memcpy(void *dest, const void *src, size_t size);
```

memcpy() copies size bytes from the memory pointed to by src to the address pointed to by dest. If the source and destination addresses overlap, its behavior is undefined. For example, the following program allocates memory to store the string "ABCDE" and displays its content:

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(void)
{
    char *arr;
    /* Allocate one extra byte for the null character. */
    arr = (char *) malloc(6);
    if(arr != NULL)
    {
        memcpy(arr, "ABCDE", 6);
        printf("%s\n", arr);
        free(arr);
    }
    return 0;
}
```

The main difference with strcpy() is that strcpy() stops copying when the null character is met. On the other hand, memcpy() does not stop copying until it copies the number of specified bytes. For example, if we have:

```c
char str2[6], str1[] = {'a', 'b', 'c', '\0', 'd', 'e'};
```

and write:

```c
memcpy(str2, str1, 6);
```

the content of str2 would be the same as of str1.

On the other hand, if we write:

```c
strcpy(str2, str1);
```

the content of str2 would be: {'a', 'b', 'c', '\0'}.

memmove() is similar to memcpy(), except that memmove() guarantees that the data will be copied correctly even if the source and destination memory overlap. Because memcpy() does not check if the two memory regions overlap, it is executed faster than memmove(). Notice that the size of the destination memory should be size bytes, at least. If it is not, the extra bytes would be written in a nonallocated memory, meaning that the existing data will be overwritten. For example, the next copy is wrong because the size of the destination memory is 3 bytes, while the copied bytes are 6:

```c
char str1[3], str2[] = "abcde";
memcpy(str1, str2, sizeof(str2));
```

> memcpy() is often very useful because it is usually implemented in a way that copying large blocks of data is probably accomplished faster than an iteration loop.

For example, the following program declares two arrays of 100000 integers, sets the values 1 to 100000 into the elements of the first array, and uses memcpy() to copy them into the second array:

```c
#include <stdio.h>
#include <string.h>

#define SIZE 100000

int main(void)
{
    int i, arr1[SIZE], arr2[SIZE];

    for(i = 0; i < SIZE; i++)
        arr1[i] = i+1;

    memcpy(arr2, arr1, sizeof(arr1));
    /* We use memcpy() instead of an iteration loop such as:
    for(i = 0; i < SIZE; i++)
        arr2[i] = arr1[i]; */
    for(i = 0; i < SIZE; i++)
        printf("%d\n", arr2[i]);
    return 0;
}
```

memcmp() is used to compare the data stored in one memory region with the data stored in another. It is declared in string.h:

```c
int memcmp(const void *ptr1, const void *ptr2, size_t size);
```

memcmp() compares size bytes of the memory regions pointed to by ptr1 and ptr2. The return value of memcmp() is as that of strcmp(). The main difference with strcmp() is that strcmp() stops comparing when it encounters the null character in either string; memcmp(), on the other hand, stops comparing only when size bytes are compared; it does not look for the null character. For example:

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
int main(void)
{
    char str1[] = {'a', 'b', 'c', '\0', 'd', 'e'};
    char str2[] = {'a', 'b', 'c', '\0', 'd', 'f'};
    if(strcmp(str1, str2) == 0)
        printf("Same\n");
    else
        printf("Different\n");
    if(memcmp(str1, str2, sizeof(str1)) == 0)
        printf("Same\n");
    else
        printf("Different\n");
    return 0;
}
```

Because strcmp() stops comparing when the null character is met, the program displays Same. On the contrary, memcmp() compares all bytes, and the program displays Different.

## Exercises

- C.14.1 How many bytes does the following malloc() allocate?

```c
double *ptr;
ptr = (double*) malloc(100*sizeof(*ptr));
```

Answer: Since ptr is a pointer to double, sizeof(*ptr) calculates the size of the double type, that is 8. Therefore, malloc() allocates 800 bytes.

- C.14.2 What is the output of the following program?

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
void test(char *p);
int main(void)
{
    char *p1, *p2;
    p1 = p2 = (char*) malloc(5);
```
