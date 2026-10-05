# F.1. DECLARING AND USING ARRAYS

The array brackets operator has two distinct meanings depending on the context:

+   At the array's declaration,
```double nums[10];```
the within the square brackets specifies the number of elements that the array can hold. The compiler uses this number along with the type of the array to determine how much memory to allocate for the array.
After the array's declaration,
```nums[3] = 10.45;```
the number within the square brackets represents an index locating a specific element within the memory allocated to the array.

![](bbox=[0.213, 0.237, 0.258, 0.273])

Declarations of arrays and non-value arrays can be interspersed, in:
```int list[5], x, s[3], *p, reg;```

Here, list and s are integer arrays, x and reg are simple integer variables, and p is a pointer to an integer (Section 10.6, for a discussion of pointers).

The contents of an array may be initialized when it is declared. The following code fragment declares three arrays and specifies their initial contents:
```int list[] = { 2, 4, 6, 8 };\double collection[10] = { 1.0, 3.5, 0.5, 7.2 };\char letters[] = { 'a', 'b', 'c' };```

The elements of the array are provided by a comma-separated list within curly braces. This comma-separated list of initial values creates an array initialization list. When an array is initialized, the square brackets can be left empty the compiler can calculate the array's size based on the number of elements in the list. If a number is provided within the square brackets, the array is allocated with the specified size, and the elements are filled within the array with the elements specified in the initialization list.

The code fragment declares three arrays: list, collection and letters. The list array is created to hold four integer values... and The collection array is created to hold 10 double-precision floating-point values, and the first four elements consist of 1.0, 3.5, 0.5, and 7.2. The letters array holds the three characters. Figure F2 shows the contents of the three arrays.

We can observe three points from Figure F2:

+   An array name represents the location of the first element in an array. For an array named list, the expressions list and list[0] within C++ source code are equivalent.
Elements in an array are stored in a contiguous block of memory. This means, for example, the memory occupied by the element at index 3 immediately follows after the memory occupied by the element at index 2 and immediately before the element at index 4. The size specified in the array's declaration determines the size this block of contiguous memory.