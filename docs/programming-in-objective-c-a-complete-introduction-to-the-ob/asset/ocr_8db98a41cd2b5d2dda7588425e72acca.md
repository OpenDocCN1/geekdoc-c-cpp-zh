# Pointers 291

would store a pointer to this function inside the pointer variable fnPtr.Writing a function name without a subsequent set of parentheses is treated in an analogous way to writing an array name without a subscript. The Objective-C compiler automatically produces a pointer to the specified function. An ampersand is permitted in front of the function name, but it's not required.

If the lookup function has not previously defined in the program, you must declare the function before the previous assignment can be made. A statement such as int lookup (void);

would be needed before a pointer to this function could be assigned to the variable fnPtr.
You can call the function directly referenced through a pointer variable by applying the function call operator to the pointer, listing any arguments to the function inside the parentheses. For example

```
entry = fnPtr ();
```

One common call that fnPtr points to, storing the returned value inside the variable entry.
A common application for pointers to functions is passing them as arguments to other functions. The Standard Library uses this in the function qsort, which performs a quick sort on an array of data elements. This function takes as one of its arguments a pointer to a function that is called whenever qsort needs to compare two elements in the actual comparison of any two elements of the array being sorted. In this manner, qsort can be used to sort arrays of any type because the actual comparison of any two elements in the array is made by a user-defined function, not the qsort function itself.

In the Foundation framework, some methods take a function pointer as an argument. For example, the method sortingUsingFunction:context: is defined in the NSArray class and calls the specified function whenever two elements in an array need to be sorted to be compared.

Another common application for pointers to functions is create dispatch tables.You cannot store functions inside the elements of an array. However, you can store function pointers inside an array. Given this, for for example, you might create a table for processing different commands and a pointer to a function to process that particular command. Now, when the user enters a command, you could look up the command inside the table and invoke the corresponding function to handle it.

# Pointers and Memory Addresses

Before we end this discussion of pointers in Objective-C, we should point out the details of how they are actually implemented. A computer's memory can be conceptualized as a sequential collection of storage cells. Each cell of the computer's memory has a number,