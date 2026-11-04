whether or not a given integer is in a C array of integers.

# LISTING 3.10: LinearSearch.c

```
#include <stdio.h>

int main()
{
    int numbers[] = {15, 3, 99, -4, 25, 8};
    int value = 25, pos = -1;
    int count = sizeof(numbers)/sizeof(numbers[0]);

    for(int i=0; i<count; i++)
    {
        if(value == numbers[i])
        {
            pos = i;
            break;
        }
    }

    printf("Array: ");
    for(int i=0; i<count; i++)
    {
        printf("%d ", numbers[i]);
    }
    printf("\n");

    printf("Value: %d\n",value);
    printf("Pos:  %d\n",pos);

    return 0;
}
```

Listing 3.10 contains a main() function that initializes a numbers array with 6 integers, as well as several scalar variables. Next, the code snippet (shown in bold) computes the size of the entire array divided by the size