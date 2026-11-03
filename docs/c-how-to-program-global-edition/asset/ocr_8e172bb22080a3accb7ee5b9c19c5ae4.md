```
```c
// Fig. 7.16: fig07_16.c
// Applying sizeof to an array name returns
// the number of bytes in the array.
#include <stdio.h>
#define SIZE 20

size_t getSize(float *ptr); // prototype

int main(void)
{
    float array[SIZE]; // create array

    printf("The number of bytes in the array is %u\n"
           "The number of bytes returned by getSize is %u\n",
           sizeof(array), getSize(array));
}

// return size of ptr
size_t getSize(float *ptr)
{
    return sizeof(ptr);
}
```
```

The number of bytes in the array is 80
The number of bytes returned by getSize is 4

Fig. 7.16 | Applying sizeof to an array name returns the number of bytes in the array.

The number of elements in an array also can be determined with sizeof. For example, consider the following array definition:

```
```c
double real[22];
```
```

Variables of type double normally are stored in 8 bytes of memory. Thus, array real contains a total of 176 bytes. To determine the number of elements in the array, the following expression can be used:

```
```c
sizeof(real) / sizeof(real[0])
```
```

The expression determines the number of bytes in array real and divides that value by the number of bytes used in memory to store the first element of array real (a double value). Even though function getSize receives an array of 20 elements as an argument, the function's parameter ptr is simply a pointer to the array's first element. When you use sizeof with a pointer, it returns the size of the pointer, not the size of the item to which it points. On our Windows and Linux test systems, the size of a pointer is 4 bytes, so getSize returns 4; on our Mac, the size of a pointer is 8 bytes, so getSize returns 8. Also, the calculation shown above for determining the number of array elements using sizeof works only when using the actual array, not when using a pointer to the array. Determining the Sizes of the Standard Types, an Array and a Pointer Figure 7.17 calculates the number of bytes used to store each of the standard data types. The results of this program are implementation dependent and often differ across platforms and