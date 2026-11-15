```
Value of ptrto : #2 /* i.e. the address of ptr*/
Value of x by dereferencing ptr : 0
Value of x by dereferencing ptrto : 0
*/
```

There are no new concepts in the above code, it’s merely an extension of what you already know about pointers:

+   1. Declare three variables called x, ptr and ptrto. x is the integer, ptr is a pointer-to-an-integer and ptrto is a pointer to a pointer-to-an-integer.
+   2. Print the address of each variable; x lives at #1, ptr at #2 and ptrto at #3.
+   3. Assign the address of x to ptr. The address of ptr is assigned to ptrto.
+   4. Print the value of each variable. x has a value of 0, ptr has a value of the address of x, i.e. #1 and ptrto has the value of the address of ptr, i.e. #2.
+   5. Print x out by indirection.

You already know what *ptr means. Further on ptrto is dereferenced twice, which is what you’ve got to do if you want to get to the integer from it. The first time you dereference ptrto you get to ptr, the second time you are effectively dereferencing ptr, which takes you to x

This, and in fact all operations with pointers, is very easily understood if you sketch what’s happening on a piece of paper: draw a diagram if you’re not sure what’s happening with your pointers.

# 5.3 Objects (C data structures)

To program effectively using the AJAX and NUCLEUS libraries you need to understand how the EMBOSS derived datatypes (objects) are defined and used. These include simple objects such as dynamic AJAX strings and arrays and more complex biological datatypes, such as sequences and alignments. To extend the functionality of the libraries with new datatypes and functions you’ll need a deeper understanding of C pointers and memory management, and their particular implementation in EMBOSS.

EMBOSS borrows the concept of objects from C++. An object can be thought of as a ‘black box’ with clearly defined inputs and outputs, but possibly more opaque internals with which the developer need not be concerned. An object stores its own (member) data and knows how to perform certain actions via member functions. From the perspective of the developer it doesn’t matter what is going on inside so long as the interface, i.e. the inputs and outputs, remains the same. The use of objects allows the programmer to model their code on the problem more closely, breaking it down into small easily managed pieces.

In EMBOSS the objects are the C data structure definitions. Elements in the structures are the member data. There are no member functions as such; however, all the functions that use an object are documented, along with the data elements, in the structured documentation in the C source file. The consistent structuring of code sections and their documentation enforces the naming and classification of all functions in sections for each datatype. This documentation (see Appendix D, Code documentation standards) is used online and is accessible via SRS (see Section 1.3, ‘Developer documentation’). EMBOSS maintains this