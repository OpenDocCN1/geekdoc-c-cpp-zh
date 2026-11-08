This declaration is incorrect as there is no actual argument present in the parameter list.

# # The Implicit Int Rule in C

Earlier versions of C included an implicit int feature, which stated that in the absence of a type specifier for a function, the default type would be assumed as int. This rule was included in C89 standard but later it was removed when C99 standard was introduced. According to this rule, if a function is declared without a prototype, then the compiler automatically assumes the return type of the function to be an int. Any deviation from this assumption causes a compilation error.

Listing 2.17 shows how implicit int rule works in C:

**Listing 2.17: Implicit int Rule in C**

```
```c
#include<stdio.h>

int main()
{
    myFunc(10,30,90);
    getch();
    return 0;
}

int myFunc(int x, int y,int z)
{
    printf("\n x [%d] Y [%d] Z[%d]", x,y,z);
    return x;
}
```
```

The output of Listing 2.17 is given as follows:

```
```
x [10] Y [30] Z[90]
```
```

The output of the function validates the presence of the implicit int rule. In this program, the function is missing its prototype definition; however, the function definition has a return type of int that matches with the implicit int rule for functions; hence, the function compiles successfully.

Listing 2.18 shows an alternative way to write this rule:

**Listing 2.18: Showing the Conflict in the Implicit Int Rule**

```
```c
#include<stdio.h>

int main()
{
    myFunc(10,30,90);
    getch();
    return 0;
}

float myFunc(int x, int y,int z)
{
    printf("\n x [%d] Y [%d] Z[%d]", x,y,z);
    return x;
}
```
```

The output of Listing 2.18 is given as follows:

```
```
conflicting types for 'myFunc'
```
```