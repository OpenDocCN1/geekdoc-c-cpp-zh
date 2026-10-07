This listing takes advantage of the escape characters discussed in Lesson 7,
“Fundamentals of Reading and Writing Information.” The printf() calls on lines 16
24 use the escape character(\t) to help format the table by aligning the columns.

Looking more closely at Listing 9.2, you can see that three arrays are created on lines
8, 9, and 10. Line 8 declares array_s of type short, line 9 declares array_f
of float, and line 10 declares array_d of type double. Line 16 prints the
column headers for the table that will be displayed. Lines 18 and 19, with lines
27 and 28, first dashed lines across the top and bottom of the data table. This is a nice
touch for a report. The number of element ctr is printed first. This is followed by the address of
element in each of the three arrays. Lines 23, 24, and 25 are

# Pointer Arithmetic

You have a pointer to the first array element; the pointer must increment by an amount
e to the size of the data type stored in the array. How do you access array elements
using pointer notation? You use pointer arithmetic.

“What I don’t need,” you might be thinking, “another kind of arithmetic to learn!”
Don’t worry. Pointer arithmetic is simple, and it makes using pointers in your programs
m easier. You have to be concerned with only two pointer operations: incrementing
and decrementing.

# Incrementing Pointers

When you increment a pointer, you increase its value. For example, when you increment
by 1, pointer arithmetic automatically increases the pointer’s value so that it
points to the next array element. In other words, C knows the data type that the pointer
points to (from the pointer declaration) and increases the address stored in the pointer by
t size of the data type.

Suppose that ptr_to_short is a pointer variable to some element of a short array. If
you execute the statement

```
ptr_to_short++;
```

the value of ptr_to_short is increased by the size of type short (usually 2 bytes), and
ptr_to_short now points to the next array element. Likewise, if ptr_to_float points to
element of a type float array, the statement

```
ptr_to_float++;
```

increases the value of ptr_to_float by the size of type float (usually 4 bytes).