Another common use of typedef is to create synonyms for complex types. For example:

```
typedef int (*pcpy)(const char *s1, const char *s2, int len);
```

pcpy is a synonym for a pointer to a function that returns an integer and takes two arguments of type const char * and an integer argument. Now, it is much easier to declare variables of that type. For example:

```
pcpy p_cpy1, p_cpy2, p_cpy3;
```

is not only easier to write but also easier to read.

# Initializing a Structure

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