# ### 3.1 Arrays

An array is a collection of elements of similar data-type, which are stored in contiguous memory locations. It means that an array can store value of same data-type, such as int, float, and char. Elements of an array are stored in the adjacent memory (memory at side by side) that is identified by a subscript number or index number. For example, an array named marks contains 5 integer values of int data-type, which can be represented as:

![](bbox=[0.242, 0.275, 0.83, 0.312])

Each blank cell represents an element of the array named marks with integer value of the int data-type. The array elements of marks are numbered from 0 to 4, since in any array, the first index is always 0. The unique identifier (index value) of first element of the array marks is marks[0], second element of the array marks is marks[1], and so on. The following is the syntax to declare an array:

```
```c
data_type Array_Name[count];
```
```

In the preceding syntax, data_type is the data type of the value that is stored in the array. Array_Name is the name of the array, and count is the number of elements that an array can store. For example, the following code snippet declares the Arr1 array of integer data type that can store 5 integer values:

```
```c
int Arr1[5];
```
```

After declaring an array, you can access its element with the name of the array and the index value. For example, the following code snippet accesses the first element of the Arr1 array and assigns an integer value in it:

```
```c
Arr1[0]=5;
```
```

In the preceding code snippet, the value 5 is assigned at the first location of the Arr1 array. Similarly, the other elements of the Arr1 array can be accessed with their index values.

You can also assign some values to an array at the time of declaration. This process is called array initialization. The following code snippet shows how to initialize an array:

```
```c
int Arr1[5]={1,2,3,4,5};
```
```

In the preceding code snippet, the Arr1 array is initialized with first 5 natural numbers at time of declaration. While initializing an array, specifying the size of the array is an optional value. For example, the following code snippet initializes an array without providing the size value: