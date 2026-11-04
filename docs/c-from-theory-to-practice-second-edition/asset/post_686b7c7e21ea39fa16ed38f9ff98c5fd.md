
We won't get into details, but if you ever write an application that uses many structures and the memory is limited, keep in mind that the order of the member declarations might affect the alignment and create holes. For example:

```
struct test1
{
    char c;
    double d;
    short s;
};
```

```
struct test2
{
    double d;
    short s;
    char c;
};
```

Although the members are the same, reordering the members, from the larger to smaller, may save memory. For example, the first structure might allocate more bytes than the second one, i.e., 24 bytes instead of 16, in case the compiler leaves holes to align the members to the larger type (i.e., double).

> To calculate the memory size of a structure variable, always use the sizeof operator; don't add the sizes of its members.

Although it is not often used, it is good to know about the offsetof macro. It is defined in stddef.h and takes two arguments. The first one is the type of the structure and the second one the name of a member. The macro calculates the number of bytes from the beginning of the structure up to the member. For example, consider the latter structure. Since C guarantees that the address of the first member is the same as the address of the entire structure, the statement

```
printf("%d\n", offsetof(struct test2, d));
```

outputs 0. If we replace d with s, printf() outputs 8. Because a structure may contain holes, if you write an application to run in different platforms and member alignment matters, that macro might be useful to check the portability of your program.

## The typedef Specifier

The typedef specifier is used to create a synonym for an existing data type. For example, the statement:

```
typedef unsigned int size_t;
```

makes size_t synonym of the unsigned int type. Therefore, the declarations:

```
unsigned int i; and size_t i; are equivalent.
```

The syntax resembles a variable declaration preceded by the typedef keyword. The name represents the stated type. For example, the statement:

```
typedef float arr[100];
```

makes arr synonym for an array of 100 floats. Pay attention, typedef does not create a variable, nor a new type, just a new name. Therefore, the statement:

```
arr arr1;
```

declares the variable arr1 as an array of 100 floats. If we ever need to make the type of the array double, we just change float to double. The declaration of the variable remains the same.

In the same way, we can use typedef to create an alias for a structure type. For example:

```
typedef struct Mybook
{
    char title[100];
    int year;
    float price;
} book;
```

Mybook is a tag and we must add the word struct when used. On the other hand, because the typedef name, that is, book, is a synonym for the structure type, it is not allowed to add the word struct. For example:

```
book b1, b2;
```

Notice that we can use the same identifier for both the structure tag and the typedef name; their meaning is still different though. Also, we can omit the tag and use the typedef name to declare variables. For example:

```
typedef struct
{
    char title[100];
    int year;
    float price;
} book;
```

typedef is used a lot with structures and unions to save writing the word struct or union, when declaring variables. Although this is very common, we don't use it so much. We prefer to clearly show the type of the variable; why hide it? It is easier and faster to read the code; why waste time searching for hidden types? The most times we are using typedef is either if the same type appears a lot in the code or we are using a data structure (e.g., list) with elements structures (or unions).

If the data types of your application depend on the running platform, typedef might be useful. For example:

```
typedef short int size_i;
```

the type of all size_i variables will be short int. In case these variables must be int in another platform, just change short int to int and they become int.

Another common use of typedef is to create synonyms for complex types. For example:

```
typedef int (*pcpy)(const char *s1, const char *s2, int len);
```

pcpy is a synonym for a pointer to a function that returns an integer and takes two arguments of type const char * and an integer argument. Now, it is much easier to declare variables of that type. For example:

```
pcpy p_cpy1, p_cpy2, p_cpy3;
```

is not only easier to write but also easier to read.

## Initializing a Structure

The most common method to access a structure member is to write the name of the structure variable followed by the . operator and the name of the member. For example, the following program displays the values of the b members:

```
#include <stdio.h>
#include <string.h>

struct book
{
    char title[100];
    int year;
    float price;
};

int main(void)
{
    struct book b;

    strcpy(b.title, "Literature");
    b.year = 2016;
    b.price = 10.85;
    printf("%s %d %.2f\n", b.title, b.year, b.price);
    return 0;
}
```

> Besides the . operator, you'll learn next how to use the -> operator to access the members of a structure.

A structure variable can be initialized when it is declared. The declaration is followed by a list of initializers enclosed in braces, separated with a comma. The list must appear in the same order as the members of the structure and should match their data types. As with arrays, the values must be constant expressions, variables are not allowed. Also, there must not be more initializers than members. Consider the following declaration:

```
struct book b = {"Literature", 2020, 10.85};
```

```c
int main(void)
{
    struct computer pc;

    printf("Enter company: ");
    read_text(pc.comp, sizeof(pc.comp), 1);

    printf("Enter model: ");
    read_text(pc.model, sizeof(pc.model), 1);

    printf("Enter cpu: ");
    read_text(pc.cpu, sizeof(pc.cpu), 1);

    printf("Enter price: ");
    scanf("%f", &pc.prc);

    printf("\nc:%s M:%s CPU:%s P:%.2f\n", pc.comp, pc.model, pc.cpu,
    pc.prc);
    return 0;
}
```

### Pointer to a Structure Member

A pointer to a structure member is used like an ordinary pointer. For example, the following program uses pointers to display the values of the b members.

```c
#include <stdio.h>
#include <string.h>

struct book
{
    char title[100];
    int year;
    float price;
};

int main(void)
{
    char *ptr1;
    int *ptr2;
    float *ptr3;
    struct book b;

    strcpy(b.title, "Literature");
    b.year = 2016;
    b.price = 10.8;

    ptr1 = b.title;
    ptr2 = &b.year;
    ptr3 = &b.price;

    printf("%s %d %.2f\n", ptr1, *ptr2, *ptr3);
    return 0;
}
```

To make a pointer variable point to a structure member, its type should be compatible with the type of the member. For example, since the type of the title member is char, ptr1 is declared as char*. As you know by now, the reason we didn't add the & operator before the name of b in the ptr1 = b.title; is that the name of the array is used as a pointer.

## Structure Operations

Although we cannot use the = operator to copy one array into another, we can use it to copy one structure into another. The structures must be of the same type. Consider the following program:

```
#include <stdio.h>

struct student
{
    int code;
    float grd;
};

int main(void)
{
    struct student s1, s2;

    s1.code = 1234;
    s1.grd = 6.7;
    s2 = s1; /* Copy structure. */
    printf("C:%d G:%.2f\n", s2.code, s2.grd);
    return 0;
}
```

The statement s2 = s1; copies s1 members into s2. It is equivalent to:

```
s2.code = s1.code;
s2.grd = s1.grd;
```

Notice that if s1 and s2 were not variables of the same structure type, the statement s2 = s1; wouldn't compile even if the two types contained the same exact members.

Notice also that if a structure contains an array (e.g., name), although it is not allowed to write s2.name = s1.name; once the structure is copied (e.g., s2 = s1), the s1 array is copied to s2. Furthermore, if it contains a pointer member, both pointers will point to the same place after the copy. We'll see such examples in the next two sections.

Besides assignment, no other operation can be performed on entire structures. For example, the operators == and != cannot be used to test whether two structures are equal or not. Therefore, you are not allowed to write:

```
if(s1 == s2) or if(s1 != s2).
```

To test whether two structures are equal, we must compare their members one by one. For example:

```
if( (s1.code == s2.code) && (s1.grd == s2.grd) )
```
