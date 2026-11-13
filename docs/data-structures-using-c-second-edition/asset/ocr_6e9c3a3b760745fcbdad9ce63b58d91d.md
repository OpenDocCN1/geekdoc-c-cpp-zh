An array is a collection of similar data elements. These data elements have the same data type. The elements of the array are stored in consecutive memory locations and are referenced by an index (also known as the subscript). The subscript is an ordinal number which is used to identify an element of the array.

![](bbox=[0.283, 0.186, 0.755, 0.363])

Figure 3.1 Twenty variables for 20 students

# 3.2 DECLARATION OF ARRAYS

We have already seen that every variable must be declared before it is used. The same concept holds true for array variables. An array must be declared before being used. Declaring an array means specifying the following:

+   * Data type—the kind of values it can store, for example, int, char, float, double.
+   * Name—to identify the array.
+   * Size—the maximum number of values that the array can hold.

Arrays are declared using the following syntax:

```
type name[size];
```

The type can be either int, float, double, char, or any other valid data type. The number within brackets indicates the size of the array, i.e., the maximum number of elements that can be stored in the array. For example, if we write,

```
int marks[10];
```

then the statement declares marks to be an array containing 10 elements. In C, the array index starts from zero. The first element will be stored in marks[0], second element in marks[1], and so on. Therefore, the last element, that is the 10th element, will be stored in marks[9]. Note that 0, 1, 2, 3 written within square brackets are the subscripts. In the memory, the array will be stored as shown in Fig. 3.2.

| 1st element | 2nd element | 3rd element | 4th element | 5th element | 6th element | 7th element | 8th element | 9th element | 10th element |
|---|---|---|---|---|---|---|---|---|---|
| marks[0] | marks[1] | marks[2] | marks[3] | marks[4] | marks[5] | marks[6] | marks[7] | marks[8] | marks[9] |

Figure 3.2 Memory representation of an array of 10 elements

Figure 3.3 shows how different types of arrays are declared.