# Chapter 4

You can determine the meaning of the second line by working from the inside, outwards. beans refers to the address of the first row of the array, so beans + i refers to row i of the array. The expression *(beans + i) is the address of the first element of row i, so *(beans + i) + j is the address of the element in row i with offset j. The whole expression therefore refers to the value of that element.

If you really want to be obscure — and it isn’t recommended that you should be — the following two statements, where you have mixed array and pointer notation, are also legal references to the same element of the array:

```
* (beans[i] + j)
(* (beans + i))[j]
```

There is yet another aspect to the use of pointers that is really the most important of all: the ability to allocate memory for variables dynamically. You’ll look into that next.

# Dynamic Memory Allocation

Working with a fixed set of variables in a program can be very restrictive. The need often arises within an application to decide the amount of space to be allocated for storing different types of variables at execution time, depending on the input data for the program. With one set of input data it may be appropriate to use a large integer array in a program, whereas with a different set of input data, a large floating-point array may be required. Obviously, because any dynamically allocated variables can’t have been defined at compile time, they can’t be named in your source program. When they are created, they are identified by their address in memory, which is contained within a pointer. With the power of pointers and the dynamic memory management tools in Visual C++ 2005, writing your programs to have this kind of flexibility is quick and easy.

# The Free Store, Alias the Heap

In most instances, when your program is executed, there is unused memory in your computer. This unused memory is called the heap in C++, or sometimes the free store. You can allocate space within the free store for a new variable of a given type using a special operator in C++ that returns the address of the space allocated. This operator is new, and it’s complemented by the operator delete, which de-allocates memory previously allocated by new.

You can allocate space in the free store for some variables in one part of a program, and then release the allocated space and return it to the free store after you have finished with the variables concerned. This makes the memory available for reuse by other dynamically allocated variables, later in the same program.

You would want to use memory from the free store whenever you need to allocate memory for items that can only be determined at run-time. One example of this might be allocating memory to hold a string entered by the user of your application. There is no way you can know in advance how large this string needs to be, so you would allocate the memory for the string at run time, using the new operator. Later, you’ll look at using the free store to dynamically allocate memory for an array, where the dimensions of the array are determined by the user at run time.