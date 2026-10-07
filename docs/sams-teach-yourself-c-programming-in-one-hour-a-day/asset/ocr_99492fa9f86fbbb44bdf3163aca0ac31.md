# Using Single-Dimensional Arrays

A *single-dimensional array* has only a single subscript. A *subscript* is a number in brackets that follows an array's name. This number can identify the number of individual elements in the array. An example should make this clear. For the expenses program, you could use the following line to declare an array of type `float:`

```
float expenses[12];
```

The array is named *expenses*, and contains 12 elements. Each of the 12 elements is the exact value of a single *float* variable.

All of C's data types can be used for arrays. C array elements are always numbered starting at 0, so the 12 elements are numbered 0 through 11. In the preceding example, January's expense total would be stored in `expenses[0]`, February's in `expenses[1]`, and so on. The expense total for December would be in `expenses[11]`**

When you declare an array, the compiler sets aside a block of memory large enough to hold the entire array. Individual elements are stored in sequential memory locations, as shown in Figure 8.2.

![](bbox=[0.125, 0.498, 0.755, 0.563])

Where you declare an array in your source code is important. As with variables that are not part of an array, the declaration's location affects how your program can use the array. The effect of a declaration's location is covered in more detail in Lesson 12, “Understanding Variable Scope.” For now, place your array declarations with other variable declarations.

An array element can be used in your program where a nonarray variable of the same type can be used. Individual elements of the array are accessed using the array name followed by the element enclosed in square brackets. For example, the following statement stores the value `89.95` in the second array element. (Remember, the first array element is `expenses[0]`, not `expenses[1]`)

```
expenses[1] = 89.95;
```

Likewise, the statement

```
expenses[10] = expenses[11];
```