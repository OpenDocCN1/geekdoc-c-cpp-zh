# PointerAddressValues.c

```
#include <stdio.h>
int main() {
    int *intPtr = NULL;// pointer variable of type int.
    int intVal = 10;
    int intArr[5] = { 10, 20, 30, 40, 50 };

    // address operator & is a must for a pointer
    // to point to basic data-type.
    intPtr = &intVal; // assign intVal's address to intPtr.
    printf(" Address of &intVal = %p \n", &intVal );
    printf(" Address of intPtr = %p \n", intPtr );
    printf(" Address of *intPtr = %d | intVal = %d\n\n", *intPtr, intVal );

    printf(" Address of &intArr  = %p \n", &intArr );
    printf(" Address of intArr[0] = %p \n", &intArr[0] );
    printf(" Address of intArr   = %p \n", intArr );

    // Variable's name of array data-type for a pointer
    // to point to array data-type.
    intPtr = intArr;
    printf(" Address of intPtr after pointing to array  = %p \n", intPtr );

    return 0;
}
```

# Output

Address of &intVal = 0061FF28
Address of intPtr = 0061FF28
Address of *intPtr = 10 | intVal = 10

Address of &intArr = 0061FF14
Address of intArr[0] = 0061FF14
Address of intArr   = 0061FF14
Address of intPtr after pointing to array  = 0061FF14