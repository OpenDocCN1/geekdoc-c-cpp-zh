their values in a printf() function call. The increment operator then increments each of the pointers so that each points to the next element in the array before continuing with the next iteration of the for loop.

You might be thinking that this program could just well have used array subscript notation and dispensed with pointers altogether. This is true, and in simple programming tasks like this, the use of pointer notation doesn't offer any advantages. As you start to write more complex programs, you will find the use of pointers advantageous.

Remember that you can't perform incrementing and decrementing operations on pointer constants. (An array name without brackets is a pointer constant.) Also remember that when you manipulate pointers to array elements, the C compiler doesn't keep track of the start and finish of the array. If you're not careful, you can increment or decrement the pointer so it points somewhere in memory before after the array. Something is stored there, but it isn't an array element. You should keep track of pointers and where they're pointing.

# Other Pointer Manipulations

The other pointer arithmetic operation that you want to use is called differencing, which refers to subtracting two pointers. If you have two pointers to different elements of the same array, you can subtract them and find how far apart they are. Again, pointer arithmetic automatically scales the answer so that it refers to the number of array elements. Thus, if ptr1 and ptr2 point to elements of an array (of any type), the following expression tells you how far the elements are:

```
ptr1 - ptr2
```

You can compare pointers. Pointer comparisons are valid only when pointers point to the same array. Under these circumstances, the relational operators ==, !=, >, >=, and < work properly. Lower array elements (that is, having a lower subscript) always have a lower address than higher array elements. Thus, if ptr1 and ptr2 point to elements of the same array, the comparison

```
ptr1 < ptr2
```

is true if ptr1 points to an earlier member of the array than ptr2 does.

This covers all allowed pointer operations. Many arithmetic operations can be performed with regular variables, such as multiplication and division, don't make sense with pointers. The C compiler doesn't allow them. For example, if ptr is a pointer, the

```
ptr *= 2;
```