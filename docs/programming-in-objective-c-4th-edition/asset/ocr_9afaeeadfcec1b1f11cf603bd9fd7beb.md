this chapter. Several of the Foundation data types, such as NSRange, NSPoint, and NSRect, require a rudimentary understanding of structures, which are described here. In such cases, you can return to this chapter and read the appropriate section to gain an understanding of the concepts.

# Arrays

The Objective-C language enables the user to define a set of ordered data items known as an array. This section describes how to define and manipulate arrays. Later sections illustrate how arrays work together with functions, structures, character strings, and pointers.

Suppose you wanted to read a set of grades into the computer and then perform operations on these grades, such as rank them in ascending order, compute their average, or find their median. In the process of ranking a set of grades, you cannot perform such an operation until you enter every grade.

In Objective-C, you can define a variable called grades that represents not a single value of a grade, but an entire set of grades. You can then reference each element of the set using a number called an index number, or subscript. Whereas in mathematics a subscripted variable, x_i refers to the ith x in a set, in Objective-C the equivalent notation is this:

```
x[i]
```

So the expression

```
grades[5]
```

(read as "grades sub 5") refers to element number 5 in the array called grades. In Objective-C, array elements begin with the number 0, so