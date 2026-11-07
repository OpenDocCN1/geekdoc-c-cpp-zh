```
```cpp
d) // print entire array z; assume zPtr is initialized
    for (size_t i = 0; i <= 5; ++i) {
        printf("%d ", zPtr[i]);
    }
e) // assign the value pointed to by sPtr to number
    number = *sPtr;
f) ++z;
```
```

# Answers to Self-Review Exercises

+   7.1 a) address. b) 0, NULL, an address. c) 0.

+   7.2 a) *False.* A pointer to void cannot be dereferenced, because there's no way to know exactly how many bytes of memory to dereference. b) *False.* Pointers of type void can be assigned pointers of other types, and pointers of type void can be assigned to pointers of other types.

+   7.3 See the answers below:

```
```cpp
a) float numbers[SIZE] =
       {0.0, 1.1, 2.2, 3.3, 4.4, 5.5, 6.6, 7.7, 8.8, 9.9};
b) float *nPtr;
```
```

```
```cpp
c) for (size_t i = 0; i < SIZE; ++i) {
       printf("%.1f ", numbers[i]);
   }
```
```

```
```cpp
d) nPtr = numbers;
   nPtr = &numbers[0];
```
```

```
```cpp
e) for (size_t i = 0; i < SIZE; ++i) {
       printf("%.1f ", *(nPtr + i));
   }
```
```

```
```cpp
f) for (size_t i = 0; i < SIZE; ++i) {
       printf("%.1f ", *(numbers + i));
   }
```
```

```
```cpp
g) for (size_t i = 0; i < SIZE; ++i) {
       printf("%.1f ", nPtr[i]);
   }
```
```

```
```cpp
h) numbers[4]
   *(numbers + 4)
   nPtr[4]
   *(nPtr + 4)
```
```

+   i) The address is 1002500 + 8 * 4 = 1002532. The value is 8.8.

+   j) The address of numbers[5] is 1002500 + 5 * 4 = 1002520.
+   The address of nPtr -= 4 is 1002520 - 4 * 4 = 1002504.
+   The value at that location is 1.1.

+   7.4 See the answers below:

```
```cpp
a) float *fPtr;
```
```