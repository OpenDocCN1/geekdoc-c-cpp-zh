```
f) for (size_t i = 0; i < SIZE; ++i) {
    printf("%.1f ", *(numbers + i));
}
```

```
g) for (size_t i = 0; i < SIZE; ++i) {
    printf("%.1f ", nPtr[i]);
}
```

h) numbers[4]
*(numbers + 4)
nPtr[4]
*(nPtr + 4)

i) The address is 1002500 + 8 * 4 = 1002532. The value is 8.8.

j) The address of numbers[5] is 1002500 + 5 * 4 = 1002520.
The address of nPtr -= 4 is 1002520 - 4 * 4 = 1002504.
The value at that location is 1.1.

# 7.4

+   a) float *fPtr;
+   b) fPtr = &number1;
+   c) printf("The value of *fPtr is %f\n", *fPtr);
+   d) number2 = *fPtr;
+   e) printf("The value of number2 is %f\n", number2);
+   f) printf("The address of number1 is %p\n", &number1);
+   g) printf("The address stored in fptr is %p\n", fPtr);
+   Yes, the value is the same.

# 7.5

+   a) void exchange(float *x, float *y);
+   b) void exchange(float *x, float *y);
+   c) int evaluate(int x, int (*poly)(int))
+   d) int evaluate(int x, int (*poly)(int));

# 7.6

+   a) Error: zPtr has not been initialized.
+   Correction: Initialize zPtr with zPtr = z; before performing the pointer arithmetic.
+   b) Error: The pointer is not dereferenced.
+   Correction: Change the statement to number = *zPtr;
+   c) Error: zPtr[2] is not a pointer and should not be dereferenced.
+   Correction: Change *zPtr[2] to zPtr[2].
+   d) Error: Referring to an array element outside the array bounds with pointer indexing.
+   Correction: Change the operator <= in the for condition to <.
+   e) Error: Dereferencing a void pointer.
+   Correction: To dereference the pointer, it must first be cast to an integer pointer.
+   Change the statement to number = *((int *) zPtr);
+   f) Error: Trying to modify an array name with pointer arithmetic.
+   Correction: Use a pointer variable instead of the array name to accomplish pointer arithmetic, or index the array name to refer to a specific element.

# Exercises

# 7.7

Answer each of the following:

+   a) The ______ pointers are generic pointers that can hold pointer values of any type.
+   b) An array name can be thought of as a ______ pointer.
+   c) The ______ operator is a unary operator that returns the address of its operand, and the ______ operator returns the value of the object to which its operand points.

# 7.8

State whether the following are true or false. If false, explain why.