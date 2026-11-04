These three members have no relation with the respective members of the company type. As another example, check the following declarations:

```
```c
int a;
struct S1 {int a[5]; } s1;
struct S2 {int *a; } s2;
```
```

Next, you'll learn that we can write s1.a[0] = a; or s2.a = &a; or s2.a = s1.a; without any problem.

Although a structure type is completed with the right brace }, a structure can contain a pointer to an instance of itself because C allows the declaration of pointers to incomplete types. For example:

```
```c
struct A
{
    struct A *p;
};
```
```

When a structure variable is declared, the compiler allocates memory to store its members in the order in which they are declared. For example, the following program displays how many bytes the variable d allocates.

```
```c
#include <stdio.h>

struct date
{
    int day;
    int month;
    int year;
};

int main(void)
{
    struct date d;

    printf("%u\n", sizeof(d));
    return 0;
}
```
```

Since d contains three integer members, the allocated memory is 3*4 = 12 bytes. However, the allocated size may be larger than the sizes of the members added together. For example, if we change the type of the day member from int to char, the program may display again 12, not 9 as might be expected.

This can happen if the compiler requires that each member is stored in an address multiple of some number (typically four). This requirement may be set for a faster access of the structure members. If we assume that the month member should be stored in an address multiple of four, the compiler would allocate three more bytes, a “hole,” right after the day member. In that case, the program would display 12. Holes may exist between members and at the end of the structure, not at the beginning.