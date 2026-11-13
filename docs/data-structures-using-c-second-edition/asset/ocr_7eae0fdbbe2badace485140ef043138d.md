![](bbox=[0.185, 0.105, 0.865, 0.295])

Figure 3.3 Declaring arrays of different data types and sizes

# 3.3 ACCESSING THE ELEMENTS OF AN ARRAY

Storing related data items in a single array enables the programmers to develop concise and efficient programs. But there is no single function that can operate on all the elements of an array.

```
// Set each element of the array to -1\nint marks[10];\nfor (i=0;i<10;i++)\nmarks[i] = -1;
```

To access all the elements, we must use a loop. That is, we can access all the elements of an array by varying the value of the subscript into the array. But note that the subscript must be an integral value or an expression that evaluates to an integral value. As shown in Fig. 3.2, the first element of the array marks[10] can be accessed by writing marks[0]. Now to process all the elements of the array, we use a loop as shown in Fig. 3.4.

Figure 3.4 Code to initialize each element of the array to -1

Figure 3.5 shows the result of the code shown in Fig. 3.4. The code accesses every individual element of the array and sets its value to -1. In the for loop, first the value of marks[0] is set to -1, then the value of the index (i) is incremented and the next value, that is, marks[1] is set to -1. The procedure continues until all the 10 elements of the array are set to -1.

| -1 | -1 | -1 | -1 | -1 | -1 | -1 | -1 | -1 | -1 |\n|---|---|---|---|---|---|---|---|---|---|\n| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

Figure 3.5 Array marks after executing the code given in Fig. 3.4

> **Note** There is no single statement that can read, access, or print all the elements of an array. To do this, we have to use a loop to execute the same statement with different index values.

# 3.3.1 Calculating the Address of Array Elements

You must be wondering how C gets to know where an individual element of an array is located in the memory. The answer is that the array name is a symbolic reference to the address of the first byte of the array. When we use the array name, we are actually referring to the first byte of the array.

The subscript or the index represents the offset from the beginning of the array to the element being referenced. That is, with just the array name and the index, C can calculate the address of any element in the array.

Since an array stores all its data elements in consecutive memory locations, storing just the base address, that is the address of the first element in the array, is sufficient. The address of