Further, programmers with social skills typecast the malloc() function to return the data type allocated. Improving upon the preceding example:

```
```c
p = (int *)malloc( sizeof(int) * 5 );
```
```

The int typecast includes the * (pointer) operator, to ensure that the memory chunk allocated is of the integer pointer data type.

Finally, you must include the stdlib.h header file in your source code to keep the compiler pleased with the malloc() function. Listing 20-1 shows an example.

# LISTING 20-1: Give Me Space

```
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *age;

    /* allocate memory */
    age = (int *)malloc(sizeof(int)*1);
    if(age == NULL)
    {
        puts("Unable to allocate memory");
        exit(1);
    }

    /* use the memory */
    printf("How old are you? ");
    scanf("%d",age);
    printf("You are %d years old.\n",*age);

    return(0);
}
```
```

The first thing to notice about Listing 20-1 is that the only variable declared is int pointer, age. This pointer isn't assigned the address of another variable, but rather is used to hold the address of memory allocated later in the code.

Line 9 uses malloc() to set aside storage for one integer. To ensure that the proper amount of storage is allocated, the sizeof operator is used. To allocate space for one integer, the value 1 is multiplied by the result of the sizeof(int) operation. The address returned is saved in the age pointer.