
Array initializers are specified in braces, left to right, in list order. C# automatically allocates an array large enough to hold the initializers that you specify. There is no need to explicitly use the new operator.

## Sort an Array

Because a one-dimensional array organizes information into an indexable linear form, it is the ideal data structure for sorting. Furthermore, sorting algorithms make some of the best examples of array handling. To that end, this example develops a version of the fairly notorious bubble sort. As you may know, there are a number of different sorting algorithms. There are the quicksort, the shaker sort, and the Shell sort, to name only three. However, one of the simplest and easiest-to-understand sorting algorithms is the bubble sort. It is also one of the worst sorts in terms of performance (although it can sometimes be used effectively for sorting very small arrays). The bubble sort has one useful characteristic, however: it makes an interesting example of array handling!

1. Create a document called Bubble.cs.
2. The bubble sort gets its name from the manner in which it performs the sorting operation. It uses repeated comparison and, if necessary, exchange of adjacent elements in the array. In this process, small values move toward one end and large ones toward the other end. The process is somewhat like bubbles finding their own level in a tank of water. The bubble sort works by making several passes through the array, exchanging out-of-order elements when necessary. The number of passes required to guarantee that the array is sorted is equal to one less than the number of elements in the array.

Here is the code that forms the core of the bubble sort. The array being sorted here is called nums. This implies changes to the parameter that gets a value type won't affect the actual argument used in the call. You can, however, alter this behavior. Using the ref and out keywords, it is possible to pass any of the value types by reference. Doing so permits a method to alter the argument used in the call. Before going into the mechanics of using ref and out, it is useful to understand why you should pass a value type by reference.

As a rule, there are two reasons: to allow a method to change the contents of its arguments, or to enable a method to return more than one value. Let's take a look at each reason in detail. Frequently, you will want a method to be able to operate on the actual arguments that are passed to it. The quintessential example of this is a "swap" method that exchanges the values of its two arguments. Because value types are passed by value, it is impossible to write such a method that swaps the values of two ints, for instance, using C#'s default call-by-value parameter-passing mechanism. The ref modifier takes care of this problem. As you probably know, a return statement enables a method to return a value to its caller. However, a method can return only one value each time it is called. What if you need to return two or more pieces of information? For instance, what if you need to create a method that computes the area of a rectangle and also determines whether that rectangle is a square? To do this requires two pieces of data to be returned: the area and a value indicating square-ness. This method cannot be written using only a single return value. The out modifier solves this problem.

Notice that the sort depends on two for loops. The inner loop checks adjacent elements in the array, looking for out-of-order elements. When an out-of-order element pair is found, the two elements are swapped. With each pass, the smallest element of those remaining moves into its correct location. The outer loop causes this process to repeat until the whole array has been sorted.

The simplest form of the multidimensional array is the two-dimensional array. In a two-dimensional array, the location of an element is specified by two indices. Think of a two-dimensional array as a table of data: one index indicates the row, the other indicates the column. To declare a two-dimensional integer array table of size 10, 20, you would write:

```csharp
int[,] table = new int[10, 20];
```

Pay careful attention to the declaration. Notice that the two dimensions are separated by a comma. In the first part of the declaration, the syntax [,] indicates that a two-dimensional array reference variable is being created. When memory is actually allocated for the array using new, this syntax is used:

```csharp
new int[10, 20]
```

This makes a 10×20 array, and again, the comma separates the dimensions. To access an element in a two-dimensional array, you must specify both indices, separating the two with a comma. For example, to assign the value 10 to location 3, 5 of array table, you would use:

```csharp
table[3, 5] = 10;
```

## Jagged Array

In the first examples, when you created a two-dimensional array, you were creating what C# calls a rectangular array. Thinking of two-dimensional arrays as tables, a rectangular array is a two-dimensional array in which the length of each row is the same for the whole array. However, C# also enables you to create a special kind of two-dimensional array called a jagged array. A jagged array is an array of arrays in which the length of each array can differ. Therefore, a jagged array can be used to create a table in which the row lengths are not the same. Jagged arrays are declared by using sets of square brackets to indicate each dimension. For example, to declare a two-dimensional jagged array, you will use this general form:

```csharp
type[][] arrayName = new type[size][];
```

Here, size indicates the number of rows in the array. The rows themselves have not been allocated. Rather, the rows are allocated separately. This allows the length of each row to differ. For example, the following code allocates memory for the first dimension of jagged at the time it is declared. It then allocates the second dimensions manually. It is easy to see how jagged arrays got their name! Once a jagged array has been created, an element is accessed by specifying each index within its own set of brackets. For instance, to assign the value 10 to element 2, 1 of jagged, you would use this statement:

```csharp
jagged[2][1] = 10;
```

Note that this differs from the syntax that is used to access an element of a rectangular array. Here is an example that uses a jagged two-dimensional array. Assume that you are writing a program that stores the number of passengers that ride an airport shuttle. If the shuttle bus runs ten times each day during the week and two times each day on Saturday and Sunday, you could use the riders array shown in the following program to store the data. Notice that the length of the second dimension for the first five rows is 10 and that the length of the second dimension for the last two rows is 2. Jagged arrays won't be used by all applications, but they can be very useful in several circumstances. For example, if you need a large two-dimensional array that is sparsely populated (that is, one in which not all of the elements will be used), then a jagged array may be an ideal solution.

## Assign Array Reference

Just as with other objects, when you assign one array reference variable to another, you are essentially causing the two variables to refer to the same array. You are not making a copy of the array be made, nor are you making the contents of one array be copied to the other. Various advantages result because C# implements arrays as objects. One stems from the fact that each array has associated with it a Length property that contains the number of elements that an
