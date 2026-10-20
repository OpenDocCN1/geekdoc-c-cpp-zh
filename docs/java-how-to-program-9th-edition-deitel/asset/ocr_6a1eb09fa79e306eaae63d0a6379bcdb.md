how to declare an array, initialize an array and refer to individual elements of an array. The chapter introduced the enhanced for statement to iterate through arrays. We used exception handling to test for ArrayIndexOutOfBoundsExceptions that occur when a program attempts to access an array element outside the bounds of an array. We also illustrated how to pass arrays to methods and how to declare and manipulate multidimensional arrays. Finally, the chapter showed how to write methods that use variable-length argument lists and how to read arguments passed to a program from the command line.

We introduced the ArrayList<> generic collection, which provides all the functionality and performance of arrays, along with other useful capabilities such as dynamic resizing. We used the add methods to add new items to the end of an ArrayList and to insert items in an ArrayList. The remove method was used to remove the first occurrence of a specified item, and an overloaded version of remove was used to remove an item at a specified index. We used the size method to obtain number of items in the ArrayList.

We continue our coverage of data structures in Chapter 20, Generic Collections. Chapter 20 introduces the Java Collections Framework, which uses generics to allow you to specify the exact types of objects that a particular data structure will store. Chapter 20 also introduces Java’s other predefined data structures. The Collections API provides class Arrays, which contains utility methods for array manipulation. Chapter 20 uses several static methods of class Arrays to perform such manipulations as sorting and searching the data in an array. You’ll be able to use some of the Arrays methods discussed in Chapter 20 after reading the current chapter, but some of the Arrays methods require knowledge of concepts presented later in the book. Chapter 21 presents the topic of generics, which provide the means to create general models of methods and classes that can be declared once, but used with many different data types. Chapter 22, Custom Generic Data Structures, shows how to build dynamic data structures, such as lists, queues, stacks and trees, that can grow and shrink as programs execute.

We’ve now introduced the basic concepts of classes, objects, control statements, methods, arrays and collections. In Chapter 8, we take a deeper look at classes and objects.

# Summary

# Section 7.1 Introduction

+   - Arrays (p. 241) are fixed-length data structures consisting of related data items of the same type.

# Section 7.2 Arrays

+   - An array is a group of variables (called elements or components; p. 242) containing values that all have the same type. Arrays are objects, so they’re considered reference types.
+   - A program refers to any one of an array’s elements with an array-access expression (p. 242) that includes the name of the array followed by the index of the particular element in square brackets ([]; p. 242).
+   - The first element in every array has index zero (p. 242) and is sometimes called the zeroth element.
+   - An index must be a nonnegative integer. A program can use an expression as an index.
+   - An array object knows its own length and stores this information in a length instance variable (p. 242).