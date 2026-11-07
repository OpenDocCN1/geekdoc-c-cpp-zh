**2** *(Discussion)* Typically, when we pass an array to a function, we also pass the array size as another argument. Alternatively, we could build the array size directly into the function definition. What’s wrong with that approach?
Answer: It would limit the function to processing arrays of a specific size, significantly reducing the function’s reusability.

# ## 7.7 `sizeof` Operator

C provides the unary operator `sizeof` to determine an object’s or type’s size in bytes. This operator is applied at compilation time unless its operand is a variable-length array (VLA; Section 6.12). When applied to an array’s name as in Fig. 7.12 (line 12), `sizeof` returns a `size_t` value the array’s total number of bytes. Variables of type `float` on our computer are stored in four bytes of memory, and `array` is defined to have 20 elements. Therefore, there are 80 bytes in `array`. `sizeof` is a compile-time operator, so it does not incur any execution-time overhead (except for VLAs).

```
```c
1  // Fig07_12.c
2  // Applying sizeof to an array name returns
3  // the number of bytes in the array.
4  #include <stdio.h>
5  #define SIZE 20
6
7  size_t getSize(const float *ptr); // prototype
8
9  int main(void){
10     float array[SIZE]; // create array
11
12     printf("Number of bytes in the array is %zu\n", sizeof(array));
13     printf("Number of bytes returned by getSize is %zu\n", getSize(array));
14 }
15
16 // return size of ptr
17 size_t getSize(const float *ptr) {
18     return sizeof(ptr);
19 }
```
```

```
```
Number of bytes in the array is 80
Number of bytes returned by getSize is 8
```
```

*Fig. 7.12 | Applying `sizeof` to an array name returns the number of bytes in the array.*

Even though function `getSize` receives an array of 20 elements as an argument, the function’s parameter `ptr` is simply a pointer to the array’s first element. When you use `sizeof` with a pointer, it returns the *pointer’s size*, not the size of the item to which it points. On our 64-bit Windows, Mac and Linux test systems, a pointer’s size is eight bytes, so `getSize` returns 8. On older 32-bit systems, a pointer’s size is typically four bytes, so `getSize` would return 4.