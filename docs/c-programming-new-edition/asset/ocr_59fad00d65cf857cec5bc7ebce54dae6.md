```
{
int x=13; return(&x);
}
```

In this program the address of i is initialized and declared in the called function and returned to the caller function which is assigned p and the value of p on the address of i is displayed using the printf statements.

# 6.9. TWO-DIMENSIONAL ARRAYS AND POINTERS

You have already been apprised about the 2 dimensional arrays in the session Arrays and you are aware that a 2dimensional array has a row and a column and it is usually a matrix. Here you will be acquainted with the representation of the 2 dimensional array with respect to a pointer.

A 2 dimensional array is actually an assortment of 1 dimensional arrays. Therefore, one can define a two dimensional array as a pointer to a group of contiguous 1 dimensional arrays.

The general format can be specified as follows. data _type (*ptrvar) [size]; According to the above format data type refers to the data type of the array, ptrvar is the name of the pointer variable. Notice the parentheses that surround the array name and the preceding asterisk in the pointer version of each declaration.

These parentheses must be present. Without them you would be defining an array of pointers rather than a pointer to a group of arrays, since these particular symbols (i.e., the square brackets and the asterisk) would normally be evaluated right to left.

+   - Example 6.2:
+     int (*a)[20];

In this a is defined to be a pointer to a group of contiguous, one-dimensional, 20-element integer arrays. Thus, a points to the first 20-element array, which is actually the first row (i.e., row 0) of the original two-dimensional array.

Similarly. (a + 1) points to the second 20-element array, which is the second row (row − 1) of the original two dimensional array, and so on, as illustrated below.

a (a + 1)