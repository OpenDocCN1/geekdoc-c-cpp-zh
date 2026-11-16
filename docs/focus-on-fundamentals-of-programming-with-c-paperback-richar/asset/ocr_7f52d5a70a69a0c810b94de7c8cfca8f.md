Now, the pointer to the `struct` is first dereferenced, giving us the `struct` itself, and _then_ the appropriate field of the `struct` is accessed. Although this syntax is correct, C programmers almost never use it! The reason is that there is a shortcut syntax that requires less keystrokes and produces clearer code. The equivalent statement looks like this:

```
ps->age = 35;
```

This _indirect component selector operator_, `->`, is made up of a hyphen and the greater than symbol without a space between them. It automatically first dereferences the pointer and then selects the appropriate field of the `struct`.
Note that this operator can only be used when you have a pointer to a `struct`
and you want to access a field of the `struct`. The example below shows the use
of this new operator:

```
```c
// student.c
#include <stdio.h>
#include <string.h>
#include <alloc.h>

typedef struct student {
    char name[30];
    int age;
    float gpa;
} STUDENT;

int main(void) {
    STUDENT *ps;

    ps = (STUDENT *) malloc(sizeof(struct student));
    strcpy(ps->name, "Haley Laurel");
    ps->age = 35;
    ps->gpa = 3.75;
    printf("%s %d %4.2f\n", ps->name, ps->age, ps->gpa);
    free(ps);
    return 0;
}
```
```