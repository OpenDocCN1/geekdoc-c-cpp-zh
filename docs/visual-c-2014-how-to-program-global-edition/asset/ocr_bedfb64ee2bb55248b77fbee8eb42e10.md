# 8.4 Examples Using Arrays 343

Creating the array c can also be performed as:

```
```
int[] c; // declare the array variable
c = new int[12]; // create the array; assign to array variable
```
```

+   - the array to be resized
- the new length

and copies the contents of the old array into the new one, then sets the variable it receives as its first argument to reference the new array. For example, in the following statements:

```
int[] newArray = new int[5];
Array.Resize(ref newArray, 10);
```
newArray initially refers to a five-element array. The Resize method then sets newArray to refer to a 10-element array containing the original array's values. If the new array is smaller than the old array, any content that cannot fit into the new array is truncated without warning. The old array's memory is reclaimed by the runtime if there are no other array variables referring to that array.

# 8.4 Examples Using Arrays

This section presents several examples that demonstrate declaring arrays, creating arrays, initializing arrays and manipulating array elements.

# 8.4.1 Creating and Initializing an Array

In Fig. 8.2 line 10 of an array-expression to create a five-element int array with values initialized to 0 by default. The resulting array's reference initializes the variable to refer to the new array object.

```
```
1 // Fig. 8.2: InitArray.cs
2 // Creating an array.
3 using System;
4 
5 class InitArray
6 {
7 static void Main()
8 {
```
```

![](bbox=[0.141, 0.896, 0.448, 0.915])

+   2. Section 10.8 discusses how the runtime reclaims the memory of objects that are no longer used.