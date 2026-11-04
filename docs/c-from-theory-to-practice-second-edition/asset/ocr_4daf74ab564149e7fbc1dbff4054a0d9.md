+   b. The statement free(p2); releases memory already released.
+   c. The first block of memory pointed to by p1 was never released.

Need more practice? Find the errors in the following program:

```
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
```

Are t->i[0] = 'a' or t->c[5] = 50 wrong? Certainly not, we just assign two integers. What about the loop? Nothing wrong with that; it uses array subscripting to display the existing values. What about the memory release? Well, here is the bug. First we have to release the memory allocated for the members of the structure and then the memory for the entire structure, not the other way around. Therefore, we must move free(t) to the end.

In large programs, where the same pointer may be used in different parts of the program, our advice is to make it NULL each time you free it for more safety. This practice helped us a lot when debugging programs with memory problems. See what happened to me once. One time, I used an array of some thousands of pointers to structures. I initialized them with NULL and memory was allocated for some of them during program execution. So far, so good. Once in a while, memory was released in random order. After that, the program was crashing. And the worse part was that the program was crashing occasionally, not always. It was really a nightmare. After days of stress and hard debugging, we concluded that the crash was due to some pointer misuse (... what else?). Here is the buggy code:

```
```c
if(arr[i] != NULL)
    x = arr[i]->member;
```
```

The if condition didn't let a null pointer access the member. That's fine, but what about a pointer that used to point to a memory and that memory is later released? For example,