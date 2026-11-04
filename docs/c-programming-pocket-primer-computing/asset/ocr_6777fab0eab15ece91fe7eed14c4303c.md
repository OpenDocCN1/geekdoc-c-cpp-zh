```
printf("Value of ptr: %d\n", *ptr2);
printf("Value of ptr2: %d\n", *ptr2);

return 0;
}
```

Listing 5.2 contains the variable x whose initial value is 7, followed by the pointer ptr that is the same as the pointer ptr in Listing 5.2. Next, the pointer ptr2 is initialized with the location of pointer ptr, after which the contents of ptr2 are changed to 5678. The result is probably what you expect: the new value of the variable is 5678. The output from Listing 5.2 is here:

Value of x:  7
Value of x: 5678
Value of ptr: 5678
Value of ptr2: 5678

Listing 5.3 displays the contents of SimplePointer3.c that illustrates how to use a pointer to change the value of a variable of type int.

# LISTING 5.3: SimplePointer3.c

```
#include <stdio.h>

int main()
{
    int x = 7;
    printf("Value of x:  %d\n", x);

    // ptr "points" to location of x:
    int *ptr = &x;
    printf("Value of ptr:  %d\n", *ptr);

    // ptr2 points to same location as ptr:
    int *ptr2 = ptr;
    printf("Value of ptr2: %d\n", *ptr2);
```